# Server Logs Analysis Pipeline

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python)
![DuckDB](https://img.shields.io/badge/DuckDB-Fast_OLAP-yellow?style=for-the-badge)
![SQL](https://img.shields.io/badge/SQL-Advanced-orange?style=for-the-badge)

Este proyecto implementa un pipeline de análisis de datos para procesar logs de servidores web. Utilizando **DuckDB** como motor OLAP en-memoria, se procesaron +5000 registros para identificar cuellos de botella de latencia, tasas de error críticas y patrones de tráfico.

## Key Findings (Hallazgos Principales)

El análisis reveló problemas críticos de infraestructura que afectan la experiencia del usuario:

* **Latencia Crítica:** Se detectó un tiempo de respuesta **p95 superior a 24 segundos** en endpoints vitales como `/api/auth/login` y `/api/checkout`, sugiriendo bloqueos en base de datos.
* **Inestabilidad en Auth:** El servicio de Login presenta una alta tasa de errores de infraestructura (**502/503**) durante picos de carga, bloqueando el ingreso de usuarios.
* **Tráfico Constante:** No se identificaron "ventanas de mantenimiento" claras (horas de tráfico cero), lo que complica las actualizaciones sin *downtime*.

## Stack Tecnológico

* **Python:** Orquestación y manejo de entorno.
* **DuckDB:** Motor SQL embebido para procesamiento analítico de alto rendimiento.
* **Pandas:** Visualización final de resultados tabulares.
* **Jupyter Notebook:** Entorno de desarrollo interactivo.

## Estructura del Proyecto

```bash
├── data/                   # (Ignorado en git) Logs crudos en formato JSON
├── notebooks/
│   └── log_analysis.ipynb  # Análisis completo (Queries + Visualización)
├── .gitignore              # Configuración para ignorar archivos temporales
└── README.md               # Documentación del proyecto
```

## Análisis SQL Realizados

El notebook incluye queries avanzadas utilizando:
1.  **Agregaciones complejas:** Cálculo de percentiles (`quantile`) para medir latencia real (p95).
2.  **Window Functions:** Uso de `RANK()` particionado para identificar los endpoints más lentos por método HTTP.
3.  **Time-Series Analysis:** Uso de `LAG()` para comparar tendencias de tráfico hora a hora.

## Cómo correr este proyecto

1.  **Clonar el repositorio:**
    ```bash
    git clone [https://github.com/juancruzgodoy/web-server-log-analysis)
    ```

2.  **Instalar dependencias:**
    ```bash
    pip install duckdb pandas notebook
    ```

3.  **Ejecutar el Notebook:**
    Abrir `notebooks/log_analysis.ipynb` en VS Code o Jupyter Lab y ejecutar todas las celdas.
