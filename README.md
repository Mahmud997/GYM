# GYM PRO — GitHub Pages + Firebase

Полностью статическая версия GYM PRO для GitHub Pages с Firebase Authentication (Google) и Cloud Firestore.

## Что исправлено

- Убран тестовый вход по ролям — роль больше не задаётся кнопкой на клиенте.
- Google Authentication восстанавливает сессию автоматически.
- Роль берётся из `users/{uid}.role` в Firestore.
- Посетитель получает только свой профиль, а не общий список клиентов.
- Метрики и карточка лояльности посетителя хранятся в `users/{uid}/private/...`.
- Общие данные склада/клиентов/активности хранятся в `gym_data`.
- Firestore Rules ограничивают запись по ролям.
- Продление абонемента теперь действительно меняет дату, а не показывает фиктивный alert.
- Добавлены проверки цены, остатка и количества товара.
- Убрана случайная генерация фиктивной статистики при первом запуске.
- Excel-импорт сохраняется в Firestore.
- Код проверен на синтаксические ошибки JavaScript.

## 1. Создайте Firebase-проект

1. Откройте Firebase Console.
2. Создайте проект.
3. Добавьте Web App.
4. Скопируйте `firebaseConfig`.
5. Включите **Authentication → Sign-in method → Google**.
6. Создайте **Cloud Firestore Database**.

## 2. Вставьте Firebase config

Откройте `index.html` и найдите:

```js
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

Замените значения на данные из Firebase Web App.

Важно: Firebase Web config не является секретным паролем. Защита данных выполняется Firestore Rules.

## 3. Опубликуйте Firestore Rules

В Firebase Console откройте Firestore → Rules и вставьте содержимое `firestore.rules`.

Или при установленном Firebase CLI:

```bash
firebase deploy --only firestore:rules
```

## 4. Создайте первого администратора

Сначала войдите через Google, чтобы узнать UID пользователя (Firebase Authentication → Users).

Затем в Firestore создайте документ:

**Коллекция:** `users`

**Document ID:** UID пользователя из Authentication

Поля:

```text
role: "admin"
```

После этого администратор сможет входить в приложение.

## 5. Создайте ресепшен

Для Google-аккаунта сотрудника создайте:

`users/{UID}`

```text
role: "reception"
```

## 6. Создайте посетителя

Для Google-аккаунта посетителя создайте:

`users/{UID}`

```text
role: "member"
clientId: 1
client: {
  name: "Алексей Смирнов",
  phone: "+7 701 111 2233",
  payDate: "2026-10-15",
  lastVisit: "2026-09-20",
  qrCode: "GYM-1-ALEX"
}
```

`clientId` должен соответствовать ID клиента, созданного администратором/ресепшеном.

## 7. GitHub Pages

1. Создайте GitHub repository.
2. Загрузите `index.html`, `firestore.rules`, `firebase.json`, `.gitignore` и `README.md`.
3. GitHub → Settings → Pages.
4. Source: **Deploy from a branch**.
5. Выберите `main` и `/root`.
6. Откройте полученный адрес.

## 8. Добавьте GitHub Pages в Firebase

В Firebase Authentication → Settings → Authorized domains добавьте домен GitHub Pages, например:

```text
yourname.github.io
```

Если приложение находится в репозитории `/gym-pro`, адрес будет вида:

```text
yourname.github.io/gym-pro/
```

## Структура

```text
GYM-PRO/
├── index.html
├── firebase.json
├── firestore.rules
├── .gitignore
└── README.md
```

## Важно

GitHub Pages здесь используется только для фронтенда. Аутентификация и данные работают через Firebase.

Не делайте Firestore `allow read, write: if true` — это откроет базу всем пользователям интернета.
