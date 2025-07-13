# Домашнее задание ШРИ 2025: Инфраструктура

## 🚀 Продакшн

Приложение задеплоено и доступно по адресу:

🖐 [http://84.201.139.38/hw/store/](http://84.201.139.38/hw/store/)

---

## ⚙️ CI/CD

### ✅ Pull Request Checks

Каждый PR запускает CI-флоу:

- npm run lint
- npm run test

Если хотя бы один шаг не прошёл — PR нельзя смерджить в main.

### 🚀 Release Flow (ручной запуск)

Workflow `release.yml`:

- отводит ветку `releases/<version>`
- собирает Docker-образ
- пушит в Yandex Container Registry с тегами:

  - `cr.yandex/crpcntqudb0hkbbnds00/app:<version>`
  - `cr.yandex/crpcntqudb0hkbbnds00/app:<version>_latest`

- создаёт GitHub Issue с инфой о релизе:
  - дата
  - автор
  - версия
  - список коммитов с предыдущего релизного или фикс-тега
  - ссылка на Docker-образ

- обновляет `CHANGELOG.md`
- создаёт Git-тег `v<version>`

### 🛠 Fix Release Flow

Workflow `fix-release.yml`:

- принимает номер релиза `version`, к которому относится фикс
- собирает Docker-образ с тегами:

  - `cr.yandex/crpcntqudb0hkbbnds00/app:<version>_fix<fix_number>`
  - `cr.yandex/crpcntqudb0hkbbnds00/app:<version>_latest`

- создаёт Git-тег `v<version>_fix<fix_number>`
- ищет предыдущий тег фикса или релиза и формирует список коммитов
- добавляет комментарий в релизный Issue с информацией о фиксе:
  - дата
  - автор
  - тег фикса
  - список коммитов

### 📆 Deploy to Production

Workflow `deploy.yml`:

- по SSH подключается к виртуальной машине
- скачивает Docker-образ из Yandex CR
- перезапускает контейнер
- добавляет комментарий в GitHub Issue

---

## 🔐 Защита ветки main

Ветка `main` защищена:

- нельзя пушить напрямую
- смердж только через Pull Request
- только после прохождения CI

---

## 📋 Файл About

В файле `./src/client/pages/About.tsx` заменено [Your Name] на **Виталий Дорохин**.  
Тест обновлён и успешно проходит.
