# Predicción de la probabilidad de default de clientes de tarjeta de crédito

Trabajo de portafolio semestral del curso **Ciencia de Datos para la Economía**.

Réplica y extensión del paper:

> Yeh, I.-C., & Lien, C.-H. (2009). *The comparisons of data mining techniques for the predictive accuracy of probability of default of credit card clients.* Expert Systems with Applications, 36(2), 2473-2480.

## Descripción

El paper compara seis técnicas de minería de datos para predecir la probabilidad de incumplimiento (*default*) de clientes de tarjeta de crédito de un banco de Taiwán, y propone el **Sorting Smoothing Method (SSM)** para evaluar qué tan bien la probabilidad predicha representa la probabilidad real de default.

En este trabajo:

1. Se replican los datos, el preprocesamiento y los resultados principales, con una revisión explícita de calidad de datos (duplicados, valores atípicos) y del significado real de las variables de historial de pago (PAY_1...PAY_6).
2. Se implementan tres de los seis modelos del paper: regresión logística, árbol de clasificación (CART) y redes neuronales (ANN).
3. Se propone e implementa un modelo adicional no usado por los autores: **Random Forest**.
4. Se comparan todos los modelos con las métricas del paper (tasa de error, area ratio, SSM) y otras equivalentes (accuracy, precision, recall, F1, AUC), incluyendo una verificación de sobreajuste (train vs. test).
5. Se concluye cuál es el mejor modelo.

## Datos

*Default of Credit Card Clients Dataset* del UCI Machine Learning Repository (id = 350), 30.000 clientes y 23 variables explicativas. Se descargan directamente desde el cuaderno con el paquete `ucimlrepo`, sin necesidad de archivos locales.

## Archivos

- `Portafolio_Default_Credit_Card.ipynb`: cuaderno principal, ejecutable de principio a fin.
- `requirements.txt`: dependencias.
## Cómo ejecutar

### Google Colab

1. Subir `Portafolio_Default_Credit_Card.ipynb` a Google Colab.
2. Ejecutar todas las celdas (`Entorno de ejecución > Ejecutar todo`). La primera celda instala `ucimlrepo` si hace falta y las demás librerías ya están disponibles en Colab.

### Local

```
pip install -r requirements.txt
jupyter notebook Portafolio_Default_Credit_Card.ipynb
```

## Resultado principal

Random Forest obtiene el mejor desempeño global (mayor AUC, area ratio y F1, y el mayor R² del SSM). Las redes neuronales quedan muy cerca y son las mejor calibradas según el criterio del paper (pendiente e intercepto casi ideales), lo que confirma cualitativamente la conclusión de los autores. Random Forest, la ANN y el árbol —los modelos capaces de capturar el quiebre no lineal entre el historial de pago (PAY_1) y el default— superan con claridad a Regresión Logística, que muestra menor recall.
