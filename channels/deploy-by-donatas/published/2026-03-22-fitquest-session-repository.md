---
channel: deploy-by-donatas
status: draft
title: "Репозиторий сессий"
post_type: architecture
component_focus: session_repository
scheduled: false
diagram: ../assets/2026-03/fitquest-session-repository.png
---

## Пост (копировать в Telegram)

**Репозиторий сессий** — хранилище сессий для проекта FitQuest.

**Архитектура**
В архитектуру проекта был добавлен репозиторий сессий в виде Redis, который будет использоваться для хранения сессий пользователей.

**Что сделано**

- добавлен репозиторий сессий в виде Redis;

**Как это работает**
1. Пользователь web/mobile отправляет login/password в BFF;
2. BFF обращается в Keycloak;
3. Получает access/refresh токены;
4. Создаёт session object;
5. Сохраняет session object в Redis;
6. Возвращает session_id клиенту;

Что из себя представляет session object?
- session_id - уникальный идентификатор сессии пользователя;
- access_token - токен для доступа к ресурсам;
- refresh_token - токен для обновления access_token;
- expires_in - время жизни access_token;
- created_at - время создания сессии;
- updated_at - время обновления сессии;
- user_id - идентификатор пользователя;

**Зачем это нужно**
- **безопасность** — токены не светятся на клиенте
- **контроль** — можно управлять сессиями
- **гибкость** — легко добавить кеш, rate limit, агрегацию
- **единая логика** для web и mobile


