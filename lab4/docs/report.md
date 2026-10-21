# Отчёт по лабораторной работе №4. n8n

**Способ установки:** Docker Desktop (образ `n8nio/n8n:latest`)

**Команда запуска:**
```
docker volume create n8n_data

docker run -it --rm \
 --name n8n \
 -p 5678:5678 \
 -e GENERIC_TIMEZONE="Europe/Minsk" \
 -e TZ="Europe/Minsk" \
 -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true \
 -e N8N_RUNNERS_ENABLED=true \
 -v n8n_data:/home/node/.n8n \
 n8nio/n8n
```