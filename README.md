# Parte-2-Challenge-Telecom-X
Challenge 3 del Programa ONE de Oracle


# Análisis de Rotación de Clientes en Telecom X

Este proyecto tiene como objetivo analizar los factores que influyen en la rotación de clientes (Churn) en la empresa de telecomunicaciones Telecom X y desarrollar modelos predictivos para identificar a los clientes con mayor probabilidad de cancelar su servicio.

## Contenido del Repositorio

*   `notebook.ipynb`: El notebook de Jupyter que contiene el análisis de datos, preprocesamiento, entrenamiento y evaluación de modelos.
*   `datos_tratados.csv`: Archivo CSV con los datos tratados utilizados en el análisis.
*   `README.md`: Este archivo.

## Análisis de Datos

El análisis se llevó a cabo utilizando el conjunto de datos de clientes de Telecom X. Se realizaron los siguientes pasos:

1.  **Carga de Datos:** Se cargaron los datos desde el archivo `datos_tratados.csv`.
2.  **Exploración de Datos:** Se realizó una exploración inicial para entender la estructura de los datos, identificar variables y sus tipos, y verificar la presencia de valores nulos.
3.  **Preprocesamiento de Datos:**
    *   Se eliminó la columna `customerID` por ser irrelevante para la predicción.
    *   Se trataron los valores categóricos, reemplazando 'No internet service' y 'No phone service' por 'No' en las columnas correspondientes.
    *   Se aplicó One-Hot Encoding a las variables categóricas.
    *   Se aplicó Label Encoding a la variable objetivo `Churn`.
    *   Se realizó un análisis de Factor de Inflación de Varianza (VIF) para identificar y eliminar variables con alta multicolinealidad.
4.  **Visualización de Correlación:** Se generaron heatmaps para visualizar la correlación entre las variables, identificando aquellas con mayor correlación con la variable objetivo `Churn`.
5.  **Análisis Dirigido:** Se realizaron box plots para visualizar la relación entre variables clave (Tenure y Charges_Total) y Churn.

## Modelado Predictivo

Se entrenaron y evaluaron los siguientes modelos de clasificación para predecir la rotación de clientes:

*   Regresión Logística
*   K-Nearest Neighbors (KNN)
*   Árbol de Decisión
*   Random Forest

Para abordar el desbalance en la variable objetivo, se utilizó la técnica de sobremuestreo SMOTE en el conjunto de entrenamiento.

Se evaluó el rendimiento de los modelos utilizando métricas como Exactitud, ROC AUC, Matriz de Confusión e Informe de Clasificación.

## Resultados y Conclusiones

El análisis de importancia de las variables en los modelos reveló que los factores más influyentes en la rotación de clientes son:

*   **Tipo de Contrato:** Los clientes con contratos mes a mes son más propensos a rotar.
*   **Antigüedad del Cliente (`tenure`):** Los clientes con menor antigüedad tienen una mayor probabilidad de cancelar.
*   **Cargos Mensuales (`Charges_Monthly`):** Cargos mensuales más altos se asocian con la rotación.
*   **Servicio de Internet (Fibra Óptica):** Los clientes con este servicio tienen una mayor propensión a cancelar.
*   **Método de Pago (Cheque Electrónico):** Este método de pago está relacionado con una mayor rotación.

Al comparar el rendimiento de los modelos, el modelo de **Regresión Logística** demostró ser el más efectivo para identificar a los clientes que probablemente cancelarán (alto recall para la clase minoritaria "Yes"), a pesar de tener una exactitud general ligeramente menor que Random Forest. Su ROC AUC también fue el más alto, indicando una buena capacidad discriminatoria.

## Recomendación

Basado en los resultados del análisis, se recomienda utilizar el modelo de **Regresión Logística** para identificar a los clientes con alto riesgo de rotación en Telecom X. Esta información puede ser utilizada para implementar estrategias de retención dirigidas y personalizadas.

## Cómo Ejecutar el Notebook

1.  Clona este repositorio.
2.  Abre el notebook `notebook.ipynb` en Google Colab o un entorno de Jupyter.
3.  Ejecuta las celdas en orden.

## Dependencias

Las principales librerías utilizadas en este proyecto son:

*   pandas
*   numpy
*   matplotlib
*   seaborn
*   plotly
*   sklearn
*   statsmodels
*   imblearn
