#### Bash

Ctrl + Alt + T - открыть терминал из графической оболочки

```bash
# Команды
$ ls              # содержимое каталога
$ ls | less       # постраничный вывод Space - вперед, b - назад, q - выход
$ less            # просмотр содержимого файла с пейджингом
$ ls -a           # показать скрытые файлы
$ ls -aF          # показать каталоги и скрытые файлы
$ ls -l           # показать каталоги и файлы с подробным описанием

$ cd              # сменить каталог
$ cd -            # возврат в предыдущую директорию

$ mkdir           # создать каталог
$ rmdir           # удалить каталог

$ which tclsh    # узнать, где лежит программа tclsh

$ pwd             # показать путь текущего каталога
$ touch           # создать файл
$ tree            # выводит сведения о директориях в древовидном формате

$ rm -r           # удалить (ключ -r рекурсивно для каталогов)
$ mv              # переименование или перемещение файла

$ xxd filename    # отобразить файл в HEX
$ cat             # просматривает файлы, с её помощью можно создавать копии файлов, присоединять содержимое одних файлов к другим
$ echo            # выводит передаваемые ей данные на экран
$ echo "$(< README.txt)" # Выводит на экран содержимое файла
$ grep            # позволяет выполнять поиск строк
$ tail            # выводит 10 последних строк файла
$ ps -A | head -5 # выведет первые 5 строчек отчёт, включая заголовок таблицы
$ ps -A | tail -5 # выведет последние 5 строчек отчёт
$ ps -A | grep "sys" #выведет все процессы с вхождениями sys
$ pidof proc_name    # узнать PID по имени процесса

$ ln -s /path/to/file linkname    # создание символической ссылки


$ chmod +x filename               # разрешить исполнение файла
$ chmod 755 filename              # разрешить исполнение файла

$ ./main &        # запуск программы в фоновом режиме

# экранирование пробелов (3 способа)
$ mv Photos\ from\ Paris Photos_from_Paris
$ mv 'Photos from Paris' Photos_from_Paris
$ mv "Photos from Paris" Photos_from_Paris

$ history | less                  # показывает историю введенных команд
$ !1937                           # выполнит команду сохраненную в истории под номером 1937
$ !!                              # выполнит последнюю сохраненную в истории команду
$ echo !:1                        # вывести второе слово из последней команды
$ echo !1937:1                    # вывести второе слово из команды номер 1937

$ mount            # Показывает все точки монтирвания



$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout key.pem -out cert.pem      # генерирует файлы ключей HTTPS
$ adduser goryachev            # создать пользователя
$ usermod -aG sudo goryachev   # добавить пользователя в группу sudo
$ su - goryachev  # Сменить пользователя
$ su -            # Сменить пользователя на root
$ exit            # Выйти из текущего пользователя

$ ps              # показать список процессов
$ ps -A           # показать все процессы
$ sudo useradd -m username    # создать пользователя вместе с домашним каталогом
$ sudo passwd username        # задать пароль пользователя
$ sudo service lightdm restart          # перезапуск x-server
$ sudo dpkg -i NOMBRE-DEL-PAQUETE.deb   # установка из пакета deb скачанного с сайта
$ echo "Hello" > /dev/tty         # вывод на стандартный терминал

$ kill -9 25609                   # убить процесс (отправит процессу сигнал 9)
$ kill -KILL 25609                # убить процесс (отправит процессу сигнал 9)
$ killall ChShell                 # убить все процессы с именем ChShell

$ date                        # показывает системное время

$ diff myfile1 myfile2 > changes.diff        # сравнивает два файла и разницу записывает в третий


$ dd if=uboot-allwinner/spl/sun4i-spl.bin of=/dev/sdb bs=1024 seek=8 conv=notrunc        # Копируем SPL (boot0)  первичный загрузчик на SD
$ sudo dd if=/dev/zero of=file.img bs=1M count=512                                       # Создает файл заполненный нулями размером 512 Мб (можно случайными числами /dev/random)
$ sync                                      # Запускает синхронизацию, чтобы убедиться, что буферы записи очищены

$ sudo mount -v ~/disk.img /mnt/            # Монтирование файловой системы
$ sudo umount /mnt                          # Размонтирование файловой системы
$ sudo fdisk -l /dev/sdb                    # Вывести все разделы на диске
$ sudo fdisk /dev/sdb                       # Разметка диска в интерактивном режиме

# Прежде чем пытаться изменить файловую систему, нужно размонтировать ее с помощью команды umount
$ mkfs.vfat /dev/sdb1 -n sun4i-boot         # Форматирование раздела в FAT16
$ mkfs.ext4 /dev/sdb2 -L sun4i-rootfs       # Форматирование раздела в ext4
$ sudo file -sL /dev/sdb1                   # Узнать тип файловой системы



$ ip a           # узнать ip-адрес
$ ip -br a       # показать ip-адреса всех устройств
$ hostname -I    # узнать ip-адрес
# Вывести список всех ip, которые пингуются
$ echo 192.168.0.{1..254}|xargs -n1 -P0 ping -c1|grep "bytes from"
$ arp -a         # выводит таблицу соответствия mac-адресов и ip-адресов

# тест запустит 12 потоков, 1000 одновременных соединений и будет работать в течение 30 секунд
$ wrk -t12 -c1000 -d30s http://localhost:8080
# узнать какой процесс занял порт
$ sudo lsof -i :8080

$ uname -a       # узнать версию ядра Linux

$ lscpu             # информация о процессоре
$ cat /proc/cpuinfo # информация о процессоре
$ free -h           # информация о памяти
$ cat /proc/meminfo # информация о памяти
$ cat /proc/devices # выводит список драйверов символьных и блочных устройств
$ ip link show      # выводит список сетевых устройств
$ lsusb             # выводит usb устройства
$ lspci             # выводит pci устройства
$ lsblk             # выводит список дисков
$ sudo lshw         # выводит информацию о системе

$ cat /dev/cdrom    # проверить наличие диска в CD-ROM
$ eject             # открыть CD-ROM

$ ping -c 3 google.com       # проверка подключения к интернету
$ curl -I https://google.com # проверка подключения к интернету

# для подключения к usb-serial
$ sudo chmod 666 /dev/ttyUSB0
$ putty
# добавить один раз пользователя в группу, чтобы всегда были права на com-порт
$ sudo usermod -a -G dialout $USER
$ sudo reboot       # перезагрузка сеанса

$ ls -l /dev/ttyUSB0                 # узнать права на usb-serial
$ stty -a -F /dev/ttyUSB0            # вывод параметров com-порта
$ stty < /dev/ttyUSB0                # узнать скорость com-порта
$ stty -F /dev/ttyUSB0 115200        # установить скорость com-порта

# послать в com-порт
$ echo "HELLO" > /dev/ttyUSB0
$ echo  -ne '\x23\x02\x01\x00\x50\x01\r' > /dev/ttyUSB0
# прочитать com-порт
$ cat /dev/ttyUSB0
# Устанавливаем скорость 115200 бод, 8 битов данных, стоп бит, без проверки четности (режим 8N1):
$ stty -F /dev/ttyUSB0 115200 cs8 -cstopb -parenb
# Сохранить параметры порта для последующего восстановления:
$ stty -g -F /dev/ttyUSB0 > save.txt
$ stty --save /dev/ttyUSB0 > save.txt
# Считываем сохраненные параметры:
$ stty -F /dev/ttyUSB0 `cat save.txt`

# отображает шестнадцатеричные данные
$ hexdump -C /dev/tty
$ hexdump -C file.txt

$ dmesg -w                # отображает события ядра

$ groups                  # в каких группах состоит пользователь
$ compgen -g              # какие есть группы вообще
$ sudo usermod -a -G tty yourname    # добавить пользователя в группу
$ newgrp groupname        # создать группу

# Просмотреть открытые сетевые порты
$ sudo apt install net-tools
$ sudo netstat -tulpn

# Архивирование файлов
$ tar -cvf archive.tar /path/to/files
# Разархивирование файлов
$ tar -xvf archive.tar.gz
```
Чтобы освободить место в коневой файловой системе
```bash
# Очистить кеш /var/cache/apt/archives 
$ sudo apt-get clean    

# Удаляет библиотеки и пакеты, которые были установлены автоматически для создания зависимостей устанавливаемого пакета
$ sudo apt-get autoremove

# Очистка логов (например, старше 3-х дней)
$ journalctl --disk-usage
$ sudo journalctl --vacuum-time=3d

# Таким образом файлы /var будут лежать в разделе /home, а из корня на /home/var будет вести симлинк. Выберите вместо /var то, что у вас больше весит, но лучше не /bin и не /usr
$ mkdir /home/var
$ sudo cp -R /var/* /home/var
$ rm -R /var
$ ln -s /home/var /var
```
Горячие клавиши:
```
Ctrl+H            # показать скрытые папки и файлы в окне
Tab               # автодописывание имени файла
Ctrl+C            # сбросить (очистить) набираемую строку
Ctrl+C            # принудительное завеошение программы
Ctrl+\            # принудительное завеошение программы
Ctrl+R            # поиск по строке
Ctrl+D            # ситуация "конец файла"
Ctrl+Ins          # копировать в буфер обмена
Shift+Ins         # вставить из буфера обмена
```
SSH
```bash
# Подключение
$ ssh  root@192.168.0.254

# При ошибке: Unable to negotiate with 192.168.0.254 port 22: no matching key exchange method found. Their offer: diffie-hellman-group1-sha1,diffie-hellman-group14-sha1
# Добавить в файл ~/.ssh/config строки:
Host 192.168.0.254
    HostkeyAlgorithms ssh-dss,ssh-rsa
    KexAlgorithms +diffie-hellman-group1-sha1

# Копирование файла по SSH
$ scp file_name user@172.18.0.1:~/WORK/
# Копирование каталога по SSH
$ scp -r catalog_name user@172.18.0.1:~/WORK/
# Копирование с удаленного компьютера на мой
$ scp user@172.18.0.1:~/WORK/file_name ~/WORK/
```
Создание iso-образа с диска:
```bash
$ dd if=/dev/cdrom of=win7.iso bs=2048
$ sudo mount -o loop win7.iso /media/ 
```
Создание нового пользователя:
```bash
$ sudo useradd -m -s /bin/bash -c "tarasov" tarasov
$ sudo passwd tarasov
$ sudo usermod -aG sudo tarasov
$ su - tarasov
```
Пример bash-скрипта:
```bash
#!/bin/sh

# объявление переменных
DIR=Photoalbum/2015
I=10

# арифметические команды
I=$(( $I + 7 ))

# логическая связка && ||
[ "$1" = "" ] && { echo "No dir name"; exit 1; }

# команда test (вместо слова test служит '[', а ']' - параметр команды, поэтому нужны пробелы)
# команда проверяет логическую истинность результата выполнения команды
[ -f "file.txt" ]         # существует ли файл с именем file.txt
[ "$I" -lt 25 ]           # значение переменной I меньше 25
[ "$A" = "abc" ]          # значение переменной A является строкой abc
[ "$A" != "abc" ]         # значение переменной A не является строкой abc

# конструкции ветвления
if [ -f "file.txt" ]; then
    cat "file.txt"
else
    echo "File not found"
fi

# конструкции ветвления без использования [ ]
if test -f "file.txt" ; then
    cat "file.txt"
else
    echo "File not found"
fi

# любая команда может быть условием
if mkdir new_dir ; then
    echo "Directory created"
else
    echo "Failed to make new directory"
fi

# цикл while
I=1
while [ $I -le 100 ]; do
    echo $I
    I=$(( I + 1 ))
done

# цикл for
for C in red orange yellow; do
    echo $C
done


echo "Количество параметров " $#

mkdir $DIR/$1
mount /mnt/flash
cp /mnt/flas/dcim/* $DIR/$1
umount /mnt/flash
```
Протоколирование:
```bash
$ script my_protocol.txt      # запуск протоколирования в файл my_protocol.txt
$ ls                          # серия команд в протоколе
$ pwd                         # серия команд в протоколе
$ [Ctrl+D]                    # завершение протоколирования
```
Перенаправление потоков ввода-вывода:
```bash
$ cmd1 > file1            # запустить программу cmd1, направив ее вывод в файл file1; если файл существует, он будет перезаписан с нуля, если не существует - будет создан
$ cmd1 >> file1           # запустить программу cmd1, дописав ее вывод в конец файла file1; если файла не существует, он будет создан
$ cmd2 < file2            # запустить программу cmd2, подав ей содержимое файла file2 в качестве стандартного ввода; если файла не существует, произойдет ошибка
$ cmd3 > file1 < file2    # запустить программу cmd3, перенаправив как ввод, так и вывод
$ cmd1 | cmd2             # запустить одновременно программы cmd1 и cmd2, подав данные со стандартного вывода первой на стандартный ввод второй (конвейер)
$ cmd4 2> errfile         # направить поток сообщений об ошибках в файл errfile
$ cmd5 2>&1 | cmd6        # объединить потоки стандартного вывода и диагностики программы cmd5 и направить на стандартный ввод программы cmd6
$ cmd1 > /dev/null        # перенаправить вывод на несуществующее устройство
```
Специальные файлы устройств:
```bash
/dev/full      # «полное устройство». Запись в него ненулевого количества байт происходит с ошибкой «недостаточно места», независимо от объёма «записанной» информации. Чтение из /dev/full эквивалентно считыванию запрошенного количества нулевых байтов, как для /dev/zero  
/dev/null      # «пустое устройство»
/dev/random    # генератор случайных чисел
/dev/urandom   # генератор псевдослучайных чисел
/dev/zero      # источник нулевых байтов 
```
Файловая система Linux:
```bash
/        # Корневая директория
/home    # Хранятся материалы пользователя
/boot    # Хранятся файлы, необходимые для запуска Linux
/bin     # Находятся исполняемые файлы
/var     # Содержит различные файлы, используемые системой и установленными в ней программами. Это могут быть файлы журналов, базы данных, кешированные материалы веб-страниц
```
Переменные окружения:
```bash
$ export        # показать все переменные окружения
$ export PATH=$PATH:/sbin:/usr/sbin       # копирует значение в переменную окружения PATH (добавляет)
$ unset MYVAR   # удалить переменную MYVAR из окружения

$ EDITOR=joe chfn    # запускает приложение с переменной окружения EDITOR=joe

$ echo $PATH    # список каталогов, в которых следует искать исполняемый файл
$ echo $HOME    # путь к домашнему каталогу
$ echo $LANG    # на каком языке выводить сообщения
$ echo $EDITOR  # имя желаемого редактора текста
```

```bash
# Узнать Wayland или Xorg
$ echo $XDG_SESSION_TYPE
```
Посмотреть неиспользуемые IP-адреса в сети
```bash
# Узнаем какой IP-адрес и сетевая маска у нашего компьютера, а, соответственно, и у нашей локальной сети
$ ifconfig
# Убедись, что установлена утилита nmap
$ nmap -v -sP 10.0.2.15/24 | grep down
```
