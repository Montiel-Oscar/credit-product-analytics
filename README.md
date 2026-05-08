# Credit Product Analytics — Bank Credit Scoring

> Proyecto final del curso de **Minería de Datos** · Facultad de Ingeniería, UNAM  
> Área asignada: **Dirección de Productos de Crédito**

---

## 📌 Descripción

Este proyecto simula el trabajo de la Dirección de Productos de Crédito de un banco.  
El objetivo es analizar el portafolio de solicitudes de crédito para identificar **qué productos generan el mejor margen**, a qué perfil de cliente conviene ofrecerlos y construir modelos de machine learning que soporten una propuesta de negocio fundamentada en datos.

El proyecto forma parte de un ejercicio institucional donde distintas áreas del banco (Riesgo, Marketing, Sucursales, Tecnología, etc.) trabajan con la misma base de datos y coordinan sus estrategias para lograr objetivos organizacionales comunes.

---

## 🎯 Objetivo del área

> Identificar los productos de crédito con mayor margen de rentabilidad, definir el perfil del cliente ideal para cada producto y proponer una estrategia de colocación basada en modelos predictivos.

**Preguntas de negocio que guían el análisis:**
- ¿Qué producto (Clásica, Oro, Crédito Auto) concentra mayor línea de crédito aprobada?
- ¿Qué perfil sociodemográfico y financiero tiene mayor probabilidad de aprobación?
- ¿Cómo se distribuye el riesgo entre los distintos productos?
- ¿Es posible predecir qué clientes serán aprobados y con qué línea?

---

## 📂 Estructura del repositorio

```
credit-product-analytics/
│
├── README.md
├── .gitignore
│
├── data/
│   ├── raw/                          # Datos originales — no modificar
│   │   ├── ProyectoMineriaBanco.csv
│   │   └── ProyectoMineri_acatalogo.xlsx
│   └── processed/                    # Datos limpios y normalizados
│   └── docs/
│       └── ProyectoMineri_aDatos.pdf
│
├── notebooks/
│   ├── 01_exploratory_analysis.ipynb # EDA: distribuciones, nulos, outliers
│   ├── 02_data_cleaning.ipynb        # Limpieza y validación vs catálogo
│   ├── 03_feature_engineering.ipynb  # Encoding, normalización, nuevas variables
│   └── 04_modeling.ipynb             # Modelos de machine learning
│
├── src/
│   ├── __init__.py
│   ├── cleaning.py                   # Funciones reutilizables de limpieza
│   └── visualization.py              # Helpers de graficación
│
├── reports/
│   ├── figures/                      # Gráficas exportadas (.png / .svg)
│   └── estrategia_area.pdf           # Documento de estrategia del área
│
└── references/                       # Papers o fuentes de respaldo
```

---

## 📊 Dataset

| Atributo | Detalle |
|---|---|
| Fuente | Banco ficticio — proyecto académico UNAM |
| Registros | 4,352 solicitudes de crédito |
| Variables | 27 columnas (numéricas, categóricas y catálogos) |
| Periodo | No especificado |
| Archivo principal | `ProyectoMineriaBanco.csv` |
| Diccionario | `ProyectoMineri_acatalogo.xlsx` (2 hojas: Metadata + Catálogos) |

**Variables clave para el área de Productos de Crédito:**

| Variable | Descripción |
|---|---|
| `PRODUCTO` | Tipo de crédito asignado: CLASICA, TARJETA_ORO, CREDITO_AUTO, PENDIENTE |
| `LINEA_CREDITO_FINAL` | Monto de la línea aprobada |
| `APROBACION_TC` | Resultado final: APROBADO, PRE-APROBADO, RECHAZADO |
| `NIVEL_RIESGO` | Riesgo estimado del cliente |
| `SCORE_CLIENTE` | Score calculado por reglas del sistema |
| `SEGMENTO_CLIENTE` | Segmento socioeconómico |

---

## 🛠️ Stack tecnológico

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas)
![Scikit--learn](https://img.shields.io/badge/Scikit--learn-1.x-F7931E?logo=scikit-learn)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.x-11557c)
![Seaborn](https://img.shields.io/badge/Seaborn-0.13-4C72B0)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter)

---

## ▶️ Cómo correr el proyecto

```bash
# 1. Clonar el repositorio
git clone https://github.com/tu-usuario/credit-product-analytics.git
cd credit-product-analytics

# 2. Crear entorno virtual (recomendado)
python -m venv venv
source venv/bin/activate        # Mac/Linux
venv\Scripts\activate           # Windows

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Correr los notebooks en orden
jupyter notebook notebooks/
```

---

## 📈 Resultados

> *En construcción — se actualizará al completar el modelado.*

---

## 👥 Equipo

Proyecto académico · Minería de Datos · Facultad de Ingeniería UNAM

---

## 📄 Licencia

Uso académico. Los datos son ficticios y fueron proporcionados con fines educativos.
