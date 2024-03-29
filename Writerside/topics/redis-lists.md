# Хранение списков с Lists

В Redis удобно работать с простыми строками. Команды `get`, `set`, `del` покрывают большинство нужд среднего проекта. Но что делать, если нужно хранить множество связанных данных?

![Связка данных](../images/redis/04-01.png)

Например, разрабатывается соц. сеть и необходимо хранить список диалогов пользователя в кэше. При этом есть знаменитости, которым пишут сообщения миллионы пользователей. Хранить всю информацию в N ключах нереально, потому что пара таких пользователей будет занимать всю память на сервере. Некоторые разработчики решают этот вопрос предварительной сериализацией списка в JSON или бинарный формат. Такой способ сработает, но имеет несколько минусов:

- дополнительная логика со стороны приложения, которая может содержать баги
- меньшая производительность по сравнению с использованием встроенных типов данных Redis
- отсутствие возможности использовать функции внутри Redis для работы со списком
- большие расходы на сериализацию/десериализацию при большом размере списка (например, 1 миллион элементов)

## Списки в Redis (Lists)

Списки в Redis — это список строк, упорядоченный в порядке вставки. Для абстракции его можно представить как обычный массив в любом языке программирования. Список может содержать более 4 миллиардов элементов. Самая главная особенность списков в Redis — это возможность получать/читать/удалять элементы с начала или конца списка за константное время O(1) даже при общем размере в несколько миллионов.

### Запись элементов

Представим, что при разработке соц. сети нужно хранить в кэше список идентификаторов опубликованных постов пользователя. Важно, чтобы посты были упорядочены для сохранения хронологии.

Имеется пользователь с ID **14**, который опубликовал 3 поста: **10**, **20**, **30**.

В абстрактном языке программирования массив постов выглядел бы следующим образом: `[30, 20, 10]`. Идентификаторы упорядочены от старшего к младшему, потому что в ленте отображаются сначала самые последние посты. Выходит, что каждый новый пост добавляется не в конец списка, а в его начало.

Для добавления элемента в начало списка (слева) существует команда `lpush key value1 [value2...]`. Если списка не существовало до этого, то Redis создаст новый:

```bash
127.0.0.1:6379> lpush user:14:recent_posts 10
(integer) 1
127.0.0.1:6379> lpush user:14:recent_posts 20 30
(integer) 3
```

Команда `lpush` возвращает количество элементов в списке после вставки.

### Получение элементов

Недавние посты пользователя хранятся в кэше. Чтобы достать элементы списка, используется команда `lrange key start_index stop_index`:

```bash
127.0.0.1:6379> lrange user:14:recent_posts 0 -1
1) "30"
2) "20"
3) "10"
```

Если указать правую границу как -1, то вернется весь список. Обратите внимание, что в Redis все атомарные значения — строки.

### Удаление элементов

Пользователь может удалить пост, и в этом случае необходимо его также удалить из кэша.

Есть несколько способов удаления элементов. Самый быстрый и рекомендуемый — это удаление первого/последнего элементов списка с помощью команд `lpop key`, `rpop key`:

```bash
127.0.0.1:6379> lpop user:14:recent_posts
"30"
127.0.0.1:6379> rpop user:14:recent_posts
"10"
```

`lpop` удаляет элемент из начала списка и возвращает его. Команда `rpop` делает то же самое только с конца.

Если количество элементов в списке маленькое, то можно использовать команду `lrem key 0 value`, которая ищет в списке значение и удаляет его. Команда `lrange` возвращает указанные элементы списка.

```bash
127.0.0.1:6379> lrem user:14:recent_posts 0 120
(integer) 0
127.0.0.1:6379> lrem user:14:recent_posts 0 20
(integer) 1
127.0.0.1:6379> lrange user:14:recent_posts 0 -1
(empty array)
```

Если элемент не был найден в списке, то возвращается `0`. В случае успешного удаления вернется `1`. Так как удалился последний элемент в списке, команда `lrange` вернула пустой массив.

### Время жизни

Любой кэш не должен храниться вечно. Добавим время жизни в 1 час на список с последними постами пользователя 14:

```bash
127.0.0.1:6379> expire user:14:recent_posts 3600
(integer) 1
127.0.0.1:6379> ttl user:14:recent_posts
(integer) 3598
```

## Резюме

- списки в Redis — самый предпочтительный способ кэширования упорядоченных данных
- добавить элементы в список можно с помощью команд `lpush`, `rpush`
- чтение списка осуществляется командой lrange
предпочтительное удаление элементов из списка происходит с начала или конца: `lpop`, `rpop`. При небольших размерах можно использовать поиск и удаление: `lrem`
- любой кэш хранится какое-то время. На список нужно добавить время жизни командой `expire`

### Дополнительные материалы

- [Redis LPUSH command](https://redis.io/commands/lpush/)
- [Redis LRANGE command](https://redis.io/commands/lrange)
- [Redis LREM command](https://redis.io/commands/lrem)
- [Redis LPOP command](https://redis.io/commands/lpop)
- [Redis RPOP command](https://redis.io/commands/rpop)
- [Redis EXPIRE command](https://redis.io/commands/expire)

### Вопросы для самопроверки

**Как можно реализовать хранение структуры данных "очередь" (первым пришел — первым ушел) в Redis?**

- использовать встроенный тип данных `Lists`. Добавление нового элемента происходит командой `lpush`. Получение следующего в очереди элемента происходит командой `lpop`
- использовать встроенный тип данных `Lists`. Добавление нового элемента происходит командой `rpush`. Получение следующего в очереди элемента происходит командой `lpop`
- хранить каждое значение в отдельном ключе и их очередность
- хранить очередь в JSON-массиве в одном ключе Redis

**Допишите команду добавления сообщения Hello world слева списка в Redis-ключ `user:1:last_messages`**

- ___ user:1:last_messages '___'

**Допишите команду добавления сообщения Hey справа списка в Redis-ключ `user:1:last_messages`**

- ___ user:1:last_messages '___'

**Допишите команду чтения и удаления самого левого сообщения из списка `user:1:last_messages` в Redis**

- ___ user:1:last_messages

**Допишите команду чтения и удаления самого правого сообщения из списка `user:1:last_messages` в Redis**

- ___ user:1:last_messages

**Допишите команду получения всех сообщений из списка `user:1:last_messages` в Redis**

- ___ user:1:last_messages ___ ___