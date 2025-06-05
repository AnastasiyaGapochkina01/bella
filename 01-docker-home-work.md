1) Запустить контейнер nginx:
- создать и прокинуть внутрь контейнера папку app (монтировать в /usr/share/nginx/html)
- в папке app создать файл index.html с таким содержимым
```
<Html>    
<Head>  
<title>  
Example of make a text B,I,U  
</title>  
</Head>  
<Body>   
<b> [This text is Bold......] </b>  
<I> [This text is Italic......] </I>  
<U> [This text is Underline......] </U>   
</Body>  
</Html> 
```
- вывесить порт 80 из контейнера на порт хоста 8090 
- при выполнении curl на ip:port должна отдаваться страница из п2
2) Запустить контейнер с mongodb:
- задать переменную ME_CONFIG_MONGODB_ADMINUSERNAME со значением admin
- задать переменную ME_CONFIG_MONGODB_ADMINPASSWORD со значением adminpassword
- создать директорию mongo_data и смонитировать ее внутрь контейнера в /data/db
- вывесить дефолтный порт монги на хост
3) Запустить контейнер с postgres 15:
- задать переменную POSTGRES_PASSWORD со значением passwd
- создать директорию pg_data и прокинуть ее в контейнер по пути /var/lib/postgresql/data
4) Дан код на python
```
from flask import Flask
import sys
import os

app = Flask(__name__)

@app.route('/')
def index():
    python_version = sys.version
    current_directory = os.getcwd()
    return f"Версия Python: {python_version}\nТекущая директория: {current_directory}"

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')
```
Необходимо собрать для него docker image и запустить из него контейненр. Для работы приложения требуется установить flask, запуск осуществляется командой ```python app.py```\
Проверить работоспособность можно комнандой ```curl 127.0.0.1:5000```. Если отдается что-то похожее на
```
anestesia@projects-dev:~$ curl 127.0.0.1:5000
Версия Python: 3.9.2 (default, Mar 20 2025, 02:07:39)
[GCC 10.2.1 20210110]
Текущая директория: /home/anestesia/python
```
то все ОК
5) Дан код на nodejs:
- `server.js`
```
const http = require('http');
const os = require('os');
const childProcess = require('child_process');

const getNodeVersion = () => {
    return childProcess.execSync('node -v').toString().trim();
};

const getOSVersion = () => {
    return os.type() + ' ' + os.release();
};

const server = http.createServer((req, res) => {
    const nodeVersion = getNodeVersion();
    const osVersion = getOSVersion();

    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end(`Версия Node.js: ${nodeVersion}\nВерсия ОС: ${osVersion}`);
});

server.listen(3000, () => {
    console.log('Сервер запущен на порту 3000');
});
```
- `package.json`
```
{
  "name": "node-info-app",
  "version": "1.0.0",
  "description": "",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "anestesia",
  "license": "ISC",
  "dependencies": {
    "express": "^4.21.1"
  },
  "scripts": {
	  "start": "node server.js"
  }
}
```
Необходимо собрать для него docker image и запустить из него контейненр. Запуск приложения осуществляется командой ```npm start```
Проверить работоспособность можно командой ```curl 127.0.0.1:3030```. Если отдается что-то похожее на
```
anestesia@projects-dev:~/node-server$ curl 127.0.0.1:3002
Версия Node.js: v23.11.0
Версия ОС: Linux 5.10.0-19-amd64
```
то все ОК
