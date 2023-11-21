#  Отмена изменений в рабочей директории

Одна из ключевых возможностей Git — это откат любых сделанных изменений буквально одной командой. Такое практически невозможно сделать без использования системы контроля версий — только если помнить все изменения наизусть. В этом уроке мы поговорим про откат изменений, которые сделаны в рабочей директории, но еще не попали в коммит.

Отдельно отметим, что откат незакоммиченных изменений безвозвратен. Не существует никакой физической возможности получить эти изменения обратно, поэтому будьте крайне осторожны.

## Неотслеживаемые файлы

Это самая простая ситуация. Представьте, что вы добавили новые файлы в репозиторий и поняли, что они вам не нужны.

В этом случае можно выполнить очистку:

```bash
mkdir one
touch two

git status

On branch main
Your branch is up to date with 'origin/main'.

# Пустые директории в Git не добавляются в принципе
# Физически директория one находится в рабочей директории,
# но при этом ее нет в Git, поэтому Git игнорирует ее
Untracked files:
  (use "git add <file>..." to include in what will be committed)
    two

# Выполняем очистку. Команда удалит все незакоммиченные изменения
# -f – force, -d – directory
git clean -fd

Removing one/
Removing two
```

Забавный факт: про эту команду знает не так много программистов. Используя ее, вы можете удивить даже опытных коллег.

## Измененные файлы в рабочей директории

Для отмены изменений в таких файлах используется команда ```git restore```. Причем Git сам напоминает об этом при проверке статуса:

```bash
echo 'new text' > INFO.md
git status

On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  # Ниже написано, как отменить изменение
  (use "git restore <file>..." to discard changes in working directory)
    modified:   INFO.md

# Отменяем
git restore INFO.md
```

## Изменения, подготовленные к коммиту

С файлами, подготовленными к коммиту, можно поступить по-разному. Первый вариант — отменить изменения совсем, второй — отменить только индексацию, не изменяя файлы в рабочей директории. Второе полезно в том случае, если изменения нужны, но мы не хотим их коммитить сейчас:

```bash
echo 'new text' > INFO.md
git add INFO.md
git status

On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
    modified:   INFO.md
```

И здесь снова помогает Git. При выводе статуса он показывает нужную команду для перевода изменений в рабочую директорию:

```bash
git restore --staged INFO.md
git status

On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   INFO.md
```

Теперь, если нужно, можно выполнить ```git restore``` и окончательно отменить изменения в выбранных файлах:

[![asciinema](https://asciinema.org/a/aqhyAjyhxnbydoaI2tnTrwXke.png)](https://asciinema.org/a/aqhyAjyhxnbydoaI2tnTrwXke/iframe?cols=130&rows=25)

### Самостоятельная работа
1. Выполните все шаги из урока