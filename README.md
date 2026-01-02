# Server Logs Analysis Pipeline

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python)
![DuckDB](https://img.shields.io/badge/DuckDB-Fast_OLAP-yellow?style=for-the-badge)
![SQL](https://img.shields.io/badge/SQL-Advanced-orange?style=for-the-badge)

Este proyecto implementa un pipeline de análisis de datos para procesar logs de servidores web. Utilizando **DuckDB** como motor OLAP en-memoria, se procesaron +5000 registros para identificar cuellos de botella de latencia, tasas de error críticas y patrones de tráfico.

## Key Findings (Hallazgos Principales)

El análisis reveló problemas críticos de infraestructura que afectan la experiencia del usuario:

* ** Latencia Crítica:** Se detectó un tiempo de respuesta **p95 superior a 24 segundos** en endpoints vitales como `/api/auth/login` y `/api/checkout`, sugiriendo bloqueos en base de datos.
* ** Inestabilidad en Auth:** El servicio de Login presenta una alta tasa de errores de infraestructura (**502/503**) durante picos de carga, bloqueando el ingreso de usuarios.
* ** Tráfico Constante:** No se identificaron "ventanas de mantenimiento" claras (horas de tráfico cero), lo que complica las actualizaciones sin *downtime*.

## Stack Tecnológico

* **Python:** Orquestación y manejo de entorno.
* **DuckDB:** Motor SQL embebido para procesamiento analítico de alto rendimiento.
* **Pandas:** Visualización final de resultados tabulares.
* **Jupyter Notebook:** Entorno de desarrollo interactivo.

## Estructura del Proyecto

```bash
├── data/                   # (Ignorado en git) Logs crudos en formato JSON/Parquet
├── notebooks/
│   └── log_analysis.ipynb  # Análisis completo (Queries + Visualización)
├── .gitignore              # Configuración para ignorar archivos temporales
└── README.md               # Documentación del proyecto
