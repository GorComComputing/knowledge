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

# Узнать версию glibc установленную на компьютере
$ ldd --version
# Собрать без использования C-кода, только код Go
$ CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o WebServer .

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

TinyGo
```bash
# Чтобы установить TinyGo, на компьютере уже должен быть установлен Go

# Установка для Linux на процессоре Intel
$ wget https://github.com/tinygo-org/tinygo/releases/download/v0.28.1/tinygo_0.28.1_amd64.deb
$ sudo dpkg -i tinygo_0.28.1_amd64.deb

# Установка для Linux на процессоре ARM
$ wget https://github.com/tinygo-org/tinygo/releases/download/v0.28.1/tinygo_0.28.1_armhf.deb
$ sudo dpkg -i tinygo_0.28.1_armhf.deb

# Нужно убедиться, что путь к tinygo исполняемому файлу находится в PATH переменной
$ export PATH=$PATH:/usr/local/bin

# Если вы используете 64-разрядную ОС ARM, и запуск tinygo завершается с ошибкой «нет такого файла или каталога», может потребоваться установить 32-разрядную библиотеку времени выполнения C++
$ sudo apt install libstdc++6:armhf

# Если интересует только компиляция кода TinyGo для WebAssembly, то установка завершена
# В противном случае продолжи установку дополнительных требований для желаемого микроконтроллера
```
