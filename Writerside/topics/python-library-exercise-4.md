# Задачи

## Задача 1 {id="25_1"}

Вычислите, сколько раз в отрывке из литературного произведения употребляются глаголы **видеть**, **увидеть**, **глядеть**, **примечать** и **узреть** во всех формах. Ответом будет одно целое число.

### Формат ввода

Текст в произвольном виде: на нескольких строчках, с различными разделителями слов (пробелы, табуляции).

### Формат вывода

Целое число.

### Пример {id="25_1_1"}

**Ввод**

```bash
От города до дачи полчаса езды. Я то и дело поглядывала по сторонам,
но ничего подозрительного узреть не смогла и вскоре успокоилась.
Затем я увидела чудо.
```

**Вывод**
```bash
2
```

## Задача 2 {id="25_2"}

Дан отрывок из литературного произведения. Выведите через пробел десять существительных, которые встречаются в тексте чаще всего. Существительные нужно поставить в начальную (нормальную) форму и отсортировать по убыванию частоты их встречи в тексте.

Если два существительных встречаются с одинаковой частотой, то их надо расположить в обратном лексикографическом порядке.

Самое важное: правильным существительным мы будем считать такое существительное (NOUN), у которого параметр `score` больше 0.5

### Формат ввода

Текст, вводимый произвольным образом. Для его чтения необходимо воспользоваться `sys.stdin`. Слова могут быть разделены пробелами, символами табуляции и переводами строк.

### Формат вывода

10 существительных в начальной форме через пробел.

### Пример {id="25_2_1"}

**Ввод**

```bash
Я родился в 1632 году в городе Йорке в зажиточной семье иностранного
происхождения. Мой отец был родом из Бремена и основался сначала в
Гулле. Нажив торговлей хорошее состояние, он оставил дела и
переселился в Йорк.
Здесь он женился на моей матери, родные которой назывались Робинзоны -
старинная фамилия в тех местах. По ним и меня назвали Робинзоном.
Фамилия отца была Крейцнер, но, по обычаю англичан коверкать
иностранные слова, нас стали называть Крузо. Теперь мы и сами так
произносим и пишем нашу фамилию; так же всегда звали меня и мои
знакомые.
   У меня было два старших брата. Один служил во Фландрии, в
английском пехотном полку, - том самом, которым когда то командовал
знаменитый полковник Локгарт; он дослужился до чина подполковника и
был убит в сражении с испанцами под Дюнкирхеном. Что сталось со
вторым моим братом - не знаю, как не знали мои отец и мать, что
сталось со мной.
```

**Вывод**
```bash
фамилия отец брат торговля сражение состояние слово семья робинзон
происхождение
```

### Примечания

Чтобы корректно обработать текст, надо «очистить» его от знаков препинания, так как в тексте могут встречаться знаки «тире» или «дефиса», их надо игнорировать. Например, слово «куда-то» должно анализироваться как пара слов: «куда» и «то».

## Задача 3 {id="25_3"}

Используя библиотеку `pymorphy`, напишите программу, которая выводит текст песни, состоящей из куплетов по три строки:

```bash
В холодильнике 99 бутылок кваса.
Возьмём одну и выпьем.
Осталось 98 бутылок кваса.
В холодильнике 98 бутылок кваса.
Возьмём одну и выпьем.
Осталось 97 бутылок кваса.
...
В холодильнике 92 бутылки кваса.
Возьмём одну и выпьем.
Осталась 91 бутылка кваса.
...
```

Последний куплет заканчивается нулём бутылок. Не забывайте склонять бутылки по правилам русского языка.

## Задача 4 {id="25_4"}

Напишите программу, которая принимает на вход слово и, если оно существительное, изменяет его по падежам и числам.

Иначе – выводит сообщение «Не существительное».

### Формат ввода

Одно слово.

### Формат вывода

Строки в формате:

