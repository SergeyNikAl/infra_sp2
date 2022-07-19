# Проект "YaMDb"
Проект "YaMDb" позволяет собирать отзывы пользователей на книги, фильмы, музыку.

Проект упакован в Docker.

### Авторы:
- [Sergey Nikulin] (https://github.com/SergeyNikAl)

### Технологии:
- Docker
- Nginx
- Gunicorn
- Python
- Django
- DRF
- SQLite3

### Установите Docker
1. Для [windows](https://docs.docker.com/desktop/windows/install/)
2. Для [macOS](https://docs.docker.com/desktop/mac/install/)
3. Для дистрибутивов [Linux](https://docs.docker.com/desktop/linux/#uninstall)

### Как запустить проект:
- Клонировать репозиторий:
```
git clone https://github.com/SergeyNikAl/infra_sp2.git
```
- Перейти в папку `./infra_sp2/infra`
```
cd infra
```

- В директории infra создать `.env` и заполнить своими данными:
```
touch .env
```
```
nano .env
```
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=password   # укажите свой пароль
DB_HOST=db
DB_PORT=5432
SECRET_KEY = 'your secret key' # укажите секретный ключ
```

Если всё успешно, все переменные на местах, запустить командой:
```
docker-compose up --build -d
```

Или загрузить готовый image в dockerHub командой:
```
docker run sergeynikal/api_yamdb:v1.1
```

- Выполнить миграции:
```
docker-compose exec web python manage.py migrate
```

- Создать суперпользователя:
```
docker-compose exec web python manage.py createsuperuser
```

- Собрать статику:
```
docker-compose exec web python manage.py collectstatic --no-input
```

### Как запустить тестовое наполнение базы:
В дирректориях созданы две тестовые базы.

Пользовательская - `fixtures.json`;

Тестовая база ЯП.

## После выполнения миграций

- Миграция пользовательской базы:
```
docker-compose exec web python manage.py loaddata fixtures.json 
``` 

- Для миграции базы ЯП необходимо войти в контейнер командой:
```
docker exec -it web bash
```

- Залить тестовые данные из CSV файлов командой:
```
python manage.py csv_manager
```
- Для выхода из консоли ввести команду:
```
exit
```

### ReDoc:
```
http://localhost/redoc/
```
