# TFM: Detección de Defectos Superficiales en Acero (NEU-DET)

Este repositorio contiene el desarrollo y los experimentos realizados para mi Trabajo de Fin de Máster (TFM), centrado en la detección automática de defectos en superficies metálicas utilizando arquitecturas de Deep Learning, específicamente la familia de modelos **YOLOv8**.

## 🚀 Resumen de Implementaciones por Rama

El proyecto se ha estructurado en diferentes ramas para aislar los experimentos de hiperparámetros, arquitecturas y técnicas de preprocesamiento:

### 🔬 Experimentos Base (YOLOv8 Nano)
*   **`experimento-50-epoch-yolov8n.pt-sin-dataaugmentation`**: Baseline del proyecto utilizando el modelo más ligero (`yolov8n`) durante 50 épocas sin técnicas de aumento de datos.
*   **`experimento-100-epoch-yolov8n.pt-dataaugmentation`**: Extensión del baseline a 100 épocas incorporando las técnicas por defecto de *Data Augmentation* de YOLOv8.
*   **`experimento-100-epoch-yolov8n.pt-dataaugmentation-imgsz-448-mixup-0-5`**: Mejora del modelo nano ajustando el tamaño de imagen a 448px e introduciendo `mixup` con un coeficiente de 0.5 para mejorar la generalización.

### 📈 Evolución a YOLOv8 Small (Versiones Tunned)
*   **`exp_100-epoch-yolov8s`**: Salto al modelo `yolov8s` para obtener una mayor capacidad de extracción de características.
*   **`exp_100-epoch-yolov8s-640`**: Evaluación del rendimiento de YOLOv8s con el tamaño de imagen estándar de 640px.
*   **`exp_100-epoch-yolov8s-448-conf-iou`**: Optimización de los umbrales de confianza y NMS (IoU) sobre la base de 448px.
*   **`exp_100-epoch_yolov8s_tunned`**: Rama con el primer ajuste fino (*fine-tuning*) de hiperparámetros tras un proceso de evolución/búsqueda.

### 🛠️ Técnicas Avanzadas y Refuerzo
*   **`exp_100-epoch_yolov8s_tunned_reinforced`**: Implementación de técnicas de refuerzo en el entrenamiento (ajustes de pesos o pérdida) sobre el modelo ya tuneado.
*   **`exp_100-epoch_yolov8s_tunned_reinforced_con_copy_paste`**: Introducción de la técnica de aumento de datos *Copy-Paste* para combatir el desbalance de clases o mejorar la detección de objetos pequeños.
*   **`exexp_100-epoch_yolov8s_tunned_reinforced_pero_con_copy_alto_cls_alto`**: Experimento extremo con altas tasas de *Copy-Paste* y mayor peso en la pérdida de clasificación (`cls`).

### 🧩 Innovaciones Arquitectónicas y Estrategias
*   **`exp_cbam_attention`**: Modificación de la arquitectura de la red para integrar módulos de atención **CBAM** (Convolutional Block Attention Module) con el fin de mejorar el foco en las regiones de interés del acero.
*   **`exp_slicing_256`**: Implementación de **Slicing Aided Hyper Inference (SAHI)** o técnicas de segmentación por ventanas de 256px para detectar micro-defectos que pasan desapercibidos en imágenes completas.
*   **`exp_doble_deteccion_modelo_nano_small`**: Estrategia de conjunto (*Ensemble*) o cascada utilizando modelos Nano y Small de forma combinada.

---

## 🛠️ Requisitos
Para replicar estos experimentos, se recomienda el uso de `ultralytics`:
```bash
pip install ultralytics
```

## 📊 Dataset
El proyecto utiliza el **NEU Surface Defect Database**, que incluye seis tipos de defectos superficiales en láminas de acero laminado en caliente: *rolled-in scale, patches, crazing, pitted surface, inclusion y scratches*.