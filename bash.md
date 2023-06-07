#### Bash


```bash
# Команды
$ ls        # содержимое каталога
$ cd        # сменить каталог
$ mkdir     # создать каталог
$ pwd       # показать путь текущего каталога
$ touch     # создать файл
$ rm -r     # удалить (ключ -r рекурсивно для каталогов)
$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout key.pem -out cert.pem   # генерирует файлы ключей HTTPS
$ su - goryachev  # Сменить пользователя
$ su -            # Сменить пользователя на root


$ ip a      # узнать ip-адрес

$ lscpu             # информация о процессоре
$ cat /proc/cpuinfo # информация о процессоре
$ free -h           # информация о памяти
$ cat /proc/meminfo # информация о памяти

$ ping -c 3 google.com       # проверка подключения к интернету
$ curl -I https://google.com # проверка подключения к интернету
```