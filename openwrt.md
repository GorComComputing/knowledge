#### OpenWrt

Добавить в автозапуск:
```bash
# Скопируйте script в каталог /etc/init.d/

#!/bin/sh /etc/rc.common
# PostgresQL autorun
START=50
start() {
	/etc/init.d/postgresql start
  cd /overlay/Embd_linux/TemplHtml
  ./main &
}  


$ chmod +x /etc/init.d/<your script>
$ /etc/init.d/<your script> enable
$ ls -lh /etc/rc.d | grep <your script>

# Проверка
$ /etc/init.d/<your script> enabled && echo on
```
