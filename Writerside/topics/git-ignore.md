# Игнорирование файлов

В процессе работы над любым проектом в директории с кодом создаются файлы, которые не являются частью исходного кода. Все эти файлы можно условно разделить на несколько групп:

- Инструментарий
  - Служебные файлы, добавляемые операционной системой — например, *.DS_Store* в MacOS
  - Конфигурационные и временные файлы редакторов — например, *.idea* или *.vscode*
- Временные файлы
  - Логи — в них содержится полезная информация для отладки, которая собирается во время запуска и работы приложения
  - Кеши — файлы, которые нужны для ускорения разных процессов
- Артефакты
  - Результаты сборки проекта — например, после компиляции или сборки фронтенда
  - Зависимости, которые устанавливаются во время разработки — например, *node_modules* или *vendor*
  - Результаты выполнения тестов — например, информация о покрытии кода тестами

Все это в обычной ситуации не должно попадать в репозиторий. В этом уроке вы узнаете, как проигнорировать эти файлы.

Как правило, эти файлы не несут никакой пользы с точки зрения исходного кода. Они создаются:

- Автоматически (кеши, логи)
- По запросу (например, скачиваются зависимости или собирается проект)

Главная проблема с этими файлами в их постоянном изменении — особенно при очень больших размерах проекта. Если добавлять их в репозиторий, то практически в каждом коммите будут не только изменения исходного кода, но и пачка изменений в этих файлах. Читать историю таких коммитов крайне сложно.

Git позволяет гибко настраивать игнорирование определенных файлов и директорий. Делается это с помощью файла **.gitignore**, который нужно создать в корне проекта. В этот файл с помощью текстового редактора добавляются имена файлов и директорий, которые надо игнорировать:

```
# В этом файле можно оставлять комментарии
# Имя файла .gitignore
# Файл нужно создать самостоятельно

# Каждая строчка — это шаблон, по которому происходит игнорирование

# Игнорируем файл в любой директории проекта
access.log

# Игнорируем директорию в любой директории проекта
node_modules/

# Игнорируем каталог в корне рабочей директории
/coverage/

# Игнорируем все файлы с расширением sqlite3 в директории db
# При этом не игнорируются такие же файлы внутри любого вложенного каталога в db
# Например, /db/something/lala.sqlite3
/db/*.sqlite3

# Игнорировать все .txt файлы в каталоге doc/ на всех уровнях вложенности
doc/**/*.txt
```

Git поддерживает игнорирование файлов, но сам его не настраивает. Для игнорирования файлов и директорий, программист должен создать файл .gitignore в корне проекта и добавить его в репозиторий. Пример вы можете посмотреть [здесь](https://github.com/Hexlet/hexlet-cv/blob/main/.gitignore).

Продолжим работать с *.gitignore*:

```bash
touch .gitignore
# Добавляем в файл правила игнорирования по примеру выше
git add .gitignore
git commit -m 'update gitignore'
```

Как только *.gitignore* создан и в него добавлен какой-то файл или директория, игнорирование заработает автоматически. Все новые файлы, попадающие под игнорирование, не отобразятся в выводе команды ```git status```.

Иногда бывает такое, что программист случайно уже добавил в репозиторий файл, который нужно проигнорировать. В этой ситуации недостаточно обновить правила игнорирования. Дополнительно придется удалить файл или директорию из Git с помощью ```git rm``` и закоммитить.

### Самостоятельная работа

1. Добавьте файл *.gitignore* в проект
2. Добавьте файл *INFO.md* в список игнорируемых файлов
3. Удалите файл *INFO.md* из репозитория
4. Создайте файл *INFO.md* и убедитесь в том, что ```git status``` его не отображает
5. Залейте изменения на GitHub

### Дополнительные материалы

1. [Коллекция полезных gitignore для всех ситуаций](https://github.com/github/gitignore)
2. [Инструкция от Atlassian по gitignore](https://www.atlassian.com/ru/git/tutorials/saving-changes/gitignore)