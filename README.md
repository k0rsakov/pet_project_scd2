# Типовая задача дата-инженера

Ты освоил SQL, немного ETL и уже представляешь, как работают пайплайны? Пора познакомиться с одной из базовых, но важных
задач в жизни дата-инженера — реализация Slowly Changing Dimension Type 2 (SCD2).

В этом [видео](https://youtu.be/Q65vYLlEDQQ) я объясняю:
- Что такое медленно изменяющиеся измерения (Slowly Changing Dimensions)
- Почему SCD2 важна для аналитики и отчётности
- Как технически реализовать SCD2: даты, флаги, версионность
- Что учитывать при работе с SCD2 в реальных проектах
- Как реализовать SCD2 на SQL

📌 Основная идея: SCD2 — это не просто техника, это способ сохранить историю изменений и повысить доверие к данным.
Каждый дата-инженер должен понимать, как её правильно реализовывать и адаптировать под нужды бизнеса.

💼 Хочешь ускорить рост в карьере? Я предлагаю менторство по дата-инженерии и IT-консультации:
- Менторство: https://korsak0v.notion.site/Data-Engineer-185c62fdf79345eb9da9928356884ea0
- Консультации: https://korsak0v.notion.site/Data-Engineer-185c62fdf79345eb9da9928356884ea0

📚 Упомянутые видео:
- Зачем нужны pet-проекты?: https://youtu.be/pVwbIntazLo
- Лучший пет-проект для дата-инженера (The best pet-project for a data-engineer): https://youtu.be/MQPHgUQvKnI

🔔 Подпишись на канал, если хочешь разбираться в реальных задачах дата-инженеров, а не только в теории. Делитесь в
комментариях, приходилось ли вам реализовывать SCD2 — и с какими трудностями вы столкнулись.

Менторство/консультации по IT – https://korsak0v.notion.site/Data-Engineer-185c62fdf79345eb9da9928356884ea0
TG канал – https://t.me/DataLikeQWERTY
Instagram – https://www.instagram.com/i__korsakov/
Habr – https://habr.com/ru/users/k0rsakov/publications/articles/

Тайминги:
00:00 – Начало
00:10 – Основная проблематика аналитики
01:28 – Что такое SCD
03:50 — SCD2 (стандарт)
05:47 – Создание репозитория
06:24 – Клонирование репозитория
06:44 – Настройка git–окружения для репозитория
07:52 – Настройка проекта
08:32 – Объяснение инфраструктуры проекта
10:00 – Запуск инфраструктуры
11:03 – Добавление примеров данных
11:21 – Демо примера SCD2 и его возможностей
14:33 – Реализация SCD2 с нуля
15:07 – Создание схем и моделей
18:05 – Наполнение raw данными
18:45 – Подключение виртуального окружения (интерпретатора) в PyCharm
21:40 – Исследование raw данных
25:10 – Создание ods данных
27:45 – Исследование ods данных
29:47 – Наполнение dds данными (построение SCD2)
32:30 – Исследование dds данных (SCD2)
35:48 – Резюме и возможные моменты для улучшения проекта

#SCD2 #SlowlyChangingDimension #dataengineering #датаинженер #ETL #SQL #Spark #профессиядатаинженер #карьеравIT
#хранилищеданных #datawarehouse #менторствоIT #аналитикаданных #историяизменений #ITкарьера #airflow #bigdata
#инженерданных #проектдлядатаинженера #типовыезадачиIT

## Создание виртуального окружения

```bash
python3.12 -m venv venv && \
source venv/bin/activate && \
pip install --upgrade pip && \
pip install poetry && \
poetry lock && \
poetry install
```

## Разворачивание инфраструктуры

```bash
docker-compose up -d
```

## Ссылки

- [Лучший пет-проект для дата-инженера (The best pet-project for a data-engineer)](https://youtu.be/MQPHgUQvKnI)
- [Описание работы API](https://earthquake.usgs.gov/fdsnws/event/1/#methods)
- [Описание полей из API](https://earthquake.usgs.gov/data/comcat/index.php)
- [airflow docker-compose](https://airflow.apache.org/docs/apache-airflow/2.10.5/docker-compose.yaml)

## Notes

Схемы и модели для демо:

```sql
CREATE SCHEMA stg;

CREATE SCHEMA raw;
DROP TABLE IF EXISTS raw.raw_users;
CREATE TABLE raw.raw_users (
	id uuid NULL,
	created_at timestamp NULL,
	updated_at timestamp NULL,
	first_name text NULL,
	last_name text NULL,
	middle_name text NULL,
	birthday date NULL,
	email text NULL,
	ts_db timestamp NULL
);

CREATE SCHEMA ods;
DROP TABLE IF EXISTS ods.dim_users;
CREATE TABLE ods.dim_users (
	id uuid PRIMARY KEY,
	created_at timestamp NULL,
	updated_at timestamp NULL,
	first_name text NULL,
	last_name text NULL,
	middle_name text NULL,
	birthday date NULL,
	email text NULL
);

CREATE SCHEMA dds;
DROP TABLE IF EXISTS dds.dim_scd2_users;
CREATE TABLE dds.dim_scd2_users (
	id uuid,
	created_at timestamp NULL,
	updated_at timestamp NULL,
	first_name text NULL,
	last_name text NULL,
	middle_name text NULL,
	birthday date NULL,
	email text NULL,
	actual_from timestamp NULL,
	actual_to timestamp NULL,
	ts_db timestamp NULL
);
```
