# Установка PostgreSQL 15 в WSL (Ubuntu) — Полный Гайд

## Шаг 1. Подключение официального репозитория PostgreSQL
```bash
sudo apt-get install lsb-release
```

Добавляем репозиторий PostgreSQL:
```bash
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ \
$(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
```

Добавляем ключ:
```bash
wget --quiet -O - https://postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```

Обновляем список пакетов:
```bash
sudo apt-get update
```
---

##  Шаг 2. Установка PostgreSQL 15

```bash
sudo apt-get install postgresql-15
```
---
## Шаг 3. Создание каталога для базы данных

Так как systemd в WSL не работает, мы не запускаем службу через systemctl — всё делаем вручную.
Создаём каталог для хранения базы (например, /var/lib/postgres_data):
```bash 
sudo mkdir -p /var/lib/postgres_data
sudo chown postgres:postgres /var/lib/postgres_data
```
---
## Шаг 4. Инициализация кластера
```bash
sudo -u postgres /usr/lib/postgresql/15/bin/initdb -D /var/lib/postgres_data
```
Если команда выполнится успешно, тогда появится сообщение:
```swift
Success. You can now start the database server using:
  /usr/lib/postgresql/15/bin/pg_ctl -D /var/lib/postgres_data -l logfile start
```
---
## Шаг 5. Запуск PostgreSQL вручную
```bash
sudo -u postgres /usr/lib/postgresql/15/bin/pg_ctl -D /var/lib/postgres_data -l /var/lib/postgres_data/logfile.log start
```
---
## Шаг 6. Проверка
Подключение к серверу:
```bash
sudo -u pustgers psql
```
Проверка даты и версии:
```sql
SELECT now();
SELECT version();
```
---
## Шаг 7. Создание пользователя и базы данных

```sql
CREATE USER myuser WITH PASSWORD 'mypassword';
CREATE DATABASE mydb OWNER myuser;
```

