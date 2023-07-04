#### UFW - брандмауэр


```bash
# Настройте параметры брандмауэра
# Если ваш сервер работает за брандмауэром, вам необходимо настроить брандмауэр для обеспечения связи с внешним миром.
# Начните с проверки порта, на котором прослушивается PostgreSQL. По умолчанию PostgreSQL прослушивает порт 5432

$ ss -tunelp | grep 5432
tcp   LISTEN 0      244            0.0.0.0:5432       0.0.0.0:*    uid:130 ino:64635 sk:11 cgroup:/system.slice/system-postgresql.slice/postgresql@15-main.service <->         
tcp   LISTEN 0      244               [::]:5432          [::]:*    uid:130 ino:64636 sk:17 cgroup:/system.slice/system-postgresql.slice/postgresql@15-main.service v6only:1 <->

# Нам нужно будет разрешить порт 5432 через брандмауэр.
$ sudo ufw allow 5432/tcp
Rules updated
Rules updated (v6)
```
