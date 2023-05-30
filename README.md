# yamdb_final
yamdb_final

[![Django-app workflow](https://github.com/BornNSK/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)](https://github.com/BornNSK/yamdb_final/actions/workflows/yamdb_workflow.yml)

### Описание

Проект YaMDb собирает отзывы пользователей на произведения («Книги», «Фильмы», «Музыка»)

### Стек:
- Python 3.7.0
- Django 3.2
- DRF 3.12.4
- Nginx
- docker-compose

[Доступ к API](http://130.193.51.77/api/v1/)
[Redoc фаил(с примерами запросов)](http://130.193.51.77/redoc/)


### Как запустить проект:

Клонировать проект из репозитория:

```bash
git clone https://github.com/BornNSK/yamdb_final

```

Установить docker на сервер:

```bash
apt install docker.io 
```

Установить docker-compose на сервер:

```bash
curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

Локально отредактировать файл infra/nginx.conf, обязательно в строке server_name вписать IP-адрес сервера
Скопировать файлы docker-compose.yml и nginx.conf из директории infra на сервер:
```bash
scp docker-compose.yml <username>@<host>:/home/<username>/docker-compose.yml
scp nginx.conf <username>@<host>:/home/<username>/nginx/nginx.conf
```
Добавить в Actions Secrets GitHub переменные окружения для работы:

    
    DB_ENGINE=<django.db.backends.postgresql>
    DB_NAME=<имя базы данных postgres>
    DB_USER=<пользователь бд>
    DB_PASSWORD=<пароль>
    DB_HOST=<db>
    DB_PORT=<5432>
    
    DOCKER_PASSWORD=<токен от DockerHub>
    DOCKER_USERNAME=<имя пользователя>

    USER=<username для подключения к серверу>
    HOST=<IP сервера>
    PASSPHRASE=<пароль для сервера, если он установлен>
    SSH_KEY=<ваш SSH ключ (для получения команда: cat ~/.ssh/id_rsa)>

    TELEGRAM_TO=<ID чата, в который придет сообщение>
    TELEGRAM_TOKEN=<токен вашего бота>
    

После запуска контенейров выполнить следующие действия (только при первом деплое):
    * провести миграции внутри контейнеров:
    ```bash
    docker-compose exec web python manage.py migrate
    ```
    * собрать статику проекта:
    ```bash
    docker-compose exec web python manage.py collectstatic --no-input
    ```  
    * Создать суперпользователя Django, после запроса от терминала ввести логин и пароль для суперпользователя:
    ```bash
    docker-compose exec web python manage.py createsuperuser
    ```
##
Автор:

Евсюков Bornki11@yandex.ru
