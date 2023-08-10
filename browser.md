#### Browser


```bash
# Установка соединения
$ telnet example.org 80

# Запрос GET на сервер (!не забыть вставить пустую строку в конце!)
GET /index.html HTTP/1.0
Host: example.org

# Ответ от сервера
HTTP/1.0 200 OK
Accept-Ranges: bytes
Age: 103895
Cache-Control: max-age=604800
Content-Type: text/html; charset=UTF-8
Date: Mon, 07 Aug 2023 06:03:18 GMT
Etag: "3147526947"
Expires: Mon, 14 Aug 2023 06:03:18 GMT
Last-Modified: Thu, 17 Oct 2019 07:18:26 GMT
Server: ECS (nyb/1D10)
Vary: Accept-Encoding
X-Cache: HIT
Content-Length: 1256
Connection: close

<!doctype html>
<html>
<head>
    <title>Example Domain</title>

...

</body>
</html>
Connection closed by foreign host.

# Запрос POST на сервер 
POST /submit HTTP/1.0
Host: example.org
Content-Length: 16

name=1&comment=2


# Запуск веб-сервера Python (отображает все файлы в каталоге, в котором запущен)
$ python3 -m http.server 8000

# Установка Duktape для Python
$ sudo apt install python3-pip
$ pip3 install dukpy

        # Проверка работы Duktape в Python
        import dukpy
        print(dukpy.evaljs("2 + 2"))
```
