# ¿Cambió el perfil del mexicano víctima de delito tras la pandemia?

**Predicción de victimización antes y después del COVID-19 — ENVIPE 2013–2025**

> Proyecto final · Tópicos de Políticas Públicas II / Seminario de Investigación · ITAM · Primavera 2026

---

## Pregunta de investigación

¿El shock por COVID-19 alteró de forma persistente el perfil sociodemográfico de las personas victimizadas en México, y qué implica ese cambio para la política pública de prevención del delito?

## Motivación

La tasa de victimización en México cayó ~5 puntos porcentuales entre 2013–2019 y 2021–2025 según ENVIPE. La narrativa dominante interpreta esta caída como mejora en seguridad pública, pero esa lectura agregada oculta dos fenómenos: (1) algunos delitos cayeron drásticamente mientras otros aumentaron, y (2) si el tipo de delito que predomina cambió, las personas expuestas también cambiaron. Un modelo de riesgo entrenado pre-pandemia puede estar mal calibrado hoy.

## Datos

- **Fuente:** Microdatos de la Encuesta Nacional de Victimización y Percepción sobre Seguridad Pública (ENVIPE), INEGI.
- **Cobertura:** 13 ediciones (2013–2025), ~80,000+ observaciones por año.
- **Unidad de análisis:** Personas de 18 años y más.
- **Períodos:**
  - PRE-pandemia: 2013–2019 (modelos)
  - Pandemia: 2020 (excluido de modelos, incluido en descriptivas)
  - POST-pandemia: 2021–2025 (modelos)
- **Variable dependiente:** Victimización binaria (persona aparece en módulo de delitos `TMod_Vic`).

## Metodología

| Componente | Método |
|---|---|
| Análisis descriptivo | Tasas de victimización por año, tipo de delito (15 categorías BPCOD), y subgrupo sociodemográfico |
| Modelos predictivos | Logistic Regression, Random Forest, Gradient Boosting, XGBoost — pipeline con imputación mediana + SMOTE + estandarización |
| Comparación formal | Regresión logística pooled con interacciones X × POST (test de cambio estructural) |
| Interpretabilidad | SHAP values para dirección y magnitud de efectos, dependence plots por NSE |
| Robustez | Threshold tuning (F1), cross-period validation, robustness check excluyendo 2021 |

## Estructura del repositorio

```
├── proyecto_victimizacion_pandemia_vfinal.ipynb   # Notebook principal
├── README.md
└── figuras/                                        # Generadas al correr el notebook
    ├── fig01_tasa_nacional.png
    ├── fig02_series_por_delito.png
    ├── fig03_perfil_descriptivo.png
    ├── fig04_roc.png
    ├── fig05_importancia_pre_post.png
    ├── fig06_interacciones.png
    ├── fig07_cambio_subgrupos.png
    ├── fig08_perfiles_riesgo.png
    ├── fig09_resumen.png
    ├── fig_shap_pre_post.png
    ├── fig_shap_estrato.png
    └── fig_prob_nse.png
```

## Hallazgos principales

**1. Caída heterogénea por tipo de delito.**
La tasa agregada cayó, pero los delitos no cayeron por igual. Robos patrimoniales y extorsión presencial: −20% a −40%. Fraudes digitales y hostigamiento sexual: +50% a +130%. La pandemia no redujo "el crimen": cambió su composición.

**2. El perfil predictivo cambió entre períodos.**
Las variables que más predicen victimización se reordenaron. El análisis SHAP muestra que la dirección del efecto del nivel socioeconómico y las conductas preventivas se modificó entre PRE y POST.

**3. Cambios estadísticamente significativos.**
La regresión logística con interacciones X × POST confirma que varias variables cambiaron su efecto de forma significativa (p < 0.05). Este resultado es robusto a la exclusión de 2021.

**4. Implicaciones para la focalización.**
Los programas de prevención diseñados bajo el perfil pre-2020 generan dos tipos de error: atender población cuyo riesgo bajó y no atender población cuyo riesgo subió.

## Requisitos

```
python >= 3.8
pandas
numpy
matplotlib
seaborn
scikit-learn
imbalanced-learn
xgboost
shap
statsmodels
simpledbf
dbfread
```

Instalar con:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn xgboost shap statsmodels simpledbf dbfread
```

## Cómo reproducir

1. Descargar los microdatos de ENVIPE 2013–2025 desde [INEGI Datos Abiertos](https://www.inegi.org.mx/programas/envipe/).
2. Ajustar la variable `BASE_PATH` en la celda 1.3 del notebook a la ruta donde se ubican las carpetas de cada año.
3. Ejecutar todas las celdas en orden (`Run All`). La carga de 13 años tarda ~10–15 minutos dependiendo del hardware.

## Marco teórico

El análisis se enmarca en la **teoría de actividades rutinarias** (Cohen & Felson, 1979): la pandemia alteró las rutinas cotidianas, reduciendo la convergencia espacio-temporal entre ofensores y víctimas para delitos predatorios, pero incrementando la exposición digital para fraudes y delitos en línea. Nuestros resultados son consistentes con la literatura internacional (Felson et al., 2020; Naylor et al., 2022; Buil-Gil & Zeng, 2022).

## Limitaciones

- No hay identificación causal; los modelos son predictivos.
- Factores de expansión no usados en modelos predictivos (sí en descriptivas).
- Los aumentos en delitos sexuales y fraudes combinan cambio real y cambio en disposición a reportar.
- Análisis nacional; no hay desagregación geográfica por entidad federativa.

## Referencias

- Cohen, L. & Felson, M. (1979). Social change and crime rate trends: a routine activity approach. *American Sociological Review*, 44(4), 588–608.
- Felson, M. et al. (2020). Routine activity effects of the Covid-19 pandemic on burglary in Detroit. *Crime Science*, 9(10).
- Naylor, J. et al. (2022). The effect of COVID-19 restrictions on routine activities and online crime. *Journal of Quantitative Criminology*, 39.
- Buil-Gil, D. & Zeng, Y. (2022). Meeting you was a fake: investigating the increase in romance fraud during COVID-19. *Journal of Financial Crime*, 29(2).
- Chen, P. et al. (2022). Interpretable machine learning models for crime prediction. *Computers, Environment and Urban Systems*, 94.
- México Evalúa (2017). Prevención del delito en México: ¿Cómo se implementa?
- INEGI (2013–2025). ENVIPE: microdatos. www.inegi.org.mx

---

*Nota: No afirmamos que la pandemia causó los cambios. Entre 2019 y 2025 ocurrieron múltiples shocks concurrentes. Documentamos que el patrón cambió; la identificación causal queda fuera del alcance.*
