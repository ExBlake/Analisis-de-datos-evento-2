# Análisis de Datos — Evento Evaluativo 2

**Instituto Tecnológico Metropolitano (ITM)**

Departamento de Sistemas · Ingeniería de Sistemas

Curso: Análisis de Datos · Docente: Daniel Alexis Nieto Mora · Semestre 2026-2

## Integrantes y participación

| Integrante | Commits principales asignados | Autor registrado en Git |
|---|---|---|
| Julián | 1, 5, 9 | Julián Zapata |
| Santiago | 2, 6, 10 | ExBlake |
| Oscar Alexis | 3, 7, 11 | Oscar Alexis Pineda Henao |
| Jacobo | 4, 8, 12 | JCobz0714 |

El historial local contiene aportes de los cuatro integrantes. El seguimiento se encuentra en [TASKS.md](TASKS.md); el commit 12 reúne la documentación y revisión final y debe registrarlo Jacobo desde su cuenta.

## Objetivo y contexto

Aplicar la metodología del segundo evento evaluativo de Análisis de Datos: comparar tres bases candidatas, justificar una selección, realizar un EDA con hipótesis exploratorias y preparar los datos para escalado y reducción de dimensionalidad mediante PCA. Los resultados describen esta muestra y no constituyen diagnósticos médicos ni relaciones causales.

## Datasets explorados y selección

| Dataset | Datos evaluados | Fortalezas y límites identificados |
|---|---|---|
| HCV Data | CSV local: 615 registros, 14 columnas incluido ID; 10 pruebas de laboratorio, edad, sexo y diagnóstico | Documentación clara, tamaño manejable y medidas continuas. Tiene faltantes y desbalance diagnóstico. |
| Absenteeism at Work | CSV local: 740 registros, 21 columnas; componente temporal de ausentismo | Sin faltantes, pero 34 filas repetidas y códigos que requieren interpretación. Solo representa 36 empleados; observaciones repetidas no son independientes. |
| Ajwa or Medjool | Comparación documental de imágenes y características de dátiles; no descargado | Modalidades tabular y visual, pero 200 imágenes corresponden a 20 frutos y la descarga es menos manejable. |

Se seleccionó **HCV Data** por su documentación, relevancia, manejabilidad y variables apropiadas para EDA, imputación, correlaciones y PCA. El Notebook 01 documenta nueve criterios y una valoración del equipo: HCV obtuvo 43/45, ausentismo 35/45 y Ajwa or Medjool 27/45. Son puntuaciones justificadas por el equipo, no un indicador externo de calidad.

Las fuentes y enlaces de origen se encuentran en el Notebook 01. HCV y ausentismo se analizan desde archivos locales; Ajwa or Medjool se compara a partir de la investigación documental previa.

## Estructura del repositorio

```text
Analisis-de-datos-evento-2/
├── README.md
├── TASKS.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── raw/
│   │   ├── hcvdat0.csv
│   │   └── Absenteeism_at_work.csv
│   └── processed/
│       └── hcv_processed.csv
├── notebooks/
│   ├── 01_exploracion_datasets.ipynb
│   ├── 02_eda_hcv.ipynb
│   └── 03_preprocesamiento_reduccion.ipynb
└── images/
    ├── comparacion_datasets.png
    ├── faltantes_por_variable.png
    ├── atipicos_por_grupo.png
    └── pca_pc1_pc2.png
```

Los datos originales se conservan. El Notebook 03 genera el CSV procesado; las figuras exportadas permiten revisar y presentar el trabajo.

## Tecnologías e instalación

Python, pandas, NumPy, Matplotlib, seaborn, SciPy, scikit-learn, IPython y Jupyter. Se recomienda Python 3.13 para reproducir el entorno indicado en los metadatos de los notebooks. Las dependencias no están fijadas a versiones exactas.

```bash
git clone https://github.com/ExBlake/Analisis-de-datos-evento-2.git
cd Analisis-de-datos-evento-2
python -m venv .venv
```

Activar el entorno según el sistema:

```powershell
# Windows PowerShell
.\.venv\Scripts\Activate.ps1
```

```bash
# Linux / macOS
source .venv/bin/activate
```

Instalar las dependencias y abrir Jupyter:

```bash
python -m pip install -r requirements.txt
python -m jupyter notebook
```

## Ejecución y metodología

Abrir y ejecutar los notebooks en orden **01 → 02 → 03**, cada uno con su kernel trabajando desde la carpeta `notebooks/`. Usar “Restart Kernel and Run All Cells” para evitar depender de variables de sesiones anteriores. Las rutas de los notebooks 01 y 02, y algunas figuras del 03, están basadas en `../data/` y `../images/`; ejecutar esas celdas desde la raíz con otro método exige ajustar el directorio de trabajo.

