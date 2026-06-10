# Pulseboard — SaaS Analytics Dashboard

Fullstack SaaS-платформа для аналитики проектов: метрики, графики,
управление проектами и real-time уведомления.

## Стек

- **Frontend:** Next.js (App Router), TypeScript, Tailwind, Recharts, Auth.js
- **Backend:** NestJS, Prisma, PostgreSQL
- **Auth:** JWT + refresh tokens, RBAC (USER / ADMIN)
- **Real-time:** WebSocket
- **Infra:** Docker, GitHub Actions, Railway + Vercel

## Структура (монорепо)

```
apps/
  web/   — Next.js фронтенд
  api/   — NestJS бэкенд
packages/
  db/    — Prisma schema (общая)
```

## Запуск

_Будет дополнено по мере разработки._

## Архитектурные решения

_Здесь по ходу проекта: почему монорепо, схема БД, стратегия токенов и т.д._

### Схема БД

- **4 сущности**\
   User — аутентификация, роли, владелец данных;\
   Application — заявка на вакансию, текущее состояние;\
   StatusChange — история переходов статусов (для аналитики динамики);\
   Notification — уведомления пользователю;\
   (Vacancy — позже, при интеграции с hh).
- **Основые enum**\
   Role: USER, ADMIN\
   ApplicationStatus: APPLIED, INTERVIEW, OFFER, REJECTED\
   Source: MANUAL, HH\
   NotificationType: INFO, INTERVIEW_REMINDER, STATUS_CHANGE, DEADLINE
- **Статус хранится в двух местах**\
   (Application.status и StatusChange) намеренно: Application — текущее состояние (быстрый доступ), StatusChange — история переходов (для аналитики динамики). Синхронность гарантируется транзакцией при смене статуса.
- **Decimal для зарплаты**, не Float — избегаем ошибок округления денег.
- **Cascade при удалении**:
  удаление User удаляет его Application и Notification; удаление Application удаляет связанные StatusChange. Данные принадлежат владельцу.
- **Нейминг**\
   camelCase в коде, а snake_case в БД через @map/@@map — каждый слой следует своей конвенции.
