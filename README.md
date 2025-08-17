# Telecom X – Churn Prediction (Parte 2)

Este proyecto desarrolla un pipeline de *Machine Learning* para predecir la cancelación de clientes (*churn*) en una empresa de telecomunicaciones (TelecomX), a partir de variables de comportamiento, servicio y facturación. A partir de los resultados obtenidos se analizan los principales factores de fuga y se proponen estrategias de retención de clientes.

---

## 📁 Estructura del repositorio

| Archivo / Carpeta                      | Descripción                                                                 |
|----------------------------------------|-----------------------------------------------------------------------------|
| `TelecomX_LATAM_2.ipynb`               | Cuaderno principal con EDA, modelado, análisis de feature importance e informe final |
| `Base_de_datos_TelecomX.csv`           | Dataset original crudo                                                     |
| `TelecomX_Base_de_datos_bool.csv`      | Dataset tratado (variables limpias y estandarizadas)                       |
| `Diccionario_TelecomX.md`              | Diccionario de variables y descripciones                                   |

---

## ⚙️ Proceso de Trabajado

### 1. **Preparación de Datos**
- Imputación de faltantes y estandarización de valores tipo “Sin servicio” → “No”.
- Conversión de la variable objetivo: `"Si"` → 1, `"No"` → 0.
- Identificación de variables:
  - **Categóricas:** tipo de contrato, métodos de pago, servicios contratados, etc.
  - **Numéricas:** cargos mensuales, total cobrado, meses de antigüedad, etc.
- Codificación *One-Hot Encoding* para variables categóricas.
- División del dataset → `train / test` (stratified, 70/30).
- Balanceo de clases en entrenamiento usando **SMOTE**.

### 2. **EDA (Exploratory Data Analysis)**
- Histogramas, boxplots y countplots por variable.
- Detección de outliers y patrones de comportamiento.
- Curvas de correlación con respecto a la variable churn.

📌 **Hallazgos clave:**  
Los contratos mensuales, altos cargos mensuales y baja antigüedad correlacionan fuertemente con el abandono del cliente.

### 3. **Modelado Predictivo**
Se entrenaron y compararon modelos:

| Modelo                 | Ajuste           | Mejores resultados |
|------------------------|------------------|--------------------|
| Regresión Logística    | Normalización    | Mejor recall y AUC |
| Random Forest          | GridSearchCV     | Mejor precisión    |
| KNN, SVM, XGBoost      | Param tuning     | Alternativas menos performantes |

✔️ Métricas evaluadas: **Accuracy**, **Precision**, **Recall**, **F1-score**, **AUC-ROC**

### 4. **Feature Importance**
Se obtuvo la importancia de variables usando:
- Coeficientes (modelos lineales)
- `feature_importances_` (modelos de árbol)
- `permutation_importance` (fallback universal)

📊 Variables más influyentes:
- Tipo de contrato (*mensual*)
- Cargo mensual
- Antigüedad del cliente
- Servicios adicionales activos

---

## 🚀 Estrategias de Retención Propuestas

| Acción sugerida                            | Justificación basada en datos                         |
|-------------------------------------------|--------------------------------------------------------|
| Migrar clientes a contratos anuales       | Reduce el churn asociado a contratos mensuales        |
| Programas de fidelización temprana        | Mayor churn en clientes <6 meses                      |
| Bundles de servicios de valor agregado    | Servicios extras (soporte, streaming) retienen clientes|
| Incentivar métodos de pago automáticos    | Menor churn que pagos manuales                        |

---

## ▶️ Cómo ejecutar el cuaderno

### 1. Clonar el repositorio

```bash
git clone https://github.com/MigXDev/CS_Datos_I_DESAFIO_3.git
````

### 2. Instalar requisitos

```bash
pip install -r requirements.txt
```

Librerías utilizadas:
`pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `imblearn`, `xgboost`.

### 3. Ejecutar el notebook

1. Abrir `TelecomX_LATAM_2.ipynb` con Google Colab, Jupyter Notebook o VSCode.
2. Verificar que el archivo `TelecomX_Data_Base.csv` esté en la misma ruta.
3. Ejecutar celda por celda siguiendo la guía de iconos del encabezado del cuaderno.

---

## 📌 Autor

> Challenge Alura + Oracle
>
> Programa ONE Next Education
> 
> Desarrollado por **Miguel Angel Ajhuacho** – Analista Junior de Ciencia de Datos
> 
> Año: 2025

---

¿Listo para anticiparte al abandono de clientes antes de que suceda? 🚀
