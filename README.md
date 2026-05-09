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
flowchart LR
    subgraph API
        direction LR
        API_E["Earthquake API"]
    end

    subgraph ETL
        direction LR
        AirFlow
    end

    subgraph Storage
        direction LR
        S3
    end

    subgraph DWH
        direction LR
        subgraph PostgreSQL
            direction LR
            subgraph model
                direction LR
                ods["ODS Layer"]
                dm["Data Mart Layer"]
            end
        end
    end

    subgraph BI
        direction LR
        MetaBase
    end

    API_E -->|Extract Data| AirFlow
    AirFlow -->|Load Data| S3
    S3 -->|Extract Data| AirFlow
    AirFlow -->|Load Data to ODS| ods
    ods -->|Extract Data| AirFlow
    AirFlow -->|Transform and Load Data to DM| dm
    dm -->|Visualize Data| MetaBase
    style API fill: #FFD1DC, stroke: #000000, stroke-width: 2px
    style ETL fill: #D9E5E4, stroke: #000000, stroke-width: 2px
    style Storage fill: #FFF2CC, stroke: #000000, stroke-width: 2px
    style DWH fill: #C9DAF7, stroke: #000000, stroke-width: 2px
    style PostgreSQL fill: #E2F0CB, stroke: #000000, stroke-width: 2px
    style BI fill: #B69CFA, stroke: #000000, stroke-width: 2px

