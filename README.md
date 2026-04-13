# Артвелл — система управления исполнительной документацией

Веб-интерфейс для загрузки, валидации и хранения строительных документов в формате XML.

## Быстрый старт

### 1) Запуск бэкенда (xml-doc-flow-backend)

Требования: установленный Docker Desktop.

В отдельном терминале:

```bash
cd xml-doc-flow-backend
docker compose up --build
```

Порты по умолчанию:
- **PostgreSQL**: `localhost:5432` (db `xml_doc_flow`, user/pass `xml_doc_flow`)
- **Backend**: `http://localhost:8080` (OpenAPI `docs/api.yaml`)

### 2) Запуск фронтенда (xml-doc-flow-frontend)

Откройте `index.html` **через локальный HTTP‑сервер** (иначе возможны ограничения для `file://`).
Важно: фронтенд запускайте на **другом порту**, чтобы не пересекаться с бэкендом на `8080`.

```bash
cd xml-doc-flow-frontend
python3 -m http.server 3000
```

Затем перейдите в браузере на `http://127.0.0.1:3000/`.

### 3) Подключение к API (Basic Auth)

Фронтенд использует **session-based login** через `/api/auth/login` и cookie-сессию.

Тестовые пользователи:
- `contractor` / пароль из `APP_SEED_DEMO_PASSWORD` (по умолчанию `artwell-local-2026!`)
- `customer` / пароль из `APP_SEED_DEMO_PASSWORD` (по умолчанию `artwell-local-2026!`)

## Структура

См. `scheme.txt`. Скрипты подключаются в порядке: `js/data.js` → `js/api.js` → `js/app.js`.

## Бэкенд

`js/api.js` использует `API_CONFIG.baseUrl = http://localhost:8080/api` и эндпоинты из `xml-doc-flow-backend/docs/api.yaml`, а также `/api/auth/*`.

Стартовый экран — **Документы**.