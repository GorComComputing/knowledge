#### Docker

Установка Docker
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
$ su - ${user}
# Проверим, все ли установлено корректно
$ docker run hello-world
```
Команды Docker
```
# Посмотреть список образов в системе
$ docker images

# Удалить образ
$ docker rmi 3b98ea9641a0
# Удалить ВСЕ образы
$ docker rmi $(docker images -q)

# Скачивает образ busybox из регистра Докера и сохраняет его локально
$ docker pull busybox

# Запустим Докер-контейнер с этим образом (--rm - удалять контейнер после завершения)
$ docker run --rm busybox
$ docker run busybox echo "hello from busybox"
# Команда run с флагом -it подключает интерактивный tty в контейнер
$ docker run -it --rm busybox sh

# Запустить контейнер в фоновом режиме из регистра Docker Hub
$ docker run -d -p 80:8081 --rm gorcomcomputing/doors

# Остановить контейнер
$ docker stop 3b98ea9641a0

# Выводит на экран список всех запущенных контейнеров
$ docker ps
$ docker ps -a

# Удалить контейнеры
$ docker rm 305297d7a235 ff0a5c3750b9
# Удалить ВСЕ завершенные контейнеры
$ docker rm $(docker ps -a -q -f status=exited)
# Удалить ВООБЩЕ ВСЕ контейнеры
$ docker rm -f $(docker ps -aq)

# По имени контейнера
$(docker container ls  | grep 'container-name' | awk '{print $1}')

# Просмотреть логи контейнера
$ docker logs e74f6f093a12
```
Dockerfile
```
# Собрать образ Docker из Dockerfile
$ docker build -t gorcomcomputing/doors .
```
Docker Hub
```
# Логин
$ docker login -u "user-name" -p "password" docker.io

# Загрузить образ на Docker Hub
$ docker push gorcomcomputing/doors

```
Установка Docker Compose
```
# Загрузка и установка Docker Compose
$ sudo curl -L "https://github.com/docker/compose/releases/download/v2.17.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose

# Проверка версии Docker Compose
$ docker-compose --version

# Настройка прав доступа
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
$ newgrp docker
```
Команды Docker Compose
```
# Собрать и запустить контейнеры
$ docker-compose up -d

```
