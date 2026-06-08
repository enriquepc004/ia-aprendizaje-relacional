# Aprendizaje automatico relacional sobre Cora

Este repositorio contiene el desarrollo de un proyecto de aprendizaje automatico relacional aplicado al dataset Cora. El objetivo principal es estudiar si la informacion estructural del grafo de citaciones ayuda a clasificar articulos cientificos en sus distintas categorias tematicas.

Para ello se comparan tres tipos de atributos:

- Atributos originales del dataset Cora, correspondientes a la presencia o ausencia de palabras en cada articulo.
- Metricas relacionales calculadas a partir del grafo de citaciones.
- Combinacion de atributos originales y metricas relacionales.

Sobre estos conjuntos de datos se entrenan y evaluan tres modelos supervisados: Naive Bayes, CART y kNN.

## Descripcion de los notebooks

1. `01_exploracion_cora.ipynb`
   Realiza la carga inicial de Cora, analiza la distribucion de clases, comprueba la consistencia de los datos y construye una primera representacion del grafo de citaciones.

2. `02_metricas_relacionales.ipynb`
   Calcula las metricas relacionales del grafo: grado, centralidad de grado, betweenness centrality, closeness centrality, clustering coefficient, PageRank y comunidades Louvain. Estas metricas se guardan en `data/processed/cora_metricas_relacionales.csv`.

3. `03_naive_bayes.ipynb`
   Entrena y evalua modelos Naive Bayes con atributos originales, metricas relacionales y atributos combinados. Incluye comparacion entre modelos base y modelos optimizados mediante `Pipeline` y `GridSearchCV`.

4. `04_cart.ipynb`
   Entrena y evalua arboles de decision CART en los tres escenarios de atributos. Incluye validacion cruzada, optimizacion de hiperparametros, matrices de confusion e interpretacion mediante importancia de variables.

5. `05_KNN.ipynb`
   Aplica kNN sobre los tres conjuntos de atributos. Como kNN depende de distancias, se normalizan las variables numericas y se codifica la comunidad Louvain cuando es necesario. Tambien se realiza optimizacion con `GridSearchCV`.

6. `06_Comparacion_Modelos.ipynb`
   Resume y compara los resultados finales de Naive Bayes, CART y kNN. Permite identificar que combinacion de modelo y atributos obtiene el mejor rendimiento global.

7. `07_modelo_final.ipynb`
   Reconstruye el modelo final seleccionado, Naive Bayes con atributos originales y metricas relacionales combinadas. Muestra sus parametros principales y el rendimiento final obtenido.

## Datos utilizados

El proyecto utiliza el dataset Cora, formado por articulos cientificos, atributos binarios de palabras y relaciones de citacion entre articulos.

Los ficheros originales se encuentran en:

- `data/raw/cora.content`
- `data/raw/cora.cites`

Los ficheros procesados generados durante el trabajo se encuentran en:

- `data/processed/cora_content_procesado.csv`
- `data/processed/cora_cites_procesado.csv`
- `data/processed/cora_metricas_relacionales.csv`

## Orden de ejecucion recomendado

Para reproducir el trabajo completo, ejecutar los notebooks en este orden:

1. `notebooks/01_exploracion_cora.ipynb`
2. `notebooks/02_metricas_relacionales.ipynb`
3. `notebooks/03_naive_bayes.ipynb`
4. `notebooks/04_cart.ipynb`
5. `notebooks/05_KNN.ipynb`
6. `notebooks/06_Comparacion_Modelos.ipynb`
7. `notebooks/07_modelo_final.ipynb`

Los notebooks 03, 04, 05, 06 y 07 dependen de los ficheros procesados generados en los notebooks anteriores.

## Resultados principales

Los experimentos muestran que las metricas relacionales aportan informacion util para la clasificacion de articulos. En particular:

- Naive Bayes obtiene su mejor resultado al combinar atributos originales y metricas relacionales.
- CART aprovecha especialmente la variable de comunidad Louvain, que resume informacion estructural del grafo.
- kNN obtiene mejores resultados con las metricas relacionales que con los atributos textuales originales, ya que trabaja mejor en un espacio de menor dimensionalidad y correctamente normalizado.

El mejor modelo global es Naive Bayes con atributos originales y metricas relacionales combinadas.
