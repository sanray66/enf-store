# Enf-store — магазин одежды

Интернет-магазин одежды на Django с онлайн-оплатой. Управление каталогом и заказами через админ-панель Django.

## Стек

- Python, Django
- PostgreSQL
- Alpine.js + htmx
- Gunicorn + Nginx
- Docker, Docker Compose
- платёжная система Sprite (бета)

## Возможности

- каталог товаров [с категориями / размерами / фильтрами]
- корзина и оформление заказа
- онлайн-оплата через Sprite (бета, тестовый режим)
- динамические обновления страниц без перезагрузки (htmx)
- управление товарами, заказами и пользователями через админку Django


## Архитектура

Три контейнера в Docker Compose:

- `db` — PostgreSQL, данные в volume, есть healthcheck
- `web` — Django за Gunicorn, миграции применяются при старте
- `nginx` — реверс-прокси, раздаёт статику и медиа, терминирует HTTPS

## Запуск

```bash
git clone <ссылка>
cd <папка>
cp .env.example .env     # заполните значения
docker compose up --build
```

Создать администратора:

```bash
docker compose exec web python manage.py createsuperuser
```

админка: /admin/

## Настройки для env 
```bash

  SECRET_KEY='example'
  
  POSTGRES_DB=enfdb
  POSTGRES_USER=enfdb
  POSTGRES_PASSWORD=enfdb
  POSTGRES_HOST=localhost # db если запускаете на vps
  POSTGRES_PORT=5432
  
  STRIPE_SECRET_KEY='example'
  STRIPE_WEBHOOK_SECRET='example'

```
