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


$ ip a      # узнать ip-адрес
$ uname -a  # узнать версию ядра Linux

$ lscpu             # информация о процессоре
$ cat /proc/cpuinfo # информация о процессоре
$ free -h           # информация о памяти
$ cat /proc/meminfo # информация о памяти

$ ping -c 3 google.com       # проверка подключения к интернету
$ curl -I https://google.com # проверка подключения к интернету
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
