1) В директории linux_labs создать директорию text_processing
2) В директории text_processing создать файл application.log с содержимым
```
2024-10-31 04:43:12,591 - DEBUG - User logged in
2024-10-31 04:43:12,591 - INFO - Warning: Low memory
2024-10-31 04:43:12,591 - WARNING - Data retrieved successfully
2024-10-31 04:43:12,591 - DEBUG - Critical error: System failure
2024-10-31 04:43:12,591 - ERROR - Application started
2024-10-31 04:43:12,591 - WARNING - Application started
2024-10-31 04:43:12,591 - DEBUG - Warning: Low memory
2024-10-31 04:43:12,591 - INFO - Application started
2024-10-31 04:43:12,592 - ERROR - Application started
2024-10-31 04:43:12,592 - DEBUG - Application started
2024-10-31 04:43:12,592 - WARNING - Critical error: System failure
2024-10-31 04:43:12,592 - ERROR - Critical error: System failure
2024-10-31 04:43:12,592 - DEBUG - Application shutting down
2024-10-31 04:43:12,592 - DEBUG - Application shutting down
2024-10-31 04:43:12,592 - ERROR - Data retrieved successfully
2024-10-31 04:43:12,592 - INFO - Data retrieved successfully
2024-10-31 04:43:12,592 - ERROR - Warning: Low memory
2024-10-31 04:43:12,592 - WARNING - Error: Failed to connect to the database
2024-10-31 04:43:12,592 - INFO - Critical error: System failure
2024-10-31 04:43:12,592 - DEBUG - Request for data received
2024-10-31 04:43:12,592 - INFO - Critical error: System failure
2024-10-31 04:43:12,592 - INFO - Error: Failed to connect to the database
```
3) Найти в файле application.log все записи уровня ERROR (уровень это та часть строки, которая записана большими буквами)
4) Найти в файле application.log записи о неудачном подключении к базе данных (поиск попробовать по database)
5) Найти в файле application.log все записи уровня WARNING и вывести для них время и сообщение
6) Найти в файле application.log все записи, в которых упомнается memory и вывести их уровень
7) В директории text_processing создать файл app_metrics с содержимым
```
# Application Metrics Log
# metric_name: metric_value
total_requests: 150
successful_requests: 145
failed_requests: 5
average_response_time_ms: 120
max_response_time_ms: 350
min_response_time_ms: 80
memory_usage_mb: 256
cpu_usage_percent: 75
total_requests: 200
successful_requests: 195
failed_requests: 5
average_response_time_ms: 110
memory_usage_mb: 270
cpu_usage_percent: 80
```
8) В файле app_metrics найти метрики, относящиеся к cpu
9) Из файла app_metrics получить занчение метрики average_response_time_ms
10) В файле app_metrics найти метрики, относящиеся к response_time и из них вывести значение метрики max_response_time
11) Выполнить команду uptime и вывести значения load average
12) Получить из вывода команды free -h размер доступной памяти (available)
13) Получить из вывода команды lscpu количество ядер (CPU(s))
14) В директории text_processing создать файл nginx.conf с содержимым
```
user www-data;
worker_processes auto;

events {
    worker_connections 1024;
}

http {
    include /etc/nginx/mime.types;
    default_type application/octet-stream;
    upstream backend {
        server 10.0.0.1;  
        server 10.0.0.2;  
        server 10.0.0.3; 
        # server 10.0.0.1 weight=3; 
        # server 10.0.0.2 max_fails=2 fail_timeout=30s;
    }
    server {
        listen 80; 
        server_name example.com;

        location / {
            proxy_pass http://backend;  
            proxy_set_header Host $host; 
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
}
```
15) В файле nginx.conf найти server_name и вывести только его значение
16) В файле nginx.conf найти все активные upstream (активный, значит в строке перед server не стоит знак #)
17) В файле nginx.conf найти все header и вывести их значения
18) В директории text_processing создать файл php-fpm.conf с содержимым
```
;;;;;;;;;;;;;;;;;;;;;
; FPM Configuration ;
;;;;;;;;;;;;;;;;;;;;;

; Global Options
[global]

pid = /run/php/php-fpm.pid

error_log = /var/log/php-fpm.log

log_level = notice

daemonize = yes

; syslog.facility = daemon
; syslog.ident = php-fpm

rlimit_files = 1024

;;;;;;;;;;;;;;;;;;
; Pool Definitions ;
;;;;;;;;;;;;;;;;;;

[www]

user = www-data
group = www-data

listen = /var/run/php/php-fpm.sock

listen.owner = www-data
listen.group = www-data
listen.mode = 0660

pm = dynamic
pm.max_children = 50
pm.start_servers = 5
pm.min_spare_servers = 5
pm.max_spare_servers = 10
pm.process_idle_timeout = 10s;

pm.max_requests = 500

php_admin_value[error_log] = /var/log/php-fpm/www-error.log
php_admin_flag[log_errors] = on

php_value[memory_limit] = 128M
php_value[max_execution_time] = 30

php_admin_value[disable_functions] = exec,passthru,shell_exec,system
```
19) В файле php-fpm.conf найти пользователя и группу
20) В файле php-fpm.conf найти значение listen
21) В файле php-fpm.conf найти куда пишется error_log
22) Вывести файл /etc/ssh/sshd_config без строк, начинающихся с #

## Часть 2
1) В директории linux_labs создать папку confs
2) Скопировать из директории text_processing файлы php-fpm.conf и nginx.conf в confs
3) Проверить с помощь grep и файла /etc/passwd, существуют ли пользователи www-data и php-fpm, если нет, то создать их
4) Сделать владельцем файла php-fpm.conf пользователя php-fpm, а группой владельцев - www-data
5) Сделать владельцем файла nginx.conf пользователя www-data, а группой владельцев - php-fpm
6) Создать пользователя devops
7) Добавить пользователя devops в группы php-fpm и www-data
8) Получить из файлов /etc/passwd и /etc/group информацию о добавленном пользователе (его id и в каких группах он состоит)
9) В директории confs создать директорию redis
10) В директории redis создать файл redis.conf
11) Посмотреть режим доступа на файл redis.conf
12) Добавить всем пользователям бит x на файл redis.conf
13) Убрать бит x у всех пользователей на файл redis.conf
14) В директории confs создать файл env
15) Установить права доступа так, чтобы только владелец мог читать и записывать в него, а остальные пользователи не имели никакого доступа
16) Установить права на файл redis.conf так, чтобы владелец имел полные права (чтение, запись, выполнение), группа могла только читать, а остальные пользователи не имели доступа
17) В директории confs создать файл inv
18) Установить права на файл inv так, чтобы владелец мог читать и записывать, группа могла читать и записывать, а остальные пользователи не имели доступа
19) В директории confs создать директорию private
20) Установить права на директорию private так, чтобы только владелец может читать и записывать файлы, а остальные пользователи не имеют прав
