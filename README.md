# Segmentación de Usuarios mediante Algoritmos No Supervisados

## 🔎 Índice

1. [Objetivos](#objetivos)
2. [Introducción](#introducción)
3. [Entorno de Trabajo](#Entorno-de-trabajo)
4. [Descripción del Conjunto de Datos](#descripción-del-conjunto-de-datos)
5. [Preprocesamiento de Datos](#preprocesamiento-de-datos)
6. [Aplicación de Algoritmos de Clustering](#aplicación-de-algoritmos-de-clustering)
7. [Visualización y Análisis de Resultados](#visualización-y-análisis-de-resultados)
8. [Resumen de Características por Clúster](#resumen-de-características-por-clúster)
9. [Comparación entre KMeans y DBSCAN](#comparación-entre-kmeans-y-dbscan)
10. [Análisis Técnico Detallado](#análisis-técnico-detallado)
11. [Conclusiones](#conclusiones)
12. [Recomendaciones](#recomendaciones)
13. [Autores](#autores)

---

## Objetivos

Implementar modelos de aprendizaje no supervisado para identificar segmentos de clientes a partir de sus características demográficas, de consumo y respuesta a campañas. Comparar modelos, validar visualmente los resultados y construir perfiles útiles para acciones de marketing personalizadas.

---

## Introducción

En este proyecto se aplican algoritmos no supervisados como KMeans y DBSCAN sobre un dataset de clientes, con el objetivo de segmentar perfiles de comportamiento y consumo. Se incluyen técnicas como PCA y t-SNE para reducir dimensionalidad y facilitar la visualización de resultados.

---
## Entorno de trabajo: versiones, librerías y herramientas.

### Entorno de Trabajo
- Google Colab Notebook (formato .ipynb)
- ython 3.x
- Ejecución basada en entorno de notebook 
________________________________________
### Librerías Importadas
#### Manipulación y Análisis de Datos:
- **pandas** – estructuras tipo DataFrame para manipular datos
- **numpy** – operaciones matemáticas y manejo de arrays
#### Visualización:
- **matplotlib.pyplot** – creación de gráficos estáticos (líneas, barras, etc.)
- **seaborn** – visualización estadística elegante sobre matplotlib
#### Preprocesamiento y Reducción de Dimensionalidad:
- **sklearn.preprocessing.StandardScaler** – estandarización de variables
- **sklearn.decomposition.PCA** – reducción lineal de dimensionalidad
- **sklearn.manifold.TSNE** – reducción no lineal para visualización avanzada
#### Algoritmos de Clustering:
- **sklearn.cluster.KMeans** – clustering particional
- **sklearn.cluster.DBSCAN** – clustering basado en densidad
#### Métricas y Evaluación:
- **sklearn.metrics.silhouette_score** – medida de calidad del clustering
- **sklearn.neighbors.NearestNeighbors** – análisis de vecinos más cercanos (para estimar eps en DBSCAN)
________________________________________
### Herramientas Técnicas Derivadas
- **Gráficas:** codo, silhouette, t-SNE, PCA
- **Análisis estadístico:** media, desviación estándar, percentiles
- **Visualización exploratoria:** mapas de calor, boxplots
- **Reducción de dimensionalidad:** PCA y t-SNE para comprensión visual
- **Evaluación del modelo:** coeficiente de Silhouette y visualización de clusters

---

## Descripción del Conjunto de Datos

El dataset contiene 2,240 registros y 29 variables, agrupadas en:
- **Demografía:** Año de nacimiento, educación, estado civil, ingresos, hijos en el hogar.
- **Comportamiento de compra:** Gastos en distintas categorías (vino, carnes, dulces...).
- **Campañas de marketing:** Aceptación de campañas, respuesta general.
- **Canales de compra:** Compras en web, catálogo, tienda, visitas al sitio.

Este conjunto permite analizar tanto el perfil socioeconómico como el comportamiento transaccional y la respuesta a estímulos comerciales.

---

## Análisis Técnico
### Preprocesamiento de Datos

- Se eliminaron columnas no informativas (ID, fechas, costos fijos).
- Las variables categóricas fueron convertidas a dummies.
- Se estandarizó el conjunto con `StandardScaler`.
- Se imputaron valores nulos.
- Se agregó una columna de edad calculada y otras métricas agregadas.

Este preprocesamiento asegura que las variables estén en la misma escala y que los algoritmos de clustering funcionen correctamente.

---

### Aplicación de Algoritmos de Clustering

#### KMeans
Se usó el método del codo para elegir el número óptimo de clústeres, identificado en **K=5**. Se aplicó el algoritmo y se interpretaron los clústeres generados mediante estadística descriptiva.

#### DBSCAN
DBSCAN no requiere un número de clústeres predefinido. Se exploraron diferentes combinaciones de los parámetros `eps` y `min_samples` mediante la gráfica de distancia de vecinos más cercanos.

---

### Visualización y Análisis de Resultados

#### Selección del Número Óptimo de Clusters
Para determinar el número óptimo de clusters se utilizaron dos métodos: el método del codo y el coeficiente de Silhouette. El método del codo evalúa la inercia (la suma de los errores cuadráticos dentro de los clusters) y mostró un punto de inflexión en K=5, lo que sugiere que añadir más clusters no mejora significativamente la segmentación. Por otro lado, el coeficiente de Silhouette mide qué tan bien está un punto dentro de su cluster en comparación con otros clusters. Aunque su valor máximo se presenta en K=2, el valor en K=5 también fue alto, lo cual valida esta elección desde otro enfoque.

#### Método del Codo y Silhouette

![Elbow y Silhouette](Imagenes/elbow_silhouette.png)

Estas gráficas confirman que K=5 ofrece una segmentación equilibrada.

### Aplicación de Modelos de Clustering y Reducción de Dimensionalidad
Posteriormente, se procedió a la aplicación de los algoritmos de clustering K-Means y DBSCAN, y se utilizaron técnicas de reducción de dimensionalidad como PCA y t-SNE para visualizar los resultados. Se generaron proyecciones en dos dimensiones para ambos algoritmos, permitiendo evaluar la coherencia visual de los clusters.

#### Visualización con PCA y t-SNE

![PCA](Imagenes/pca_kmeans.png)
Facilita la reducción de dimensiones a 2 usando PCA, esto para la visualización.

#### K-Means con t-SNE (Visualización No Lineal)
![t-SNE](Imagenes/tsne_projection.png)

Las visualizaciones obtenidas muestran que el algoritmo K-Means produce agrupaciones simétricas y bien definidas tanto en PCA como en t-SNE. Por su parte, DBSCAN permite identificar agrupaciones más libres y detecta puntos de ruido (outliers), los cuales aparecen dispersos. Con t-SNE se aprecia una mejor separación entre clusters, lo que permite visualizar estructuras complejas que PCA no logra capturar completamente.

PCA permite ver una distribución lineal. t-SNE expone relaciones no lineales y muestra mejor separación entre los clústeres generados por KMeans.



### Visualización Comparativa de Modelos
#### Comparativa entre K-Means y DBSCAN con PCA

![Comparativa](Imagenes/comparativa_pca_kmeans_dbscan.png)

En la parte izquierda de la imagen, K-Means logra separar los datos en cinco agrupaciones bastante diferenciadas. 
Se observa una distribución más compacta y organizada, con límites claros entre los grupos. Por otro lado, DBSCAN (parte derecha) identifica un único cluster principal y solo unos pocos puntos como ruido (etiquetados como -1). 
Esto indica que, con la configuración actual de parámetros (eps y min_samples), DBSCAN no encuentra estructura suficiente para generar múltiples grupos significativos en este conjunto de datos escalados.

#### DBSCAN con PCA (zoom para ver ruido)

![DBSCAN con PCA](Imagenes/dbscan_pca.png)

Aquí se confirma que DBSCAN clasificó a casi todos los puntos dentro de un único grupo, con solo algunos considerados como ruido. La falta de subdivisión en varios grupos podría deberse a una configuración de eps demasiado grande o a una baja variabilidad entre los datos tras PCA.


#### k-Distance Plot para DBSCAN

![k-distance](Imagenes/k_distance_plot.png)

Ayuda a seleccionar el `eps` óptimo para DBSCAN. La "rodilla" indica la distancia crítica.

---

## Resumen de Características por Clúster

Se presentaron estadísticas como media e IQR por grupo. Algunas observaciones:
- Clúster 0: Ingresos altos, alto gasto en productos premium.
- Clúster 2: Menor interacción digital pero buena respuesta a campañas.
- DBSCAN agrupó la mayoría en un solo clúster, útil para detección de outliers.

Estas características permitieron desarrollar perfiles de clientes bien diferenciados.

---

## Comparación entre KMeans y DBSCAN

KMeans produjo clústeres más simétricos y balanceados. DBSCAN fue más útil para detección de ruido y patrones densos sin estructura clara. PCA y t-SNE validaron visualmente las agrupaciones de KMeans, especialmente en espacios no lineales.

---

## Análisis Técnico Detallado

- El método del codo detectó que a partir de K=5, la ganancia de información adicional disminuye.
- El coeficiente de Silhouette fue alto para K=5, validando la cohesión intra-clúster.
- DBSCAN fue sensible al valor de `eps`. El valor ideal se encontró cerca de 3.5.
- Visualmente, PCA y t-SNE confirmaron una estructura interna coherente en KMeans.
- Variables clave como `Income`, `MntWines`, `MntGoldProds`, `NumWebPurchases` y `AcceptedCmpX` fueron cruciales para definir los perfiles.

Limitaciones:
- DBSCAN requiere ajuste fino de parámetros. Un eps mal elegido puede agrupar todo en un clúster.
- El escalado estándar asigna igual peso a todas las variables, lo que puede no reflejar su importancia real.

---
## ANÁLISIS ESTADÍSTICO
La tabla proporciona estadísticas como la media, desviación estándar, mínimo, máximo, cuartiles (25%, 50%, 75%) para las columnas numéricas.
A continuación, se presenta el análisis estadístico por clúster. En lugar de usar gráficos como mapas de calor o histogramas, se utilizaron tablas que muestran los valores promedio por grupo.

| Variable            | count |   mean   |   std   | min  | 25%   | 50%   | 75%    | max    |
|:--------------------|------:|---------:|--------:|-----:|------:|------:|-------:|-------:|
| Year_Birth          |  2216 | 1968.82  |  11.99  | 1893 | 1959  | 1970  | 1977   | 1996   |
| Income              |  2216 | 52247.25 | 25173.1 | 1730 | 35303 | 51381 | 68522  | 666666 |
| Kidhome             |  2216 | 0.44     | 0.54    | 0    | 0     | 0     | 1      | 2      |
| Teenhome            |  2216 | 0.50     | 0.54    | 0    | 0     | 0     | 1      | 2      |
| Recency             |  2216 | 49.01    | 28.95   | 0    | 24    | 49    | 74     | 99     |
| MntWines            |  2216 | 305.09   | 337.33  | 0    | 24    | 174.5 | 505    | 1493   |
| MntFruits           |  2216 | 26.36    | 39.79   | 0    | 2     | 8     | 33     | 199    |
| MntMeatProducts     |  2216 | 166.99   | 224.28  | 0    | 16    | 68    | 232.25 | 1725   |
| MntFishProducts     |  2216 | 37.64    | 54.75   | 0    | 3     | 12    | 50     | 259    |
| MntSweetProducts    |  2216 | 27.03    | 41.07   | 0    | 1     | 8     | 33     | 262    |
| MntGoldProds        |  2216 | 43.97    | 51.82   | 0    | 9     | 24.5  | 56     | 321    |
| NumDealsPurchases   |  2216 | 2.32     | 1.92    | 0    | 1     | 2     | 3      | 15     |
| NumWebPurchases     |  2216 | 4.09     | 2.74    | 0    | 2     | 4     | 6      | 27     |
| NumCatalogPurchases |  2216 | 2.67     | 2.93    | 0    | 0     | 2     | 4      | 28     |
| NumStorePurchases   |  2216 | 5.80     | 3.25    | 0    | 3     | 5     | 8      | 13     |
| NumWebVisitsMonth   |  2216 | 5.32     | 2.43    | 0    | 3     | 6     | 7      | 20     |
| AcceptedCmp3        |  2216 | 0.07     | 0.26    | 0    | 0     | 0     | 0      | 1      |
| AcceptedCmp4        |  2216 | 0.07     | 0.26    | 0    | 0     | 0     | 0      | 1      |
| AcceptedCmp5        |  2216 | 0.07     | 0.26    | 0    | 0     | 0     | 0      | 1      |
| AcceptedCmp1        |  2216 | 0.06     | 0.24    | 0    | 0     | 0     | 0      | 1      |
| AcceptedCmp2        |  2216 | 0.01     | 0.12    | 0    | 0     | 0     | 0      | 1      |
| Complain            |  2216 | 0.01     | 0.10    | 0    | 0     | 0     | 0      | 1      |
| Response            |  2216 | 0.15     | 0.36    | 0    | 0     | 0     | 0      | 1      |


## Conclusiones

- KMeans con **K=5** proporciona una segmentación robusta, interpretable y útil para estrategias comerciales.
- DBSCAN se recomienda como herramienta exploratoria para detección de valores atípicos.
- Las visualizaciones con t-SNE confirmaron que los grupos de KMeans son estructuralmente válidos.
- La segmentación permite diseñar campañas diferenciadas y mejorar la eficiencia de las acciones de marketing.

---

## Recomendaciones

- Utilizar los segmentos como insumo en sistemas CRM y campañas específicas.
- Ajustar DBSCAN dinámicamente o aplicar HDBSCAN para mayor granularidad.
- Incorporar análisis de importancia de variables o técnicas de reducción supervisada.
- Reentrenar el modelo con datos recientes de clientes activos.

---


---

## Autores

Francisco Estupiñan 
María Fernanda Bolaños
Fernando Montaño  
Proyecto de Segmentación de Usuarios - 2025
