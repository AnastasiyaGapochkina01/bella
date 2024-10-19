1) В домашней диреткории создать папку text_processing
2) В text_processing создать файл products с содержимым
```
Handle:Title:SKU:Location:On hand:Available:Count
product-1:Product A:PROD-A:Warehouse A:100
product-1:Product A:PROD-A:Warehouse A:50
product-2:Product B:PROD-B:Warehouse B:200
product-2:Product B:PROD-B:Warehouse B:150
product-3:Product C:PROD-C:Warehouse C:300
product-4:Product D:PROD-D:Warehouse A:400
product-4:Product D:PROD-D:Warehouse A:250
product-5:Product E:PROD-E:Warehouse B:500
product-5:Product E:PROD-E:Warehouse B:300
product-6:Product F:PROD-F:Warehouse C:600
product-6:Product F:PROD-F:Warehouse C:400
```
3) С помощью grep найти в файле products все строки, содержащие слово PROD-C
4) С помощью grep найти в файле products все строки, содержащие слово product-3 и вывести для них последний столбец
5) С помощью grep найти в файле products все строки, у которых столбец Available равен C и для них вывести первый и последний столбец
6) В директории text_processing создать файл hosts с содержимым
```
hostname,interval,timestamp,%user,%system,%memory
sel-srv1,600,2023-10-08 00:00:01 UTC,30.01,20.77,96.21
sel-srv1,600,2023-10-08 00:05:01 UTC,40.07,13.00,84.55
sel-srv1,600,2023-10-08 00:10:01 UTC,5.00,90.55,89.23
sel-srv2,600,2023-10-09 00:15:01 UTC,25.01,15.77,92.21
sel-srv3,600,2023-10-09 00:20:01 UTC,35.07,10.00,80.55
sel-srv3,600,2023-10-09 00:25:01 UTC,10.00,85.55,88.23
sel-srv2,600,2023-10-09 00:30:01 UTC,20.01,25.77,95.21
sel-srv2,600,2023-10-09 00:35:01 UTC,45.07,12.00,82.55
sel-srv3,600,2023-10-09 00:40:01 UTC,15.00,80.55,87.23
```
7) С помощью grep найти в файле hosts строки, содержащие sel-srv2 и вывести 3 столбец
8) С помощью grep найти в файле hosts строки, содержащие дату 2023-10-08
9) Отфильровать вывод команды lscpu так, чтобы получить значение CPU MHz
10) Отфильровать вывод команды lscpu так, чтобы получить значение Hypervisor vendor
11) Из файла /proc/meminfo получить все строки. относящиеся к HugePages
12) Отфильтровать вывод команды lsblk так, чтобы получить все разделы (раздел это та строка, где 6 поле имеет значение part)
13) Для полученных в предыдущем задании разделов вывести их имена
14) С помощью awk вывести из файла /etc/passwd имена всех пользователей (первое поле)
15) С помощью awk вывести из файла /etc/passwd последнее поле
16) Отфильтровать вывод команды free -h так, чтобы получить размер Swap
17) Из файла text_processing/products с помощью awk вывести все строки, содержащие слово PROD-C
18) Из файла text_processing/products с помощью awk вывести все строки, содержащие слово product-3 и вывести для них последний столбец
19) С помощью grep найти в файле /etc/passwd пользователя games и вывести для него первое, третье и последнее поля
20) С помощью grep найти в файле /proc/meminfo информацию о HugePages
