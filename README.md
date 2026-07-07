# Clustering de perfiles sensoriales de café arábica

Proyecto final del módulo **Aprendizaje No Supervisado**. El objetivo es identificar perfiles sensoriales naturales en cafés arábica mediante técnicas de clustering y comparar su comportamiento cuantitativo e interpretativo.

## Dataset

Se utiliza el conjunto público **Arabica Coffee Quality Data**, perteneciente al repositorio Coffee Quality Database:

- Repositorio: https://github.com/jldbc/coffee-quality-database
- Archivo utilizado: `data/arabica_data_cleaned.csv`

El notebook descarga automáticamente el dataset cuando el archivo no se encuentra de forma local.

## Variables analizadas

Las variables utilizadas para formar los clústeres son:

- Aroma
- Flavor
- Aftertaste
- Acidity
- Body
- Balance

`Uniformity`, `Clean.Cup` y `Sweetness` se reservan para interpretación debido a su fuerte efecto techo. `Total.Cup.Points` se utiliza como validación contextual y no como entrada del clustering.

## Metodología

El proyecto incluye:

1. Análisis de calidad de datos, faltantes, duplicados y valores atípicos.
2. Estadísticas descriptivas, distribuciones y correlaciones.
3. Estandarización con `StandardScaler`.
4. Optimización de hiperparámetros para:
   - Gaussian Mixture Models (GMM)
   - Clustering jerárquico aglomerativo
   - Clustering espectral
5. Evaluación mediante:
   - Silhouette
   - Calinski-Harabasz
   - Davies-Bouldin
   - Adjusted Rand Index
   - Normalized Mutual Information
6. Visualización con PCA e Isomap.
7. Interpretación sensorial y análisis descriptivo por país.

## Resultados principales

El clustering jerárquico con enlace de Ward produjo el mejor equilibrio global entre cohesión y separación. El clustering espectral obtuvo resultados próximos y presentó la mayor concordancia con la partición jerárquica. GMM mostró una separación menos favorable, pero permitió analizar probabilidades de pertenencia e identificar observaciones ambiguas.

| Método | Silhouette | Calinski-Harabasz | Davies-Bouldin |
|---|---:|---:|---:|
| Jerárquico | 0.389 | 580.928 | 0.958 |
| Espectral | 0.365 | 626.934 | 0.989 |
| GMM | 0.354 | 78.909 | 3.142 |

Los resultados sugieren dos perfiles principales: un grupo con puntuaciones sensoriales globalmente más altas y otro con valores medios menores y mayor heterogeneidad. Estos grupos se interpretan como una segmentación exploratoria, no como categorías oficiales de calidad.

## Estructura del repositorio

```text
.
├── notebooks/
│   └── Clustering_CQI_NuviaM.ipynb
├── results/
│   ├── metrics_comparison.csv
│   ├── cluster_agreement.csv
│   ├── gmm_tuning_results.csv
│   ├── agglomerative_tuning_results.csv
│   ├── spectral_tuning_results.csv
│   └── coffee_clusters_results.csv
├── report/
│   └── README.md
├── presentation/
│   └── README.md
├── requirements.txt
├── .gitignore
└── README.md
```

## Ejecución

### Opción 1: Google Colab

1. Abrir `notebooks/Clustering_CQI.ipynb` en Google Colab.
2. Seleccionar **Entorno de ejecución → Ejecutar todo**.
3. Verificar que todas las celdas finalicen sin errores.

### Opción 2: entorno local

```bash
python -m venv .venv
```

Activar el entorno virtual e instalar las dependencias:

```bash
pip install -r requirements.txt
jupyter notebook notebooks/Clustering_CQI.ipynb
```

El análisis utiliza `random_state=42` en los procedimientos aleatorios para favorecer la reproducibilidad.

## Archivos generados

El notebook exporta automáticamente las tablas de métricas, resultados de optimización, concordancia entre algoritmos y asignaciones finales de clústeres en formato CSV.

## Autora

**Nuvia Meza**
