## Практическое занятие №3
## Группа: ЭФМО-02-25  
## ФИО: Евдоков Богдан Вадимович

## 🚀 Что умеет этот сервер?

Сервер представляет собой REST API для управления задачами (To-Do list) и работает на стандартной библиотеке Go `net/http`. 

### 📍 Доступные эндпоинты:

1. **`GET /health`** — проверка статуса сервера
2. **`GET /tasks`** — получение списка всех задач (с поддержкой фильтрации)
3. **`POST /tasks`** — создание новой задачи
4. **`GET /tasks/{id}`** — получение конкретной задачи по ID

## 📦 Требования для запуска

- **Go 1.21+** - [скачать с официального сайта](https://go.dev/dl/)
- **Git** - [скачать с официального сайта](https://git-scm.com/downloads)

## 🛠 Быстрый старт

### Шаг 1: Скачивание и подготовка проекта

```powershell
# Клонируем репозиторий
git clone https://github.com/jervissss/pz3-http.git
cd pz3-http

# Инициализируем модуль Go
```powershell
go mod init example.com/pz3-http
```

### Шаг 2: Запуск сервера
```powershell
# Через исходный код
go run ./cmd/server/main.go
```
При успешном запуске вы увидите сообщение: `listening on :8080`

## 🔍 Тестирование API
### 1. Проверка здоровья сервера
```powershell
curl -i http://localhost:8080/health
```
Ответ: `{"status":"ok"}`

### 2. Создание новой задачи
```powershell
curl -i -X POST http://localhost:8080/tasks `
  -H "Content-Type: application/json" `
  -d '{"title":"Купить молоко"}'
```
Ответ: `{"id":1,"title":"Купить молоко","done":false}`

### 3. Получение списка задач
```powershell
curl -i http://localhost:8080/tasks
```
### 4. Фильтрация задач
```powershell
curl -i "http://localhost:8080/tasks?q=молоко"
```

### 5. Получение конкретной задачи
```powershell
curl -i http://localhost:8080/tasks/1
```

## 📁 Структура проекта
<img width="362" height="372" alt="image" src="https://github.com/user-attachments/assets/692de358-daa0-42f0-b3d0-48ce3fc9531a" />

## 🔧 Ключевые особенности реализации
### 🎯 Обработка запросов
* GET параметры - фильтрация через ?q=текст
* Path параметры - извлечение ID из URL /tasks/{id}
* JSON body - валидация и парсинг для POST запросов

### 📊 Логирование
Middleware записывает в консоль:
* Метод запроса
* URL путь
* Статус ответа
* Время выполнения

### Коды статуса:
*	200 OK — успешный ответ
*	201 Created — ресурс создан
*	204 No Content — успешно, без тела
*	400 Bad Request — неверные данные
*	404 Not Found — ресурс не найден
*	422 Unprocessable Entity — некорректные данные по смыслу
*	500 Internal Server Error — внутренняя ошибка

## 📸 Отчетные материалы
GET /health `curl -i http://localhost:8080/health`
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c39c2f7c-66fe-44a0-86fa-8a58edff8544" />

```powershell
curl -Method POST http://localhost:8080/tasks `
  -Headers @{"Content-Type"="application/json"}`
  -Body '{"title":"Купить молоко"}'
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/63ee10d1-6f0c-489c-87b0-fc3d326d5fd2" />

---
*Этот проект был создан в качестве учебного задания.*