1. **Notebook 01:** investigación, calidad inicial, tabla comparativa y selección de HCV.
2. **Notebook 02:** estructura y clasificación de variables; faltantes, duplicados y formatos; estadística descriptiva, distribuciones y atípicos; análisis bivariado y multivariado con Pearson y Spearman; cuatro hipótesis e insights.
3. **Notebook 03:** retirada del ID, revisión de duplicados, imputación, indicador de faltante, transformaciones logarítmicas y One-Hot Encoding; exportación del CSV; StandardScaler y PCA sobre 11 variables cuantitativas.

Las columnas `Category_*` del CSV procesado son etiquetas y no deben incluirse como predictores del diagnóstico. El archivo se guarda antes del escalado: no contiene variables estandarizadas ni puntuaciones PCA.

## Principales resultados

- **Desbalance:** 533 de los 615 registros son donantes (86.67%); hay 75 pacientes y 7 donantes sospechosos.
- **Faltantes:** 31 celdas ausentes en 26 filas. `ALP` concentra 18 y `CHOL` 10; en fibrosis faltan 9 de las 21 mediciones de ALP. No se detectaron duplicados clínicos.
- **Atípicos:** IQR identificó 65 en GGT y 64 en AST; 51 de los atípicos de AST pertenecen a pacientes. Se conservaron los extremos por su posible significado clínico.
- **Relaciones descritas:** ALB–PROT y AST–GGT presentan asociaciones positivas moderadas. ALT–AST resulta más marcada con Spearman que con Pearson, en concordancia con el sesgo observado. Las celdas correspondientes deben ejecutarse para regenerar sus salidas.
- **Hipótesis implementadas:** Welch para log(AST), Welch para ALB con sensibilidad al posible error, chi-cuadrado sexo–grupo clínico y prueba de correlación ALB–PROT. Las interpretaciones previas reportan tres rechazos de H0 y ausencia de rechazo para sexo, pero las celdas de contraste no tienen resultados guardados; se requiere verificar sus p-valores antes de presentar esas decisiones como resultados finales reproducidos.
- **Preprocesamiento guardado:** 615 filas y 19 columnas numéricas sin faltantes, con seis marcadores transformados mediante log1p.
- **PCA guardado:** PC1 explica 21.23% y PC2 18.46%; juntas, 39.69%. Siete componentes conservan 83.95% y nueve 93.41% de la varianza de las entradas estandarizadas.

![Varianza y perfiles proyectados en las dos primeras componentes](images/pca_pc1_pc2.png)

La proyección muestra separación parcial de cirrosis y sospechosos respecto a donantes, con superposición entre clases. La varianza retenida no equivale a exactitud de clasificación.

## Conclusiones y límites

HCV permitió integrar calidad, estadística exploratoria, relaciones entre variables y reducción dimensional. El desbalance, los faltantes concentrados y las colas largas justifican decisiones contextualizadas, en lugar de eliminar automáticamente registros. PCA ofrece una vista de perfiles multivariados, pero dos componentes dejan fuera 60.31% de la varianza; para modelar se debe comparar la representación completa con otras cantidades de componentes mediante validación.

La revisión final identificó dos pendientes analíticos:

- El EDA señala `ALB = 82.2` del registro 217 como posible error porque supera `PROT = 67.4`. El preprocesamiento actual conserva ese valor. Las cifras de PCA describen esa versión; una corrección exige recalcular los resultados.
- La imputación por categoría utiliza el diagnóstico y se ajusta sobre toda la base. Aunque PCA excluye las columnas diagnósticas, sus entradas imputadas dependen de ellas. Para predecir un diagnóstico desconocido se necesita imputación sin esa etiqueta y separar entrenamiento y prueba antes de ajustar imputación, escalado y PCA.

Las cuatro pruebas son exploratorias, sin ajuste por comparaciones múltiples. No rechazar una asociación sexo–diagnóstico no demuestra independencia ni descarta confusión.

## Estado de revisión y entregables

Se revisaron las rutas referidas, las dependencias importadas, el historial de autores, los títulos y etiquetas definidos en el código y las salidas existentes. No hay errores guardados, pero existen celdas sin ejecutar en el Notebook 02. **No se ejecutaron los notebooks ni pruebas durante el cierre**, conforme a la indicación del usuario; la ejecución de principio a fin y la inspección de figuras regeneradas quedan pendientes. El commit 12 permanece pendiente de esa validación.

Entregables: los tres notebooks, datos originales y procesados, figuras, documentación y video explicativo de máximo 8 minutos.