```bash
Единственное число:
Именительный падеж: <слово>
Родительный падеж: <слово>
...
Предложный падеж: <слово>
Множественное число:
Именительный падеж: <слово>
Родительный падеж: <слово>
...
Предложный падеж: <слово>
```

Или фраза «`Не существительное`», если введённое слово не является существительным.

### Пример {id="25_4_1"}

**Ввод**

```bash
Питон
```

**Вывод**
```bash
Единственное число:
Именительный падеж: питон
Родительный падеж: питона
Дательный падеж: питону
Винительный падеж: питона
Творительный падеж: питоном
Предложный падеж: питоне
Множественное число:
Именительный падеж: питоны
Родительный падеж: питонов
Дательный падеж: питонам
Винительный падеж: питонов
Творительный падеж: питонами
Предложный падеж: питонах
```

## Задача 5 {id="25_5"}

Напишите программу, которая на вход принимает слово, а потом, если это глагол, изменяет его следующим образом:
- в прошедшем времени по родам,
- в прошедшем времени во множественном числе,
- в настоящем времени по лицам и числам.

Если на вход подан не глагол, программа должна вывести сообщение «Не глагол».

### Формат ввода

Одно слово.

### Формат вывода

Строки в формате:

```bash
Прошедшее время:
<слово в прошедшем времени мужском роде>
<слово в прошедшем времени женском роде>
<слово в прошедшем времени среднем роде>
<слово в прошедшем времени мн. числе>
Настоящее время:
<слово в настоящем времени 1 лицо ед. число>
<слово в настоящем времени 1 лицо мн. число>
<слово в настоящем времени 2 лицо ед. число>
<слово в настоящем времени 2 лицо мн. число>
<слово в настоящем времени 3 лицо ед. число>
<слово в настоящем времени 3 лицо мн. число>
```

Или фраза «`Не глагол`», если введённое слово не является глаголом.


```bash
Единственное число:
Именительный падеж: <слово>
Родительный падеж: <слово>
...
Предложный падеж: <слово>
Множественное число:
Именительный падеж: <слово>
Родительный падеж: <слово>
...
Предложный падеж: <слово>
```

Или фраза «`Не существительное`», если введённое слово не является существительным.

### Пример 1 {id="25_5_1"}

**Ввод**

```bash
учиться
```

**Вывод**
```bash
Прошедшее время:
учился
училась
училось
учились
Настоящее время:
учусь
учимся
учишься
учитесь
учится
учатся
```

### Пример 2 {id="25_5_2"}

**Ввод**

```bash
ехал
```

**Вывод**
```bash
Прошедшее время:
ехал
ехала
ехало
ехали
Настоящее время:
еду
едем
едешь
едете
едет
едут
```

## Задача 6 {id="25_6"}

Напишите программу, которая принимает из стандартного потока заранее неизвестное количество строк, в каждой из которых записано одно слово.

Для каждого слова выведите (в том порядке, в котором слова идут в стандартном потоке ввода) фразу «Живое» или «Не живое» в зависимости от того, является ли существительное одушевлённым по мнению библиотеки `pymorphy2`. Фраза должна быть согласована по роду и числу с анализируемым словом.

Если анализируемое слово не является существительным, выведите фразу «Не существительное».

### Формат ввода

Слова в стандартном потоке ввода, по одному на каждой строке.

### Формат вывода

Результаты анализа каждого слова. Каждый результат с новой строки.


### Пример 1 {id="25_6_1"}

**Ввод**

```bash
Кот
Кошка
Стол
Окно
Пила
Люди
Столы
Пилить
```

**Вывод**
```bash
Живой
Живая
Не живой
Не живое
Не живая
Живые
Не живые
Не существительное
```

### Пример 2 {id="25_6_2"}

**Ввод**

```bash
Конь
Улица
Фонарь
Аптека
Тусклый
Свет
```

**Вывод**
```bash
Живой
Не живая
Не живой
Не живая
Не существительное
Не живой
```
