# Задачи

## Задача 1 {id="1_1"}

Напишите класс `LittleBell`, который при вызове метода sound печатает слово "**ding**".

### Пример 1 {id="1_1_1"}

**Ввод**

```python
# Ваш код

bell = LittleBell()
bell.sound()
```

**Вывод**
```python
ding
```

### Пример 2 {id="1_1_2"}

**Ввод**

```python
# Ваш код

bell = LittleBell()
bell.sound()
bell.sound()
bell.sound()
```

**Вывод**
```python
ding
ding
ding
```

## Задача 2 {id="1_2"}

Напишите класс кнопки `Button`, экземпляры которого будут измерять количество нажатий на кнопку-объект.

Метод `click` увеличивает количество нажатий, метод `click_count` возвращает число нажатий. Метод `reset` обнуляет количество нажатий.

### Пример 1 {id="1_2_1"}

**Ввод**

```python
# Ваш код

button = Button()
button.click()
button.click()
print(button.click_count())
button.click()
print(button.click_count())
```

**Вывод**
```python
2
3
```

### Пример 2 {id="1_2_2"}

**Ввод**

```python
# Ваш код

button = Button()
button.click()
button.click()
print(button.click_count())
button.reset()
button.click()
print(button.click_count())
```

**Вывод**
```python
2
1
```

### Пример 3 {id="1_2_3"}

**Ввод**

```python
# Ваш код

button = Button()
button.click()
print(button.click_count())
```

**Вывод**
```python
1
```

## Задача 3 {id="1_3"}

Напишите класс `Balance` для описания весов с двумя чашами. На левую и правую чашу объекта будут добавляться грузы с различным весом, ваша задача определить положение чаш.
Метод `add_right` принимает целое число — вес, положенный на правую чашу весов, `add_left` — на левую чашу. Метод `result` должен возвращать символ **=**, если вес на чашах одинаковый, **R** — если перевесила правая, **L** — если перевесила левая.

### Пример 1 {id="1_3_1"}

**Ввод**

```python
# Ваш код

balance = Balance()
balance.add_right(10)
balance.add_left(9)
balance.add_left(2)
print(balance.result())
```

**Вывод**
```python
L
```

### Пример 2 {id="1_3_2"}

**Ввод**

```python
# Ваш код

balance = Balance()
balance.add_right(10)
balance.add_left(5)
balance.add_left(5)
print(balance.result())
balance.add_left(1)
print(balance.result())
```

**Вывод**
```python
=
R
```

## Задача 4 {id="1_4"}

Напишите класс `OddEvenSeparator`, в который можно добавлять числа, получая потом отдельно чётные и нечётные. Числа добавляются в объект с помощью метода `add_number`. Методы `even` и `odd` должны возвращать списки чётных и нечётных чисел соответственно. Числа в списке должны идти в том же порядке, что и при добавлении в объект.

### Пример 1 {id="1_4_1"}

**Ввод**

```python
# Ваш код

separator = OddEvenSeparator()
separator.add_number(1)
separator.add_number(5)
separator.add_number(6)
separator.add_number(8)
separator.add_number(3)
print(' '.join(map(str, separator.even())))
print(' '.join(map(str, separator.odd())))
```

**Вывод**
```python
6 8
1 5 3
```

## Задача 5 {id="1_5"}

Напишите класс `BigBell`, который при вызове метода sound печатает попеременно слова **ding** и **dong**, начиная c **ding**.

### Пример 1 {id="1_5_1"}

**Ввод**

```python
# Ваш код

bell = BigBell()
bell.sound()
bell.sound()
bell.sound()
```

**Вывод**
```python
ding
dong
ding
```

## Задача 6 {id="1_6"}

Напишите класс `MinMaxWordFinder`. Класс должен уметь анализировать текст и находить в нём слова наименьшей и наибольшей длины. Текст состоит из предложений, которые добавляются в обработку методом `add_sentence`. Метод `shortest_words` возвращает список самых коротких на данный момент слов, метод `longest_words` — самых длинных. Слова, возвращаемые методами `shortest_words` и `longest_words`, должны быть отсортированы по алфавиту.
Если одно из самых коротких слов встретилось в исходных предложениях несколько раз, оно должно столько же раз повториться в списке самых коротких слов. Самые длинные слова наоборот должны входить в список без повторов.

