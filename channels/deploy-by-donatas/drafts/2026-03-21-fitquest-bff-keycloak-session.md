---
channel: deploy-by-donatas
status: draft
post_type: component
component_focus: bff
# scheduled:
diagram: ../assets/2026-03/fitquest-bff-keycloak-session.png
---

## Пост (копировать в Telegram)

**Базовая компонентная схема проекта FitQuest 👇**

**Архитектура**

*(Прикрепи к посту картинку из репозитория: `channels/deploy-by-donatas/assets/2026-03/fitquest-bff-keycloak-session.png` — на схеме: Web/Mobile, BFF, Auth/Keycloak, Backend и стрелки login/password, session_id, access/refresh, api_request.)*

На старте решил не идти в «прямые запросы с фронта в backend», а сразу заложить более правильную модель — **через BFF (Backend For Frontend)**.

**Что сделано**

- заложена связка **клиенты → BFF → backend**, без прямых вызовов фронта в backend;
- вход через **Keycloak**: BFF получает access/refresh, выпускает **session_id** клиенту;
- **JWT на клиент не отдаём** — токены остаются на стороне сервера.

**Как это работает**

1. Пользователь (web / mobile) отправляет логин и пароль в BFF
2. BFF обращается в Keycloak
3. Получает access/refresh токены
4. Создаёт session_id и возвращает его клиенту

👉 **При этом JWT не уходит на клиент** — он хранится на стороне сервера.

**Как идут запросы дальше**

- клиент → BFF (с session_id)
- BFF → backend (уже с токеном)

**Зачем это нужно**

- **безопасность** — токены не светятся на клиенте
- **контроль** — можно управлять сессиями
- **гибкость** — легко добавить кеш, rate limit, агрегацию
- **единая логика** для web и mobile

---

В дальнейшем эта схема будет дорабатываться и совершенствоваться.

**Дальше планирую добавить:**

- хранение сессий
- базу данных
- AI-агента для анализа тренировок

```
#fitquest #bff #keycloak #architecture #security #devlog
```

<!--
Чеклист:
- [ ] схема `fitquest-bff-keycloak-session.png` прикреплена к посту, читаемо на телефоне
- [ ] теги одной строкой в Telegram (скопируй из блока выше без обратных кавычек)
- [ ] нет утечек секретов и внутренних URL в тексте
-->
