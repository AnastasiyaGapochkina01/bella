Проект secure_storage - файловое хранилище с контролем доступа
1) В директории /srv создать следуюущю структуру каталогов
```
/srv/secure_storage/
├── uploads/       
├── approved/    
├── quarantined/   
└── logs/          
```
Назначить права так, чтобы только владелец (root) имел доступ к /srv/secure_storage
2) Создать группы и назначить им доступы
- uploaders: могут писать в uploads.
- auditors: могут читать из approved и quarantined.
- security: могут удалять файлы в quarantined
3) Создать пользователей
- user1 (в группе uploaders)
- audit_user (в группе auditors)
- sec_user (в группе security)
4) Написать скрипт, который сгенериует 10 файлов в диреткории uploads с разыми именами и в 4 из них запишет строку #malicious
5) Написать скрипт /srv/secure_storage/scripts/scan_files.sh, который:
- перемещает все файлы из uploads в quarantined, если они содержат строку #malicious
- остальные файлы перемещает в approved.
- записывает в /srv/secure_storage/logs/scan.log время операции и имена обработанных файлов.
6) Написать скрипт notify_sec.sh, который:
- проверяет, есть ли файлы в quarantined, и отправляет сообщение в файл /srv/secure_storage/logs/security_alert.txt с их списком.
- запускается только от пользователя sec_user
7) Написать сервис file_scanner.service, который:
- запускает scan_files.sh каждые 5 минут.
- зависит от network.target
- останавливается при ошибке
8) Написать скрипт, который если скрипт scan_files.sh "висит" более 10 минут, завершит его принудительно и отправит уведомление в security_alert.txt
