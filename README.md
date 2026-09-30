# Análisis de Datos — Evento Evaluativo 2

**Instituto Tecnológico Metropolitano (ITM)**
Departamento de Sistemas · Ingeniería de Sistemas
Curso: Análisis de Datos · Docente: Daniel Alexis Nieto Mora · Semestre 2026-2

## Integrantes

- Julián
- Santiago
- Oscar Alexis
- Jacobo

## Descripción

Proyecto práctico que aplica lo visto en las primeras semanas del curso: explorar
varias bases de datos, justificar la elección de una de ellas, realizar un análisis
exploratorio completo (EDA) y aplicar técnicas de preprocesamiento y reducción de
dimensionalidad. La participación de cada integrante queda registrada mediante sus
commits en este repositorio.

## Fases del proyecto

1. **Exploración de bases de datos** — al menos 3 bases de datos de al menos 2 tipos
   diferentes, documentando fuente y tipo (primaria, secundaria o terciaria),
   características básicas, nivel de documentación y posibles aplicaciones. La base
   final se selecciona según completitud, relevancia, documentación y manejabilidad.
2. **Análisis Exploratorio de Datos (EDA)** — valores faltantes, valores atípicos,
   distribuciones, análisis univariado y multivariado, relaciones entre variables,
   hipótesis iniciales, visualizaciones clave e insights principales.
3. **Preprocesamiento y reducción** — codificación de variables categóricas, escalado
   o normalización de variables numéricas y reducción de dimensionalidad (PCA) con
   visualización de resultados.

## Estructura del repositorio

```text
analisis-datos-evento-2/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── raw/          # datos originales, sin modificar
│   └── processed/    # datos resultantes del preprocesamiento
├── notebooks/
│   ├── 01_exploracion_datasets.ipynb       # Fase 1
│   ├── 02_eda_hcv.ipynb                    # Fase 2
│   └── 03_preprocesamiento_reduccion.ipynb # Fase 3
└── images/           # gráficas exportadas para el README y el video
```

## Instalación

Requiere Python 3.8 o superior.

```bash
git clone <url-del-repositorio>
cd analisis-datos-evento-2
python -m venv venv
# Windows
venv\Scripts\activate
# Linux / macOS
source venv/bin/activate
pip install -r requirements.txt
```

## Ejecución

```bash
jupyter notebook
```

Abrir los notebooks de la carpeta `notebooks/` en orden (01 → 02 → 03). Los notebooks
leen los datos mediante rutas relativas a la carpeta `data/`.

## Entregables

- Repositorio en GitHub con los notebooks organizados por módulos, este README y los
  commits de cada integrante.
- Video explicativo de máximo 8 minutos.
