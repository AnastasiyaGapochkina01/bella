# Часть 1 - Установка ПО
1) Установить на ВМ docker по инструкции с официального сайта; добавить себя в группу docker и перелогиниться
2) В домашней директории создать директорию soft-install. В ней создать файл compose.yml с сожержимым
```
services:
  system:
    image: debian:stable-slim
    container_name: lightweight-os
    command: "sleep infinity"
```
находять в директории soft-install выполнить команды
```
docker compose up -d
CONT=$(docker compose ps --format '{{.Name}}')
docker exec -it $CONT bash
```
дальше работа будет идти в контейнере. Выполнить команду ```whereis wget```, вывод будет такой
```
root@fb47544e56d5:/wget-1.25.0# whereis wget
wget:
```
Это значит утилиты нет и надо ее поставить, это и будем делать ниже
3) Установить пакеты ```build-essential, pkg-config, curl, libgnutls28-dev``` с помощью apt
4) Создать директорию /usr/src/wget и скачать туда с помощью curl архив https://ftp.gnu.org/gnu/wget/wget-latest.tar.gz
5) Распаковать архив wget-latest.tar.gz и перейти в папку wget-1.25.0
6) Выполнить
```
./configure
make
make install
```
7) Снова выполнить whereis
```
root@fb47544e56d5:/wget-1.25.0# whereis wget
wget: /usr/local/bin/wget
```
8) Создать папку /usr/src/netcat и перейти в нее
9) С помощью wget скачать архив https://github.com/AnastasiyaGapochkina01/bella/raw/refs/heads/main/netcat-0.7.1.tar.gz
10) Распаковать архив netcat-0.7.1.tar.gz и перейти в директорию netcat-0.7.1
11) Собрать из исходников netcat
12) Установить из deb пакета утилиту memtester (https://packages.debian.org/bookworm/amd64/memtester/download)
13) Выйти из контейнера и остановить его
```
exit
docker compose down
```
# Часть 2 - работа с ФС
1) Добавить к ВМ дополнительный диск
2) Установить postgresql, убедиться что он запущен
3) Выяснить, где находится директория с данными
```
sudo su - postgres
psql
# SHOW data_directory;
```
4) Создать тестовую БД bookstore с табличками
- books

|book_id|author_id|title|author|price|ISBN|
|:---:|:---:|:---:|:---:|:---:|:---:|
|1|2|Underground|H.Murakami|599|978-3-16-148239-7|
|2|1|Ulysses|J.Joyce|490|978-3-12-987654-3|
|3|3|The Trial|F.Kafka|350|978-5-17-123456-1|

- authors

|author_id|name|
|:---:|:---:|
|1|J.Joyce|
|2|H.Murakami|
|3|F.Kafka|

4) Вынести директорию с данными postgres на дополнительный диск без потери данных (обязательно рестартануть сервис и проверить что БД на месте)
