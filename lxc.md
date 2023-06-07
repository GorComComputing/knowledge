#### LXC


```bash

# Установка LXC под Ubuntu
$ sudo apt install lxc

# 1. создать контейнер с именем myapp
$ sudo lxc-create -t download -n myapp -- -d ubuntu -r focal -a amd64

# 2. посмотреть список контейнеров
$ sudo lxc-ls -f

# 3. запустить контейнер
$ sudo lxc-start myapp

# 4. остановить
$ sudo lxc-stop myapp

# 5. зайти в shell контейнера
$ sudo lxc-attach myapp

# 6. посмотреть файловую систему контейнера
$ ls -al /var/lib/lxc/myapp/rootfs

# Копирование файла в контейнер work
$ sudo cp buildroot-2023.02.1.tar.gz /var/lib/lxc/work/rootfs/home/goryachev/embd/buildroot-2023.02.1.tar.gz


# Сменить пользователя в контейнере
$ su - goryachev
```
