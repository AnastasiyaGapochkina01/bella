1) В директории linux_labs/logs создать файл haproxy.log с содержимым
```
Apr 26 07:00:00 hostname haproxy[1234]: 127.0.0.1:54321 [26/Apr/2025:07:00:00.000] http_front servers/server1 0/0/1/2/3 200 1234 - - ---- 1/1/1/0/0 0/0
Apr 26 07:01:00 hostname haproxy[1234]: 127.0.0.1:54322 [26/Apr/2025:07:01:00.000] http_front servers/server1 0/0/2/3/4 404 567 - - ---- 1/1/0/0/0 0/0
Apr 26 07:02:00 hostname haproxy[1234]: 192.168.1.1:54323 [26/Apr/2025:07:02:00.000] http_front servers/server2 0/0/3/4/5 503 890 - - SC-- 1/1/1/0/0 0/0
Apr 26 07:00:00 hostname haproxy[1234]: 192.168.1.1:54321 [26/Apr/2025:07:00:00.000] http_front servers/server1 0/0/1/2/3 200 1234 - - ---- 1/1/1/0/0 0/0
Apr 26 07:01:00 hostname haproxy[1234]: 172.17.2.14:54322 [26/Apr/2025:07:01:00.100] http_front servers/server1 0/0/2/3/5 404 567 - - ---- 1/1/0/0/0 0/0
Apr 26 07:02:00 hostname haproxy[1234]: 172.17.3.1:54323 [26/Apr/2025:07:02:00.200] http_front servers/server2 0/0/3/4/6 503 890 - - SC-- 1/1/1/0/0 0/0
Apr 26 07:03:00 hostname haproxy[1234]: 10.10.1.4:54324 [26/Apr/2025:07:03:00.300] http_front servers/server1 0/0/1/1/2 200 2345 - - ---- 2/2/2/0/0 0/0
Apr 26 07:04:00 hostname haproxy[1234]: 10.10.1.5:54325 [26/Apr/2025:07:04:00.400] http_front servers/server2 0/0/4/5/7 301 678 - - ---- 1/1/1/0/0 0/0
Apr 26 07:05:00 hostname haproxy[1234]: 127.0.0.6:54326 [26/Apr/2025:07:05:00.500] http_front servers/server1 0/0/2/2/4 200 1456 - - ---- 3/3/3/0/0 0/0
Apr 26 07:06:00 hostname haproxy[1234]: 127.0.0.0:54327 [26/Apr/2025:07:06:00.600] http_front servers/server2 0/0/3/3/5 500 789 - - SC-- 1/1/1/0/0 0/0
Apr 26 07:07:00 hostname haproxy[1234]: 203.11.56.8:54328 [26/Apr/2025:07:07:00.700] http_front servers/server1 0/0/1/2/3 200 1123 - - ---- 2/2/2/0/0 0/0
Apr 26 07:08:00 hostname haproxy[1234]: 203.11.56.9:54329 [26/Apr/2025:07:08:00.800] http_front servers/server2 0/0/4/6/8 404 456 - - ---- 1/1/0/0/0 0/0
Apr 26 07:09:00 hostname haproxy[1234]: 203.11.56.10:54330 [26/Apr/2025:07:09:00.900] http_front servers/server1 0/0/2/3/4 200 1345 - - ---- 3/3/3/0/0 0/0
Apr 26 07:10:00 hostname haproxy[1234]: 105.6.4.11:54331 [26/Apr/2025:07:10:00.100] http_front servers/server2 0/0/3/5/7 503 987 - - SC-- 1/1/1/0/0 0/0
Apr 26 07:11:00 hostname haproxy[1234]: 105.6.4.12:54332 [26/Apr/2025:07:11:00.200] http_front servers/server1 0/0/1/1/2 200 1567 - - ---- 2/2/2/0/0 0/0
Apr 26 07:12:00 hostname haproxy[1234]: 105.6.4.13:54333 [26/Apr/2025:07:12:00.300] http_front servers/server2 0/0/4/5/6 301 678 - - ---- 1/1/1/0/0 0/0
Apr 26 07:13:00 hostname haproxy[1234]: 105.6.4.14:54334 [26/Apr/2025:07:13:00.400] http_front servers/server1 0/0/2/2/3 200 1789 - - ---- 3/3/3/0/0 0/0
Apr 26 07:14:00 hostname haproxy[1234]: 105.6.4.15:54335 [26/Apr/2025:07:14:00.500] http_front servers/server2 0/0/3/4/5 500 890 - - SC-- 1/1/1/0/0 0/0
```
2) В найти haproxy.log все запросы от ip адреса 192.168.1
3) Проверить, существует ли директория /etc/nginx; если да, то найти в ней все файлы, содержащие директиву server_name
4) Проверить, существует ли пользователь nginx; если его нет, то создать; если есть - не трогать
5) В директории linux_labs создать директории nginx/conf.d; установить права 640 на файлы в nginx/conf.d ```root:nginx```
6) В nginx/conf.d создать файл .env; запретить доступ к файлу .env всем кроме владельца
7) В директории linux_labs создать директории www/html/wp-content/uploads и в этой папке разрешить запись только для пользователя www-data
8) Установить на ВМ percona db и создать БД wordpress_db с пользователем wp_user
9) Установить PHP-FPM и модули
- php-mysql
- php-curl
- php-pdo
10) Найти 5 процессов, потребляющих больше всего CPU
11) Найти все процессы nginx (если их нет, то проверить статус сервиса nginx; если сервиса нет, то надо установить nginx)
12) Проверить статус сервиса nginx после убийства процессов. Запустить сервис
13) Проверить статус php-fpm
14) Найти в /etc/php файл, содержащий строку listen
15) Создать файл /usr/local/bin/logmonitor.sh с содержимым
```
#!/bin/bash

LOG_FILE="/var/log/nginx/error.log"  
SERVICE_NAME="logmonitor"            

if [ ! -f "$LOG_FILE" ]; then
    echo "Error: Log file $LOG_FILE not found!" | systemd-cat -t "$SERVICE_NAME" -p err
    exit 1
fi

tail -n 0 -F "$LOG_FILE" | while read line; do
    echo "$line" | systemd-cat -t "$SERVICE_NAME" -p info
done
```
- сделать скрипт исполняемым
- создать unit-файл для systemd
- запустить сервис и добавить его в автозагрузку
- проверить работу сервиса
