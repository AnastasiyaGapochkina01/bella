# Система организации файлов
1) Создать корневую директорию `/global/media` с подпапками:
- incoming (для новых файлов)
- processed (для отсортированных файлов)
- reports (для текстовых отчетов)
2) Создать группу `media_users`
- группа `media_users` должна иметь полный доступ ко всем директориям.
- остальные пользователи — только чтение
3) Написать скрипт `processor.sh`, который:
- берет файлы из `/global/media/incoming`.
- используя `exiftool`, извлекает дату создания из метаданных.
- переименовывает файл в формат `DD-MM-YYY_HH-MM-SS_filename.расширение`.
- перемещает файл в `/global/media/processed/YYYY/MM/DD`
- обработать ошибки (например, отсутствие метаданных)
4) Создать 3 пользователя: `editor`, `viewer`, `guest`
- добавить `editor` и `viewer` в группу `media_users`
- запретить `guest` доступ к `/global/media/processed`
5) Создать сервис `media-processor.service`, который запускает скрипт `processor.sh` и .path-юнит для отслеживания изменений в incoming
> [!TIP]
> про path юнит можно почитать тут https://habr.com/ru/articles/536040/
6) Написать скрипт `report.sh`  который:
- собирает данные о количестве файлов в `/global/media/processed` по месяцам/дням
- сохраняет отчет в `/global/media/reports/report_ГГГГ-ММ-ДД.txt`
