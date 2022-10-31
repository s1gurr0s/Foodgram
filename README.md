# Проект Foodgram - «Продуктовый помощник»
![Build Status](https://github.com/s1gurr0s/foodgram-project-react/actions/workflows/foodgram.yml/badge.svg)

### Описание:
Сервис, который позволяет создавать/просматривать рецепты блюд, 
подписываться на авторов, добавлять рецепты в избранное и в список покупок. 
Список покупок выгружается в виде файла (shopping-list.txt), в котором сохранены все
ингредиенты для рецептов из списка покупок.

### Используемые технологии
- Django
- Django Rest Framework
- Docker
- Docker-compose
- Gunicorn
- Nginx
- PostgreSQL

### Workflow
- **tests:** Проверка кода на соответствие PEP8.
- **push Docker image to Docker Hub:** Сборка и публикация образа на DockerHub.
- **deploy:** Автоматический деплой на боевой сервер при пуше в главную ветку main.
- **send_massage:** Отправка уведомления в телеграм-чат.

### Подготовка и запуск проекта
- Выполнить вход на удаленный сервер
- Установить docker на сервер:
```bash
sudo apt install docker.io 
```
- Установить docker-compose на сервер:
```bash
sudo apt-get update
sudo apt install docker-compose
```
- Скопировать файл docker-compose.yml и nginx.conf из директории infra на сервер:
```bash
scp docker-compose.yml <username>@<host>:/home/<username>/
scp nginx.conf <username>@<host>:/home/<username>/
```
- Для работы с Workflow добавить в Secrets GitHub переменные окружения:
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432

DOCKER_PASSWORD=<пароль DockerHub>
DOCKER_USERNAME=<имя пользователя DockerHub>

USER=<username для подключения к серверу>
HOST=<IP сервера>
PASSPHRASE=<пароль для сервера, если он установлен>
SSH_KEY=<ваш SSH ключ (для получения команда: cat ~/.ssh/id_rsa)>

TELEGRAM_TO=<ID своего телеграм-аккаунта>
TELEGRAM_TOKEN=<токен вашего бота>
```
- После деплоя изменений в git, дождитесь выполнения всех Actions.
- Зайдите на боевой сервер и выполните команды:
  * Создаем и применяем миграции
    ```bash
    sudo docker-compose exec backend python manage.py migrate
    ```
  * Подгружаем статику
    ```bash
    sudo docker-compose exec backend python manage.py collectstatic --no-input 
    ```
  * Создать суперпользователя Django
    ```bash
    sudo docker-compose exec backend python manage.py createsuperuser
    ```
  * Загрузить подготовленный список ингредиентов
    ```bash
    sudo docker-compose exec backend python manage.py loaddata ingredients.json
    ```

- Проект будет доступен по вашему IP-адресу.

Проект доступен по адресу: <http://51.250.26.190/>

Доступ в админку:

```bash
   email - ad@min.ru
   пароль - foodgram13
```

Пользователь:

```bash
   email - iv@an.ru
   пароль - foodgram13
```
#### Автор:
Агукин Владимир - [https://github.com/s1gurr0s](https://github.com/s1gurr0s)
