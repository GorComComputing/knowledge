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
В файле /etc/chrony/chrony.conf список NTP-серверов. В конце файла добавить строку и перезапустить сервер времени:
```
$ sudo nano /etc/chrony/chrony.conf

server pool.ntp.org
allow 192.168/16
```
```
# Установка
$ sudo apt install chrony

$ chronyc activity          # Статус активности и количество подключенных серверов и пиров
$ chronyc tracking          # показать какой сервер отслеживает chrony
$ chronyc sources -v        # список серверов доступных системе
$ chronyc sourcestats -v    # дополнительная статистика каждого сервера

$ sudo systemctl status chronyd       # узнать статус демона chronyd
$ sudo systemctl restart chronyd      # перезапуск демона chronyd
$ sudo timedatectl set-ntp true       # синхронизировать сервер

$ /etc/init.d/chrony restart          # перезапуск сервера времени

$ sudo chronyc clients                # показать список добавленных клиентов

$ chronyc makestep                    # ручное обновление времени
```
gpsd
```
# Установка
$ sudo apt-get install gpsd
$ sudo apt-get install gpsd-clients

$ sudo gpscat -s 9600 /dev/ttyUSB0       # Просмотреть прямой вывод с устройства (9600 — скорость обмена)
$ sudo gpsmon /dev/ttyUSB0               # Форматный вывод с распарсиванием строки
$ sudo gpsd -S 2727 /dev/ttyUSB0 9600    # Запускаем GPSD daemon транслировать данные на localhost:2727
$ gpsmon localhost:2727                  # Проверяем приход данных на локальный порт

$ gpsd /dev/ttyUSB0                      # запуск демона
$ xgps                                   # запуск клиента GUI
```

