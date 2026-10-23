# Predicción de la Severidad de Accidentes de Tránsito — Short-Paper (versión final)

**Curso:** Machine Learning Applied — Ingeniería de Sistemas, Universidad EAFIT

**Autores:** Jose Muñoz Ríos, Santiago Álvarez Peña

Clasificación supervisada de la severidad de accidentes de tránsito (leve, grave o fatal) con el *Road Traffic Accident Dataset of Addis Ababa City* (12,316 registros, 2017–2020; [doi:10.17632/xytv86278f.1](https://doi.org/10.17632/xytv86278f.1)). El conjunto está fuertemente desbalanceado (84.6% leves, 14.2% graves, 1.3% fatales), así que el trabajo compara estrategias frente al desbalance, con particiones por siniestro para evitar fuga de información.

## Contenido

| Archivo | Qué es |
|---|---|
| `ShortPaper_Final_Accidentes_Transito.pdf` / `.docx` | Paper final (formato IEEE). |
| `data_s5_eda.ipynb` | Análisis exploratorio y limpieza; genera `cleaned.csv` y la Fig. 1 del paper. |
| `modelado.ipynb` | Comparación de estrategias frente al desbalance; genera las Tablas III y IV y la Fig. 2. |
| `RTA_Dataset.csv` | Datos originales. |
| `cleaned.csv` | Datos depurados (22 predictoras + `Accident_severity`). |
| `resultados/` | Tablas que genera `modelado.ipynb` y de las que salen las cifras del paper. |
| `figuras/` | Figuras que generan los notebooks. |

## Resultados

F1-macro en validación cruzada (5 folds por grupos de siniestro):

| Estrategia | Random Forest | Gradient Boosting | AdaBoost |
|---|---|---|---|
| Sin tratamiento (línea base) | 0.305 | 0.329 | 0.324 |
| Pesos por clase | **0.385** | 0.367 | 0.348 |
| SMOTENC | 0.357 | 0.351 | 0.357 |
| SMOTEN | 0.338 | 0.350 | 0.356 |

En prueba, el mejor modelo (Random Forest con pesos por clase) obtiene un F1-macro de 0.37 frente a 0.33 de la línea base, y detecta el 28% de los casos graves, pero ningún caso fatal. Todas las estrategias llegan a un techo similar, lo que indica que el límite está en la información de las variables más que en la técnica de balanceo.

## Cómo ejecutar

```bash
pip install pandas numpy matplotlib scipy scikit-learn imbalanced-learn jupyter
```

1. `data_s5_eda.ipynb` (menos de 1 minuto).
2. `modelado.ipynb` (alrededor de 1 hora).
