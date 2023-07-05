#### Make


```bash
# создание Makefile
$ touch Makefile
$ vi Makefile

# запуск сборки
$ make
$ make -j8
```
Пример Makefile:
```make
#CC=/home/gor/imx6ull-nano-2e/buildroot/output/host/usr/bin/arm-buildroot-linux-uclibcgnueabihf-gcc
#GO=/bin/go

.PHONY: clean
.PHONY: all

all: helloARM helloGO

# для отступов используются Tab
helloARM: helloARM.c
        $(CC) -o $@ $<

helloGO: *.go deps
        GOOS=linux GOARCH=arm go build -o $@ $<

clean:
        rm -f helloARM
        rm -f helloGO

.PHONY: deps
deps:
	go get github.com/gorilla/sessions
```
