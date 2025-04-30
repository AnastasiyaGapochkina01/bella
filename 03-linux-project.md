# Часть 1
1) Подключиться по ssh на выданную ВМ:
- login: devops
- pass: 0000
- ip: 89.169.160.83
2) В директории /var/www создать папку projects и перейти в нее
3) Создать внутри подпапки docs, scripts, backups
4) Вывести список содержимого папки projects
5) В папке docs создать файл notes.txt и  файл строку "Hello, Linux!" командой echo
6) Скопировать notes.txt в папку backups
7) В папке scripts создать исполняемый файл hello.sh с содержимым
```
#!/bin/bash
echo "Hello from script!"
```
8) Запустить скрипт hello.sh
9) В папке docs создать 5 файлов: file1.txt, file2.log, file3.txt, file4.log, file5.txt
- file1.txt
```
This is a sample text file.
Created for Linux console practice.
Project: Mastering CLI
Date: 2023-10-01
```
- file2.log
```
[2023-10-01 10:00] INFO: System started
[2023-10-01 10:05] ERROR: Failed to connect to database
[2023-10-01 10:10] WARNING: High memory usage (85%)
```
- file3.txt
```
Shopping List:
- Apples
- Milk
- Bread
- Eggs

TODO:
1. Practice Linux commands
2. Write backup script
```
- file4.log
```
[2023-10-01 11:30] ERROR: File not found: config.ini
[2023-10-01 11:35] INFO: Backup completed successfully
[2023-10-01 11:40] DEBUG: Checking network latency
```
- file5.txt
```
Linux Cheat Sheet:
* ls - list files
* grep - search patterns
* chmod - change permissions
* cron - schedule tasks

Tip: Use 'man command' for help!
```
10) Найти все файлы с расширением .txt и вывести их список
11) Отфильтровать содержимое всех файлов .log на наличие слова "error"
12) Создать скрипт backup.sh в папке scripts, который будет архивировать папку docs в backups с датой в имени файла
13) Удалить docs/
# Часть 2
## Создать сервис для мониторинга ресурсов системы с автоматической ротацией логов
1) Установить sysstat и jq
2) Создать директорию /opt/logguardian; в ней - директории scripts и logs
3) Написать скрипт scripts/monitor.sh, который
- получает LA за 5 минут
- получает сколько использовано RAM
- сколько использовано диска
- выводит всю эту информацию в файл logs/system_${date}.log
4) Написать systemd-unit logguardian.service для скрипта и logguardian.timer для запуска по расписанию
5) Написать скрипт scripts/log_rotate.sh, который удаляет фалы логов старше N дней (N передавать как аргумент)
  
