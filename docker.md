#### Docker

```
# Установка
$ sudo apt update
# Установите пакеты, которые необходимы для работы пакетного менеджера apt по протоколу HTTPS
$ sudo apt install curl software-properties-common ca-certificates apt-transport-https -y
# Добавьте GPG-ключ репозитория Docker
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
# Добавьте репозиторий Docker
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
$ sudo apt update
# Переключитесь в репозиторий Docker, чтобы его установить
$ apt-cache policy docker-ce
# Установите Docker
$ sudo apt install docker-ce -y
# Проверьте работоспособность программы
$ sudo systemctl status docker
# Чтобы использовать утилиту docker, нужно добавить ваше имя пользователя в группу Docker
# Для этого введите в терминале команду
# Где user — имя пользователя
$ sudo usermod -aG docker ${user}





```
