# Bash script to send information about HDD Temperature of your server to [Telegram](https://web.telegram.org/)

### Modification of telegram-send from [Konstantin Bogomolov](https://bogomolov.tech/Telegram-notification-on-SSH-login/)

### Don't forget to create [telegram-send](https://github.com/purwo-martono/telegram-send) file first

This bash script will check your processors server temperature

In this example I use Ubuntu Server 16.04 (yes I know, it's old doh! )


As always, update first on your console box
```
$ sudo apt-get update
```


Get the sensors
```
$ sudo apt-get install hddtemp
```


Create bash script to call hddtemp and send it to telegram, ofc with [telegram-send](https://github.com/purwo-martono/telegram-send) I mention before 
```
#!/bin/bash

br=$'\n'
ipAddress=$(hostname -I)
lines=""
hddtemp /dev/sda | (while read line;
do
  IN="$line"
  arrIN=(${IN/:/})
  lines+="${br}${arrIN[1]} ${arrIN[2]} "
done
telegram-send "HDDTEMP YOUR_SERVER $ipAddress$lines")
```
