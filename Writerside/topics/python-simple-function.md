# Простые встроенные функции

## Типы данных

Пока единственным типом данных, с которым мы работали, были строки. Теперь нам предстоит рассмотреть целые и вещественные числа. У каждого элемента данных, который встречается в программе, есть свой тип.

Например, «привет» — это строка, а вот 15.3 — это число (дробное). Даже если данные не записаны прямо в программе, а получаются откуда-то еще, у них есть совершенно определенный тип. Например, на место `input()` всегда подставляется строка, а 2 + 2 даст именно число 4, а не строку "4".

```python
a = input()
print(a + 1)
```

Как вы думаете, что получится?

Ошибка возникнет потому, что в переменную а у нас попадает строка, а в функции print мы пытаемся сложить эту строку из переменной а и число 1.

А если нам надо работать с числами? Мы пока будем рассматривать целые и вещественные числа.
Когда речь идет о числовых данных, они записываются **без кавычек**.

А для вещественных чисел, чтобы отделить дробную часть от целой, используют **точку**.

```python
print('10' + '20') #1020
print(10 + 20) #30
print(10.0 + 20.0) #30.0
print(10.0 + 20) #30.0
```

## Операции над числами

- <shortcut>+</shortcut> Сложение
- <shortcut>-</shortcut> Вычитание
- <shortcut>*</shortcut> Умножение
- <shortcut>/</shortcut> Деление
- <shortcut>**</shortcut> Возведение в степень
- <shortcut>//</shortcut> Целая часть от деления
- <shortcut>%</shortcut> Остаток от деления


## Приоритет операций

1. Возведение в степень `(**)`.
2. Унарный минус `(-)`. Используется для получения, например, противоположного числа.
3. Умножение, деление `(* / % //)`.
4. Сложение и вычитание `(+ -)`.
5. Операции сравнения `(<= < > >=)`.
6. Операции равенства `(== !=)`.
7. Операции присваивания `(=)`.
8. Логические операции `(not or and)`.

## Простейшие функции

- `int(x)` - Приведение к целому числу
- `float(x)` - Приведение к числу с плавающей точкой
- `str(x)` - Приведение к строке
- `len(x)` - Длина строки
- `abs(x)` - Модуль (абсолют) числа


```python
a = input()
b = int(a)
print(b + 1)
```

## Обмен значениями переменных

Необходимо поменять значения в переменных местами

```python
a = 3
b = 5
...
...
print(a)
print(b)
```

Классическое решение через 3 переменную

```python
a = 3
b = 5
с = a
a = b
b = c
print(a)
print(b)
```

Решение в Python

```python
a = 3
b = 5
a, b = b, a
print(a)
print(b)

a = b = c = 5
```