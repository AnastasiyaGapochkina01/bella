# Часть 1
1) Создать репозиторий jenkins-php
2) Создать в репозитории файлы
- index.php
```
<?php
if (!defined('PHPUNIT_TEST')) {
    header('Content-Type: application/json');
}

// Dummy response
echo json_encode([
    'status' => 'success',
    'message' => 'Hello from Docker PHP!'
]);
?>
```
- Dockerfile
```
FROM php:8.1-apache

WORKDIR /var/www/html

COPY index.php /var/www/html/

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

RUN a2enmod rewrite

EXPOSE 80
```
3) Подключить репозиторий к jenkins
4) Написать pipeline, который будет собирать image и пушить его в docker hub
# Часть 2
1) Сделать форк или самостоятельную копию репозитория https://github.com/AnastasiyaGapochkina01/node-app
2) Написать Dockerfile для приложения
3) Подключить репозиторий к jenkins
4) Написать pipeline, который будет собирать image и пушить его в docker hub
