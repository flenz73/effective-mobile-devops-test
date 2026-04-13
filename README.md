# Effective Mobile — тестовое задание (DevOps)

Небольшой проект из двух контейнеров:
- `backend` на Python отвечает текстом `Hello from Effective Mobile!`
- `nginx` принимает запросы с хоста и проксирует их в backend

## Что внутри

```text
.
├── .env.example
├── backend/
│   ├── app.py
│   └── Dockerfile
├── nginx/
│   └── nginx.conf
├── docker-compose.yml
└── README.md
```

## Требования

- Docker
- Docker Compose (plugin `docker compose`)

## Как запустить

1. Перейти в директорию проекта:

   ```bash
   cd EffectiveMobile
   ```

2. Создать `.env` из примера:

   ```bash
   cp .env.example .env
   ```

3. Запустить сервисы:

   ```bash
   docker compose up --build -d
   ```

4. Проверить, что контейнеры поднялись:

   ```bash
   docker compose ps
   ```

## Проверка результата

Команда:

```bash
curl http://localhost
```

Ожидаемый ответ:

```text
Hello from Effective Mobile!
```

## Как работает схема

`nginx` слушает `80` порт на хосте и проксирует `GET /` на `backend:8080` внутри docker-сети.

Backend наружу не публикуется (только `expose`), поэтому доступ к нему есть только из контейнерной сети.

```text
Client -> localhost:80 -> nginx -> backend:8080 -> "Hello from Effective Mobile!"
```

## Дополнительно

- Для backend используется отдельный `Dockerfile`
- Для nginx подключен отдельный конфиг `nginx/nginx.conf`
- В `docker-compose.yml` добавлены healthcheck для обоих сервисов
- Порт наружу проброшен только у nginx

## Остановка

```bash
docker compose down
```
