#### Chrome


```bash
# Установка 
$ wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
$ sudo dpkg -i --force-depends google-chrome-stable_current_amd64.deb

# Добавить нового пользователя в sudoers (вводить из-под root)
$ usermod -aG sudo username
```
