# TURAN GYM — GitHub-ready

Готовая веб-версия TURAN с Firebase Authentication/Firestore.

## Уже настроено
- Название системы: TURAN
- Вход через Google
- Главный администратор: `sayremi025@gmail.com`
- Роли: admin, reception, member
- Клиент видит только свои данные и свои задания
- Администратор управляет клиентами, тренерами, категориями и заданиями
- Индивидуальные задания: клиент/клиенты, тренер, беговая дорожка, скорость, время, дистанция, повторения, дата и комментарий
- Firebase-конфигурация уже вставлена в `firebase-config.js`

## Firebase
В проекте используется Firebase project `gym-6ff42`.

Перед публикацией проверь в Firebase Console:
1. Authentication → Sign-in method → Google — включён.
2. Authentication → Settings → Authorized domains — добавлен домен GitHub Pages.
3. Firestore Database создана.
4. Содержимое `firestore.rules` опубликовано в Firestore Rules.

## Публикация на GitHub Pages
Загрузите содержимое этой папки в репозиторий и включите GitHub Pages для ветки/папки, где находится `index.html`.

Не удаляйте `firebase-config.js` и `firestore.rules`.
