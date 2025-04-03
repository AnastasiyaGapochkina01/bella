1) В ломашней директории создать директорию linux_labs
2) В директории linux_labs создать директорию storage
3) Не переходя в директорию storage создать в ней директории media, src и docs
4) В директории media создать пустые файлы less_01, less_02, less_03
5) В директории src создать файлы
- example_01.py с содержимым
```
from flask import Flask

app = Flask(__name__)


# the minimal Flask application
@app.route('/')
def index():
    return '<h1>Hello, World!</h1>'
```
- example_02.go с содержимым
```
package main
import (
    "fmt"
    "html"
    "log"
    "net/http"
)
func main() {
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Hello, %q", html.EscapeString(r.URL.Path))
    })
    http.HandleFunc("/hi", func(w http.ResponseWriter, r *http.Request){
        fmt.Fprintf(w, "Hi")
    })
    log.Fatal(http.ListenAndServe(":8081", nil))
}
```
- example_03.conf с содержимым
```
server {
    listen 80;
    server_name site1.com www.site1.com;

    location / {
        proxy_pass http://backend1.local;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
server {
    listen 80;
    server_name site2.com www.site2.com;

    location / {
        proxy_pass http://backend2.local;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

server {
    listen 80;
    server_name site3.com www.site3.com;

    location / {
        proxy_pass http://backend3.local;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

server {
    listen 80;
    server_name site4.com www.site4.com;

    location / {
        proxy_pass http://backend4.local;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

# Сайт 5
server {
    listen 80;
    server_name site5.com www.site5.com;

    location / {
        proxy_pass http://backend5.local;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

server {
    listen 80;
    server_name site6.com www.site6.com;

    location / {
        proxy_pass http://backend6.local;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

server {
    listen 80;
    server_name site7.com www.site7.com;

    location / {
        proxy_pass http://backend7.local;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

server {
    listen 80;
    server_name site8.com www.site8.com;

    location / {
        proxy_pass http://backend8.local;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

server {
    listen 80;
    server_name site9.com www.site9.com;

    location / {
        proxy_pass http://backend9.local;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

server {
    listen 80;
    server_name site10.com www.site10.com;

    location / {
        proxy_pass http://backend10.local;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

```
6) В директории docs создать файл readme.md с содержимым
```
# This is lessons project
```
7) Переместить файл docs/readme.md в директорию linux_labs/storage
8) Переименовать файлы less_01, less_02, less_03 в lesson_01.pptx, lesson_02.pptx, lesson_03.pptx
9) В директории linux_labs создать директорию backups
10) Скопировать __ВСЕ__ содержимое storage в backups
11) Переименовать backups/storage в storage_bkp
