# Parte-2-Challenge-Telecom-X
Challenge 3 del Programa ONE de Oracle


# Análisis de Rotación de Clientes en Telecom X

El objetivo principal de este proyecto es predecir la rotación de clientes (Churn) en Telecom X. Utilizando un conjunto de datos que contiene información sobre diversos aspectos de los clientes, buscamos identificar los factores clave que influyen en la decisión de un cliente de cancelar su servicio y desarrollar un modelo predictivo que permita a la empresa anticipar y gestionar el riesgo de rotación.

## Estructura del Proyecto

El proyecto se organiza de la siguiente manera:

*   `Telecom_X_Parte_2.ipynb`: Cuaderno principal de Jupyter que contiene todo el código para el análisis, desde la carga de datos hasta la evaluación de modelos.
*   `datos_tratados.csv`: Archivo CSV que contiene el conjunto de datos preprocesado utilizado en el análisis.
*   `visualizaciones/`: (Opcional) Carpeta que podría contener gráficos y visualizaciones generadas durante el Análisis Exploratorio de Datos (EDA).

## Proceso de Preparación de Datos

El proceso de preparación de datos incluyó las siguientes etapas:

1.  **Carga de Datos:** Los datos se cargaron desde un archivo CSV (`datos_tratados.csv`) utilizando la librería pandas.
2.  **Clasificación de Variables:** Las variables se clasificaron en categóricas y numéricas para aplicar las técnicas de preprocesamiento adecuadas.
3.  **Limpieza y Transformación:**
    *   Se eliminó la columna `customerID` por ser irrelevante para la predicción.
    *   Se reemplazaron los valores 'No internet service' y 'No phone service' por 'No' en las columnas correspondientes para simplificar la codificación.
4.  **Codificación de Variables Categóricas:** Se aplicó One-Hot Encoding a las variables categóricas para convertirlas en un formato numérico que pudiera ser utilizado por los modelos de Machine Learning. Se utilizó `OneHotEncoder` de scikit-learn con `drop='if_binary'` para evitar la multicolinealidad en el caso de variables binarias y `handle_unknown='ignore'` para manejar posibles valores desconocidos en el conjunto de prueba.
5.  **Codificación de la Variable Objetivo:** La variable objetivo `Churn` se codificó utilizando `LabelEncoder` para transformarla en valores numéricos (0 para 'No' y 1 para 'Yes').
6.  **Análisis de Varianza Inflada (VIF):** Se calculó el VIF para identificar y eliminar variables con alta multicolinealidad, lo que podría afectar la estabilidad y interpretabilidad de los modelos lineales. Se eliminaron variables con VIF infinito o muy alto, como `PhoneService_Yes`, `MultipleLines_No phone service`, `InternetService_No`, `Cuentas Diarias`, `StreamingMovies_Yes`, `MultipleLines_No phone service`, `Contract_Two year`, `Charges_Total`, `PaymentMethod_Mailed check`, `MultipleLines_No`, y `InternetService_DSL`.
7.  **Separación de Datos:** Los datos se dividieron en conjuntos de entrenamiento (70%) y prueba (30%) utilizando `train_test_split` con `random_state` para reproducibilidad y `stratify=y` para mantener la proporción de la variable objetivo en ambos conjuntos, lo cual es importante debido al desbalance observado.
8.  **Normalización de Variables Numéricas:** Se aplicó `StandardScaler` a las variables numéricas para escalarlas y asegurar que ninguna característica dominara a las demás debido a su magnitud. Esto es particularmente importante para modelos sensibles a la escala como la Regresión Logística y KNN.
9.  **Balanceo de Clases:** Dado el desbalance en la variable objetivo, se utilizó SMOTE (`Synthetic Minority Over-sampling Technique`) en el conjunto de entrenamiento para crear instancias sintéticas de la clase minoritaria (`Churn=Yes`) y equilibrar la distribución de clases.

## Análisis Exploratorio de Datos (EDA)

Durante el EDA, se obtuvieron los siguientes insights clave:

*   **Distribución de Churn:** Se confirmó el desbalance de clases en la variable objetivo.
*   **Correlaciones:** El heatmap de correlación reveló que variables como el tipo de contrato (`Contract`), la antigüedad del cliente (`tenure`), el servicio de Internet (especialmente `Fiber optic`) y el método de pago (`Electronic check`) están fuertemente correlacionadas con la rotación.
*   **Box Plots:** Los box plots de `Tenure` y `Charges_Total` vs `Churn` mostraron que los clientes que rotan tienden a tener menor antigüedad y cargos totales más bajos.

Se recomienda revisar el cuaderno para visualizar los gráficos de correlación y box plots generados durante el EDA.

## Modelización y Evaluación

Se entrenaron y evaluaron cuatro modelos de clasificación para predecir Churn:

*   Regresión Logística
*   K-Nearest Neighbors (KNN)
*   Árbol de Decisión
*   Random Forest

El rendimiento de los modelos se evaluó utilizando métricas como Exactitud, ROC AUC, Matriz de Confusión y el Informe de Clasificación (Precisión, Recall, F1-score).

El análisis detallado del rendimiento de cada modelo (presentado en el informe final dentro del cuaderno) llevó a la recomendación de utilizar el modelo de **Regresión Logística** como el más adecuado para este problema, principalmente debido a su buen equilibrio entre ROC AUC y recall para la clase minoritaria, lo cual es crucial para identificar a los clientes con alto riesgo de rotación.
