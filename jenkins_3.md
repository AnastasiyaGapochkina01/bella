1) Создат форк репозитория https://github.com/AnastasiyaGapochkina01/actions-test
2) Написать compose.yml для запуска этого приложения через docker compose
3) Написать пайплайн Jenkins, который будет
- собирать docker image и пушить его в docker hub
- деплоить приложение с помощью docker compose
- тестировать запущенное в контейнере приложение
  - зайти в контейнер с помощью docker exec
  - выполнить команду ```npx mocha test/app.test.js```
- оповещать о результате сборки в telegram
