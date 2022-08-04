# infra_sp2:

## Описание:

Контейнер с API для проектра YaMDb.

Проект YaMDb собирает отзывы пользователей на произведения.
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
Произведения разделены на категории. Произведению может быть присвоен жанр.
Произведения и жанры могут добывалять только администраторы.
Пользователи могут оставлять отзывы и выставлять оценку.
На основе оценок составляется рейтинг произведения.

## Технологии:
Python 3.7, 
Django 2.2.19, 
PostgreSQL, 
Docker, 
Nginx

## Шаблон наполнения env-файла:

```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
SECRET_KEY=p&l%385147kslhtyn^##a1)ilz@4zqj=rq&agdol^##zgl9(vs
```

## Как запустить проект:

Клонировать репозиторий с Docker Hub:

```
docker pull kirppu/api_yamdb:v1.2
```

Создать и запустить контейнеры:

```
docker run api_yamdb
```

Выполните миграции:

```
docker-compose exec web python manage.py migrate
```
Для создания суперпользователя введите:

```
docker-compose exec web python manage.py createsuperuser
```

Запустите команду для сбора статики:

```
docker-compose exec web python manage.py collectstatic --no-input
```
Команда для загрузки базы данных из дампа:

```
docker-compose exec web python manage.py loaddata dump.json
```

## Примеры:
Проект доступен по [localhost](http://localhost/)

Регистрация новго пользователя.

POST /api/v1/auth/signup/

```
{
    "email": "string",
    "username": "string"
}
```

Получение JWT-токена.

POST /api/v1/auth/token/

```
{
    "username": "string",
    "confirmation_code": "string"
}
```

Получение информации о произведении.

GET /api/v1/titles/{titles_id}/


Частичное обновление отзыва по id. Обновить отзыв может только автор комментария, модератор или администратор. Анонимные запросы запрещены.

PATCH /api/v1/titles/{title_id}/reviews/{review_id}/

```
{
    "text": "string",
    "score": 1
}
```
