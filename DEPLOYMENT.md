# Развертывание на Timeweb App Platform

## 📋 Требования

- Аккаунт на [timeweb.com](https://timeweb.com)
- GitHub репозиторий (этот репозиторий)
- API ключ Wildberries

## 🚀 Шаги развертывания

### 1. Подготовка репозитория

Репозиторий уже содержит необходимые конфигурационные файлы:
- `app.json` - конфигурация для App Platform
- `Procfile` - описание процессов
- `package.json` - зависимости Node.js
- `.env.example` - пример переменных окружения

### 2. Подключение к App Platform

1. Перейдите в Timeweb управляющую панель
2. Выберите **App Platform**
3. Нажмите **Создать приложение**
4. Выберите **Из GitHub репозитория**
5. Авторизуйте доступ к вашему GitHub аккаунту
6. Выберите репозиторий: `avovmvmvmyvmyvm-cmyk/wildberries-`

### 3. Настройка конфигурации

В процессе создания приложения:

**Основные параметры:**
- **Name**: wildberries-sdk-app
- **Region**: выберите ближайший к вам регион
- **Environment**: Production

**Переменные окружения:**
```
NODE_ENV=production
API_PORT=3000
LOG_LEVEL=info
WILDBERRIES_API_KEY=<ваш_api_ключ>
```

**Объем ресурсов:**
- RAM: 512 MB (начальная)
- CPU: 1 ядро (начальная)
- Тип: Node.js 18+

### 4. Развертывание

После заполнения всех параметров:
1. Нажмите **Развернуть**
2. Дождитесь успешного завершения

Приложение будет доступно по адресу:
```
https://your-app-id.app.timeweb.cloud
```

## 🔌 API Endpoints

После развертывания доступны следующие endpoint'ы:

### Health Check
```
GET /health
```
Проверка статуса приложения.

**Ответ:**
```json
{
  "status": "OK",
  "timestamp": "2024-01-01T00:00:00.000Z",
  "uptime": 123.45,
  "environment": "production"
}
```

### API Status
```
GET /api/status
```
Информация о статусе API и конфигурации.

**Ответ:**
```json
{
  "service": "Wildberries SDK Gateway",
  "version": "1.0.0",
  "status": "running",
  "api_configured": true,
  "timestamp": "2024-01-01T00:00:00.000Z"
}
```

### API Documentation
```
GET /api/docs
```
Полная документация доступных endpoint'ов.

### Seller Information
```
GET /api/v1/seller-info
```
Получить информацию о продавце (требует конфигурации Wildberries API).

## 🔧 Переменные окружения

| Переменная | Описание | Обязательно | По умолчанию |
|-----------|---------|-----------|-------------|
| `WILDBERRIES_API_KEY` | API ключ Wildberries | ✅ Да | - |
| `API_PORT` | Порт для сервера | ❌ Нет | 3000 |
| `NODE_ENV` | Окружение (development/production) | ❌ Нет | production |
| `LOG_LEVEL` | Уровень логирования (debug/info/warn/error) | ❌ Нет | info |
| `CORS_ORIGIN` | CORS origin | ❌ Нет | * |

## 📊 Мониторинг

### Просмотр логов
```bash
# В управляющей панели Timeweb перейдите в раздел Logs
# Или используйте Timeweb CLI:
timeweb app logs wildberries-sdk-app
```

### Метрики
- CPU использование
- Память (RAM)
- Входящий/исходящий трафик
- Ошибки приложения

## 🔄 Автоматическое развертывание

При push'е в ветку `main` GitHub Actions:
1. Установит зависимости
2. Запустит тесты
3. Развернет приложение на App Platform

## 🛠 Локальная разработка

### Установка зависимостей
```bash
npm install
```

### Запуск в режиме разработки
```bash
npm run dev
```

### Копирование .env файла
```bash
cp .env.example .env
# Добавьте ваш WILDBERRIES_API_KEY в .env
```

## 📖 Полезные ссылки

- [Документация Timeweb App Platform](https://timeweb.com/ru/help/category/app-platform)
- [Wildberries SDK GitHub](https://github.com/eslazarev/wildberries-sdk)
- [Express.js документация](https://expressjs.com/)
- [Node.js документация](https://nodejs.org/)

## 🆘 Решение проблем

### Приложение не запускается
1. Проверьте логи в управляющей панели
2. Убедитесь, что `WILDBERRIES_API_KEY` установлен
3. Проверьте версию Node.js (требуется 18+)

### Ошибка при подключении к Wildberries API
1. Проверьте корректность API ключа
2. Убедитесь в наличии необходимых прав доступа
3. Проверьте сетевое соединение

### Высокое использование памяти
1. Уменьшите количество одновременных соединений
2. Увеличьте выделенную память в настройках App Platform
3. Проверьте наличие утечек памяти

## 📝 Лицензия

MIT License - см. LICENSE файл в репозитории
