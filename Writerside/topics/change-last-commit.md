# Изменение последнего коммита

Довольно часто разработчики делают коммит и сразу замечают, что забыли добавить часть файлов через ```git add```. Оставшуюся часть изменений можно добавить в следующем коммите.

Однако есть еще один метод. Если изменения еще не были отправлены во внешнюю систему, их можно добавить к текущему коммиту. Для этого во время коммита используется флаг ```--amend```:

```bash
echo 'experiment with amend' >> INFO.md
echo 'experiment with amend' >> README.md
git add INFO.md
# Забыли сделать подготовку README.md к коммиту
git commit -m 'add content to INFO.md and README.md'

[main 256de25] add content to INFO.md and README.md
 1 file changed, 1 insertion(+)

git status

On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   README.md

# Увидели, что забыли добавить файл
# Добавляем

git add README.md
git commit --amend
# После этой команды откроется редактор, ожидающий ввода описания коммита
# Здесь можно поменять сообщение или выйти из редактора, оставив старое

[main d96151a] add content to INFO.md and README.md
 Date: Sat Sep 26 16:02:07 2020 -0400
 2 files changed, 2 insertions(+)

git status

On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

Фактически, ```--amend``` не добавляет изменения к существующему коммиту. Этот флаг вызывает отмену последнего коммита через ```git reset``` и создание нового коммита с обновленными данными. Из-за этого в истории коммитов виден только один коммит, несмотря на то, что команда ```git commit``` была запущена дважды (первый раз - для неправильного коммита).

Чтобы избежать открытия редактора для ввода нового описания коммита при использовании команды ```git commit --amend```, можно добавить опцию ```--no-edit```. Это предотвратит изменение описания коммита:

[![asciinema](https://asciinema.org/a/fBl8nyMlVyfIeX4aoa7PK16ja.png)](https://asciinema.org/a/fBl8nyMlVyfIeX4aoa7PK16ja/iframe?cols=130)

### Самостоятельная работа
1. Выполните все шаги из урока
2. Залейте изменения на GitHub

### Дополнительные материалы
1. [Перезапись истории](https://git-scm.com/book/ru/v2/Инструменты-Git-Перезапись-истории)