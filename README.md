# Limpieza-de-Dataset-de-Peliculas-con-Python
Investigar el conjunto de datos de películas, para detectar inconsistencias de datos.

## Problema Principal
  Column Shifting por comas en títulos.
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
│   └── data_cleaning.ipynb # Proceso paso a paso y documentación
├── scripts/                # Funciones de limpieza modulares (.py)
├── .gitignore              # Archivos excluidos (venv, checkpoints, etc.)
└── README.md               # Documentación del proyecto
