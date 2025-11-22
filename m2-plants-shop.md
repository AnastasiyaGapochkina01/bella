# Установка
## Mariadb
Приниципиальна версия 11.4. Ставим
```bash
curl -LsS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup | sudo bash -s -- --mariadb-server-version=11.4
apt update
apt install -y mariadb-server mariadb-client
mysql_secure_installation

mysql -uroot -p
```
Создаем БД и пользователя
```sql
CREATE USER 'magento'@'localhost' IDENTIFIED BY 'password';
create database magento;
grant all privileges on magento.* to 'magento'@'localhost';
flush privileges;
exit
```
## Nginx + PHP
Ставим nginx и php
```bash
sudo apt install nginx php8.3 php8.3-fpm php8.3-common php8.3-gmp php8.3-curl php8.3-soap php8.3-bcmath php8.3-intl php8.3-mbstring php8.3-xmlrpc php8.3-mysql php8.3-gd php8.3-xml php8.3-cli php8.3-zip -y
```
Ставим composer (нужен для установки зависимостей php)
```bash
curl -sS https://getcomposer.org/installer | php

sudo mv composer.phar /usr/local/bin/composer
```

## M2
Ключи либо сгенируй на сайте adobe сама (https://commercemarketplace.adobe.com/customer/accessKeys/) либо на той тачке, что мне давала в `/var/www/.config/composer/auth.json`

```bash
sudo apt install -y unzip
sudo chown -R www-data:www-data
sudo vim /etc/passwd
# в этом файлике поменяй пользаку www-data последнее поле на /bin/bash
sudo su - www-data
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition /var/www/plants-shop
cd /var/www/plants-shop
php bin/magento setup:install \
  --base-url=http://18.219.201.97 \
  --db-host=localhost \
  --db-name=magento \
  --db-user=magento \
  --db-password=password \
  --admin-firstname=Admin \
  --admin-lastname=User \
  --admin-email=admin@example.com \
  --admin-user=adminuser \
  --admin-password=admin123 \
  --language=en_US \
  --currency=USD \
  --timezone=America/New_York \
  --use-rewrites=1

exit 
```

## Конфигурируем Nginx

`sudo nano /etc/nginx/sites-available/magento`
```text
upstream fastcgi_backend {
  server  unix:/run/php/php8.3-fpm.sock;
}

server {

  listen 80;
  server_name 18.219.201.97;
  set $MAGE_ROOT /var/www/plants-shop;
  include /var/www/plants-shop/nginx.conf.sample;
}
```

```bash
sudo ln -s /etc/nginx/sites-available/magento /etc/nginx/sites-enabled/
sudo nginx -t
sudo nginx -s reload
```

## Ставим тему
```bash
cd

wget https://d39kc01zfxgus5.cloudfront.net/2021/08/theme-30074.zip
unzip theme-30074.zip
sudo rsync -a app/ var/www/plants-shop/app/
sudo chown -R www-data:www-data /var/www/plants-shop
sudo su - www-data
cd /var/www/plants-shop
composer require laminas/laminas-serializer
```
Затем в `/var/www/bloomly/app/design/frontend/theme-30074/theme-30074/Magento_Checkout/templates/cart/minicart.phtml` Zend_Json меянем на Laminas\Json\Json

Применяем изменения
```bash
php bin/magento setup:upgrade
php bin/magento setup:static-content:deploy -f
php bin/magento cache:clean
```
Потом идем в админку и тыкаем кнопочки

<img width="587" height="260" alt="image" src="https://github.com/user-attachments/assets/ce2a3726-cec6-42c0-92bb-70d485cecdd5" />


По итогу должно получиться
<img width="1434" height="761" alt="image" src="https://github.com/user-attachments/assets/83964036-f20d-473a-b4c9-9985018d4707" />
