## Веб-сервер для локальной разработки на PHP + MySQL + Redis

### На борту:

 - PHP FPM     8.0
 - MySQL       8.0.25
 - Redis       6.2.4
 - Nginx       1.21.0
 - PHP MyAdmin 5.1.1
 - Composer    2
 - ОС Alpine Linux

### Сначала

После git clone заходим в терминале в данную папку. Все последующие консольные команды должны выполняться именно в ней.

Создаем файл `.env` по примеру `env-example`.

В нем прописываем порты и пути к папкам:

 - `DB_DIR`  - здесь будут храниться базы данных `MySQL` и `Redis`
 - `WEB_DIR` - папка для создания проектов (доменов)
 - `LOG_DIR` - папка для логов 

Чтобы стек можно было обновлять из `github`, создавайте перечисленные папки вне папки стека (по умолчанию они располагаются на уровень выше).

_Папки создаются автоматически при запуске стека._

### Запуск

Командой `./start`. При первом старте нужно дождаться, пока развернется база данных. Последующие запуски проходят быстрее.

### Разработка

Все сайты находятся в директории `WEB_DIR`. Содержимое `localhost` доступно по адресу http://localhost/ , другие папки в `WEB_DIR` работают как поддомены, например, `http://test.localhost/`. Поддомены можно создавать и открывать в браузере без перезапуска стека.

### Подключение к сервисам в коде проектов

1. MySQL:

 - сервер: `mysql`
 - логин: `root`
 - пароль: `root`
 - порт: `3306`

2. Redis

 - сервер: `redis`
 - порт: `6379`

### Другие команды

 - `./hardstop`      - останавливает и удаляет контейнеры
 - `./rebuild`       - пересборка изменившихся контейнеров
 - `./restart-nginx` - перезапуск веб-сервера для применения новых конфигов
 - `./stop`          - остановка стека, выгрузка контейнеров

### Логи 

Находятся в папке `LOG_DIR`

### Управление базой данных

`MyAdmin` доступен по адресу `http://mysql.localhost/`

### Настройка портов

В файле `.env` можно указать порты для любого из сервисов. Настройки применяются после перезапуска (`start` - `stop`)