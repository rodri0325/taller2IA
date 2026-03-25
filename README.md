# Workshop 2 – Machine Learning & Deep Learning Aplicado

**Universidad EAFIT · Introducción a la Inteligencia Artificial**  
Autores: Abraham Navarro · David Rodriguez

---

## Descripción general

Este workshop implementa el ciclo completo de un proyecto de Machine Learning y Deep Learning sobre dos problemas supervisados independientes:

- **Problema 1 – Clasificación:** Detección de fatiga muscular en ciclismo a partir de señales de electromiografía (EMG).
- **Problema 2 – Regresión:** Estimación de edad a partir de imágenes faciales usando una Red Neuronal Convolucional (CNN).

Cada problema cubre desde el análisis del dataset hasta la evaluación final del modelo, incluyendo exploración de datos, preprocesamiento, entrenamiento, comparación de modelos y análisis crítico de resultados.

---

## Problema 1 – Clasificación: Detección de Fatiga Muscular

**Dataset:** Muscle Fatigue Cycling  
**Fuente:** HuggingFace – `YominE/Muscle_Fatigue_Cycling`

Se trabaja con señales EMG registradas en 8 músculos de la pierna dominante de sujetos realizando sprints en bicicleta. El objetivo es clasificar el estado muscular del sujeto en dos categorías:

- `0` = Condición normal
- `1` = Desgaste muscular

El flujo del problema incluye extracción de características en el dominio del tiempo y la frecuencia sobre ventanas de 1 segundo, análisis exploratorio, comparación de cinco clasificadores (kNN, Decision Tree, Random Forest, Gradient Boosting y DNN) con ajuste de hiperparámetros, y evaluación final con matriz de confusión y métricas de clasificación.

> Este problema fue desarrollado por el compañero de equipo. Ver su notebook para detalles de implementación.

---

## Problema 2 – Regresión: Estimación de Edad a partir de Imágenes Faciales

**Dataset:** Faces: Age Detection from Images  
**Fuente:** Kaggle – `arashnic/faces-age-detection-dataset`

El objetivo es entrenar una CNN que estime la edad de una persona a partir de los píxeles de su imagen facial. Dado que el dataset provee etiquetas categóricas (YOUNG, MIDDLE, OLD), se realiza un mapeo a valores numéricos de edad para convertirlo en un problema de regresión.

El flujo incluye análisis exploratorio, preprocesamiento de imágenes, data augmentation, entrenamiento de una CNN con regularización, y evaluación con métricas MAE, RMSE y R².

---

## Guía de instalación y ejecución – Problema 2

### Requisitos previos

- Cuenta en [Google Colab](https://colab.research.google.com)
- Cuenta en [Kaggle](https://www.kaggle.com) (gratuita)
- Cuenta en [Google Drive](https://drive.google.com)

No se requiere instalación local. Todo corre en la nube.

---

### Paso 1 – Descargar el dataset desde Kaggle

1. Inicia sesión en [kaggle.com](https://www.kaggle.com)
2. Ve al dataset: `kaggle.com/datasets/arashnic/faces-age-detection-dataset`
3. Haz clic en el botón **Download** para descargar el archivo `.zip` a tu computador

---

### Paso 2 – Subir el dataset a Google Drive

1. Ve a [drive.google.com](https://drive.google.com)
2. Crea una carpeta con esta ruta exacta: `Mi unidad / Faces-Age-Detection / faces /`
3. Descomprime el zip descargado y sube la carpeta `Train/` y el archivo `train.csv` dentro de esa carpeta

La estructura en Drive debe quedar así:

```
Mi unidad/
└── Faces-Age-Detection/
    └── faces/
        ├── Train/
        │   ├── 00001.jpg
        │   ├── 00002.jpg
        │   └── ... (imágenes)
        └── train.csv
```

---

### Paso 3 – Abrir el notebook en Google Colab

1. Sube el archivo `workshop2_final.ipynb` a Google Colab  
   *(Archivo → Subir notebook)*
2. Activa la GPU para acelerar el entrenamiento:  
   **Runtime → Change runtime type → T4 GPU → Save**

---

### Paso 4 – Ejecutar el notebook

Ejecuta las celdas **en orden de arriba a abajo**. El flujo es el siguiente:

| Celda | Qué hace |
|-------|----------|
| Montar Drive | Conecta Google Drive con Colab |
| Librerías | Importa todas las dependencias necesarias |
| Leer CSV | Carga las etiquetas del dataset |
| Mapeo de etiquetas | Convierte YOUNG/MIDDLE/OLD a valores numéricos de edad |
| Carga de imágenes | Lee las imágenes desde Drive |
| EDA | Genera gráficos exploratorios con interpretaciones |
| Preprocesamiento | Redimensiona, normaliza y divide en train/val/test |
| Entrenamiento | Entrena la CNN con data augmentation y callbacks |
| Evaluación | Calcula MAE, RMSE y R² en los tres conjuntos |
| Prueba | Predice sobre una imagen individual y analiza perturbaciones |

> **Nota:** La carga de imágenes desde Drive puede tardar varios minutos dependiendo de la conexión. Si quieres acelerar el proceso, reduce el número de imágenes cambiando el valor en `df.sample(2000)`.

---

### Dependencias

El notebook usa únicamente librerías disponibles por defecto en Google Colab. No se requiere instalar nada adicional:

```
tensorflow
opencv-python (cv2)
numpy
pandas
matplotlib
seaborn
scikit-learn
```

---

### Parámetros configurables

Si deseas ajustar el experimento, estos son los valores que puedes modificar en el notebook:

| Parámetro | Valor por defecto | Descripción |
|-----------|-------------------|-------------|
| `IMG_SIZE` | `128` | Tamaño de las imágenes en píxeles |
| `df.sample(n)` | `2000` | Número de imágenes a usar |
| `epochs` | `15` | Número de épocas de entrenamiento |
| `batch_size` | `32` | Tamaño del batch |

---

## Estructura del repositorio

```
workshop2/
├── README.md                     ← este archivo
├── workshop2_final.ipynb         ← notebook Problema 2 (regresión)
└── clasificacion_compañero.ipynb ← notebook Problema 1 (clasificación)
```

---
