# README - Система управления студентами с REST API

## Описание проекта
Веб-приложение для управления данными студентов с клиент-серверной архитектурой. Серверная часть предоставляет REST API для CRUD операций с данными студентов, клиентская часть взаимодействует с этим API.

## Требования
- Node.js версии 12 или выше
- Доступ к порту 3000 (или другому, указанному в переменной окружения PORT)

## Установка и запуск

### Серверная часть
1. Перейдите в папку сервера:
   ```bash
   cd backend
   ```
2. Установите зависимости (если есть):
   ```bash
   npm install
   ```
3. Запустите сервер:
   ```bash
   node index.js
   ```

### Клиентская часть
1. Откройте отдельный терминал
2. Перейдите в папку клиента
3. Запустите клиентское приложение (например, через Live Server)

## API Endpoints

### Получить список студентов
```
GET /api/students
```
Параметры:
- `search` - поисковая строка (опционально)

### Создать нового студента
```
POST /api/students
```
Тело запроса должно содержать объект студента

### Получить данные студента
```
GET /api/students/{id}
```

### Обновить данные студента
```
PATCH /api/students/{id}
```
Тело запроса должно содержать обновляемые поля

### Удалить студента
```
DELETE /api/students/{id}
```

## Структура данных студента
```javascript
{
  id: string,             // Уникальный идентификатор
  name: string,           // Имя (обязательное)
  surname: string,        // Фамилия (обязательное)
  lastname: string,       // Отчество (обязательное)
  birthday: string,       // Дата рождения (обязательное)
  studyStart: string,     // Год начала обучения (обязательное)
  faculty: string,        // Факультет (обязательное)
  createdAt: string,      // Дата создания
  updatedAt: string       // Дата последнего обновления
}
```

## Клиентские функции

### Загрузка студентов
```javascript
async function loadStudents() {
  const response = await fetch('/api/students');
  if (!response.ok) throw new Error('Ошибка загрузки');
  return await response.json();
}
```

### Добавление студента
```javascript
async function addStudent(studentData) {
  const response = await fetch('/api/students', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(studentData)
  });
  if (!response.ok) throw new Error('Ошибка добавления');
  return await response.json();
}
```

### Удаление студента
```javascript
async function deleteStudent(studentId) {
  const response = await fetch(`/api/students/${studentId}`, {
    method: 'DELETE'
  });
  if (!response.ok) throw new Error('Ошибка удаления');
}
```

## Особенности реализации
- Полное разделение клиентской и серверной частей
- Валидация данных на сервере
- Поддержка CORS для кросс-доменных запросов
- Поиск по всем полям студента
- Автоматическая генерация ID и временных меток
- Сохранение данных в JSON файле
