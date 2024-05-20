# Задачи

## Задача 1 {id="18_1"}

Напишите функцию, которая создает, заполняет и возвращает матрицу заданного размера. При этом (в зависимости от переданных аргументов) она должна вести себя так:
- `matrix()` — создает матрицу `1 × 1`, в которой единственное число равно `нулю`.
- `matrix(n)` — создает матрицу `n × n`, заполненную `нулями`.
- `matrix(n, m)` — создает матрицу из `n` строк и `m` столбцов, заполненную `нулями`.
- `matrix(n, m, a)` — создает матрицу из `n` строк и `m` столбцов, в которой каждый элемент равен `a`.

При создании функции пользуйтесь аргументами по умолчанию.

### Пример 1 {id="18_1_1"}

**Ввод**

```python
rows = matrix()
for row in rows:
    print(*row)
```

**Вывод**
```bash
0
```

### Пример 2 {id="18_1_2"}

**Ввод**

```python
rows = matrix(2)
for row in rows:
    print(*row)
```

**Вывод**
```bash
0 0
0 0
```

## Задача 2 {id="18_2"}

Напишите функцию, которая будет готовить и возвращать текст письма для почтовой рассылки. В письмо подставляются аргументы: имя, место и дата встречи, email получателя. Если место не указано, в письмо должен быть подставлен город, в котором вы живете.

### Шаблон письма:

```text
To: {email}
Здравствуйте, {имя}!
Были бы рады видеть вас на встрече начинающих программистов в {место}, которая пройдет {дата}.
```

Вызовите эту функцию, чтобы подготовить письма двум вашим соседям по классу. При вызове используйте именованные аргументы. Функция и аргументы должны быть названы так, чтобы по названиям параметров точно было понятно, что они делают.

## Задача 3 {id="18_3"}

Напишите функцию `encrypt_caesar(msg, shift)`, которая кодирует сообщение шифром Цезаря и возвращает его. Шифр Цезаря заменяет каждую букву в тексте на букву, которая отстоит в алфавите на некоторое фиксированное число позиций.

В функцию передается сообщение и сдвиг алфавита. Если сдвиг не указан, то пусть ваша функция кодирует сдвиг алфавита на 3 позиции:

```text
А → Г,
Б → Д,
В → Е,
…
Э → А,
Ю → Б,
Я → В
```

Все символы, кроме русских букв должны остаться неизменными. Маленькие буквы должны превращаться в маленькие, большие — в большие.

Напишите также функцию декодирования `decrypt_caesar(msg, shift)`, также использующую сдвиг по умолчанию. При написании функции декодирования используйте вашу функцию кодирования.

### Пример 1 {id="18_3_1"}

**Ввод**

```python
msg = "Да здравствует салат Цезарь!"
shift = 3
encrypted = encrypt_caesar(msg, shift)
decrypted = decrypt_caesar(encrypted, shift)
print(encrypted)
print(decrypted)
```

**Вывод**
```bash
Зг кзугефхецих фгогх Щикгуя!
Да здравствует салат Цезарь!
```

### Пример 2 {id="18_3_2"}

**Ввод**

```python
msg = "Да здравствует салат Цезарь!"
shift = 5
encrypted = encrypt_caesar(msg, shift)
decrypted = decrypt_caesar(encrypted, shift)
print(encrypted)
print(decrypted)
```

**Вывод**
```bash
Йе мйхезцчзшкч цереч Ыкмехб!
Да здравствует салат Цезарь!
```

## Задача 4 {id="18_4"}

**k-ой частичной суммой** списка называется сумма первых `k` элементов списка. Напишите функцию `partial_sums`, которая принимает неограниченное число аргументов, а возвращает список частичных сумм этих элементов: на нулевой позиции — 0, на первой позиции — первое число, на второй — сумму первого и второго чисел, затем — сумму первого, второго и третьего и т.д.

Обратите внимание, что функция должна принимать не список, а именно неограниченное число аргументов.

