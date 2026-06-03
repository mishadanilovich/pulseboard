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
