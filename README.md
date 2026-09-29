# TURAN — Fitness Management

Готовая GitHub Pages структура на базе исходного GYM PRO с сохранением существующих модулей.

## Что добавлено

- Вход только через Google Firebase Authentication.
- Роли `admin`, `reception`, `member` определяются через Firestore.
- Название системы: **TURAN**.
- Админ может назначать роль Google-аккаунту: клиент / ресепшен / админ.
- Админ может изменять и удалять клиентов.
- Клиент автоматически связывается с его Google UID/email.
- Раздел **Задания клиентам**: выбрать одного или нескольких клиентов, тренера, дату, скорость, длительность, дистанцию, повторения и комментарий.
- Клиент видит только свои задания и может отметить их выполненными.
- Раздел **Тренеры**: имя, категория, фото по URL, описание.
- Раздел **Категории тренеров**: добавление и удаление.
- Остальные исходные функции проекта сохранены: отчёты, QR, абонемент, метрики, лояльность, магазин, склад, Excel и т.д.

## Настройка Firebase

1. Создайте Firebase project.
2. В Authentication включите **Google**.
3. Создайте Firestore Database.
4. Вставьте Web App config в `firebase-config.js`.
5. В `firebase-config.js` укажите хотя бы один email владельца в `adminEmails`.
6. В Firestore Rules загрузите `firestore.rules`.
7. Добавьте домен GitHub Pages в Firebase Authentication → Settings → Authorized domains.
8. Откройте GitHub Pages.

### Первый вход

Email из `adminEmails` получает роль `admin`. После входа админ открывает **Доступ и роли** и назначает остальные Google-аккаунты как `reception` или `member`.

## Важно

Firebase Web config можно хранить в клиентском GitHub-коде: безопасность обеспечивается Authentication и Firestore Security Rules. Не размещайте service-account JSON или приватные серверные ключи в репозитории.

## Структура

- `index.html` — приложение.
- `firebase-config.js` — конфигурация Firebase.
- `firestore.rules` — правила доступа.
