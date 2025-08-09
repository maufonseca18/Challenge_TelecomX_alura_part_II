# 📊 Challenge TelecomX - Modelos Predictivos de Churn

## 📌 Introducción
Este proyecto forma parte del **Challenge TelecomX** de la formación en *Data Science*, cuyo objetivo es predecir la **fuga de clientes (Churn)** de una empresa de telecomunicaciones utilizando **modelos de Machine Learning**.

En la **Parte 1** del reto, se realizó un proceso de **ETL (Extract, Transform, Load)** para limpiar y preparar la base de datos.  
En esta **Parte 2**, a partir de los datos tratados, se desarrollan modelos predictivos para clasificar a los clientes en **churners** (clientes que abandonan) y **no churners**.

La meta es construir un pipeline reproducible, evaluar varios algoritmos y generar recomendaciones basadas en las variables más influyentes para la retención de clientes.

---

## ⚙️ Desarrollo del proyecto

### 1️⃣ Preparación de datos
- Archivo base: `datos_tratados.csv` generado en la Parte 1.
- Separación de columnas:
  - **Numéricas:** métricas de uso, cargos, antigüedad, etc.
  - **Categóricas:** género, tipo de contrato, método de pago, etc.
- Variable objetivo: `Churn`.
- División en **train** y **test** con estratificación para mantener proporción de clases.

### 2️⃣ Balanceo de clases
- Aplicación de **SMOTENC** para balancear la clase minoritaria.
- Tamaño después del balanceo: `(7556, 20)` registros de entrenamiento.

### 3️⃣ Preprocesamiento
- **ColumnTransformer** para:
  - Escalar numéricos con `StandardScaler`.
  - Codificar categóricos con `OneHotEncoder`.

### 4️⃣ Modelado
Se entrenaron y evaluaron los siguientes modelos:
- **Logistic Regression**
- **Random Forest Classifier**
- **Support Vector Classifier (SVC)**
- **XGBoost Classifier**

Todos implementados en pipelines que incluyen preprocesamiento.

### 5️⃣ Evaluación
Métricas obtenidas en el set de test:

| Modelo              | Accuracy | Precision | Recall | F1    | AUC    |
|---------------------|----------|-----------|--------|-------|--------|
| LogisticRegression  | 0.7698   | 0.5416    | 0.6845 | 0.6047| 0.8284 |
| RandomForest        | 0.7772   | 0.5606    | 0.6185 | 0.5881| 0.8138 |
| SVC                 | 0.7717   | 0.5468    | 0.6560 | 0.5964| 0.8138 |
| XGBoost             | 0.7680   | 0.5455    | 0.5882 | 0.5660| 0.8092 |

📌 **Mejor modelo por F1:** **Logistic Regression** (`F1 = 0.6047`).

---

## 💡 Conclusiones y Recomendaciones
- **Dataset:** 7,267 registros totales, 21 columnas tras preprocesamiento.
- **Proporción global de churn:** ~25.7%.
- Los modelos evaluados presentan **AUC > 0.80**, lo que indica una buena capacidad discriminativa.
- **Logistic Regression** presentó el mejor balance entre precisión y recall para detectar churn.

**Recomendaciones:**
1. **Focalizar retención** en segmentos definidos por:
   - `account_Contract` (tipo de contrato).
   - `account_PaymentMethod` (método de pago).
   - `customer_tenure` (antigüedad del cliente).
2. Revisar condiciones de **planes mensuales** y **métodos de pago electrónicos**, ya que estos presentan mayor probabilidad de churn.
3. Implementar **programas de fidelización** para clientes con menor tenure y cargos altos.

