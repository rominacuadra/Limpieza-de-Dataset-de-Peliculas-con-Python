# Limpieza-de-Dataset-de-Peliculas-con-Python
Investigar el conjunto de datos de películas, para detectar inconsistencias de datos.

**Problema Principal:** Column Shifting por comas en títulos.
**Herramientas:** Jupyter Notebook, Pandas.

**Hitos:**
1. **Importación:** Mostrar el error de desplazamiento.
2. **Sanitización:** Uso de `quotechar` y manejo de encodings.
3. **Conversión de Tipos:** Transformar Budget/Revenue de String a Numeric.
4. **Normalización:** Estandarizar nombres de géneros y directores.
5. **Exportación:** Generar un CSV limpio listo para BigQuery.

**Estructura del projecto**
.
├── data/
│   ├── raw/                # Dataset original con errores de desplazamiento (CSV sucio)
│   └── processed/          # Dataset final normalizado y limpio (listo para BigQuery/BI)
├── notebooks/
│   └── data_cleaning.ipynb # Jupyter Notebook con el paso a paso detallado y visualizaciones
├── scripts/                # Funciones auxiliares de limpieza (.py) para mayor modularidad
└── README.md               # Documentación general del proyecto y hallazgos
