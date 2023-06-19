#### Bash


```bash
# Команды
$ ls        # содержимое каталога
$ ls | less       # постраничный вывод Space - вперед, b - назад, q - выход
$ cd        # сменить каталог
$ mkdir     # создать каталог
$ pwd       # показать путь текущего каталога
$ touch     # создать файл
$ rm -r     # удалить (ключ -r рекурсивно для каталогов)
$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout key.pem -out cert.pem   # генерирует файлы ключей HTTPS
$ adduser goryachev            # создать пользователя
$ usermod -aG sudo goryachev   # добавить пользователя в группу sudo
$ su - goryachev  # Сменить пользователя
$ su -            # Сменить пользователя на root
$ ps        # показать список процессов
$ sudo useradd -m username    # создать пользователя вместе с домашним каталогом
$ sudo passwd username        # задать пароль пользователя
$ sudo service lightdm restart      # перезапуск x-server
$ sudo dpkg -i NOMBRE-DEL-PAQUETE.deb   # установка из пакета deb скачанного с сайта

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



$ ip a      # узнать ip-адрес
$ uname -a  # узнать версию ядра Linux

$ lscpu             # информация о процессоре
$ cat /proc/cpuinfo # информация о процессоре
$ free -h           # информация о памяти
$ cat /proc/meminfo # информация о памяти
$ cat /proc/devices # выводит список драйверов символьных и блочных устройств
$ ip link show      # выводит список сетевых устройств
$ lsusb             # выводит usb устройства
$ lspci             # выводит pci устройства

$ cat /dev/cdrom    # проверить наличие диска в CD-ROM
$ eject             # открыть CD-ROM

$ ping -c 3 google.com       # проверка подключения к интернету
$ curl -I https://google.com # проверка подключения к интернету

# для подключения к usb-serial
$ sudo chmod 666 /dev/ttyUSB0
$ putty
$ stty < /dev/ttyS0          # узнать скорость com-порта
```
Чтобы освободить место в коневой файловой системе
```
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
Показать скрытые папки и файлы в окне
```
Ctrl+H
```
SSH
```
# Подключение
$ ssh  root@192.168.0.254

# При ошибке: Unable to negotiate with 192.168.0.254 port 22: no matching key exchange method found. Their offer: diffie-hellman-group1-sha1,diffie-hellman-group14-sha1
# Добавить в файл ~/.ssh/config строки:
Host 192.168.0.254
    HostkeyAlgorithms ssh-dss,ssh-rsa
    KexAlgorithms +diffie-hellman-group1-sha1
```
Создание iso-образа с диска:
```
dd if=/dev/cdrom of=win7.iso bs=2048
sudo mount -o loop win7.iso /media/ 
```

