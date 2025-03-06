Дан репозиторий с тремя Dockerfile - https://github.com/AnastasiyaGapochkina01/jenkins_params_ex/tree/main.\
Написать пайплайн, который будет
1) Собирать image на основе выбранного при запуске dockerfile
2) Пушить собранный image в docker hub
3) Если при запуске установлена галка Run Deploy, то производить деплой собранного image на удаленный хост
