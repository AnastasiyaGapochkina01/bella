> [!TIP]
> Быть готовым показать ВСЮ домашку.

1) Проверить, существует ли в домашней директории директория linux_labs; если да, то переходим к п2, если нет - создаем эту директорию
2) В директории linux_labs создать директорию logs
3) В директории logs создать файлы
- nginx_access.log с содержимым
```
192.168.1.105 - - [15/Oct/2023:14:32:01 +0300] "GET / HTTP/1.1" 200 5432 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/117.0.0.0 Safari/537.36"
192.168.1.105 - - [15/Oct/2023:14:32:02 +0300] "GET /static/css/main.css HTTP/1.1" 200 1234 "http://example.com/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/117.0.0.0 Safari/537.36"
203.0.113.42 - admin [15/Oct/2023:14:33:15 +0300] "POST /admin/login HTTP/1.1" 200 832 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Safari/605.1.15"
91.234.123.22 - - [15/Oct/2023:14:33:45 +0300] "GET /products/123 HTTP/1.1" 404 162 "-" "Mozilla/5.0 (Linux; Android 10; SM-A505FN) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Mobile Safari/537.36"
192.168.1.105 - - [15/Oct/2023:14:34:01 +0300] "GET /favicon.ico HTTP/1.1" 404 162 "http://example.com/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/117.0.0.0 Safari/537.36"
66.249.79.12 - - [15/Oct/2023:14:35:22 +0300] "GET /robots.txt HTTP/1.1" 200 123 "-" "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
198.51.100.34 - - [15/Oct/2023:14:36:10 +0300] "GET /wp-admin HTTP/1.1" 403 162 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/117.0.0.0 Safari/537.36"
```
- nginx_error.log с содержимым
```
2023/10/15 14:33:45 [error] 12345#12345: *98765 open() "/var/www/example.com/products/123" failed (2: No such file or directory), client: 91.234.123.22, server: example.com, request: "GET /products/123 HTTP/1.1", host: "example.com"
2023/10/15 14:34:01 [error] 12345#12345: *98766 open() "/var/www/example.com/favicon.ico" failed (2: No such file or directory), client: 192.168.1.105, server: example.com, request: "GET /favicon.ico HTTP/1.1", referrer: "http://example.com/"
2023/10/15 14:36:10 [error] 12345#12345: *98767 access forbidden by rule, client: 198.51.100.34, server: example.com, request: "GET /wp-admin HTTP/1.1", host: "example.com"
2023/10/15 14:37:22 [error] 12345#12345: *98768 upstream timed out (110: Connection timed out) while reading response header from upstream, client: 203.0.113.89, server: api.example.com, request: "GET /data/users HTTP/1.1", upstream: "http://127.0.0.1:8000/data/users", host: "api.example.com"
```
4) В файлах nginx_access.log и nginx_error.log:
- найти все запросы, которые вернули код ответа 404
- определить, сколько запросов пришло с мобильных устройств
- найти все ошибки, связанные с таймаутом соединения
- определить IP-адрес, с которого было больше всего запросов
- найти все запросы к административной панели (/admin или /wp-admin)
- определить, какие файлы не были найдены на сервере
- найти все запросы от поисковых роботов
5) В директории linux_labs создать директорию users_access
6) В директории users_access создать директории user_01, user_02, shared
7) Создать польователей user_01 и user_02, группу temp-users
8) Назначить
- владельцем директории user_01 пользователя user_01, а группой - temp-users
- владельцем директории user_02 пользователя user_02, а группой - temp-users
9) Назначить права на директории user_01 и user_02 так, чтобы владельцы имели все права, группа - только читать, а все остальные не имели никаких прав
10) Назначить права на директорию sharedd так чтобы все имели к ней полный доступ
11) Установить на ВМ go (https://go.dev/doc/install)
12) Запустить приложение https://github.com/AnastasiyaGapochkina01/web-go как systemd-unit
13) В директории linux_labs создать исполняемый файл ping-sleep.sh с содержимым
```
#!/bin/bash

ping google.com > ping1.log 2>&1 &
ping bing.com > ping2.log 2>&1 &

sleep 10000 > sleep1.log 2>&1 &
sleep 15000 > sleep2.log 2>&1 &
```
14) Запустить скрипт ping-sleep.sh в фоновом режиме
15) Проверить, появились ли в директории файлы ping* и sleep*
16) С помощью ps найти все процессы ping и посчитать их количество
17) С помощью ps найти все процессы sleep и посчитать их количество
18) Для найденных процессов ping вывести ppid,pid,comm
