# GitVerse REST API OpenAPI Description

[![GitVerse](https://img.shields.io/badge/GitVerse-API%20Specifications-blue)](https://gitverse.ru)
[![OpenAPI 2.0](https://img.shields.io/badge/OpenAPI-2.0-green)](https://swagger.io/specification/v2/)

Официальные спецификации Публичного API GitVerse в формате **OpenAPI 2.0 (Swagger)**.

## Что такое OpenAPI?

[OpenAPI Specification](https://github.com/OAI/OpenAPI-Specification) (ранее Swagger) — это стандартный, не зависящий от языка программирования интерфейс для описания HTTP API, который позволяет как людям, так и компьютерам понимать возможности сервиса без доступа к исходному коду, документации или анализу сетевого трафика.

## Статус проекта

Спецификации считаются **стабильными** и готовы к использованию. Репозиторий автоматически обновляется при релизе новой версии API или обновлении документации.

## Структура репозитория

```
/v1/
  ├── openapi-1.0.json
  ├── openapi-1.1.json
  ├── openapi-1.2.json
  └── openapi-1.3.json
/v2/
  ├── openapi-2.0.json
  ├── openapi-2.1.json
  └── openapi-2.2.json
/v3/
  ├── openapi-3.0.json
  └── openapi-3.1.json
...
```

### Версионирование

Каждая директория (`/v1`, `/v2`, `/v3`, …) соответствует **MAJOR-версии API**, как определено в [политике версионирования GitVerse](https://gitverse.ru/docs/public-api/using-public-api/api-versioning/).

1. **MAJOR-версия API** (например, `version=2`) определяет **контракт** (эндпоинты, параметры, форматы)
2. **Минорные версии спецификации** (например, `2.0` → `2.1`) **не меняют контракт** — они вносят только уточнения в документацию, исправления описаний или примеров
3. Все минорные версии в рамках одной MAJOR-версии **полностью совместимы**

## Использование

### Прямые ссылки

- **Версия 1**: [`/v1/openapi-1.0.json`](v1/openapi-1.0.json)
- **Версия 2**: [`/v2/openapi-2.0.json`](v2/openapi-2.0.json)  
- **Версия 3**: [`/v3/openapi-3.0.json`](v3/openapi-3.0.json)

Эти URL можно подключать напрямую в **Swagger UI**, **Postman** или любые другие инструменты, поддерживающие OpenAPI.

### Генерация клиентских SDK

Используйте спецификации для генерации клиентских SDK на любом языке программирования:

```bash
# Пример использования OpenAPI Generator
openapi-generator generate -i https://gitverse.ru/api-specs/v3/openapi-3.0.json -g python -o ./gitverse-client
```

### Интеграция с инструментами

- **Swagger UI**: Импортируйте JSON-файл для интерактивной документации
- **Postman**: Используйте прямые ссылки для создания коллекций
- **Автотесты**: Валидация запросов и ответов по спецификации
- **Мониторинг**: Проверка соответствия API контракту

## Быстрый старт

### Указание версии API

Всегда указывайте версию API через заголовок `Accept` при работе с эндпоинтами:

```http
GET /api/users/me HTTP/1.1
Host: api.gitverse.ru
Accept: application/vnd.gitverse.object+json; version=2
Authorization: Bearer YOUR_ACCESS_TOKEN
```

### Пример запроса с cURL

```bash
curl -H "Accept: application/vnd.gitverse.object+json; version=2" \
     -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
     https://api.gitverse.ru/users/me
```

## ⚠️ Важно

1. **Независимость версий**: Версии API **не привязаны** к внутренним релизам GitVerse
2. **Поддержка версий**: Устаревшие MAJOR-версии удаляются из репозитория **после окончания срока поддержки** (6 месяцев с момента выхода следующей MAJOR-версии)
3. **Миграция**: При переходе между MAJOR-версиями внимательно изучайте [CHANGELOG.md](CHANGELOG.md) для понимания breaking changes

## Ограничения

- Спецификация описывает только публичные эндпоинты API
- Некоторые параметры могут требовать дополнительной кодировки
- Для работы с API требуется [аутентификация](https://gitverse.ru/docs/public-api/authentication/)

## Внесение вклада

Мы приветствуем сообщество к улучшению документации! Если вы обнаружили:

- Несоответствие между поведением API и спецификацией
- Опечатки или неточности в описаниях
- Отсутствующие примеры или документацию

### Процесс контрибьютинга

1. Создайте [issue](issues/new) с описанием проблемы
2. Для значительных изменений обсудите их в issue перед реализацией
3. Следуйте руководству в [CONTRIBUTING.md](CONTRIBUTING.md)

**Примечание**: Из-за того, что эти спецификации используются во всей экосистеме GitVerse, мы не принимаем прямые пул-реквесты, изменяющие контракт API. Этот репозиторий автоматически синхронизируется с описаниями, используемыми для валидации запросов API GitVerse.

## Лицензия

Этот проект лицензирован по лицензии MIT. Подробнее см. в файле [LICENSE](LICENSE).

## Контакты

- Документация: [GitVerse Public API Docs](https://gitverse.ru/docs/public-api/)
- Поддержка: [support@gitverse.ru](mailto:support@gitverse.ru)
- Сообщения о проблемах: [GitHub Issues](issues)

---

**Примечание**: Этот репозиторий содержит только спецификации OpenAPI. Для работы с API GitVerse вам потребуется [зарегистрировать приложение](https://gitverse.ru/settings/developers) и получить токен доступа.
