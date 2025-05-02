# Часть 1
1) В директории /opt создать директорию services
2) В директории /opt/services создать файл web-server.go
```
package main

import (
	"encoding/json"
	"fmt"
	"net/http"
)

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "Hello, world!\n")
	})

	http.HandleFunc("/ping", func(w http.ResponseWriter, r *http.Request) {
		w.Header().Set("Content-Type", "application/json")
		json.NewEncoder(w).Encode(map[string]string{
			"status":  "ok",
			"version": "1.0",
		})
	})

	// Запуск сервера на порту 8080
	fmt.Println("Server started at http://localhost:8080")
	if err := http.ListenAndServe(":8080", nil); err != nil {
		fmt.Printf("Server error: %v\n", err)
	}
}
```
3) Установить golang (если еще не установлен)
4) Написать systemd юнит для программы web-server.go и запустить ее как демон
- проверка осуществляется командами
```
anestesia@a-tech-compute-1 scripts $ curl 127.0.0.1:8080
Hello, world!
anestesia@a-tech-compute-1 scripts $ curl 127.0.0.1:8080/ping
{"status":"ok","version":"1.0"}
```
# Часть 2
1) В директории /opt/services создать файл simple_info.py
```
import http.server
import socket
import os
import getpass

# Получаем имя пользователя
username = getpass.getuser()

# Получаем версию ОС
os_version = f"{os.sys.platform} {os.sys.version}"

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
s.connect(("8.8.8.8", 80))
local_ip = s.getsockname()[0]
s.close()

greeting = f"Привет, {username}!"

class RequestHandler(http.server.BaseHTTPRequestHandler):
    def do_GET(self):
        if self.path != "/":
            self.send_response(404)
            self.send_header("Content-type", "text/plain")
            self.end_headers()
            self.wfile.write(b"404 Not Found")
            return

        self.send_response(200)
        self.send_header("Content-type", "text/plain")
        self.end_headers()

        response = f"Версия ОС: {os_version}\nПриветствие: {greeting}\nЛокальный IP: {local_ip}"
        self.wfile.write(response.encode())

def run_server():
    server_address = ('', 3000)
    httpd = http.server.HTTPServer(server_address, RequestHandler)
    print("Сервер запущен на порту 3000")
    httpd.serve_forever()

if __name__ == "__main__":
    run_server()
```
2) Написать systemd юнит для запуска этого кода как демона
- проверка осуществляется командой
```
anestesia@a-tech-compute-1 scripts $ curl 127.0.0.1:3000
Версия ОС: linux 3.8.10 (default, Mar 18 2025, 20:04:55)
[GCC 9.4.0]
Приветствие: Привет, anestesia!
Локальный IP: 10.129.0.12
```
# Часть 3
1) В директории /opt/services создать файл simple_server.js
```
const http = require('http');
const os = require('os');

const server = http.createServer((req, res) => {
  // Роутинг
  switch(req.url) {
    case '/':
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.end('Hello, world!\n');
      break;

    case '/ping':
      res.writeHead(200, {'Content-Type': 'application/json'});
      res.end(JSON.stringify({
        status: 'ok',
        version: process.versions.node,
        hostname: os.hostname()
      }));
      break;

    default:
      res.writeHead(404);
      res.end();
  }
});

// Получение порта из переменной окружения
const port = process.env.PORT || 8080;

server.listen(port, () => {
  console.log(`Server running at http://localhost:${port}`);
});


// Обработка ошибок
server.on('error', (err) => {
  console.error('Server error:', err);
});
```
2) Написать systemd юнит для запуска этого кода как демона
- проверка осуществляется командой
```
anestesia@a-tech-compute-1 scripts $ curl 127.0.0.1:8080
Hello, world!
```
