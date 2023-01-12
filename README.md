# yamdb_final
yamdb_final - 16ый спринт
Итоговое задание - Проект: CI и CD проекта api_yamdb

![example workflow](https://github.com/Nezhinskiy/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

[Путь до API](http://51.250.108.30/api/v1/)

API для получения информации и обсуждения наиболее интересных произведений. 

Для автоматизации развертывания на боевых серверах используется среда виртуализации Docker, а также Docker-compose - инструмент для запуска многоконтейнерных приложений. 

 

## Стек технологий: 

- Python 3 

- DRF (Django REST framework) 

- Django ORM 

- Docker 

- Gunicorn 

- nginx 

- Яндекс Облако(Ubuntu 18.04) 

- Django 2.2 TLS 

- PostgreSQL 

- GIT 

 

## О проекте: 

Реализована регистрация с кодом подтверждения и дальнейшая авторизация с использованием JWT токена, при отправке запроса к API. 

 

Проект **YaMDb** собирает **отзывы** (**Review**) пользователей на **произведения** (**Titles**). Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список **категорий** (**Category**) может быть расширен администратором (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»). 

 

В каждой категории есть **произведения**: книги, фильмы или музыка. Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Насекомые» и вторая сюита Баха. 

 

Произведению может быть присвоен **жанр** (**Genre**) из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). Новые жанры может создавать только администратор. 

 

Благодарные или возмущённые пользователи оставляют к произведениям текстовые **отзывы** (**Review**) и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — **рейтинг** (целое число). На одно произведение пользователь может оставить только один отзыв. 

 

### Как запустить проект: 

 

Все описанное ниже относится к ОС Linux. 

Клонируем репозиторий и переходим в него: 

```bash 

git clone https://github.com/Nezhinskiy/infra_sp2 

cd infra_sp2 

cd api_yamdb 

``` 

 

Создаем и активируем виртуальное окружение: 

```bash 

python3 -m venv venv 

source /venv/bin/activate (source /venv/Scripts/activate - для Windows) 

python -m pip install --upgrade pip 

``` 

 

Ставим зависимости из requirements.txt: 

```bash 

pip install -r requirements.txt 

``` 

 

Переходим в папку с файлом docker-compose.yaml: 

```bash 

cd infra 

``` 

 

Поднимаем контейнеры (infra_db_1, infra_web_1, infra_nginx_1): 

```bash 

docker-compose up -d --build 

``` 

 

Выполняем миграции: 

```bash 

docker-compose exec web python manage.py makemigrations reviews 

``` 

```bash 

docker-compose exec web python manage.py migrate 

``` 

 

Создаем суперпользователя: 

```bash 

docker-compose exec web python manage.py createsuperuser 

``` 

 

Србираем статику: 

```bash 

docker-compose exec web python manage.py collectstatic --no-input 

``` 

 

Создаем дамп базы данных (нет в текущем репозитории): 

```bash 

docker-compose exec web python manage.py dumpdata > dumpPostrgeSQL.json 

``` 

 

Останавливаем контейнеры: 

```bash 

docker-compose down -v 

``` 

 

### Шаблон наполнения .env (не включен в текущий репозиторий) расположенный по пути infra/.env 

``` 

DB_ENGINE=django.db.backends.postgresql 

DB_NAME=postgres 

POSTGRES_USER=postgres 

POSTGRES_PASSWORD=postgres 

DB_HOST=db 

DB_PORT=5432 

``` 

 

### Документация API YaMDb 

Документация доступна по эндпойнту: http://localhost/redoc/ 

 

Авторы: 

=== 

 Работа выполнялась в команде, я (Nezhinskiy) был выбран в роли "Тимлида", распределял задачи между коллегами, разбирался и фиксил недочеты с ошибками. 

[Ссылка на репозиторий, в котором велась разработка проекта в команде](https://github.com/Nezhinskiy/api_yamdb) 

 

https://github.com/Nezhinskiy 

https://github.com/sidelkin1 

https://github.com/SankakuSpace
