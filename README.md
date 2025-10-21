# Kittygram

[![Main Kittygram workflow](https://github.com/etrifonoff/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/etrifonoff/kittygram_final/actions/workflows/main.yml)

## Описание проекта

**Kittygram** — это социальная сеть для обмена фотографиями любимых питомцев. Пользователи могут регистрироваться, загружать фотографии своих котиков с описанием их достижений, просматривать питомцев других пользователей и следить за обновлениями.

### Основные функции:

- 🐱 Регистрация и аутентификация пользователей
- 📸 Загрузка фотографий котиков
- ✏️ Добавление описания и достижений питомцев
- 🎨 Указание цвета и года рождения питомца
- 📋 Просмотр карточек других котиков
- 🔐 Управление своими публикациями (редактирование и удаление)

## Технологии

### Backend:
- **Python 3.9**
- **Django 3.2** — веб-фреймворк
- **Django REST Framework** — для создания API
- **Djoser** — для аутентификации
- **PostgreSQL 13** — база данных
- **Gunicorn** — WSGI-сервер

### Frontend:
- **React** — библиотека для создания пользовательского интерфейса
- **Node.js 18** — среда выполнения JavaScript

### DevOps:
- **Docker** и **Docker Compose** — контейнеризация
- **Nginx** — веб-сервер и reverse proxy
- **GitHub Actions** — CI/CD

## Развертывание проекта

### Предварительные требования:

- Установленный Docker и Docker Compose
- Сервер с Ubuntu (для production)
- Доменное имя (опционально)

### Локальный запуск:

1. Клонируйте репозиторий:
```bash
git clone https://github.com/evtrifonoff/kittygram_final.git
cd kittygram_final
```

2. Создайте файл `.env` в корневой директории проекта (см. раздел "Переменные окружения")

3. Запустите проект:
```bash
docker compose up -d
```

4. Выполните миграции и соберите статику:
```bash
docker compose exec backend python manage.py migrate
docker compose exec backend python manage.py collectstatic
docker compose exec backend cp -r /app/collected_static/. /backend_static/static/
```

5. Проект будет доступен по адресу: `http://localhost:9000`

### Production развертывание:

1. Форкните репозиторий и клонируйте его на свой сервер

2. Настройте GitHub Secrets в репозитории:
   - `DOCKER_USERNAME` — логин на DockerHub
   - `DOCKER_PASSWORD` — пароль от DockerHub
   - `HOST` — IP-адрес вашего сервера
   - `USER` — имя пользователя на сервере
   - `SSH_KEY` — приватный SSH-ключ
   - `SSH_PASSPHRASE` — пароль от SSH-ключа (если есть)
   - `TELEGRAM_TO` — ID вашего Telegram-аккаунта
   - `TELEGRAM_TOKEN` — токен Telegram-бота
   - Переменные окружения (см. следующий раздел)

3. При пуше в ветку `main` автоматически запустится:
   - Тестирование кода
   - Сборка и публикация Docker-образов
   - Деплой на сервер
   - Отправка уведомления в Telegram

## Переменные окружения

Создайте файл `.env` в корневой директории проекта со следующими переменными:

```env
# PostgreSQL
POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_password

# Database connection
DB_HOST=db
DB_PORT=5432

# Django
SECRET_KEY=your-secret-key-here
DEBUG=False
ALLOWED_HOSTS=localhost,127.0.0.1,your-domain.com
```

### Описание переменных:

- `POSTGRES_DB` — имя базы данных
- `POSTGRES_USER` — имя пользователя БД
- `POSTGRES_PASSWORD` — пароль пользователя БД
- `DB_HOST` — хост базы данных (для Docker используйте `db`)
- `DB_PORT` — порт базы данных (по умолчанию `5432`)
- `SECRET_KEY` — секретный ключ Django (сгенерируйте уникальный)
- `DEBUG` — режим отладки (`True` для разработки, `False` для production)
- `ALLOWED_HOSTS` — список разрешенных хостов через запятую

### Генерация SECRET_KEY:

```python
from django.core.management.utils import get_random_secret_key
print(get_random_secret_key())
```

## Автор

**Евгений Трифонов**

- GitHub: [@evtrifonoff](https://github.com/evtrifonoff)
- Проект: [Kittygram](https://ekittygram.webhop.me)

---

Проект создан в рамках обучения на курсе Python-разработчик в Яндекс.Практикум.
