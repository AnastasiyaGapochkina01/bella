1) Запустить в docker приложение на php
```php
<?php
if (!defined('PHPUNIT_TEST')) {
    header('Content-Type: application/json');
}

// Dummy response
echo json_encode([
    'status' => 'success',
    'message' => 'Hello from Docker PHP!'
]);
?>
```
И написать к нему pipeline, который  будет собирать image, пушить его в docker hub и деплоить его

2) Запустить в docker приложение https://github.com/AnastasiyaGapochkina01/node-app и написать pipeline, который  будет собирать image, пушить его в docker hub и деплоить его
3) Запустить в docker приложение
```go
package main

import (
	"encoding/json"
	"math/rand"
	"net/http"
	"time"
)

type Metrics struct {
	Status string `json:"status"`
	Data   struct {
		Metrics struct {
			CPU     float64 `json:"cpu_usage"`
			Memory  float64 `json:"memory_usage"`
			Threads int     `json:"thread_count"`
		} `json:"metrics"`
	} `json:"data"`
}

func main() {
	rand.Seed(time.Now().UnixNano())

	http.HandleFunc("/metrics", func(w http.ResponseWriter, r *http.Request) {
		w.Header().Set("Content-Type", "application/json")

		metrics := Metrics{Status: "success"}
		metrics.Data.Metrics.CPU = rand.Float64()
		metrics.Data.Metrics.Memory = rand.Float64() * 100
		metrics.Data.Metrics.Threads = rand.Intn(500) + 1

		json.NewEncoder(w).Encode(metrics)
	})

	http.ListenAndServe(":9200", nil)
}
```
И написать к нему pipeline, который  будет собирать image, пушить его в docker hub, деплоить его и потом проверять его работоспособность с помощью запроса
```bash
curl http://localhost:9200/metrics
```
Пример ответа
```json
{
  "status": "success",
  "data": {
    "metrics": {
      "cpu_usage": 0.754,
      "memory_usage": 34.21,
      "thread_count": 287
    }
  }
}
```
4) Для написанных пайплайнов настроить деплой по пушу в репозиторий
