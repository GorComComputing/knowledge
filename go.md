#### Go

```bash
# Установка (лучший вариант)
# Удалить все предыдущие установки Go
$ sudo rm -rf /usr/local/go
# Затем извлечь загруженный архив (https://go.dev/doc/install)
$ sudo tar -C /usr/local -xzf go1.21.3.linux-amd64.tar.gz
$ export PATH=$PATH:/usr/local/go/bin
# Проверка установки
$ go version
```
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

# Проверка установки
$ tinygo version

# Если вы используете 64-разрядную ОС ARM, и запуск tinygo завершается с ошибкой «нет такого файла или каталога», может потребоваться установить 32-разрядную библиотеку времени выполнения C++
$ sudo apt install libstdc++6:armhf

# Если интересует только компиляция кода TinyGo для WebAssembly, то установка завершена
# В противном случае продолжи установку дополнительных требований для желаемого микроконтроллера
# Для процессоров AVR
$ sudo apt-get install avrdude
```

Wasm
```bash
# Компиляция на обычном Go (файл занимает 2 Мб)
$ cp "$(go env GOROOT)/misc/wasm/wasm_exec.js" .
$ GOOS=js GOARCH=wasm go build -o main.wasm

# Компиляция на TinyGo (файл занимает 400 Кб)
$ wget https://raw.githubusercontent.com/tinygo-org/tinygo/v0.19.0/targets/wasm_exec.js
$ tinygo build -o main.wasm -target wasm .
```

Запуск Wasm
```html
<html>
    <head>
        <meta charset="utf-8"/>
        <script src="wasm_exec.js"></script>

    </head>
    <body>
        <h1>WASM Experiments</h1>
        <script>
            // This is a polyfill for FireFox and Safari
            if (!WebAssembly.instantiateStreaming) { 
                WebAssembly.instantiateStreaming = async (resp, importObject) => {
                    const source = await (await resp).arrayBuffer()
                    return await WebAssembly.instantiate(source, importObject)
                }
            }

            // Promise to load the wasm file
           function loadWasm(path) {
             const go = new Go()

             return new Promise((resolve, reject) => {
               WebAssembly.instantiateStreaming(fetch(path), go.importObject)
               .then(result => {
                 go.run(result.instance)
                 resolve(result.instance)
               })
               .catch(error => {
                 reject(error)
               })
             })
           }

         // Load the wasm file
         loadWasm("main.wasm").then(wasm => {
             console.log("main.wasm is loaded 👋")
         }).catch(error => {
             console.log("ouch", error)
         }) 

        </script>
    </body>
</html>
```
Пример кода на Go для Wasm (используя библиотеку syscall/js)
```go
package main

import (
    "syscall/js"
)

func main() {
	message := "👋 Hello World 🌍"

	document := js.Global().Get("document")
    	h2 := document.Call("createElement", "h2")
    	h2.Set("innerHTML", message)
    	document.Get("body").Call("appendChild", h2)

    	<-make(chan bool)
}
```
чистый Wasm:
```bash
# Установка транслятора Wasm
$ sudo apt install wabt

# Трансляция из WAT в бинарник WASM 
$ wat2wasm sprite.wat -o sprite.wasm
```
