# Контрольная работа

## Поиск в логах

В директории `logs` находится файл `access.log`, который содержит логи подключения к серверу. Вам нужно найти в этом файле предполагаемые попытки взлома:

```text
02.01.2021 05:33:50 localhost ssh: denied wrong password from 156.78.198.42
02.01.2021 06:28:29 localhost ssh: successfully authenticated from 108.117.162.5
02.01.2021 07:27:32 localhost ssh: successfully logged out from 254.199.78.117
02.01.2021 11:24:56 localhost ssh: connection dropped by timeout from 227.65.89.157
02.01.2021 11:59:29 localhost ssh: denied wrong password from 252.175.99.156
02.01.2021 12:17:44 localhost ssh: connection dropped by timeout from 50.26.154.246
```

Запишите в файл `solution` команду, которая находит в файле `access.log` строки с подстрокой "**denied wrong password**". Команда должна сортировать их в обратном порядке и выводит на экран пять самых свежих записей.

## ПриглашениеPrompt Statement

Вы уже много раз видели в терминале, как выглядит приглашение командной строки для ввода новых команд. Например:

```bash
/usr/src/app$
```

Переменная `PS1` определяет, как будет выглядеть это приглашение. В этом испытании вам нужно определенным образом его изменить.

### Задание

Запишите в файл `solution` команду, которая глобально меняет значение переменной окружения `PS1` так, чтобы приглашение выглядело следующим образом:

```bash
> tirion@app$
```
Здесь `tirion` – это текущий пользователь, а `app` – текущая рабочая директория

Посмотрим текущую рабочую директорию:

```bash
> tirion@app$ pwd
/usr/src/app
```

Узнаем, под каким пользователем мы выполнили вход в систему:

```bash
> tirion@app$ whoami
tirion
```

### Подсказки
- [Controlling the Prompt](https://www.gnu.org/software/bash/manual/html_node/Controlling-the-Prompt.html)
- Выводите текст как есть, без цветового оформления


