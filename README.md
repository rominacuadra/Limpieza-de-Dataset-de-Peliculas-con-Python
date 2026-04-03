# Limpieza-de-Dataset-de-Peliculas-con-Python
Investigar el conjunto de datos de películas, para detectar inconsistencias de datos.

## Problema Principal
El archivo Movie-Data.csv contiene información sobre películas de los últimos 20 años. El separador de este archivo es el caracter coma (,). Al querer transformar este archivo en una tabla en BigQuery, el proceso falla por Column Shifting por comas en títulos. 
Esto significa que algunos títulos que contienen una coma como parte del título, lo que genera un problema ya que es el mismo que el separador del archivo. Los títulos que vienen de esta manera estan encerrados en comillas dobles, lo cual facilita a Python la deteccion de éste patrón para detectar si ignora o no la coma como separador, evitando asi Column Shifting.
## Herramientas
Jupyter Notebook, Pandas.


## Hitos
1. **Importación:** Mostrar el error de desplazamiento.
2. **Sanitización:** Uso de `quotechar` y manejo de encodings.
3. **Conversión de Tipos:** Transformar Budget/Revenue de String a Numeric.
4. **Normalización:** Estandarizar nombres de géneros y directores.
5. **Exportación:** Generar un CSV limpio listo para BigQuery.

## Estructura del Proyecto

```text
.
├── data/
│   ├── raw/                # Dataset original (CSV con desplazamiento de columnas)
│   └── processed/          # Dataset limpio y normalizado
├── notebooks/
│   └── data_cleaning.ipynb # Jupyter Notebook con el paso a paso detallado y visualizaciones
├── scripts/                # Funciones auxiliares de limpieza (.py) para mayor modularidad
└── README.md               # Documentación general del proyecto y hallazgos

# 🎓 Lección: El estándar RFC 4180
* **Hallazgo:** No todos los lectores de CSV son iguales. 
* **GitHub/Pandas:** Respetan las comillas dobles como encapsuladores por defecto.
* **Excel/BigQuery:** Pueden fallar si la configuración regional o el esquema manual no coinciden.
* **Conclusión:** Como Analista, mi trabajo es asegurar que el dato sea "portable" y se vea bien en CUALQUIER herramienta, no solo en las más inteligentes.