### Пример 1 {id="1_6_1"}

**Ввод**

```python
# Ваш код

finder = MinMaxWordFinder()
finder.add_sentence('hello abc world')
finder.add_sentence('def asdf qwert')
print(' '.join(finder.shortest_words()))
print(' '.join(finder.longest_words()))
```

**Вывод**
```python
abc def
hello qwert world
```

### Пример 2 {id="1_6_2"}

**Ввод**

```python
# Ваш код

finder = MinMaxWordFinder()
finder.add_sentence('hello')
finder.add_sentence('abc')
finder.add_sentence('world')
finder.add_sentence('def')
finder.add_sentence('asdf')
finder.add_sentence('qwert')
print(' '.join(finder.shortest_words()))
print(' '.join(finder.longest_words()))
```

**Вывод**
```python
abc def
hello qwert world
```

### Пример 3 {id="1_6_3"}

**Ввод**

```python
# Ваш код

finder = MinMaxWordFinder()
finder.add_sentence('hello')
finder.add_sentence('  abc     def    ')
finder.add_sentence('world')
finder.add_sentence('            abc          ')
finder.add_sentence('asdf')
finder.add_sentence('qwert')
print(' '.join(finder.shortest_words()))
print(' '.join(finder.longest_words()))
```

**Вывод**
```python
abc abc def
hello qwert world
```

## Задача 7 {id="1_7"}

Создайте класс `BoundingRectangle`, который обрабатывает точки на плоскости и строит по ним прямоугольник минимального размера, в который входят все эти точки. Если точка лежит на границе прямоугольника, считается, что она в него входит.
Нужно определить следующие методы (`rect` – экземпляр `BoundingRectangle`):
- `rect.add_point(x, y)` — добавить новую точку.
- `rect.width()` — ширина прямоугольника.
- `rect.height()` — высота прямоугольника.
- `rect.bottom_y()` — Y-координата нижней границы прямоугольника.
- `rect.top_y()` — Y-координата верхней границы прямоугольника.
- `rect.left_x()` — X-координата левой границы прямоугольника.
- `rect.right_x()` — X-координата правой границы прямоугольника.

Гарантируется, что хотя бы одна точка будет добавлена в экземпляр до вызова методов, возвращающих описание прямоугольника.


### Пример 1 {id="1_7_1"}

**Ввод**

```python
# Ваш код

rect = BoundingRectangle()
rect.add_point(-1, -2)
rect.add_point(3, 4)
print(rect.left_x(), rect.right_x())
print(rect.bottom_y(), rect.top_y())
print(rect.width(), rect.height())
```

**Вывод**
```python
-1 3
-2 4
4 6
```

### Пример 2 {id="1_7_2"}

**Ввод**

```python
# Ваш код

rect = BoundingRectangle()
rect.add_point(10, 20)
rect.add_point(5, 7)
rect.add_point(6, 3)
print(rect.left_x(), rect.right_x())
print(rect.bottom_y(), rect.top_y())
print(rect.width(), rect.height())
```

**Вывод**
```python
5 10
3 20
5 17
```

### Пример 3 {id="1_7_3"}

**Ввод**

```python
# Ваш код

rect = BoundingRectangle()
rect.add_point(-11, -12)
rect.add_point(13, -14)
rect.add_point(-15, 10)
print(rect.left_x(), rect.right_x())
print(rect.bottom_y(), rect.top_y())
print(rect.width(), rect.height())
print()
rect.add_point(-21, -12)
rect.add_point(13, -14)
rect.add_point(-15, 36)
print(rect.width(), rect.height())
print(rect.left_x(), rect.right_x())
print(rect.bottom_y(), rect.top_y())
print()
rect.add_point(-21, 78)
rect.add_point(13, -14)
rect.add_point(-55, 36)
print(rect.bottom_y(), rect.top_y())
print(rect.width(), rect.height())
print(rect.left_x(), rect.right_x())
```

**Вывод**
```python
-15 13
-14 10
28 24

34 50
-21 13
-14 36

-14 78
68 92
-55 13
```