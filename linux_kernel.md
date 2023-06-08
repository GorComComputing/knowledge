#### Linux kernel


```bash
# Клонирование с репозитория
$ git clone git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git linux
$ cd linux
$ git checkout v5.19.0

# Запуск меню конфигуратора
$ make ARCH=arm menuconfig 
```
