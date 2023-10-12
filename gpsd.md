#### gpsd

```bash
# Просмотреть распарсиный вывод NMEA
$ gpsmon /dev/ttyUSB0

# Запускаем GPSD daemon транслировать данные на localhost:2727
$ gpsd -S 2727 /dev/ttyUSB0 9600

# Проверяем приход данных на локальный порт
$ gpsmon localhost:2727

# Запуск с настройками по умолчанию (порт 2947)
$ gpsd /dev/ttyS1

# gpsd will read NMEA data from device even if no client is running
$ gpsd /dev/ttyS1 -n 

# gpsd will read NMEA data from device  even if no client is running, don't send gpsd into background, debug setting 3 (verbose)
$ gpsd /dev/ttyS1 -n -N -D 3

# Клиент запускается после запуска gpsd
$ cgps -s
```
