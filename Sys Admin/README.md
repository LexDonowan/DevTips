### Полный cheat-sheet комманд:
---
http://www.f-notes.info/linux:linux_command

MySQL шпаргалки
https://habrahabr.ru/post/105954/

---

**Смена прав на файлы и директории**

```
sudo find /usr/share/nginx/www/madhog/amper/ -type d -exec chmod 755 {} \;
sudo find /usr/share/nginx/www/madhog/amper/ -type f -exec chmod 644 {} \;
```
---
Рекурсивная смена прав
`$ sudo chmod -R 755 /usr/share/nginx/www/madhog/amper/`

Смена пользователя
`$ sudo chown -R -v user1 /var/www/`

Сменить владельца и группу владельца файла
`$ sudo chown -R -v user1:user1 /var/www/`

Сменить группу-владельца файла file1 на group1
`$ chgrp group1 file1`

рекурсивное удаление файлов и каталогов
`$ rm -r examples/`

удалить директорию с именем 'dir1' и рекурсивно всё её содержимое
`$ rm -rf dir1`

переименовать или переместить файл или директорию
`$ mv dir1 new_dir`

Добавить пользователя в группу
`$ usermod -a -G group user`

Поменять первичную группу пользователю
`$ usermod -g group user`

Чтобы занести пользователя в группу:
`$ gpasswd -a [user] [group]`

Вывод пользователя из группы:
`$ gpasswd -d [user] [group]`

И для того, чтобы удалить группу, введем следующие:
`$ groupdel [group]`

---
`$ sudo service vsftpd restart`

`$ sudo nano /etc/vsftpd.conf`


Upgrade:
`$ sudo apt-get update; sudo apt-get upgrade`

Restart:
`$ sudo shutdown -r now`

Hard restart:
`$ sudo reboot`

Shutdown:
`$ sudo shutdown -h now`

Свернуть / развернуть nano
`ctrl-z` и `bg`

apache config
`/etc/apache2/sites-available/`

apache logs
`/var/log/apache2/`

---
поиск файлов

```
$ find -name '*.php' -print0 | xargs -0 grep -rli '${';
$ find -name '*.php' -print0 | xargs -0 grep -rli preg_replace.*\/e;
$ find -name '*.php' -print0 | xargs -0 grep -rli ';}}';
$ find -name '*.php' -print0 | xargs -0 grep -rli "<?php if (@";
$ find -name '*.php' -print0 | xargs -0 grep -rliE '/(\$\{(.*)eval)|(eval(.*)\$\{)/gmi';
$ find -name '*.php' -print0 | xargs -0 grep -rliE '/(\$t(.*)\$GLOBALS)|(\$GLOBALS(.*)\$t)/gmi';
$ find -name '*.php' -print0 | xargs -0 grep -rliE '/<?php(.*)\$\{/gmi';
```
---

Создать архив:
`$ tar czf <имя_файла.tar.gz <имя_директории>`
`$ xz -9 -c big3.txt >> big3.txt.xz`

распаковать архив:
`$ tar xzf <имя_файла.tar.gz <имя_директории>`
`$ gzip -d <имя_файла.gz>`

---
Изменить текст приветствия
`$ vi /etc/motd`

---

### Установка локали

Проверяем, какая локаль сейчас установлена в системе:
`$ locale -a`

Проверяем, поддерживается ли русская локаль
`$ less /usr/share/i18n/SUPPORTED | grep ru_RU`

Если нет, устанавливаем
`$ sudo apt-get install language-pack-ru-base`

Устанавливаем русскую локаль в систему
`$ sudo locale-gen ru_RU.CP1251`

Обновляем настройки локали в системе:
`$ sudo dpkg-reconfigure locales`

### Посмотреть версию Linux

`cat /proc/version`

`cat /etc/*release`