### Пример 1 {id="18_4_1"}

**Ввод**

```python
print(partial_sums(13))
```

**Вывод**
```bash
[0, 13]
```

### Пример 2{id="18_4_2"}

**Ввод**

```python
print(partial_sums(1, 0.5, 0.25, 0.125))
```

**Вывод**
```bash
[0, 1, 1.5, 1.75, 1.875]
```

## Задача 5 {id="18_5"}

Стандартная мишень для игры в дартс разделена на 20 ячеек с номерами от 1 до 20. В центре расположено «яблочко», попадание в которое приносит игроку 50 очков. Вокруг него — зелёное кольцо, при попадании в которое засчитывается 25 очков. Попадание во внешнее (узкое) кольцо мишени удваивает число сектора, а во внутреннее — утраивает.

Эти правила показались игрокам слишком простыми, поэтому они решили присвоить секторам во внешнем и внутреннем кольцах случайные значения. В глобальной переменной scoring хранится словарь для подсчета очков (обратите внимание, что в случае внутреннего и внешнего колец значениями являются словари, ключами в которых являются номера сектора, а значениями –– количество очков):

- Яблочко: 50
- Зеленое кольцо: 25
- Внешнее кольцо: 1: 8, 2: 6, 3: 42,…, 20: 50
- Внутреннее кольцо: 1: 2, 2: 9, 3: 56,…, 20: 3

Напишите функцию `score()`, которая принимает на вход 1 (если это «Яблочко» или «Зеленое кольцо») или 2 аргумента (если это внутреннее или внешнее кольцо, то название кольца и номер сектора) и возвращает количество очков.

### Пример 1 {id="18_5_1"}

**Ввод**

```python
print(score("Яблочко"))
```

**Вывод**
```bash
50
```

### Пример 2 {id="18_5_2"}

**Ввод**

```python
print(score("Внешнее_кольцо", 1))
```

**Вывод**
```bash
8
```

## Задача 6 {id="18_6"}

Сделайте функцию `solve(*coefficients)`, которая умеет решать уравнения степени не выше второй (квадратные и линейные).
- Если у функции три аргумента, их надо трактовать как `a`, `b` и `c` в уравнении `ax^2 + bx + c = 0`.
- Если два — как коэффициенты `b` и `c` в уравнении `bx + c = 0`.
- Если один — как коэффициент c в уравнении `c = 0`.
- Если список коэффициентов пуст или коэффициентов больше трёх, то функция должна вернуть `None`.

### Пример 1 {id="18_6_1"}

**Ввод**

```python
print(sorted(solve(1, 2, 1)))
```

**Вывод**
```bash
[-1.0]
```

### Пример 2 {id="18_6_2"}

**Ввод**

```python
print(sorted(solve(1, -3, 2)))
```

**Вывод**
```bash
[1.0, 2.0]
```

## Задача 7 {id="1_7"}

Напишите программу, которая запрашивает у пользователя строку с коэффициентами уравнения (степени не выше второй), затем печатает корни уравнения.

Коэффициенты уравнения вводятся в одну строку в порядке от наибольшей степени неизвестной к свободному члену, через пробел. Их количество заранее неизвестно: от 3 до 1 коэффициентов – для квадратного уравнения, линейного уравнения и уравнения, не зависящего от x вовсе – аналогично прошлым частям этой задачи.

Ответ выводится на экран так же, в одну строку через пробел.

При решении задачи используйте написанную в прошлой задаче функцию `solve(*coefficients)`.
Обратите внимание, что функции `solve` и `print` могут принимать списки аргументов различной длины. Благодаря этому вам не потребуется разбирать случаи различного числа коэффициентов и различного числа корней, а решение можно записать буквально в одну строку.



### Пример 1 {id="18_7_1"}

**Ввод**

```python
1 2 1
```

**Вывод**
```bash
-1
```

### Пример 2 {id="18_7_2"}

**Ввод**

```python
1 -3 2
```

**Вывод**
```bash
1 2
```