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

Отключить DHCP-сервер:
```
# В файле /etc/config/dhcp добавить в lan интерфейс
option ignore	1
```
Добавление сертификатов
```
# Скачать CA cacert.pem по ссылке и добавить в один из каталогов:
# https://curl.se/docs/caextract.html

/etc/ssl/certs/ca-certificates.crt
/etc/pki/tls/certs/ca-bundle.crt
/etc/ssl/ca-bundle.pem
/etc/pki/tls/cacert.pem
/etc/pki/ca-trust/extracted/pem/tls-ca-bundle.pem
/etc/ssl/cert.pem

# Для исправления ошибки x509: certificate signed by unknown authority
```
