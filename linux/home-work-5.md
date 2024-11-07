1) Написать юнит-файл для запуска [скрипта](https://gist.github.com/AnastasiyaGapochkina01/8e77f63f288139e5ddd87b105d1e3c12) как сервиса systemd, создать таймер для периодического выполнения задачи
про таймеры тут https://youtu.be/hTkaCE5Mz8I
если сервис хотя бы раз удачно отработал, то должен появиться файл /var/log/dsk-usage.log с записью примерно такого вида
```
1730956510 [ALARM] Disk usage for / is greater then 5: current value is 35
```
2) Написать юнит-файл для запуска простого [веб-сервера на python](https://gist.github.com/AnastasiyaGapochkina01/ac33a8174326f80a1af1ed9f4754541e). После того как сервис запустится выполнить команду
```
curl 127.0.0.1:9999
```
ответ должен быть _Hello from Python_
