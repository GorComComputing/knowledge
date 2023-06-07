#### CURL


```bash
# POST-запрос
$ curl -X POST -F 'name=andreyex' -F 'email=andreyex@example.ru' https://example.ru/contact.php

$ curl -X POST -d 'name=andreyex&email=andreyex@example.ru' https://example.ru/contact.php

# POST-запрос JSON
$ curl -X POST -H "Content-Type: application/json" \ -d '{"name": "andreyex", "email": "andreyex@example.ru"}' \ https://example/contact

# POST-запрос загрузка файлов
$ curl -X POST -F 'image=@/home/user/Pictures/wallpaper.jpg' http://example.ru/upload
```
