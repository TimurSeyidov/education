# KV хранилище

При работе над бэкэндом сколько-нибудь крупного проекта перед разработчиком рано или поздно встает вопрос выбора хранилища. На определенном этапе РСУБД перестает удовлетворять потребности проекта:

1. Требование на быструю запись/чтение. При высоких нагрузках скорость ответа от базы растет. РСУБД можно ускорять разными путями: оптимизировать настройки, профилировать и улучшать запросы, шардировать и реплицировать. Однако эти оптимизации все равно не позволят стабильно отвечать на запросы за несколько мс.
2. Строгая структура таблиц. Сегодня в любом бизнесе важна скорость доставки ценности до конечного пользователя. Вследствие этого на проектах происходят частые изменения, которые затрагивают схемы таблиц. Сперва может показаться, что это не проблема, но, во-первых, составление миграций занимает время, во-вторых, в таблице может храниться слишком много записей для изменений "в бою".

В вышеперечисленных случаях можно использовать key-value (далее "KV") хранилища.

## Redis как key-value хранилище

Рассмотрим стандартный пример использования Redis как KV: хранение информации о сессиях пользователей. Когда пользователь авторизуется на сайте, генерируется идентификатор сессии и используется как ключ. В значении сохранятся идентификатор пользователя (user_id) и любая нужная персональная информация. Обычно сессия записывается в cookie браузера. После этого backend моментально определяет, от какого пользователя пришел запрос.

### Запись новой сессии

![Запись новой сессии](../images/redis/01-01.png)

Попробуем реализовать пример на практике. Представим, что пользователь с идентификатором _120_ авторизовался, и серверу нужно создать для него сессию. Обычно идентификатор сессии состоит из большой рандомизированной строки. В данном уроке для простоты будет использоваться числовое представление.

Подключаемся к Redis серверу с помощью `redis-cli` и записываем значение `user_id` по ключу сессии:

```bash
127.0.0.1:6379> set session:1 120
OK
```

Команда записи в Redis имеет простую конструкцию:

```bash
set ключ значение
```

Сразу стоит обратить внимание на пару важных моментов:

1. в ключах рекомендуется использовать двоеточие как разделитель слов (хотя и встречаются другие подходы к наименованию). В примере с сессией ключ имеет вид `session:{session_id}`.
2. команда `set` записывает значение как строку. Одиночное слово пишется без кавычек, но предложение придется писать в одинарных или двойных кавычках `set key1 'hello world'`.

### Получение существующей сессии

![Получение существующей сессии](../images/redis/01-02.png)

Сессия сформирована и записана в Redis и cookie. Теперь при следующем запросе от клиента сервер увидит сессию и пойдет в Redis, чтобы определить пользователя:

```bash
127.0.0.1:6379> get session:1
"120"
```

Redis вернул строку, так как сессия существовала. Но что будет, если клиент пришлет несуществующую сессию?

```bash
127.0.0.1:6379> get session:N
(nil)
```

Вернется значение `(nil)`, означающее отсутствие ключа.

Если необходимо проверить сессию на существование без получения идентификатора пользователя, то используется соответствующая команда:

```bash
127.0.0.1:6379> exists session:1
(integer) 1
127.0.0.1:6379> exists session:N
(integer) 0
```

Если ключ существует, Redis возвращает целое число `1`. В противном случае вернется `0`.

### Удаление сессии

![Удаление сессии](../images/redis/01-03.png)

При выходе из аккаунта сессия пользователя должна удаляться:

```bash
127.0.0.1:6379> del session:1
(integer) 1
127.0.0.1:6379> del session:N
(integer) 0
```

Ответ Redis идентичен команде `exists`:

- `1`, если ключ существовал, и он был успешно удален
- `0`, если ключа не было, поэтому ничего не было удалено

### Хранение дополнительной информации

Допустим, в сессии нужно хранить не только идентификатор (`user_id`), но и электронную почту пользователя (`email`). Для этого достаточно в значение положить **JSON-объект**, содержащий всю необходимую информацию:

```bash
127.0.0.1:6379> set session:1 '{"user_id":120,"email":"test@test.com"}'
OK
127.0.0.1:6379> get session:1
"{\"user_id\":120,\"email\":\"test@test.com\"}"
```

Этот метод имеет некоторые недостатки:

1. логика по конвертированию в JSON выносится на уровень приложения. В следующих уроках мы рассмотрим стандартный тип данных в Redis, который позволяет хранить несколько значений по одному ключу
2. для получения одного поля `user_id` нужно достать весь JSON и декодировать его. В Redis существует модуль [RedisJSON](https://github.com/RedisJSON/RedisJSON) для решения этой проблемы. Например, получение поля реализуется одной командой:

```bash
127.0.0.1:6379> JSON.GET session1 .user_id
```

## Резюме

- БД в проекте выбираются под конкретные задачи.
- в Redis все значения хранятся по ключам. Абстрактно можно представить в виде хэш-таблицы или словаря. Из-за этого любое чтение/запись имеет очень высокую производительность. Например, Redis без труда выполняет запрос за 3мс при нагрузке в 5000+ RPS (запросов в секунду).
- в Redis хранятся неструктурированные значения. Если необходимо добавить новое поле в существующую структуру, то изменения вносятся только на уровне кода.
- основные команды для работы со значениями: `set`, `get`, `del`, `exists`.

### Дополнительные материалы
1. [Redis Session Management](https://redis.com/solutions/use-cases/session-management/)
2. [Простые команды в Redis](https://redis.io/commands/?group=string)

### Вопросы для самопроверки

**Представим, что в проекте необходимо хранить данные авиарейсов, пассажиров и линий выдачи багажа для прибывающих пассажиров. Ресурс не нагруженный, и нет ограничений по скорости ответа. Какой тип хранилища лучше использовать?**

- key-value хранилище, потому что данные можно получить быстро
- key-value хранилище, потому что всех пассажиров рейса удобнее хранить в одном ключе
- РСУБД, потому что между данными существуют отношения

**Допишите команду получения данных ключа user:1 из Redis**

- ___ user:1

**Допишите команду записи электронной почты test@test.com пользователя по ключу `user:1` в Redis**

- ___ user:1 ___

**Какие преимущества key-value хранилища перед РСУБД?**
_(нужно выбрать все корректные ответы)_

- динамическая структура хранимых данных
- удобное получение агрегированных данных с помощью специального языка запросов
- скорость чтения/записи атомарных значений
- строгая типизация данных по ключам

**Допишите команду удаления данных по ключу `user:10` в Redis.**

- ___ user:10