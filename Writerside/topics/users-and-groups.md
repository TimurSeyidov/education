# Пользователи и группы

Взаимодействие с операционной системой всегда ведется от какого-то конкретного пользователя, созданного в системе. В этом уроке мы изучим концепцию пользователей и групп. Эта тема нужна, чтобы лучше понять права пользователей, которые мы будем обсуждать далее в курсе.

Тема пользователей и их прав в системе в первую очередь относится к функционированию самой операционной системы. Оболочка лишь предоставляет утилиты, позволяющие анализировать доступы и изменять их.

Команда `whoami` позволяет выяснить имя пользователя:

```bash
whoami

kirill.m
```

## Права пользователей

Абсолютно любой процесс, запускаемый в операционной системе, стартует от имени некоторого пользователя. Соответственно, его возможности по влиянию на файловую систему ограничены **правами пользователя**, от имени которого процесс запущен.

Обратите внимание, что мы говорим не «пользователь запустил процесс», а «процесс запускается от имени пользователя». Дело в том, что присутствие пользователя для запуска необязательно. Работая в командной строке, мы запускаем все сами. Но когда система загружается, то она запускает множество различных процессов автоматически.

Для многих процессов в системе создаются собственные пользователи с ограниченным набором прав.

Команда `ps` (сокращение от *process status*) выводит отчет о работающих процессах. Информацию о том, какой процесс и под каким пользователем запущен, можно получить из вывода `ps aux`:

```bash
ps aux

# Левый столбец — это имя пользователя
root      7717  0.0  0.0   4244  1504 ?        S    10:52   0:00 mpstat 1 3
kirill.m  7718  0.0  0.1  36084  3236 pts/0    R+   10:52   0:00 ps aux
alexand+ 10542  0.0  0.1  21500  2892 pts/1    Ss+  10:10   0:00 -bash
root     11113  0.0  0.1  92796  2596 ?        Ss   08:50   0:00 sshd: kirill.m [priv]
kirill.m 11116  0.0  0.0  45276  1408 ?        Ss   08:50   0:00 /lib/systemd/systemd --user
kirill.m 11119  0.0  0.0  61148  1860 ?        S    08:50   0:00 (sd-pam)
kirill.m 11194  0.0  0.0  92796  1800 ?        S    08:50   0:00 sshd: kirill.m@pts/0
kirill.m 11195  0.0  0.2  21388  4448 pts/0    Ss   08:50   0:00 -bash
root     12195  0.0  0.0      0     0 ?        S    10:13   0:00 [kworker/u30:1]
root     12880  0.0  0.1  92796  2748 ?        Ss   08:55   0:00 sshd: alexander.v [priv]
alexand+ 12883  0.0  0.0  45276  1924 ?        Ss   08:55   0:00 /lib/systemd/systemd --user
alexand+ 12884  0.0  0.0  61148  1860 ?        S    08:55   0:00 (sd-pam)
alexand+ 12920  0.0  0.1  92796  2420 ?        S    08:55   0:00 sshd: alexander.v@pts/1,pts/2
```

Взаимодействие с файловой системой происходит через запуск тех или иных утилит, которые модифицируют, создают или анализируют файловую структуру.

Например, мы запускаем утилиту `touch`. Мы от своего имени стартуем процесс, внутри которого запускается программа `touch`. Эта программа создает файл и делает вас владельцем нового файла.

Кстати, модификация существующих файлов не влияет на владельца — для его смены нужно воспользоваться специальной утилитой. В домашней директории пользователя все принадлежит пользователю:

```bash
ls -la

total 44
drwxr-xr-x 5 kirill.m kirill.m 4096 Aug 29 11:34 .
drwxr-xr-x 8 root     root     4096 Apr 26 10:38 ..
-rw------- 1 kirill.m kirill.m 2540 Aug 30 07:26 .bash_history
-rw-r--r-- 1 kirill.m kirill.m  220 Aug 31  2015 .bash_logout
-rw-r--r-- 1 kirill.m kirill.m 3771 Aug 31  2015 .bashrc
drwx------ 2 kirill.m kirill.m 4096 Mar 30 18:10 .cache
-rw------- 1 kirill.m kirill.m   55 Aug 28 18:49 .lesshst
drwxrwxr-x 2 kirill.m kirill.m 4096 Aug 29 08:35 .nano
-rw-r--r-- 1 kirill.m kirill.m  655 May 16  2017 .profile
-rw-rw-r-- 1 kirill.m kirill.m    0 Aug 29 11:27 renamed-file
drwx------ 2 kirill.m kirill.m 4096 Jan 22  2018 .ssh
-rw------- 1 kirill.m kirill.m  513 Aug 29 08:06 .viminfo
```

Третий столбец в этом выводе — как раз владелец. Единственная запись, которая выбивается из всего списка — это `..`, то есть родительская директория.

