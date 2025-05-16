Проект: "App Sandbox" — создание изолированных среды для пользователей, где они могут запускать свои приложения

1) Создать корневую директорию `/sandbox`\
Внутри нее:
- `apps/` — для пользовательских приложений (каждый пользователь имеет свою поддиректорию, например, `/sandbox/apps/user1`).
- `bin/` — для общих скриптов управления.
- `units/` — для systemd юнит-файлов.
2) Создать группу sandbox_users.
3) Создать пользователей (например, alice, bob) и добавить их в группу.
4) Настроить права:
- Пользователи имеют полный доступ только к своим директориям в `/sandbox/apps`.
- Группа sandbox_users может читать/запускать скрипты в `/sandbox/bin`.
5) Создать скрипт `/sandbox/bin/create_app.sh`, который:
- Принимает имя пользователя и название приложения.
- Создает директорию для приложения.
6) Написать systemd юнит-файл для запуска скрипта (скрипт написать в директории, инициализированной с помощью `/sandbox/bin/create_app.sh`)
```
#!/usr/bin/env python3

import time
import signal
import sys

running = True

def handle_sigterm(signum, frame):
    global running
    running = False

signal.signal(signal.SIGTERM, handle_sigterm)
signal.signal(signal.SIGINT, handle_sigterm)

def main():
    while running:
        # Здесь размещается основная логика демона
        print("Демон работает...")
        time.sleep(5)
    print("Демон завершает работу.")

if __name__ == "__main__":
    main()

```
