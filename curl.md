#### CURL


```bash
# POST-запрос
$ curl -X POST -F 'name=andreyex' -F 'email=andreyex@example.ru' https://example.ru/contact.php
$ curl --data "param1=test1&param2=test2" http://test.com

$ curl -X POST -d 'name=andreyex&email=andreyex@example.ru' https://example.ru/contact.php

# POST-запрос JSON
$ curl -X POST -H "Content-Type: application/json" -d '{"name": "andreyex", "email": "andreyex@example.ru"}' https://example/contact
$ curl -X POST -d "{\"msg\":\"event\",\"level\":\"info\",\"id\":\"1234\",\"ip\":\"10.1.10.17\",\"name\":\"Poveleck\",\"source\":\"system\",\"event\":\"ref_corr\",\"body\":\"qqqqqq\"}" -H "Content-Type: application/json" http://localhost:8080/event
$ curl -X POST -d "{\"level\":\"info\",\"ident\":\"1234\",\"is_check\":\"true\",\"object\":\"88\",\"source\":\"systemS\",\"body\":\"body1\", \"cmd\":\"ins_evnt\"}" -H "Content-Type: application/json" http://localhost:8085/json

# POST-запрос загрузка файлов
$ curl -X POST -F 'image=@/home/user/Pictures/wallpaper.jpg' http://example.ru/upload

# Если никакие аргументы не указаны, то команда curl выполняет HTTP-запрос get и отображает статическое содержимое страницы
# Оно аналогично тому, что мы видим при просмотре исходного кода в браузере
$ curl www.google.com

# Просмотр HTTP-заголовков
$ curl -I https://www.google.com

# Скачать файл
$ curl -O https://testdomain.com/testfile.tar.gz
$ curl -o custom_file.tar.gz https://testdomain.com/testfile.tar.gz

# Игнорирование ошибки неправильных или самоподписанных сертификатов
$ curl -k https://localhost/my_test_endpoint

$ curl -k -X POST https://pay4partner.ru:8080/v1/admin/users/18 \
    -H "Content-Type: application/json" \
    -H "Authorization: YOUR_TOKEN_HERE" \
    -d '{"key":"value"}'

```
