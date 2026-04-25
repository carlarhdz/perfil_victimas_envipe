# ¿Cambió el perfil del mexicano que es víctima de delito entre 2013–2019 y 2021–2025?

## Predicción de victimización antes y después del COVID-19 usando ENVIPE (2013–2025)

Proyecto de investigación desarrollado para **Tópicos de Políticas Públicas II / Seminario de Investigación**.

Este trabajo analiza si el shock generado por la pandemia de COVID-19 modificó de forma persistente el perfil sociodemográfico de las personas víctimas de delito en México, utilizando microdatos de la **ENVIPE (Encuesta Nacional de Victimización y Percepción sobre Seguridad Pública)** de **INEGI** para el periodo 2013–2025.

---

## Pregunta de investigación

**¿El shock por COVID-19 alteró de forma persistente el perfil sociodemográfico de las personas victimizadas en México, y qué implica ese cambio para la política pública de prevención del delito?**

### Subpreguntas

- ¿La caída en la tasa de victimización después de la pandemia fue uniforme entre tipos de delito?
- ¿Los mismos factores sociodemográficos siguen prediciendo quién es víctima hoy?
- ¿Los cambios observados son estadísticamente robustos?
- ¿Cómo cambió la relación entre nivel socioeconómico y probabilidad de victimización?

---

## Motivación

Entre 2013–2019 y 2021–2025, la tasa de victimización en México cayó aproximadamente **5 puntos porcentuales**, y no se ha recuperado.

Sin embargo, esta caída agregada puede ocultar dos fenómenos importantes:

### 1. Cambio en la composición del crimen

Algunos delitos disminuyeron considerablemente:

- robo en calle
- extorsión presencial
- robo en transporte

Mientras que otros aumentaron:

- fraude bancario
- fraude al consumidor
- hostigamiento sexual

### 2. Cambio en el perfil de riesgo

Si cambió el tipo de delito predominante, también cambió el perfil de las personas más expuestas.

Esto implica que un modelo entrenado con datos pre-pandemia podría estar mal calibrado para identificar riesgo actualmente.

---

## Fuente de datos

### ENVIPE 2013–2025 (INEGI)

- 13 años de microdatos
- población de 18 años y más
- unidad de análisis: persona-año
- tablas relacionales originales en DBF y CSV

### Definición de víctima

Se define como víctima a:

> Persona que aparece al menos una vez en `TMod_Vic`

Esto permite mantener comparabilidad longitudinal entre todos los años.

---

## Metodología

El proyecto combina:

- análisis descriptivo
- machine learning
- inferencia causal / estadística
- validación econométrica

### Modelos utilizados

- Logistic Regression
- Random Forest
- Gradient Boosting
- XGBoost

### Técnicas complementarias

- SMOTE para desbalance de clases
- AUC-ROC
- Average Precision (AP)
- SHAP values para interpretabilidad
- regresiones logísticas con interacciones
- comparación PRE vs POST pandemia

---

## Estructura del proyecto

### Sección 1 — Configuración del entorno

- instalación de librerías
- imports
- parámetros globales
- rutas y configuración por año

### Sección 2 — Construcción del dataset longitudinal

- lectura de DBF / CSV
- homologación de variables
- unión de tablas
- definición consistente de victimización

### Sección 3 — Evolución de la tasa de victimización

- cálculo directo desde microdatos
- tasas anuales
- tasas ponderadas (`FAC_ELE`)
- visualización temporal 2013–2025

### Sección 4 — Cambio en composición del crimen

- análisis por tipo de delito (`BPCOD`)
- comparación PRE vs POST
- delitos que cayeron vs delitos que aumentaron

### Sección 5+ (modelado)

- predicción de victimización
- comparación de desempeño pre y post pandemia
- interpretación de cambios estructurales

---

## Resultados esperados

El objetivo no es únicamente mostrar si bajó la victimización, sino responder:

> ¿Quién dejó de ser víctima y quién sigue siéndolo?

Esto permite generar mejores recomendaciones de política pública para prevención del delito, focalización territorial y asignación eficiente de recursos.

---

## Librerías principales

```python
pandas
numpy
matplotlib
seaborn
scikit-learn
xgboost
shap
imbalanced-learn
statsmodels
simpledbf
dbfread
```

## Cómo correr el proyecto
### Clonar repositorio
```
git clone git@github.com:carlarhdz/perfil_victimas_envipe.git
```

### Instalar librerías principales

### Ajustar ruta local
Modificar
```
BASE_PATH = 'tu_ruta_local/'
```
