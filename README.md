# Laboratorio Dry Bean ML

Proyecto académico de Machine Learning desarrollado como simulación de un proyecto profesional de Ciencia de Datos e IA. El objetivo es **clasificar 7 variedades de frijol seco** a partir de 16 features morfológicos extraídos de imágenes, aplicando metodologías profesionales de trabajo en equipo (**CRISP-DM + TDSP + Scrum ML**) y flujo colaborativo con Git/GitHub.

> Universidad Autónoma de Occidente — Gestión de IA y Ciencia de Datos

---

## Tabla de contenido

1. [Descripción del problema](#1-descripción-del-problema)
2. [Metodología](#2-metodología)
3. [Equipo y roles](#3-equipo-y-roles)
4. [Estructura del proyecto (TDSP)](#4-estructura-del-proyecto-tdsp)
5. [Dataset](#5-dataset)
6. [Cómo ejecutar el proyecto](#6-cómo-ejecutar-el-proyecto)
7. [Desarrollo por sprints](#7-desarrollo-por-sprints)
8. [Resultados](#8-resultados)
9. [Flujo de trabajo con GitHub](#9-flujo-de-trabajo-con-github)
10. [Definition of Done](#10-definition-of-done)

---

## 1. Descripción del problema

El **Dry Bean Dataset** contiene 13.611 muestras de granos de frijol pertenecientes a 7 variedades distintas (*Barbunya, Bombay, Cali, Dermason, Horoz, Seker, Sira*). Cada muestra está descrita por 16 atributos morfológicos (área, perímetro, ejes, excentricidad, factores de forma, etc.) calculados a partir de imágenes capturadas por un sistema de visión por computadora.

El objetivo del laboratorio es construir un modelo que, dadas las características morfológicas de un grano, **prediga su variedad** con alta precisión y permita comparar el desempeño de un modelo lineal (baseline) frente a un modelo no lineal (alternativo).

---

## 2. Metodología

El proyecto integra tres marcos de trabajo complementarios:

| Marco | Aporte al proyecto |
|-------|--------------------|
| **CRISP-DM** | Define las fases del ciclo de vida de Data Mining: comprensión del negocio, comprensión de los datos, preparación, modelado, evaluación y despliegue. |
| **TDSP** (Microsoft) | Aporta la **estructura estandarizada de carpetas** del repositorio y separa claramente datos crudos, procesados, notebooks, código fuente y entregables. |
| **Scrum ML** | Organiza el trabajo en **sprints incrementales** con roles definidos, Product Backlog, Daily Scrum y Retrospectivas. |

---

## 3. Equipo y roles

El equipo está conformado por **5 integrantes**. A diferencia del plan original que combina Data Engineer y Data Analyst, en nuestro equipo separamos ambos roles para distribuir mejor las responsabilidades de ingeniería de datos y análisis exploratorio.

| Rol | Integrante | Responsabilidades principales |
|-----|------------|-------------------------------|
| **Product Owner** | Juan Manuel Cajigas Eraso | Define los objetivos del proyecto, prioriza el Product Backlog y valida los entregables finales. |
| **Scrum Master** | Lady Johana Lara Aldana | Coordina las reuniones, mantiene el tablero Scrum y asegura el cumplimiento de los sprints. |
| **Data Engineer** | Jonathan Giraldo Diaz | Ingestión del dataset desde Kaggle, configuración del entorno y generación del dataset procesado. |
| **Data Analyst** | Eliphas Levi Arias Abrahan | Análisis exploratorio (EDA), análisis de calidad de datos y visualizaciones por clase. |
| **ML Engineer** | Jhon Stiven Loaiza Rodrigez | Entrenamiento, evaluación y comparación de modelos; serialización y feature importance. |

---

## 4. Estructura del proyecto (TDSP)

```
laboratorio_drybean_ml/
│
├── data/
│   ├── raw/                  # Dataset original descargado de Kaggle
│   │   └── DryBeanDataset/
│   │       ├── Dry_Bean_Dataset.arff
│   │       ├── Dry_Bean_Dataset.txt
│   │       └── Dry_Bean_Dataset.xlsx
│   └── processed/            # Dataset limpio listo para modelar
│       └── dry_beans_clean.csv
│
├── notebooks/
│   ├── Ingestion.ipynb       # Descarga y limpieza inicial del dataset
│   ├── EDA.ipynb             # Análisis exploratorio
│   └── Training.ipynb        # Entrenamiento, evaluación y guardado de modelos
│
├── outputs/
│   └── models/
│       └── reports/
│           ├── baseline_model.joblib       # Logistic Regression entrenada
│           └── random_forest_model.joblib  # Random Forest entrenado
│
├── src/                      # Código fuente reutilizable
├── requirements.txt          # Dependencias del proyecto
├── README.md                 # Documentación principal
└── .gitignore
```

---

## 5. Dataset

| Atributo | Valor |
|---------|-------|
| **Fuente** | [Kaggle — Dry Beans (joebeachcapital)](https://www.kaggle.com/datasets/joebeachcapital/dry-beans) |
| **Licencia** | CC BY 4.0 |
| **Registros** | 13.611 |
| **Features** | 16 numéricos (12 dimensiones + 4 factores de forma) |
| **Variable objetivo** | `Class` — variedad de frijol (7 clases) |
| **Clases** | BARBUNYA, BOMBAY, CALI, DERMASON, HOROZ, SEKER, SIRA |
| **Valores nulos** | 0 |
| **Duplicados removidos** | sí (en la fase de ingestión) |

### Features principales

`Area`, `Perimeter`, `MajorAxisLength`, `MinorAxisLength`, `AspectRation`, `Eccentricity`, `ConvexArea`, `EquivDiameter`, `Extent`, `Solidity`, `roundness`, `Compactness`, `ShapeFactor1`, `ShapeFactor2`, `ShapeFactor3`, `ShapeFactor4`.

---

## 6. Cómo ejecutar el proyecto

### Requisitos previos

- Python 3.10+
- Cuenta de Kaggle con un archivo `kaggle.json` válido (token de API).

### Pasos

1. **Clonar el repositorio**
   ```bash
   git clone https://github.com/jmcajigas/Laboratorio-Dry-Bean-ML.git
   cd Laboratorio-Dry-Bean-ML
   ```

2. **Configurar credenciales de Kaggle**
   Colocar el archivo `kaggle.json` en la raíz del proyecto (ya está contemplado en el `.gitignore` para no subirlo al repositorio).

3. **Instalar dependencias**
   ```bash
   pip install -r requirements.txt
   ```

4. **Ejecutar los notebooks en orden**
   1. [notebooks/Ingestion.ipynb](notebooks/Ingestion.ipynb) — descarga y limpia el dataset.
   2. [notebooks/EDA.ipynb](notebooks/EDA.ipynb) — análisis exploratorio.
   3. [notebooks/Training.ipynb](notebooks/Training.ipynb) — entrenamiento y evaluación.

---

## 7. Desarrollo por sprints

### Sprint 1 — Comprensión y Preparación

**Responsables principales:** Data Engineer, Product Owner, Scrum Master.

**Tareas realizadas:**
- Creación del repositorio en GitHub e inicialización con la estructura TDSP.
- Configuración del entorno y del token de Kaggle (`kaggle.json`).
- Descarga del Dry Bean Dataset mediante la API de Kaggle.
- Inspección inicial: tipos de datos, valores nulos y duplicados.
- Eliminación de duplicados y exportación a `data/processed/dry_beans_clean.csv`.

**Entregables:**
- [notebooks/Ingestion.ipynb](notebooks/Ingestion.ipynb)
- [data/processed/dry_beans_clean.csv](data/processed/dry_beans_clean.csv)
- Repositorio configurado con la estructura TDSP.

---

### Sprint 2 — Análisis Exploratorio y Modelado

**Responsables principales:** Data Analyst, ML Engineer.

**Tareas realizadas (EDA):**
- Análisis de la **distribución de clases** (dataset desbalanceado, con BOMBAY como clase minoritaria).
- Histogramas y boxplots de las 16 features numéricas.
- **Matriz de correlación** entre features.
- Boxplots y pairplots por clase para identificar features discriminantes.

**Tareas realizadas (Modelado):**
- División *train/test* 80/20 estratificada por clase (`random_state=42`).
- Entrenamiento del **modelo baseline**: `LogisticRegression` con `StandardScaler` dentro de un `Pipeline` de scikit-learn.
- Entrenamiento del **modelo alternativo**: `RandomForestClassifier` (`n_estimators=200`, `class_weight="balanced"`).
- Evaluación con **Accuracy** y **F1 macro**.
- **Matrices de confusión** para ambos modelos.
- Comparación de **importancia de features** entre ambos modelos.
- Serialización de los modelos entrenados con `joblib`.

**Entregables:**
- [notebooks/EDA.ipynb](notebooks/EDA.ipynb)
- [notebooks/Training.ipynb](notebooks/Training.ipynb)
- [outputs/models/reports/baseline_model.joblib](outputs/models/reports/baseline_model.joblib)
- [outputs/models/reports/random_forest_model.joblib](outputs/models/reports/random_forest_model.joblib)

---

## 8. Resultados

### Comparación de modelos

| Modelo | Accuracy | F1 macro |
|--------|----------|----------|
| **Logistic Regression** (baseline) | 0.9192 | 0.9302 |
| **Random Forest** (alternativo)    | 0.9192 | 0.9303 |

### Reporte por clase — Logistic Regression

| Clase     | Precision | Recall | F1-score | Support |
|-----------|-----------|--------|----------|---------|
| BARBUNYA  | 0.93 | 0.89 | 0.91 | 265 |
| BOMBAY    | 1.00 | 1.00 | 1.00 | 104 |
| CALI      | 0.91 | 0.94 | 0.93 | 326 |
| DERMASON  | 0.93 | 0.91 | 0.92 | 709 |
| HOROZ     | 0.96 | 0.94 | 0.95 | 372 |
| SEKER     | 0.93 | 0.94 | 0.94 | 406 |
| SIRA      | 0.86 | 0.88 | 0.87 | 527 |

### Reporte por clase — Random Forest

| Clase     | Precision | Recall | F1-score | Support |
|-----------|-----------|--------|----------|---------|
| BARBUNYA  | 0.92 | 0.89 | 0.90 | 265 |
| BOMBAY    | 1.00 | 1.00 | 1.00 | 104 |
| CALI      | 0.92 | 0.94 | 0.93 | 326 |
| DERMASON  | 0.91 | 0.92 | 0.92 | 709 |
| HOROZ     | 0.96 | 0.95 | 0.95 | 372 |
| SEKER     | 0.95 | 0.95 | 0.95 | 406 |
| SIRA      | 0.87 | 0.86 | 0.86 | 527 |

### Conclusiones parciales

- Ambos modelos alcanzan un desempeño muy similar (~92% accuracy, ~93% F1 macro), lo que sugiere que las features están bien separadas linealmente para la mayoría de clases.
- La clase **BOMBAY** se clasifica perfectamente (F1 = 1.00) gracias a su tamaño claramente distinto al de las demás variedades.
- Las clases **SIRA** y **DERMASON** son las más difíciles de separar entre sí, lo cual coincide con su cercanía morfológica observada en el EDA.

---

## 9. Flujo de trabajo con GitHub

El equipo siguió el flujo de trabajo propuesto en la guía:

1. Creación del repositorio remoto en GitHub.
2. Inicialización local con `git init` y subida con `git push`.
3. Cada integrante clona el repositorio y trabaja en su propia rama `feature/<nombre>`.
4. Los cambios se integran a `main` mediante **Pull Requests** revisados por el equipo.

**Comandos más utilizados:**

```bash
git clone <url>
git checkout -b feature/<nombre-rama>
git add .
git commit -m "mensaje descriptivo"
git push origin feature/<nombre-rama>
git pull origin main
```

---

## 10. Definition of Done

Criterios de aceptación cumplidos hasta el momento:

- [x] El notebook de ingestión corre sin errores y descarga el dataset desde Kaggle.
- [x] El dataset se limpia y se guarda en `data/processed/`.
- [x] Se realiza un análisis exploratorio (EDA) completo.
- [x] Se entrena un **modelo baseline** (Logistic Regression).
- [x] Se entrena un **modelo alternativo** (Random Forest).
- [x] Se comparan métricas **Accuracy** y **F1 macro**.
- [x] Se incluyen **matrices de confusión** para ambos modelos.
- [x] Los modelos entrenados se serializan en formato `.joblib`.
- [x] El proyecto sigue la estructura TDSP y es reproducible.