# Telegram Bot с PostgreSQL и Redis

Telegram бот на aiogram с поддержкой PostgreSQL, Redis, многоязычности и админ-панели.

## Возможности

- 🤖 Эхо-бот с базой данных PostgreSQL
- 🌍 Многоязычность (русский/английский)
- 👥 Система ролей (пользователь/админ)
- 📊 Статистика активности пользователей
- 🚫 Shadow ban система
- ⚙️ Настройка языка интерфейса
- 🔧 Админ-команды (ban/unban/статистика)

## Быстрый старт

### 1. Клонирование и установка зависимостей

```bash
git clone <repository-url>
cd PythonProject11
python -m venv .venv
# Windows
.venv\Scripts\activate
# Linux/Mac
source .venv/bin/activate

pip install -r requirements.txt
```

### 2. Настройка окружения

Скопируйте `env.example` в `.env` и заполните переменные:

```bash
cp env.example .env
```

Отредактируйте `.env`:
```env
BOT_TOKEN=your_bot_token_here
ADMIN_IDS=123456789,987654321
```

### 3. Запуск через Docker (рекомендуется)

```bash
# Запуск контейнеров
docker compose up -d

# Проверка статуса
docker ps

# Создание таблиц
python -m migrations.create_tables

# Запуск бота
python main.py
```

### 4. Запуск без Docker

Убедитесь, что PostgreSQL и Redis запущены локально, затем:

```bash
# Создание таблиц
python -m migrations.create_tables

# Запуск бота
python main.py
```

## Структура проекта

```
PythonProject11/
├── app/
│   ├── bot/
│   │   ├── handlers/          # Обработчики сообщений
│   │   ├── middlewares/       # Middleware
│   │   ├── keyboards/         # Клавиатуры
│   │   ├── filters/           # Фильтры
│   │   ├── states/            # FSM состояния
│   │   ├── enums/             # Перечисления
│   │   └── i18n/              # Интернационализация
│   └── infrastructure/
│       └── database/          # Работа с БД
├── config/                    # Конфигурация
├── locales/                   # Переводы
├── migrations/                # Миграции БД
├── docker-compose.yml         # Docker конфигурация
└── requirements.txt           # Зависимости
```

## Команды бота

### Для всех пользователей
- `/start` - запуск бота
- `/help` - справка
- `/lang` - настройка языка

### Для администраторов
- `/ban <user_id|@username>` - заблокировать пользователя
- `/unban <user_id|@username>` - разблокировать пользователя
- `/statistics` - статистика активности

## Технологии

- **aiogram 3.20** - Telegram Bot API
- **PostgreSQL** - основная база данных
- **Redis** - FSM storage и кэширование
- **psycopg** - PostgreSQL драйвер
- **Docker** - контейнеризация

## Переменные окружения

| Переменная | Описание | Пример |
|------------|----------|---------|
| `BOT_TOKEN` | Токен бота от @BotFather | `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11` |
| `ADMIN_IDS` | ID администраторов через запятую | `123456789,987654321` |
| `POSTGRES_*` | Настройки PostgreSQL | см. env.example |
| `REDIS_*` | Настройки Redis | см. env.example |

## Разработка

### Добавление нового языка

1. Создайте файл `locales/{lang}/txt.py`
2. Добавьте словарь с переводами
3. Обновите `app/bot/i18n/translator.py`

### Добавление новой команды

1. Создайте обработчик в `app/bot/handlers/`
2. Добавьте команду в `app/bot/keyboards/menu_button.py`
3. Добавьте переводы в `locales/`