Ее владельцем является пользователь `root`, о котором мы позже поговорим. Если хорошо подумать, то это логично, ведь директория `/home` не является собственностью пользователей системы:

```bash
ls -la /home/

total 32
drwxr-xr-x  8 root              root              4096 Apr 26 10:38 .
drwxr-xr-x 23 root              root              4096 Aug 27 06:53 ..
drwxr-xr-x  5 alexander.v       alexander.v       4096 Jan 22  2018 alexander.v
drwxr-xr-x  5 kirill.m          kirill.m          4096 Aug 29 11:34 kirill.m
drwxr-xr-x  4 rakhim            rakhim            4096 Apr 26 10:05 rakhim
drwxr-xr-x  4 rakhim.d          rakhim.d          4096 Apr 26 10:41 rakhim.d
```

Каждый каталог в директории `/home` — это домашний каталог конкретного пользователя. Поэтому они все имеют разных владельцев, как правило, совпадающих с именем директории.

Имя пользователя в системе должно быть уникальным, но его можно менять. Если посмотреть под капот этой системы, то мы увидим, что имя пользователя связано с идентификатором, называемым **UID**. Это число, которое и определяет пользователя.

Если поменяется имя пользователя, но идентификатор UID останется прежним, то все доступы останутся. Если сменится идентификатор, то фактически сменится и пользователь. Соответственно, новый пользователь потеряет доступы к старому аккаунту.

Посмотреть свой идентификатор можно разными способами. Первый способ — с помощью команды `id`:

```bash
id

uid=1002(kirill.m) gid=1002(kirill.m) groups=1002(kirill.m),999(docker)
```

Второй способ связан с просмотром одного важного файла, который выступает основным хранилищем пользователей в *nix-системах. Да, это обычный текстовый файл, как и все остальное:

```bash
cat /etc/passwd

root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
kirill.m:x:1002:1002::/home/kirill.m:/bin/bash
```

![Схема записей в файле /ect/passwd](../images/cli/image_15_1.png)

Кроме имени и идентификатора, здесь указана командная оболочка по умолчанию и домашняя директория пользователя, которую можно поменять. Запись `/usr/sbin/nologin` говорит, что пользователь не может входить в систему. Такие пользователи нужны для запуска программ, у которых ограниченные права — естественно, входить в систему им не нужно.

## Права групп пользователей

Кроме имени, у пользователей *nix-систем есть связанное с ним понятие — **группа**. Она создана для группового доступа к разделяемому (общему) ресурсу — например, файлу.

Например, у нас есть группа разработчиков, которые регулярно заходят на сервер. Им нужно дать одинаковые возможности по управлению определенными файлами. Владелец у файла ровно один, поэтому мы не можем решить этот вопрос через смену владельца. Для этого нужно создать группу и привязать ее к самому пользователю.

Группы, ассоциированные с текущим пользователем, показываются в выводе команды `id`:

```bash
id

uid=1002(kirill.m) gid=1002(kirill.m) groups=1002(kirill.m),999(docker)
```

Здесь группа `kirill.m` считается **основной** — такая группа может быть только одна, и именно в нее входят любые создаваемые файлы от имени текущего пользователя. Кроме основной, пользователь может входить в произвольное число дополнительных групп. То, как это влияет на доступы, мы рассмотрим в одном из следующих уроков.

В любой *nix-системе присутствует специальный пользователь — `root` или **суперпользователь**. Главная его особенность — это идентификатор со значением `0`. Этот пользователь имеет особое значение и может выполнять абсолютно любые действия в системе. У пользователя `root` в файле `/etc/passwd` будет вот такая запись:

![Схема записей в /ect/passwd пользователя root](../images/cli/image_15_2.png)

Крайне не рекомендуем использовать `root` на регулярной основе, и ни в коем случае не входить под ним в систему. Суперпользователь — это прямой доступ ко всему и большая дыра в безопасности системы. Кроме того, через него систему очень легко убить: например, удалить не тот файл или испортить важную конфигурацию, после чего вход в систему станет невозможным.

Несмотря на это, `root` нужен для выполнения некоторых привилегированных действий, которые недоступны обычным пользователям. Об этом мы поговорим в следующем уроке.

### Дополнительные материалы

1. [Подробнее о команде ps](https://www.baeldung.com/linux/ps-command)

### Вопросы для самопроверки

**Какой командой можно узнать идентификатор своего пользователя?**

- `whoami`
- `id`
- `uid`

**В каком файле хранится информация о пользователях?**

- `/etc/passwd`
- Такая информация не предоставляется в открытом доступе
- В домашней директории каждого пользователя

**Для чего нужна группа?**

- Чтобы организовывать совместный доступ к разделяемым ресурсам
- Чтобы было красиво
- Чтобы определять уровень доступа к ресурсу