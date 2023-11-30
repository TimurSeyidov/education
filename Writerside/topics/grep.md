# Grep

Слово «грепать» входит в топ самых популярных терминов, используемых разработчиками. Оно происходит от одноименной консольной утилиты `grep` (сокращение от *global regular expression print*). Эта утилита выполняет поиск определенного текста по файлу или файлам.

В этом уроке мы научимся грепать и разберемся в особенностях этого процесса.

Для разработчиков «грепать» — то же самое, что гуглить для активных пользователей интернета. Как правило, грепают файлы с исходным кодом или логи во время отладки:

```bash
man grep

SYNOPSIS
grep [OPTIONS] PATTERN [FILE...]
grep [OPTIONS] [-e PATTERN]...  [-f FILE]...  [FILE...]
```

Рассмотрим этот пример подробнее:

- `PATTERN` — это то, что мы хотим найти. Это может быть конкретная строчка или определенный шаблон с [регулярными выражениями](https://ru.wikipedia.org/wiki/Регулярные_выражения
- `FILE` — путь до файла, в котором нужно искать

Посмотрите на еще один пример:

```bash
# Поиск всех строк в файле .bashrc, в которых встречается слово aliases
grep aliases .bashrc

# enable color support of ls and also add handy aliases
# some more ls aliases
# ~/.bash_aliases, instead of adding them here directly.
if [ -f ~/.bash_aliases ]; then
. ~/.bash_aliases
```

В примере выше утилита `grep` нашла пять строк. Найденные строчки выводятся на экран в том же порядке, в котором они встречаются в исходном файле.

В некоторых ситуациях нам нужно увидеть не только саму строку, но и текст вокруг нее. Количество выводимых соседних строк регулируется тремя опциями:

- Количество отображаемых строк до искомой строки — `-B` или `--before-context`
- Количество отображаемых строк после искомой — `-A` или `--after-context`
- Количество отображаемых строк до и после искомой строки — `-C` или `--context`

Изучим пример использования `-C` со значением `1`. Это значит, что для каждой найденной строки будет выведена одна строка выше и одна строка ниже:

```bash
grep -C 1 aliases .bashrc

# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
--

# some more ls aliases
alias ll='ls -alF'
--
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
. ~/.bash_aliases
fi
```

[![asciinema](https://asciinema.org/a/o1rPb82PaRkEa6OKkVzGLO4Wz.png)](https://asciinema.org/a/o1rPb82PaRkEa6OKkVzGLO4Wz/iframe?preload=1&cols=120&rows=17)

Иногда мы не знаем, в каком файле находится то, что мы ищем. При этом мы можем знать директорию, в которой лежит этот файл.

В такой ситуации нужно сделать два изменения:

1. Добавить опцию `-r` — она указывает, что надо искать внутри директории. Обратите внимание, что поиск идет рекурсивно, то есть с включением всех поддиректорий
2. Указать путь до директории, а не файла

Попробуем применить утилиту `grep` с опцией `-r`:

```bash
grep -r bashrc .

./.profile:    # include .bashrc if it exists
./.profile:    if [ -f "$HOME/.bashrc" ]; then
./.profile: . "$HOME/.bashrc"
./.bash_history:du -sh .bashrc
./.bash_history:stat .bashrc
./.bash_history:stat -h .bashrc
./.bash_history:file .bashrc
./.bash_history:stat .bashrc
./.bash_history:cat .bashrc
./.bashrc:# ~/.bashrc: executed by bash(1) for non-login shells.
./.bashrc:# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
./.bashrc:# sources /etc/bash.bashrc).
```
При таком поиске в выводе указывается файл, в котором была найдена строка. Если добавить опцию `n`, то дополнительно отобразится номер строки:

```bash
grep -rn bashrc .

./.profile:13:    # include .bashrc if it exists
./.profile:14:    if [ -f "$HOME/.bashrc" ]; then
./.profile:15:  . "$HOME/.bashrc"
./.bash_history:56:du -sh .bashrc
./.bash_history:57:stat .bashrc
./.bash_history:58:stat -h .bashrc
./.bash_history:60:file .bashrc
./.bash_history:61:stat .bashrc
./.bash_history:63:cat .bashrc
./.bashrc:1:# ~/.bashrc: executed by bash(1) for non-login shells.
./.bashrc:109:# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
./.bashrc:110:# sources /etc/bash.bashrc).
```

### Дополнительные материалы

1. [Поиск файлов](https://ru.wikipedia.org/wiki/Find)

### Вопросы для самопроверки

**Что означает фраза «грепать файл»?**

- Выводить на экран содержимое файла
- Искать в файле все строчки, соответствующие шаблону
- Искать файл
- Удалять файл

**Что будет выведено на экран при выполнении команды `grep -C 3 alias ~/.bashrc`?**


- Результат поиска, сгруппированный по три строки
- Строки, содержащие `alias` с тремя соседними строками до и после нее
- Три первые строки из файла *.bashrc*, содержащие `alias`
- Список искомых строк

**Где будет произведен поиск, если указана команда grep -r myname?**

- В первом найденном файле
- В файлах текущей директории и всех вложенных поддиректориях
- В файлах текущей директории
- В скрытых файлах текущей директории