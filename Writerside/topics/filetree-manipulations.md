# Манипулирование файловой структурой

Файловую структуру можно не только просматривать, но и всячески модифицировать. В прошлом уроке мы научились создавать файлы через перенаправление потоков, а сейчас обсудим, как это делать напрямую.

Учтите, что возможность модифицировать файловую структуру завязана на **правах пользователя**. Если у вас нет соответствующих прав, вы получите ошибку доступа. Место, где вы гарантированно можете экспериментировать — ваша домашняя директория. Внутри нее все доступно на запись.

Для примеров этого урока мы создали каталог `test` в домашней директории. То есть все демонстрируемые команды выполняются в директории по адресу: `~/test.`

## Основные команды

Для создания файлов принято использовать утилиту `touch`. Основная задача этой утилиты — поменять время последнего доступа к файлу, но она обладает побочным эффектом.

Если файла не существует, то он будет создан — именно поэтому ее используют для создания файлов, хотя это не основное предназначение:

```bash
# В текущей директории создается пустой файл
touch empty-file
```
[![asciinema](https://asciinema.org/a/EK9l2zlzVa8CsHYA9SzTJTrKZ.png)](https://asciinema.org/a/EK9l2zlzVa8CsHYA9SzTJTrKZ/iframe?preload=1&cols=120&rows=17)

Удалить файл можно командой rm (сокращение от remove):

```bash
rm empty-file
```

[![asciinema](https://asciinema.org/a/z9BTi5w3UOy0Fp1misw630u38.png)](https://asciinema.org/a/z9BTi5w3UOy0Fp1misw630u38/iframe?preload=1&cols=120&rows=17)

В *nix-системах не существует понятия «переименовать файл». Переименование всегда равносильно перемещению, которое выполняется командой mv (move):

```bash
touch file
mv file renamed-file
```

[![asciinema](https://asciinema.org/a/nHCJLgmnw0HoOKp4Sh0Yp9m6k.png)](https://asciinema.org/a/nHCJLgmnw0HoOKp4Sh0Yp9m6k/iframe?preload=1&cols=120&rows=17)

Для копирования файлов и директорий используется утилита `cp` (copy).

У этой утилиты два аргумента:

- Имя источника (откуда копируем)
- Имя приемника (куда копируем)

Посмотрим, как эта утилита работает на практике:

```bash
cp renamed-file renamed-file-copy
```

[![asciinema](https://asciinema.org/a/Pag7yOALRusxRXNYL9n7Ef1I0.png)](https://asciinema.org/a/Pag7yOALRusxRXNYL9n7Ef1I0/iframe?preload=1&cols=120&rows=17)

Для копирования директории нужно добавить флаг `-r` (*recursive*).

Все эти и последующие утилиты работают с файлами и директориями, расположенными в любом месте файловой системы. Поэтому вы всегда можете передать любой путь: `touch /tmp/tempfile`.

Утилиты для работы с директориями частично отличаются. Создание директории выполняется командой `mkdir` (*make directory*):

```bash
mkdir my-dir
```

[![asciinema](https://asciinema.org/a/o9hWi8qsQiLddJKGDP4WXHy84.png)](https://asciinema.org/a/o9hWi8qsQiLddJKGDP4WXHy84/iframe?preload=1&cols=120&rows=17)

По умолчанию эта команда не создает вложенных директорий:

```bash
mkdir one/two/three
mkdir: cannot create directory ‘one/two/three’: No such file or directory
```

[![asciinema](https://asciinema.org/a/TvPdYV7ZBKp3TLzbDXjWJrkig.png)](https://asciinema.org/a/TvPdYV7ZBKp3TLzbDXjWJrkig/iframe?preload=1&cols=120&rows=17)

В такой ситуации придется создавать каждую директорию отдельно. Но есть и другой способ — воспользоваться флагом `-p` (`--parents`), который создает директории рекурсивно:

```bash
mkdir -p one/two/three
```

[![asciinema](https://asciinema.org/a/795AjrJ5Mo52KbzIxdZa0npzB.png)](https://asciinema.org/a/795AjrJ5Mo52KbzIxdZa0npzB/iframe?preload=1&cols=120&rows=17)

Удаление директорий выполняется той же командой, что и удаление файлов, но без флагов оно выдает предупреждение:

```bash
rm my-dir/
rm: cannot remove 'my-dir/': Is a directory
```

[![asciinema](https://asciinema.org/a/qYUXYAB52YDBVQAV8V1EGdARg.png)](https://asciinema.org/a/qYUXYAB52YDBVQAV8V1EGdARg/iframe?preload=1&cols=120&rows=17)

Чтобы не было ошибки, нужно добавить флаг `-r` (*recursion*). Он включает режим рекурсивного удаления содержимого директорий. Другими словами, идет просмотр содержимого во всех вложенных директориях и поддиректориях до самого конца:

```bash
rm -r my-dir
```

[![asciinema](https://asciinema.org/a/Jz48g4nO2bQttoiSVXfV31vuP.png)](https://asciinema.org/a/Jz48g4nO2bQttoiSVXfV31vuP/iframe?preload=1&cols=120&rows=17)

Теперь представим такую ситуацию: внутри директории содержатся файлы или директории с ограниченными правами доступа, например, доступные только для чтения. В таком случае команда rm начнет задавать вопрос по каждому из них, нужно ли удалять файл.

Если вы точно уверены, что удалить нужно все, добавьте флаг `-f` (`--force`). Этот флаг позволяет игнорировать несуществующие файлы и не запрашивать подтверждение на удаление. В таком случае `rm` удалит всю директорию без вопросов:

```bash
rm -rf one
```

[![asciinema](https://asciinema.org/a/C8ioOzvimAT9NHHtj49LROikL.png)](https://asciinema.org/a/C8ioOzvimAT9NHHtj49LROikL/iframe?preload=1&cols=120&rows=17)

### Вопросы для самопроверки

**Какой командой создается пустой файл?**

- `create`
- `cp`
- `file`
- `touch`

**Подставьте команду, которая поможет переименовать файл:**

`____ source.png dest.png`

**Добавьте флаг, который поможет удалить директорию:**

`rm ____ mydir`