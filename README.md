# 🎬 Data Pipeline: Normalización y Limpieza de Inversiones Cinematográficas (2013-2015)

## 📌 Objetivo del Proyecto
Este proyecto documenta el proceso de **Data Wrangling** y limpieza de un conjunto de datos sobre la industria del cine. El enfoque principal fue resolver problemas críticos de estructura y tipado para transformar un archivo CSV "sucio" en una fuente de datos confiable y lista para análisis avanzado en **Google BigQuery**.

## 🚩 Problema Principal: Column Shifting & Delimitación
El archivo original `Movie-Data.csv` presentaba una inconsistencia estructural grave:
* **El Desafío:** El delimitador es la coma (`,`), pero muchos títulos de películas contienen comas como parte de su nombre (ej: *"The Way, Way Back"*). 
* **El Impacto:** Las herramientas de análisis interpretaban esas comas internas como separadores de columna, desplazando los datos financieros hacia la derecha (*Column Shifting*) y corrompiendo la integridad del dataset.
* **La Causa:** Falta de estandarización (RFC 4180) en el archivo de origen, lo que impedía una ingesta directa en herramientas de Data Warehouse.

## 🛠️ Stack Tecnológico
* **Python & Pandas:** Motor principal de procesamiento y transformación.
* **Jupyter Notebook:** Entorno de desarrollo para la documentación del paso a paso.
* **BigQuery:** Plataforma de destino para el almacenamiento y consultas SQL.

## 🚀 Hitos del Pipeline
1. **Diagnóstico de Datos:** Identificación del error de *Column Shifting* mediante la carga de datos sin calificadores, exponiendo visualmente el desajuste de las columnas.
2. **Ingeniería de Ingesta:** Implementación de parámetros avanzados (`quotechar='"'`) en Pandas para encapsular los títulos y proteger la integridad de los datos frente a las comas internas.
3. **Normalización de Esquema:** Transformación de encabezados (eliminación de paréntesis y espacios) hacia una convención **snake_case**, garantizando la compatibilidad técnica con motores SQL.
4. **Aseguramiento de Tipos (Data Typing):** Se detectó mediante `df.info()` que las métricas de `budget` y `revenue` se importaron originalmente como `object` (strings). Se aplicó una conversión explícita a tipos numéricos (`pd.to_numeric`), habilitando la capacidad de realizar cálculos aritméticos.Limpieza de espacios en blanco en todas las columnas de texto.
5. **Control de Calidad:**  Validación de valores únicos (distinct) en categorías como Genre para asegurar la consistencia semántica del dataset. Conteo de valores nulos por columnas, para analizar coerencia de falta de valores. Busqueda de duplicados.
6. **Exportación del dataset procesado:** Generación del archivo final `Movie-Data-Clean.csv` para la ingesta en el Data Warehouse.

## 📂 Estructura del Proyecto
```text
.
├── data/
│   ├── raw/                # Dataset original (Inconsistente)
│   └── processed/          # Dataset normalizado (Listo para producción)
├── notebooks/
│   └── data_cleaning.ipynb # Notebook con el proceso de ETL detallado
└── README.md               # Documentación estratégica
```

## Conclusiones
1. Integridad Estructural: La falta de adherencia al estándar RFC 4180 en el origen de los datos puede comprometer la integridad de todo un pipeline. Identificar y mitigar el Column Shifting prematuramente evitó la pérdida de información crítica en las métricas financieras.
2. Optimización para SQL: La normalización de encabezados a snake_case no es solo estética; es una necesidad técnica para asegurar la compatibilidad y fluidez en entornos de almacenamiento como Google BigQuery, eliminando errores de sintaxis en las consultas..
3. Calidad de Métricas: La transformación de tipos de datos (Strings a Numeric/Datetime) permitió convertir un archivo de texto plano en un activo analítico. La limpieza de símbolos monetarios y la validación de rangos (mínimos/máximos) garantizan que cualquier cálculo posterior (como el ROI) sea fiable.
4. Tratamiento de Valores Faltantes: Se determinó que los nulos en columnas de reparto (Cast) y dirección secundaria eran "ausencias lógicas" y no errores de carga. La decisión de estandarizarlos como "N/A" mejora la legibilidad y evita interpretaciones erróneas en las herramientas de visualización.
5. Portabilidad de Datos: El resultado final es un dataset agnóstico a la herramienta, listo para ser consumido en entornos de producción, cumpliendo con los estándares de calidad de un ciclo de vida de datos profesional.

