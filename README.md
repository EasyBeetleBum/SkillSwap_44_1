# SkillSwap

Платформа для обмена навыками по модели «Учу / Хочу научиться». Пользователи публикуют навыки, которыми готовы делиться, и навыки, которым хотят научиться. Сервис находит взаимно подходящие пары, позволяет отправлять заявки на обмен и вести историю сессий.

## Стек

- **Frontend:** React, TypeScript, Redux Toolkit, React Router, Feature-Sliced Design (FSD), Vite
- **Backend:** NestJS, TypeORM, PostgreSQL, JWT (access + refresh), Passport.js, WebSocket
- **Инфраструктура:** Docker, Jest (Unit + E2E), Swagger

## Что реализовано

### Frontend
- Архитектура на Feature-Sliced Design (слои `widgets`, `shared/ui`, `entities`).
- Страница авторизации с валидацией форм через `react-hook-form` и управлением состоянием в `Redux Toolkit`.
- Компонент `HeaderButtons` (навигация, переключение темы).
- Работа с избранным: синхронизация карточки навыка с глобальным хранилищем.
- Рефакторинг UI-компонентов: доступность (`:focus-visible`), адаптивность, устранение багов вёрстки.

### Backend
- JWT-авторизация с access и refresh токенами, эндпоинт `POST /auth/refresh`, стратегия `RefreshTokenStrategy`, гарда `RefreshTokenGuard`.
- Управление профилем: `PATCH /users/me`, `PATCH /users/me/password`.
- Глобальный фильтр исключений (`AllExceptionFilter`): 404, 409, 413, 500.
- CRUD категорий с защитой прав администратора (`POST`, `PATCH`, `DELETE /categories`).
- Сидинг базы данных тестовыми навыками (`seed-skills.ts`).
- Настройка Jest для Unit- и E2E-тестов (маппинг путей, покрытие ≥70%).

## Запуск

```bash
# Клонировать репозиторий
git clone https://github.com/<username>/skillswap.git
cd skillswap

# Установить зависимости (frontend и backend)
cd client && npm install
cd ../server && npm install

# Настроить переменные окружения
cp server/.env.example server/.env
# заполнить DATABASE_URL, JWT_SECRET, JWT_REFRESH_SECRET и др.

# Запустить базу данных (Docker)
docker compose up -d db

# Запустить backend
cd server && npm run start:dev

# Запустить frontend
cd client && npm run dev
