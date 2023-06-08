#### Go


```bash
# Установка
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install golang
go env -w GO111MODULE=off
# Проверка работы
$ go version

# Запуск без создания файла
$ go run main.go

# Запуск c созданием файла
$ go build main.go

# Подключение пакетов
go get github.com/lib/pq
```

Среда разработки для Go: LiteIDE
