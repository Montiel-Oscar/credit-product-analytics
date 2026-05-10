# Credit Product Analytics — Bank Credit Scoring

> **Minería de Datos** · Facultad de Ingeniería, UNAM  
> Área asignada: **Dirección de Productos de Crédito**

---

## Descripción

Proyecto final del curso de Minería de Datos que simula el trabajo de la Dirección de Productos de Crédito de un banco. El objetivo es analizar un portafolio de 4,349 solicitudes de crédito para identificar qué productos generan el mejor margen, perfilar al cliente ideal para cada uno y construir modelos predictivos que soporten una propuesta de negocio fundamentada en datos.

El proyecto forma parte de un ejercicio institucional donde 7 áreas del banco trabajan con la misma base de datos y coordinan estrategias para lograr objetivos organizacionales comunes.

---

## Hallazgo principal

| Producto | Línea promedio | Participación actual | Potencial |
|---|---|---|---|
| CREDITO_AUTO | $237,785 | 0.9% | Alto |
| TARJETA_ORO | $170,408 | 0.6% | Alto |
| CLASICA | $21,883 | 36.2% | Bajo |

**CREDITO_AUTO tiene una línea de crédito promedio 10x mayor que CLASICA.** Los productos de mayor margen representan menos del 2% del portafolio — la estrategia del área apunta a cambiar esa proporción.

---

## Resultados de los modelos

### M1 — Modelo de Aprobación (Random Forest)

| Métrica | Valor |
|---|---|
| Accuracy | 1.000 |
| F1 Macro | 1.000 |
| ROC-AUC | 1.000 |
| Kappa de Cohen | 1.000 |

> Las métricas perfectas son esperables en un dataset sintético con reglas deterministas. La validación cruzada de 5 folds confirma estabilidad (std=0.000), descartando sobreajuste. En datos reales se esperarían métricas entre 0.75 y 0.90.

### M2 — Modelo de Producto (Gradient Boosting + SMOTE)

| Métrica | Valor |
|---|---|
| F1 Macro | 0.874 |
| Kappa de Cohen | 0.885 |
| ROC-AUC | 0.997 |
| Accuracy | 0.991 |

> SMOTE aplicado al train (k=3) para compensar desbalance extremo: 96.1% CLASICA / 1.5% ORO / 2.4% AUTO.

---

## Estructura del repositorio

```
credit-product-analytics/
│
├── README.md
├── .gitignore
│
├── data/
│   ├── raw/                              # Datos originales — no modificar
│   │   ├── ProyectoMineriaBanco.csv      # 4,352 solicitudes, 27 variables
│   │   └── ProyectoMineri_acatalogo.xlsx # Diccionario + restricciones (2 hojas)
│   ├── processed/                        # Outputs de los notebooks
│   │   ├── banco_clean.csv               # Dataset limpio (4,349 × 28)
│   │   ├── banco_features.csv            # Dataset con 64 features (4,349 × 64)
│   │   ├── features_modelo_aprobacion.csv# Features M1 sin leakage (4,349 × 33)
│   │   ├── features_modelo_producto.csv  # Features M2 solo aprobados (1,637 × 40)
│   │   ├── predicciones_aprobacion.csv   # Dataset M1 + predicciones + probabilidades
│   │   └── predicciones_producto.csv     # Dataset M2 + predicciones + probabilidades
│   └── docs/
│       └── ProyectoMineri_aDatos.pdf     # Instrucciones del proyecto
│
├── notebooks/
│   ├── 01_exploratory_analysis.ipynb    # EDA: distribuciones, nulos, outliers, correlaciones
│   ├── 02_data_cleaning.ipynb           # Limpieza: 8 problemas resueltos, 2,654 correcciones
│   ├── 03_feature_engineering.ipynb     # Encoding, normalización, 36 nuevas variables
│   └── 04_modeling.ipynb                # Modelos ML, métricas, SMOTE, validación cruzada
│
├── models/
│   ├── modelo_aprobacion.pkl            # Random Forest M1
│   ├── modelo_producto.pkl              # Gradient Boosting M2
│   ├── scaler_standard.pkl              # StandardScaler (10 variables)
│   └── scaler_minmax.pkl                # MinMaxScaler (3 variables)
│
├── reports/
│   ├── Proyecto_ProductosCredito.docx   # Documento completo (5 secciones, 17 imágenes)
│   ├── Productos_Credito_Presentacion.pptx # Presentación 20 slides
│   └── figures/                         # Gráficas exportadas por los notebooks
│       ├── 01_*.png                     # EDA
│       ├── 02_*.png                     # Limpieza
│       ├── 03_*.png                     # Feature engineering
│       └── 04_*.png                     # Modelado
│
└── docs/                                # Dashboard y documentación adicional (en desarrollo)
```

