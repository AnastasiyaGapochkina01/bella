1) Написать параметизированный Freestyle Job, который выводит на экран строку `Building project-1 for version v1`, где
- `project-1` - параметр типа строка
- `v1` - параметр-выбор из списка (v1.0, v2.0 и тд)
2) Написать параметизированный Freestyle Job, который мониторит систему. Параметры:
- SERVER_IP (строка)
- CHECK_TYPE (выбор: disk/cpu/memory)
3) Написать Freestyle Job, который делает ежедневный дамп PostgreSQL
4) Написать Freestyle Job, который деплоит проект https://github.com/AnastasiyaGapochkina01/nuxt
```bash
npm ci --cache .npm --prefer-offline
npm run generate
```
