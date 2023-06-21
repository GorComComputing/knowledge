#### Go


```bash
# Установка
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install golang
$ go env -w GO111MODULE=off
# Проверка работы
$ go version

# Запуск без создания файла
$ go run main.go

# Запуск c созданием файла
$ go build main.go
$ GOOS=linux GOARCH=mips GOMIPS=softfloat go build main.go

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
