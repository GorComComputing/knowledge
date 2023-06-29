#### WinSCP в Ubuntu


```bash
# Установка Wine под Ubuntu
$ sudo apt update
$ sudo apt upgrade

$ sudo dpkg --add-architecture i386
$ wget -qO - https://dl.winehq.org/wine-builds/winehq.key | sudo apt-key add -
$ sudo apt-add-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ focal main'
$ sudo apt update 
$ sudo apt install --install-recommends winehq-stable

# Установка WinSCP под Ubuntu
# Скачать дистрибутив с сайта https://winscp.net/eng/index.php
$ cd ~/Загрузки
$ wine WinSCP-*-Setup.exe
```
