# Angular Development with Docker

## Структура проекта

angular-dev-skeleton/
├── app/ # исходный код приложения Angular
├── docker-compose.yml # конфиг Docker Compose
├── Dockerfile.dev # Dockerfile для dev окружения
├── .env # Переменные окружения (создайте из .env.example)
└── .dockerignore # Файлы, игнорируемые при сборке образа


## Требования

- Docker Desktop 20.10+ & Docker Compose 2.0+
или
- Podman 5.7.1 (Podman Desktop 1.24.2 - по желанию для GUI)

## Quick Start

1. Склонируйте репозиторий или создайте приложение в папке /app
2. Скопируйте `.env.example` в `.env` и настройте параметры в нем
3. Запустите контейнер:

```bash
docker-compose up --build
#or
podman compose up --build
```
Открываем в браузере: http://localhost:4200
	
## Команды
###  Разработка

```bash
# Start development server
docker-compose up
#or
podman compose up

# Start in background
docker-compose up -d
#or
podman compose up -d

# View logs
docker-compose logs -f
#or
podman compose logs -f

# Stop containers
docker-compose down
#or
podman compose down
```

### Управление контейнерами
angular-dev - имя контейнера
```bash
# Enter container shell
docker-compose exec angular-dev sh
#or
podman compose exec angular-dev sh

# Run Angular CLI commands
docker-compose exec angular-dev ng generate component my-component
#or
podman compose exec angular-dev ng generate component my-component

# Run tests
docker-compose exec angular-dev npm test
#or
podman compose exec angular-dev npm test

# Install new package
docker-compose exec angular-dev npm install lodash
#or
podman compose exec angular-dev npm install lodash
```
## Очистка

```bash
# Stop and remove containers, networks
docker-compose down -v
#or
podman compose down -v

# Remove all Docker resources
docker system prune -a
#or
podman system prune -a
```

## Переменные окружения

Отредактируйте .env файл:

    NODE_VERSION: версия Node.js (по умолчанию: 18)

    ANGULAR_CLI_VERSION: версия Angular CLI (по умолчанию: latest)

    HOST_PORT: Порт для приложения Angular dev server (по умолчанию: 4200)

    PROJECT_NAME: Название проекта/контейнера (по умолчанию: my-angular-app)

## Настройка WebStorm/IntelliJ

    Откройте проект в WebStorm

    Меню Run → Edit Configurations

    Добавьте новую конфигурацию Docker Compose:

        Compose files: docker-compose.yml

        Services: angular-dev

        Environment file: .env

    Для отладки, добавьте конфиг удаленной отладки для Node.js на порту 9229	
	
## Частые проблемы
Не работает горячая перезагрузка

    Убедитесь, что задано значение CHOKIDAR_USEPOLLING=true

    Добавьте флаг --poll 1000 при `npm start`

Port already in use

    Измените значение HOST_PORT в .env файле

    Остановите все сервисы, использующие порт 4200

Permission issues
```bash
# Fix file permissions
sudo chown -R $USER:$USER .
```
## Фичи

    Изолированное Node.js окружение

    Настройка версий через .env

    Поддержка горячей перезагрузки приложения

    Интеграция с WebStorm/IntelliJ

    Test runner support (port 9876)

    Debugging support (port 9229)	