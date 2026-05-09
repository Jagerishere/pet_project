# 🌍 Pet-проект: ETL для землетрясений – анализ сейсмической активности

Автоматизированный ETL-конвейер для сбора, обработки и визуализации данных о землетрясениях по всему миру.

---

## 🎯 О проекте

Основная цель этого проекта — показать, как с помощью современных инструментов (`Airflow`, `PostgreSQL`, `MinIO`, `Metabase` и `Docker`) собрать production-like пайплайн обработки данных, от источника данных до визуализации.

### Ключевые возможности
-   **Оркестрация ETL**: `Apache Airflow` управляет пайплайном, который загружает данные из USGS Earthquake API и раскладывает их по слоям `raw`, `staging` и `mart`.
-   **Эффективное хранение**: `MinIO`, S3-совместимое хранилище, используется как `Data Lake` для сырых и промежуточных данных.
-   **Аналитическая база**: `PostgreSQL` в роли `Data Warehouse` для хранения финальных витрин данных.
-   **Наглядная визуализация**: `Metabase` подключается напрямую к витринам, позволяя строить дашборды с картами землетрясений и графиками их активности.
-   **Полная изоляция**: Весь проект поднимается одной командой благодаря `Docker Compose`.

---

## 🛠️ Используемые технологии

-   **Инфраструктура**: Docker, Docker Compose
-   **Оркестрация**: Apache Airflow
-   **Хранилище данных**: PostgreSQL
-   **Data Lake**: MinIO (S3-совместимое)
-   **Визуализация**: Metabase
-   **Язык**: Python
-   **Источник данных**: [USGS Earthquake API](https://earthquake.usgs.gov/fdsnws/event/1/)

---

##  Data Architecture
<img width="2166" height="721" alt="Untitled" src="https://github.com/user-attachments/assets/6af5cce6-1266-4e20-9f6f-80d8e5e7707f" />


## Создание виртуального окружения
```
python3 -m venv venv && \
source venv/bin/activate && \
pip install --upgrade pip && \
pip install -r requirements.txt
```

## Разворачивание инфраструктуры
```
docker-compose up -d
```


