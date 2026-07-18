# Predicción de Remesas Familiares hacia El Salvador

Proyecto desarrollado como Trabajo Fin de Máster (TFM) en el marco de la **Maestría en Análisis y Visualización de Datos Masivos**.

El objetivo del proyecto es desarrollar y comparar modelos predictivos para estimar el volumen mensual de remesas familiares hacia El Salvador, integrando información histórica de remesas, variables macroeconómicas de Estados Unidos y El Salvador, datos de deportaciones y variables derivadas de la propia dinámica temporal de la serie.

---

## Objetivo del proyecto

Construir un flujo analítico reproducible que permita:

- integrar información procedente de múltiples fuentes;
- homologar variables con distintas frecuencias temporales;
- construir un dataset maestro mensual;
- realizar análisis exploratorio de datos;
- examinar tendencia, estacionalidad y dependencia temporal;
- entrenar y evaluar distintos modelos predictivos;
- comparar su desempeño sobre un período de prueba común;
- integrar los resultados en un prototipo de análisis y visualización.

---

## Período de estudio

El dataset maestro comprende observaciones mensuales desde:

**enero de 1991 hasta diciembre de 2025**

La evaluación final de los modelos utiliza una división cronológica:

- **Entrenamiento:** período histórico disponible hasta diciembre de 2019.
- **Prueba:** enero de 2020 a diciembre de 2025.

Después de considerar la disponibilidad de los rezagos temporales requeridos para el modelado, el período efectivo de entrenamiento comienza en enero de 1992.

La división se realiza respetando el orden temporal de las observaciones para evitar fuga de información entre pasado y futuro.

---

## Fuentes de datos

El proyecto integra información procedente de:

- **Banco Central de Reserva de El Salvador (BCR):** remesas familiares.
- **Federal Reserve Economic Data (FRED):** variables macroeconómicas de Estados Unidos.
- **Banco Mundial:** indicadores macroeconómicos de El Salvador.
- **Department of Homeland Security (DHS):** información histórica de deportaciones.

Las fuentes presentan diferentes frecuencias y coberturas temporales, por lo que el flujo incluye procesos de limpieza, homologación, transformación e integración.

---

## Variable objetivo

La variable objetivo del estudio es:

`Remesas_Millones_USD`

Representa el volumen mensual de remesas familiares expresado en millones de dólares estadounidenses.

---

## Variables predictoras

El dataset integra variables relacionadas con:

- desempleo hispano en Estados Unidos;
- desempleo general en Estados Unidos;
- inflación de Estados Unidos;
- salario promedio en Estados Unidos;
- PIB de Estados Unidos;
- PIB de El Salvador;
- inflación de El Salvador;
- deportaciones;
- rezagos temporales de remesas;
- variables dummy asociadas a períodos específicos definidos metodológicamente.

Entre las variables temporales derivadas se incluyen:

- `Remesas_Lag1`
- `Remesas_Lag2`
- `Remesas_Lag3`
- `Remesas_Lag12`

---

## Modelos evaluados

Se implementaron y compararon cuatro enfoques predictivos:

### 1. Regresión Lineal Múltiple

Utilizada como modelo de referencia para representar relaciones lineales entre la variable objetivo y los predictores disponibles.

### 2. Random Forest

Modelo de ensamble basado en árboles de decisión. La configuración final utiliza un subconjunto de variables temporales y dummy, priorizando información histórica directamente relacionada con la dinámica de las remesas.

### 3. XGBoost

Modelo de boosting secuencial con mecanismos de regularización y capacidad para representar relaciones no lineales entre los predictores y la variable objetivo.

### 4. LSTM

Red neuronal recurrente Long Short-Term Memory diseñada para trabajar con secuencias temporales. Se utiliza una ventana histórica de 12 meses y el período de prueba conserva las 72 observaciones mensuales mediante el uso de contexto histórico procedente del final del conjunto de entrenamiento.

---

## Métricas de evaluación

Los modelos se comparan mediante:

- **RMSE** — Root Mean Squared Error
- **MAE** — Mean Absolute Error
- **R²** — Coeficiente de determinación
- **MAPE** — Mean Absolute Percentage Error

Todos los modelos se evalúan sobre el mismo período de prueba:

**enero de 2020 a diciembre de 2025**

---

## Estructura del repositorio

