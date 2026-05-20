# Predicción de Churn en Telecomunicaciones

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.3+-orange.svg)](https://scikit-learn.org/)
[![pandas](https://img.shields.io/badge/pandas-1.5+-blue.svg)](https://pandas.pydata.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## Resumen Ejecutivo

Este proyecto desarrolla un sistema completo de **predicción de churn** (abandono de clientes) para una empresa de telecomunicaciones. El trabajo comienza con un análisis exploratorio en `notebook-EDA/analisis.ipynb` y luego avanza al modelado en `02_modeling/analisisML.ipynb`.

El notebook de EDA incluye:

- carga y revisión inicial de datos
- limpieza y conversión de variables numéricas
- análisis de churn por contrato y método de pago
- análisis del impacto de los cargos mensuales
- visualizaciones de distribución y comparación bivariada
- generación de `telco_clean.csv` para su uso en modelado

El análisis termina con conclusiones y recomendaciones de negocio para la siguiente fase.

## Visualizaciones clave

### Churn por tipo de contrato

![Churn por tipo de contrato](02_modeling/images/README_contract_churn.png)

![Churn por método de pago](02_modeling/images/README_payment_churn.png)

### Churn por método de pago

![Churn por método de pago](README_payment_churn.png)

### Resultados Clave
- **Modelo Principal**: Regresión Logística con **80.6% accuracy** y **84.7% AUC-ROC**
- **Modelo Alternativo**: Random Forest con **78.1% accuracy** y **82.3% AUC-ROC**
- **Variables Críticas**: TotalCharges, Tenure, MonthlyCharges, Contract Type
- **Validación**: Cross-validation confirma estabilidad del rendimiento

## Estructura del Proyecto

```
Proyecto-telecomunicaciones/
├── 02_modeling/
│   ├── analisisML.ipynb          # Notebook principal de ML
│   └── telco_clean.csv          # Dataset procesado
├── notebook-EDA/
│   ├── analisis.ipynb           # Análisis exploratorio
│   └── WA_Fn-UseC_-Telco-Customer-Churn.csv  # Dataset original
└── README.md                    # Este archivo
```

## Inicio Rápido

### Prerrequisitos

- Python 3.8+
- Conda (recomendado para gestión de entornos)

### Instalación

1. **Clonar el repositorio**
   ```bash
   git clone https://github.com/tu-usuario/proyecto-telecomunicaciones.git
   cd proyecto-telecomunicaciones
   ```

2. **Crear entorno virtual**
   ```bash
   conda create -n telco-ml python=3.11
   conda activate telco-ml
   ```

3. **Instalar dependencias**
   ```bash
   pip install pandas numpy scikit-learn matplotlib seaborn jupyter
   ```

### Uso

1. **Ejecutar análisis exploratorio**
   ```bash
   jupyter notebook notebook-EDA/analisis.ipynb
   ```

2. **Ejecutar modelo de ML**
   ```bash
   jupyter notebook 02_modeling/analisisML.ipynb
   ```

## Metodología

### 1. Exploración de Datos (EDA)
- Análisis univariado y bivariado
- Identificación de patrones de churn
- Limpieza y transformación de datos

### 2. Preprocesamiento
- **Variables Numéricas**: Estandarización (StandardScaler)
- **Variables Categóricas**: Codificación One-Hot (OneHotEncoder)
- **División**: 75% entrenamiento, 25% prueba con estratificación

### 3. Modelado
- **Regresión Logística**: Modelo baseline interpretable
- **Random Forest**: Modelo ensemble para comparación
- **Evaluación**: Accuracy, Precision, Recall, F1-Score, ROC-AUC

### 4. Validación
- Cross-validation 5-fold
- Análisis de importancia de características
- Curvas ROC y matrices de confusión

## Resultados Detallados

### Comparación de Modelos

| Modelo              | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---------------------|----------|-----------|--------|----------|---------|
| Regresión Logística | 0.8064   | 0.6607    | 0.5546 | 0.6030   | 0.8466  |
| Random Forest       | 0.7808   | 0.6147    | 0.4647 | 0.5293   | 0.8228  |

### Variables Más Importantes
1. **TotalCharges** (16.1%) - Cargos totales acumulados
2. **Tenure** (13.7%) - Meses como cliente
3. **MonthlyCharges** (13.6%) - Cargos mensuales
4. **Contract_Month-to-month** (5.0%) - Tipo de contrato
5. **OnlineSecurity_No** (3.3%) - Falta de seguridad online

## Recomendaciones de Negocio

### Estrategias de Retención

** Segmentación por Riesgo:**
- **Alto Riesgo**: Contratos mensuales, altos cargos, baja permanencia
- **Medio Riesgo**: Contratos anuales con altos cargos totales
- **Bajo Riesgo**: Clientes leales con contratos largos

** Acciones Preventivas:**
- Ofertas personalizadas de renovación
- Descuentos para clientes de alto riesgo
- Migración a planes más económicos
- Atención prioritaria y soporte proactivo

### Métricas de Éxito
- **Reducción de Churn**: Objetivo 15-20%
- **ROI de Retención**: Costo retención vs. adquisición
- **Satisfacción**: Aumento en NPS
- **Valor Lifetime**: Incremento en CLV

## 🛠️ Arquitectura Técnica

### Opciones de Deployment

**Opción 1: Batch Processing**
- Predicciones diarias/semanalmente
- Integración con ETL existente
- Dashboard estático

**Opción 2: Real-time Scoring**
- API REST (FastAPI/Flask)
- Base de datos para scores
- Dashboard en tiempo real

**Opción 3: Cloud-Native**
- AWS SageMaker / Google AI Platform
- Auto-scaling automático
- MLOps con CI/CD

### Monitoreo
- **Modelo**: Accuracy, AUC-ROC, drift detection
- **Negocio**: Tasa churn real vs. predicha, ROI
- **Sistema**: Latencia, uptime, errores

## Limitaciones y Supuestos

### Limitaciones
- Datos históricos limitados
- Variables externas no incluidas (competencia, economía)
- Sesgo potencial en datos existentes

### Supuestos
- Patrones históricos se mantendrán
- Independencia entre observaciones
- Representatividad del conjunto de prueba

## Referencias

- [Scikit-learn Documentation](https://scikit-learn.org/stable/)
- [Hands-On Machine Learning](https://www.oreilly.com/library/view/hands-on-machine-learning/)
- [Telco Customer Churn Dataset - Kaggle](https://www.kaggle.com/blastchar/telco-customer-churn)

