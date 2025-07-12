# Часть 1
## Инфраструктура
| server_name  | public_ipv4 | OS | role |
| ------------- | ------------- | ------------- | ------------- |
| edy-server-1  | 89.169.182.203  | Ubuntu 24.04 | application server |
| edy-server-2  | 89.169.181.190  | Debian 12 | database server |
| edy-balancer-1 | 89.169.185.219 | Ubuntu 24.04 | web-server, balancer |

## Проект - CMDB
### Описание
Система для управления инфраструктурой: содержит необходимую информацию об аппаратных и программных компонентах инфраструктуры. 

Работает на домене https://cmdb.anestesia.fun/
### Стек
1) Фронтенд: HTML5, CSS3, JavaScript (ES6)
2) Бэкенд: Python Flask
3) База данных: MariaDB
4) Веб-сервер: Nginx
### API Endpoints
| Метод |	Endpoint | Описание |
| ------------- | ------------- | ------------- |
| GET |	/api/assets	| Получить все активы |
| POST | /api/assets	| Создать новый актив |
| PUT	| /api/assets/:id |	Обновить актив |
| DELETE | /api/assets/:id	| Удалить актив |

Примеры запросов 
```bash
# Создать актив
curl -X POST http://localhost/api/assets \
  -H "Content-Type: application/json" \
  -d '{"name": "Web Server", "type": "server", "description": "Production web server"}'

# Получить все активы
curl http://localhost/api/assets
```
