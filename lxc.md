#### LXC


```bash

# Установка LXC под Ubuntu
$ sudo apt install lxc libvirt-daemon-system libvirt-clients

# 1. создать контейнер с именем myapp
$ sudo lxc-create -t download -n myapp -- -d ubuntu -r focal -a amd64
$ adduser goryachev            # создать пользователя
$ usermod -aG sudo goryachev   # добавить пользователя в группу sudo
$ su - goryachev  # Сменить пользователя

# 2. посмотреть список контейнеров
$ sudo lxc-ls -f

# 3. запустить контейнер
$ sudo lxc-start -n myapp

# 4. остановить
$ sudo lxc-stop -n myapp

# 5. зайти в shell контейнера
$ sudo lxc-attach -n myapp

# 6. посмотреть файловую систему контейнера
$ ls -al /var/lib/lxc/myapp/rootfs

# Копирование файла в контейнер work
$ sudo cp buildroot-2023.02.1.tar.gz /var/lib/lxc/work/rootfs/home/goryachev/embd/buildroot-2023.02.1.tar.gz

# Удалить контейнер
$ sudo lxc-destroy -n myapp


$ lxc-info -n base      # информация о контейнере
$ lxc-freeze -n base    # заморозка всех процессов заданного контейнера
$ lxc-unfreeze -n base  # разморозка всех процессов заданного контейнера
$ lxc-copy -n base -N base2       # копирование контейнеров -n источник -N клонированный контейнер. С начала необходимо остановить контейнер
$ lxc-snapshot -n base  # создать снимок контейнера. С начала необходимо остановить контейнер
```
