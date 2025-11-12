# Análisis del Informe y Cumplimiento de Requisitos

Este documento analiza el informe generado (`Z_ProyectoYolo/informe.md`) y justifica cómo los resultados se relacionan con los requisitos del proyecto definidos en la estructura del trabajo.

## Propósito del informe
- Comunicar de forma breve (3–5 páginas) el objetivo, la preparación/uso del dataset, la configuración de entrenamiento, los resultados cuantitativos (Precision, Recall, mAP@0.5) y ejemplos cualitativos de inferencia.
- Dejar trazabilidad de las decisiones (modelo elegido, hiperparámetros, augmentaciones por defecto) y proponer mejoras futuras.

## Trazabilidad en la estructura del trabajo
A continuación se mapea cada sección/entregable solicitado a su evidencia:

1) Setup
- Instalación mínima (`ultralytics`, `opencv-python-headless`, `matplotlib`, `pandas`, `pyyaml`).
- Variables definidas: `PROJECT_ROOT`, `DATASET_ROOT`, `RANDOM_SEED`, `DEVICE` y carpetas de salida.  
Evidencia: primeras celdas del notebook (sección 0) y `print` de versiones.

2) Objetivo y justificación
- Descripción breve del problema (detección bici/auto) y utilidades (tráfico, seguridad, estacionamientos).  
Evidencia: celda 1 del notebook y primera sección del informe.

3) Verificación de dataset (YOLOv8 mínimo)
- Comprobación de `images/train`, `images/val|valid`, `labels/train`, `labels/val|valid`.
- Conteo de imágenes y verificación de `.txt` pareados, conteo por clase y advertencias por bajo soporte.  
Evidencia: celda 2 del notebook (mensajes de conteo y advertencia si <50 instancias).

4) Visualización rápida
- Muestra 6–8 imágenes con cajas a partir de labels.  
Evidencia: celda 3 + figura `evaluation/figures/dataset_samples.png`.

5) data.yaml
- Crear/usar `data.yaml` con `train`, `val`, `nc=2`, `names=['bicicleta','auto']`.  
Evidencia: celda 4, impresión del contenido.

6) Selección de modelo
- `MODEL_BACKBONE = yolov8n.pt` (opcional `yolov8s.pt`), trade-off velocidad/precisión.  
Evidencia: celda 5, mensajes impresos.

7) Entrenamiento básico
- `yolo detect train` con `imgsz`, `epochs`, `batch`, `project=runs`, `name=exp_bici_auto`.  
- Early stopping y configuración segura para CPU/GPU.  
Evidencia: celda 6, carpeta `runs/exp_bici_auto` con `best.pt`.

8) Métricas y gráficos
- Extraer Precision, Recall, mAP@0.5; graficar pérdidas y P/R/mAP.  
Evidencia: celda 7, figuras en `evaluation/figures/` y `evaluation/metrics/metrics.json`.

9) Inferencia
- Sobre `images/val|valid` y `inference/images_new/` cuando existan.  
- Guardar resultados en `inference/results_images/` y mostrar ejemplos.  
Evidencia: celda 8, carpeta `inference/tmp_pred/predict*` y copias en `inference/results_images/`.

10) Entrega mínima
- Copiar `best.pt` a `modelo/best.pt`.  
- Confirmar existencia de `data.yaml`, `modelo/best.pt`, `inference/results_images/*`.  
Evidencia: celda 6 (copiado), celda 8 (resultados), informe generado en celda 9.

## Justificación de los resultados
- Métricas: `Precision`, `Recall`, `mAP@0.5` miden la calidad de detección y localización. El `mAP@0.5` es estándar en detección y facilita comparar variantes (nano vs small) y diferentes épocas.
- Visuales: ejemplos cualitativos de validación y de imágenes nuevas permiten detectar over/underfitting y problemas de rotulación.
- Decisiones técnicas: `yolov8n.pt` prioriza tiempos razonables en CPU/Colab; las augmentaciones por defecto (mosaic, flips, hsv) y early stopping ayudan a converger con pocas épocas.
- Fusión de datasets: al unificar fuentes y remapear ids (bicicleta→0, auto→1), se asegura consistencia de clases y se aprovechan más ejemplos; la verificación de `val|valid` cubre distintos orígenes (Roboflow).

## Cumplimiento de requisitos
- Ejecutable en Colab/local con dependencias mínimas: Sí.
- Uso de rutas relativas dentro de `Z_ProyectoYolo`: Sí.
- Verificación y visualización de dataset: Sí.
- Entrenamiento con YOLOv8 y parámetros básicos: Sí.
- Métricas y figuras guardadas: Sí.
- Inferencia sobre validación e imágenes nuevas: Sí.
- Entrega mínima (`best.pt`, `data.yaml`, `results_images`, `informe.md`): Sí.

## Riesgos y mejoras
- Desbalance de clases o baja cobertura (<50 instancias) penaliza métricas; se recomienda recolectar/anotar más ejemplos.
- Cambiar a `yolov8s.pt` y aumentar épocas en GPU puede mejorar mAP.
- Curar muestras atípicas, revisar labels dudosos y ajustar umbrales de confianza/IoU.
