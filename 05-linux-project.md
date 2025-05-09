1) Создать директорию, если ее нет `/var/www/`
2) Склонировать в `/var/www` проект https://gitlab.com/devops201206/it-mtb-blog#
3) Установить на ВМ nginx, если еще не установлен
4) В директории `/var/www/it-mtb-blog` создать директории
- logs
- scripts
5) Настроить nginx так, чтобы на ip вирутальной машины отдавался блог
<img width="1191" alt="image" src="https://github.com/user-attachments/assets/cc7f0eee-82c2-41f9-a4d0-ae6325dd7339" />
6) В директории scripts написать bash-скрипт `it-mtb-blog_monitor.sh`, который будет проверять доступность блога раз в минуту

- если сайт недоступен — перезапускает его и пишет ошибку в `/var/www/it-mtb-blog/logs/errors.log`
- записывает статистику (дата, нагрузка CPU, свободная память) в `/var/www/it-mtb-blog/logs/status.log`

7) Создать демон `it-mtb-blog_monitor.service`, который:
- запускает скрипт `it-mtb-blog_monitor.sh` при старте системы
- перезапускает скрипт при его аварийном завершении
- включить автозагрузку службы и проверить ее статус

8) Имитировать падение nginx:
- убедиться, что скрипт `it-mtb-blog_monitor.sh` перезапустил сервер и записал ошибку в лог.
- проверить, что служба `it-mtb-blog_monitor.service` активна.
