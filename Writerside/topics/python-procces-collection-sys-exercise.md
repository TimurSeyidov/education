# Задачи

## Задача 1 {id="20_1"}

С клавиатуры вводится строка из разделённых пробелами слов. Выведите на экран в строку, разделённую пробелами, список слов, отсортированных в лексикографическом порядке.

Введённые слова могут быть написаны в различных регистрах. Сортироваться слова должны независимо от регистра, а выводиться на печать в том виде, в котором переданы на вход программы.

Напомним, что функция `sorted` сортирует элементы в лексикографическом порядке, но при этом по-умолчанию любая буква в верхнем регистре считается идущей раньше, чем буква в нижнем регистре (вам такой вариант не подходит).



### Пример {id="20_1_1"}

**Ввод**

```bash
cats dog CAT DOGGY monkey
```

**Вывод**
```bash
CAT cats dog DOGGY monkey
```

## Задача 2 {id="20_2"}

Учитель проверял контрольные работы по информатике в нескольких классах и решил убедиться, что в каждом классе есть хотя бы один отличник.

Помогите учителю осуществить такую проверку.

### Формат ввода

1. На первой строке вводится количество классов.
2. Затем для каждого класса вводится блок информации вида:
3. На первой строке – N – количество учеников в классе.
4. Далее вводится N строк вида: «Фамилия Оценка»

### Формат вывода
«ДА» если в каждом классе есть отличник, и «НЕТ» в противном случае.

> При решении задачи используйте конструкции `all` и `any`.

### Пример {id="20_2_1"}

**Ввод**

```bash
4
3
Иванов 4
Петров 5
Сидоров 3
2
Кузнецов 5
Петренко 5
3
Лебедев 4
Иваненко 4
Смирнов 5
2
Овчинников 4
Козлов 5
```

**Вывод**
```bash
ДА
```

## Задача 3 {id="20_3"}

Программисту Васе поставили задачу разработать систему, вычисляющую средний рост учеников в классе.

Данные в эту систему поступают последовательно, рост указывается в сантиметрах, каждое число на отдельной строке.

Но вот беда: изначально неизвестно, сколько учеников учится в классе. Программа должна вывести ответ после того, как ввод данных прекратился.

Помогите Васе справиться с поставленной задачей.

### Формат ввода

Последовательность натуральных чисел, каждое на отдельной строке.

### Формат вывода

Вещественное число. Никаких округлений производить не надо. В случае, если никаких данных не поступало, следует вывести -1

### Пример 1 {id="20_3_1"}

**Ввод**

```bash
130
127
131
```

**Вывод**
```bash
129.33333333333334
```

### Пример 2 {id="20_3_2"}

**Ввод**

```bash
<пустая_строка>
```

**Вывод**
```bash
-1
```

## Задача 4 {id="20_4"}

На вход вашей программы передаётся текст файла с программой на языке Python.

Ваша задача – посчитать и напечатать число строк кода, содержащих только комментарий (т.е. в которых первый непробельный символ – символ решётки `#`).

> При решении используйте лямбда-функцию.

### Пример {id="20_4_1"}

**Ввод**

```bash
import sys   
for line in sys.stdin:   
    # rstrip(’\n’) "отрезает" от строки line, идущий справа символ
    # перевода строки, ведь print сам переводит строку   
    print(line.rstrip(’\n’))

```

**Вывод**
```bash
2
```

## Задача 5 {id="20_5"}

Напишите программу, которая ищет нули в таблице чисел и печатает `True`, если нули нашлись.

В противном случае надо напечатать `False`.

Эту задачу надо постараться решить «в одну строчку». В этом вам помогут функции `any` и `all`.

### Формат ввода

Текст c матрицей (таблицей) целых чисел в диапазоне от 0 до 99, разделённых пробелами и символами перевода строки (см. пример).

### Формат вывода

`True` или `False`

### Пример {id="20_5_1"}

**Ввод**

```bash
64 33 79 56 78 70 45 71 82  3
96 27  8 36 72 14 91 10 21 65
95 28 91 23 78 38 21 50 64 37
97 54 94  6 48 17 37 19 78 58
69 58 35  1 70 24 60 17  3 11
48  9 13 23 82 49 79 55 29 53
9   2 67 90  0 17 34 55 49 63
98 98 23 71 66 57 15 94 34 81
58 37 32 29 10 19 53 46 95 19
41 24 95 47 58 17 74 69 62  4

```

**Вывод**
```bash
True
```

## Задача 6 {id="20_6"}

При помощи итераторов и функций высшего порядка выведите список комментариев с указанием номера строки у каждого из них (нумерация строк с единицы).

Знаки решетки и пробелы в начале строки (а также в начале комментария – после символа решётки) отбросьте. Также отбросьте пробелы и символы табуляции, если они встречаются в конце строки.

Оформление строки вывода сделайте аналогично примеру. Пробел между двоеточием и комментарием не должен зависеть от содержания комментария (так как лидирующие и замыкающие пробелы в строке комментария отбрасываются).


### Пример {id="20_6_1"}

**Ввод**

```bash
import sys
for line in sys.stdin:
    # rstrip(’\n’) "отрезает" от строки line,
    # идущий справа символ перевода строки,
    # ведь print сам переводит строку
    print(line.rstrip(’\n’))

```

**Вывод**
```bash
Line 3: rstrip(’\n’) "отрезает" от строки line,
Line 4: идущий справа символ перевода строки,
Line 5: ведь print сам переводит строку
```

## Задача 7 {id="1_7"}

Словесной гематрией называется сумма номеров (кодов, числовых значений) входящих в слово букв.

На вход программы поступает список английских слов. На одной строке записано одно слово, количество слов неизвестно.

Для вычисления гематрии поступим следующим образом:
1.	Переведём слово в верхний регистр.
2.	Числовое значение буквы вычислим как `КодБуквы - КодБуквыA + 1`

Выведите полученные слова в порядке возрастания их гематрии. Если для каких-то слов гематрия совпадает, то их выводите в алфавитном порядке.

### Формат ввода

Набор слов на английском языке, каждое слово на отдельной строке.

### Формат вывода

Набор слов в требуемом порядке.

> Для получения кода символа воспользуйтесь функцией `ord(c)`. Слова во входных данных могут повторяться.

### Пример 1 {id="20_7_1"}

**Ввод**

```bash
mother
Daddy
sIster
```

**Вывод**
```bash
Daddy
mother
sIster
```

### Пример 2 {id="20_7_2"}

**Ввод**

```bash
bBb
aaaaaa
word
```

**Вывод**
```bash
aaaaaa
bBb
word
```
