#### CURL


```bash
# POST-запрос
$ curl -X POST -F 'name=andreyex' -F 'email=andreyex@example.ru' https://example.ru/contact.php

$ curl -X POST -d 'name=andreyex&email=andreyex@example.ru' https://example.ru/contact.php

# POST-запрос JSON
$ curl -X POST -H "Content-Type: application/json" -d '{"name": "andreyex", "email": "andreyex@example.ru"}' https://example/contact
$ curl -X POST -d "{\"msg\":\"event\",\"level\":\"info\",\"id\":\"1234\",\"ip\":\"10.1.10.17\",\"name\":\"Poveleck\",\"source\":\"system\",\"event\":\"ref_corr\",\"body\":\"qqqqqq\"}" -H "Content-Type: application/json" http://localhost:8080/event

# POST-запрос загрузка файлов
$ curl -X POST -F 'image=@/home/user/Pictures/wallpaper.jpg' http://example.ru/upload
```