---

## Pipeline completo

```
raw CSV (4,352 × 27)
    │
    ├── 01_EDA ──────────── Análisis exploratorio: nulos, outliers, correlaciones
    │
    ├── 02_Cleaning ─────── 8 problemas resueltos · banco_clean.csv (4,349 × 28)
    │
    ├── 03_Features ─────── 36 nuevas variables · banco_features.csv (4,349 × 64)
    │       ├── 2 targets definidos
    │       ├── 4 flags binarios
    │       ├── 5 ratios financieros
    │       ├── 5 encodings ordinales
    │       ├── 7 dummies OHE
    │       ├── 13 variables normalizadas
    │       └── 9 variables de leakage documentadas y excluidas de M1
    │
    └── 04_Modeling
            ├── M1: 4,349 registros · 3 algoritmos · Random Forest final
            └── M2: 1,637 registros · SMOTE · Gradient Boosting final
```

---

## Stack tecnológico

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.x-F7931E?logo=scikit-learn&logoColor=white)
![Imbalanced-learn](https://img.shields.io/badge/imbalanced--learn-SMOTE-orange)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.x-11557c)
![Seaborn](https://img.shields.io/badge/Seaborn-0.13-4C72B0)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)

---

## Cómo correr el proyecto

```bash
# 1. Clonar el repositorio
git clone https://github.com/tu-usuario/credit-product-analytics.git
cd credit-product-analytics

# 2. Crear entorno virtual
python -m venv venv
source venv/bin/activate        # Mac / Linux
venv\Scripts\activate           # Windows

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Correr los notebooks en orden
jupyter notebook notebooks/
```

### requirements.txt

```
pandas>=2.0
numpy>=1.24
scikit-learn>=1.3
imbalanced-learn>=0.11
matplotlib>=3.7
seaborn>=0.12
joblib>=1.3
openpyxl>=3.1
jupyter>=1.0
```

---

## Decisiones técnicas clave

**¿Por qué SMOTE en M2 y no en M1?**
M1 tiene desbalance moderado (62%/38%) — manejable con `class_weight='balanced'`. M2 tiene desbalance extremo (96%/2%/2%) donde `class_weight` no es suficiente para aprender las clases minoritarias.

**¿Por qué Gradient Boosting para M2 y Random Forest para M1?**
Gradient Boosting supera a Random Forest en F1 macro de M2 (0.874 vs 0.830), especialmente en TARJETA_ORO (4/5 correctas vs 3/5). Para M1 ambos dan resultados idénticos; se eligió Random Forest por sus feature importances directamente utilizables en la propuesta de negocio.

**¿Por qué las métricas de M1 son perfectas?**
El dataset es sintético — las reglas de aprobación fueron generadas directamente a partir de los scores del cliente. El modelo redescubre esa regla determinista. La validación cruzada 5-fold con std=0.000 confirma que es una propiedad del dato, no sobreajuste.

**¿Qué es data leakage y por qué importa?**
9 variables se excluyeron de M1 porque solo existen después de tomar la decisión de aprobación (`SALDO_CUENTA`, `CAPACIDAD_TC`, `MESES_VENCIDOS`, etc.). Incluirlas daría al modelo información del futuro durante el entrenamiento.

---

## Propuesta de negocio

1. **Pre-aprobación proactiva** — Implementar M1 en el CRM para identificar candidatos con probabilidad >80% y hacer oferta antes de que soliciten el crédito.

2. **Segmentación por producto** — Candidatos CLASICA (perfil estándar), ORO (score >220, ingreso >$25K), AUTO (ratio deuda/ingreso <0.3).

3. **Reducción del volumen PENDIENTE** — El 62.3% del portafolio no tiene producto asignado. M1 prioriza la revisión de los más probables de aprobar.

---

## Documentación

| Archivo | Descripción |
|---|---|
| `reports/Proyecto_ProductosCredito.docx` | Reporte completo: plan de trabajo, estrategia, análisis, modelos y conclusiones |
| `reports/Productos_Credito_Presentacion.pptx` | Presentación de 20 slides con gráficas de los notebooks integradas |
| `data/docs/ProyectoMineri_aDatos.pdf` | Instrucciones originales del proyecto |

---

## Equipo

Proyecto académico · Minería de Datos · Facultad de Ingeniería UNAM · 2025

---

## Licencia

Uso académico. Los datos son sintéticos y fueron proporcionados con fines educativos por la Facultad de Ingeniería de la UNAM.
