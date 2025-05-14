1) Создать файловую структуру под проект `auto_backups`
```
~$ tree -a auto_backups/
auto_backups/
├── backups
├── bin
├── config
├── logs
└── restore
```
2) Создать директорию `important_data` и в ней сделать структуру
```
~$ tree -a important_data/
important_data/
├── documents
│   ├── notes.md
│   └── report.txt
└── images
    ├── photo1.jpg
    └── photo2.jpg
```
3) Написать скрипт `backup.sh`, который:
- копирует файлы из `~/important_data` в папку `backups` с датой в имени.
- фильтрует файлы по расширению (например, только .txt и .md).
- логирует действия
4) Создать пользователя backupadmin
- выдать backupadmin права на чтение `important_data` и запись в `auto_backups`
- запретить другим пользователям доступ к `backups`
5) Создать systemd-сервис для ежедневного бэкапа с таймером для запуска в 23:00 каждый день
6) Проверить работу сервиса
7) Написать скрипт для принудительной остановки бэкапа
8) Написать скрипт `restore.sh` для восстановления файлов из бэкапа
