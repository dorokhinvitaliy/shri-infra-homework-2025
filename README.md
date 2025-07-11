# Домашнее задание ШРИ 2025: Инфраструктура

## 🚀 Продакшн

Приложение задеплоено и доступно по адресу:

🖐 [http://84.201.139.38/](http://84.201.139.38/)

---

## 📦 Docker

### Сборка образа

```bash
npm run build:docker
```

Это соберёт образ с тегом `shri-infra`.

### Запуск образа

```bash
npm run start:docker
```

Это запустит контейнер на порту `3000`.

---

## ⚙️ CI/CD

### ✅ Pull Request Checks

Каждый PR запускает CI-флоу:

- `npm run lint`
- `npm run test`

Если хотя бы один шаг не прошёл — PR нельзя смерджить в `main`.

### 🚀 Release Flow (ручной запуск)

Workflow `release.yml`:

- отводит ветку `releases/<version>`
- собирает Docker-образ
- пушит в Yandex Container Registry с тегами:

  - `cr.yandex/crpcntqudb0hkbbnds00/app:<version>`
  - `cr.yandex/crpcntqudb0hkbbnds00/app:<version>_latest`

- создаёт GitHub Issue с инфой о релизе
- обновляет `CHANGELOG.md`
- создаёт Git-тег `v<version>`

### 📆 Deploy to Production

Workflow `deploy.yml`:

- по SSH подключается к виртуальной машине
- скачивает Docker-образ из Yandex CR
- перезапускает контейнер
- добавляет комментарий в GitHub Issue

---

## 🔐 Защита ветки `main`

Ветка `main` защищена:

- нельзя пушить напрямую
- смердж только через Pull Request
- только после прохождения CI

---

## 📋 Файл About

В файле `./src/client/pages/About.tsx` заменено `[Your Name]` на **Виталий Дорохин**. &#x20;
Тест обновлён и успешно проходит.

---

## 📌 Использованные технологии

- Node.js
- Docker
- GitHub Actions
- Yandex Cloud (Container Registry + Compute Cloud)
- GitHub CLI (`gh`)