```text
TFM-Prediccion-Remesas-El-Salvador/
│
├── data/
│   ├── Dataset_Maestro_Final.csv
│   └── archivos fuente utilizados en la construcción del dataset
│
├── notebooks/
│   ├── 01_Creacion_dataset_maestro.ipynb
│   ├── 02_EDA_Remesas_ElSalvador.ipynb
│   ├── 03_Modelado_Remesas_ElSalvador.ipynb
│   └── 04_Prototipo_Resultados.ipynb
│
├── outputs_eda/
│   ├── figuras del análisis exploratorio
│   └── tablas estadísticas exportadas
│
├── outputs_modelado/
│   ├── figuras de predicción
│   ├── importancias de variables
│   ├── tabla comparativa de modelos
│   ├── resultados del prototipo
│   └── conclusiones exportadas
│
├── Informe_Ejecutivo.html
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Flujo de ejecución

Para reproducir el proyecto se recomienda ejecutar los notebooks en el siguiente orden:

### 1. Construcción del dataset maestro

`01_Creacion_dataset_maestro.ipynb`

Realiza la integración, transformación y preparación de las fuentes utilizadas en el proyecto.

### 2. Análisis exploratorio

`02_EDA_Remesas_ElSalvador.ipynb`

Desarrolla el análisis descriptivo y temporal de los datos, incluyendo:

- evolución histórica;
- distribución anual;
- patrón mensual;
- histogramas y diagramas de caja;
- matriz de correlación;
- descomposición temporal;
- diagramas de dispersión;
- ACF y PACF;
- prueba ADF de estacionariedad.

### 3. Modelado predictivo

`03_Modelado_Remesas_ElSalvador.ipynb`

Implementa:

- preparación de features;
- división cronológica train/test;
- escalado;
- validación temporal;
- Regresión Lineal;
- Random Forest;
- XGBoost;
- LSTM;
- evaluación mediante métricas comunes;
- exportación de resultados comparativos.

### 4. Prototipo de resultados

`04_Prototipo_Resultados.ipynb`

Integra y presenta:

- serie histórica;
- patrón estacional;
- pipeline metodológico;
- figuras de predicción;
- importancia de variables;
- comparación final de modelos;
- conclusiones sobre efectividad;
- generación automática del archivo `Informe_Ejecutivo.html`.

---

## Informe Ejecutivo

La ejecución del Notebook 4 genera automáticamente el archivo `Informe_Ejecutivo.html`, el cual integra los principales resultados del estudio en un dashboard interactivo.

El informe presenta:

- resumen del proyecto;
- métricas oficiales de evaluación;
- comparación entre modelos;
- visualizaciones interactivas;
- figuras complementarias;
- conclusiones finales.

Este archivo constituye el producto final de integración del flujo analítico y puede visualizarse directamente desde un navegador web moderno.

---

## Reproducibilidad

El proyecto utiliza una división cronológica de los datos y evita mezclar observaciones futuras con períodos anteriores durante la evaluación.

Los escaladores se ajustan exclusivamente con información del conjunto de entrenamiento y posteriormente se aplican al conjunto de prueba.

Para los componentes con aleatoriedad se utilizan semillas de reproducibilidad. En el caso de TensorFlow/Keras también se solicitan operaciones deterministas cuando están disponibles en el entorno de ejecución.

Aun con estas medidas, pueden existir pequeñas variaciones entre ejecuciones debido a diferencias de entorno, versiones de bibliotecas, hardware, operaciones numéricas y comportamiento de determinados algoritmos.

Los archivos incluidos en `outputs_eda/` y `outputs_modelado/` corresponden a artefactos generados durante la ejecución reproducible del flujo disponible en este repositorio.

---

## Consideraciones metodológicas

Las relaciones observadas entre variables se interpretan con cautela:

- correlación no implica causalidad;
- algunas variables presentan tendencias temporales comunes;
- los modelos basados en árboles pueden presentar limitaciones al extrapolar fuera del rango observado durante entrenamiento;
- las importancias de variables describen contribuciones internas de cada modelo y no efectos causales;
- el período 2020–2025 presenta condiciones distintas a buena parte del período histórico de entrenamiento.

---

## Tecnologías utilizadas

- Python
- pandas
- NumPy
- Matplotlib
- Seaborn
- Plotly
- scikit-learn
- statsmodels
- XGBoost
- TensorFlow / Keras
- Jupyter Notebook

---

## Autores

**Kelly Mabel Vílchez González, Herbert Fernando Ramírez Aguilar**

Trabajo Fin de Máster  
Maestría en Análisis y Visualización de Datos Masivos  
2026
