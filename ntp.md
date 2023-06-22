#### NTP


```bash
$ timedatectl status                         # информация о системном времени
$ timedatectl timesync-status                # информация о NTP 
$ timedatectl list-timezones | column        # список всех часовых поясов из каталога /usr/share/zoneinfo/
$ timedatectl set-timezone Europe/Samara     # установить часовой пояс
$ date                                       # выводит текущую дату и время
```

[Список NTP-серверов:](https://support.ntp.org/Servers/StratumTwoTimeServers)
```
pool.ntp.org
time.apple.com
```

Chrony:
- chronyd - демон
- chronyc - инструмент командной строки
В файле /etc/chrony/chrony.conf список NTP-серверов
```
# Установка
$ sudo apt install chrony

# Статус активности и количество подключенных серверов и пиров
$ chronyc activity
```

