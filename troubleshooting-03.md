# Вводная
На ВМ edy-server-1 с помощью docker развернуто приложение Grades Tracker.\
Исходный код лежит в папке `/var/www/grade_tracker`. Все файлы докера уже есть, приложение не запускается. Надо починить

## Проверка работоспособности
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"name":"Анна Ковалева","grade":5,"subject":"Химия","date":"2023-09-20"}' \
http://localhost:3000/grades
```

```bash
curl http://localhost:3000/grades
```

## Дополнительно
- Добавить healthcheck для mariadb
- Добавить перед приложением nginx в роли reverse proxy
