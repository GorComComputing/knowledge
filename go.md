#### Go


```bash
# Установка
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install golang git
$ go env -w GO111MODULE=off
# Проверка работы
$ go version

# Запуск без создания файла
$ go run main.go

# Запуск c созданием файла
$ go build -o main main.go
$ GOOS=linux GOARCH=mips GOMIPS=softfloat go build -o main main.go
$ GOOS=linux GOARCH=arm go build -o main main.go

# Подключение пакетов
$ go get github.com/lib/pq
```
Тестовая программа на Go (Hello World):
```
package main
import "fmt"
func main() {
    fmt.Println("Hello World")
}
```

Среда разработки для Go: LiteIDE
```
# Makefile запуск:
$ make


.PHONY: main
main: *.go deps
	GOOS=linux GOARCH=arm go build -o ChShell .
	./ChShell


.PHONY:deps
deps:
	go get github.com/gorilla/sessions
```
