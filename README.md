# ⛽ Proyecto Histórico de Combustibles (Microsoft Fabric)

Este proyecto implementa una canalización de datos *end-to-end* en **Microsoft Fabric** aplicando la **Arquitectura Medallón** (Bronze, Silver y Gold) para analizar el histórico de precios de combustibles (API de la EIA).

## 🛠️ Arquitectura del Pipeline
* **Bronze:** Ingesta del archivo JSON crudo desde la API mediante una canalización de datos (*Copy Data*).
* **Silver (Estrategia Append Only):** Limpieza y desduplicación en **PySpark**. Se utiliza una carga **Append Only** e idempotente mediante `MERGE` en Delta Lake, asegurando que solo se agreguen registros nuevos sin duplicar ni alterar la historia.
* **Gold (Modelo Dimensional):** Creación de un **Esquema en Estrella** con dimensiones (`dim_combustible`, `dim_mes`) y tablas de hechos (`fact_precios_mensual`, `fact_ultimo_precio_semanal`).
* **Power BI:** Modelo semántico configurado en modo **Direct Lake** para visualización y tarjetas KPI.
