# Типовая задача дата-инженера

...

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
