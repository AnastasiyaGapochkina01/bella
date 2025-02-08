1) Создать github репозиторий go_workers, в нем создать файлы
- server.go
```
package main

import (
	"fmt"
	"log"
	"net/http"
	"os"
)

func main() {
	port := os.Args[1] 
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "Hello, Go from forked process!\n")
		log.Printf("Request from: %s %s\n", r.Method, r.URL.Path)
	})

	addr := ":" + port
	log.Printf("Server listening on %s\n", addr)
	log.Fatal(http.ListenAndServe(addr, nil))
}
```
- main.go
```
package main

import (
	"fmt"
	"io/ioutil"
	"log"
	"os"
	"os/exec"
	"strconv"
)

func main() {
	port := os.Getenv("PORT")
	if port == "" {
		port = "3000"
	}

	// Path to the PID file
	pidFile := "/run/goserver.pid"

	// Fork the actual server process
	cmd := exec.Command("./server", port) 
	err := cmd.Start()
	if err != nil {
		log.Fatalf("Failed to start server process: %v", err)
	}
	fmt.Printf("Server process started with PID: %d\n", cmd.Process.Pid)

	pid := cmd.Process.Pid
	pidStr := strconv.Itoa(pid)
	err = ioutil.WriteFile(pidFile, []byte(pidStr), 0644)
	if err != nil {
		log.Fatalf("Failed to write PID to file: %v", err)
	}
	fmt.Printf("PID written to %s\n", pidFile)

	os.Exit(0)
}
```
- Dockerfile
```
FROM golang AS builder
WORKDIR /app
COPY *.go ./
RUN CGO_ENABLED=0 GOOS=linux go build ./main.go
RUN CGO_ENABLED=0 GOOS=linux go build -o server ./server.go

FROM alpine
WORKDIR /server
COPY ./docker-entrypoint.sh ./
COPY --from=builder /app/main ./
COPY --from=builder /app/server ./
ENTRYPOINT ["/server/docker-entrypoint.sh"]
```
- docker-entrypoint.sh
```
#!/bin/sh
./server "$PORT"
```
2) Подключить репозиторий к jenkins
3) Написать pipeline, который будет собирать image и пушить его в docker hub
