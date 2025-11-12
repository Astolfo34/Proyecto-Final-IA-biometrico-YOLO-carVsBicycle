# Proyecto YOLOv8: Detección de Autos vs Bicicletas

Este proyecto entrena y evalúa un detector de objetos (YOLOv8) para clasificar y localizar dos clases: bicicletas y autos. Se centra en un flujo reproducible, sencillo de ejecutar en Google Colab o en CPU local, y produce métricas y resultados visuales mínimos requeridos para un analisis basico

## Propósito
- Construir un detector práctico para escenarios de tráfico, como para estacionamientos inteligentes y seguridad por ejemplo.
- Integrar datasets preanotados en formato YOLOv8, verificarlos, entrenar un modelo base, evaluar métricas clave (Precision, Recall, mAP@0.5) y generar inferencias.

## Librerías y por qué se usan
- Ultralytics YOLOv8: framework de alto nivel para entrenamiento e inferencia de modelos YOLO (v8), con CLI y API en Python, soporte de augmentaciones y logging de métricas.
- PyTorch: backend de cómputo para el entrenamiento e inferencia del modelo.
- OpenCV (headless): lectura/escritura de imágenes y utilidades de visualización en entornos sin GUI.
- Matplotlib: generación de figuras de pérdidas y métricas (curvas de entrenamiento y P/R/mAP).
- Pandas: lectura de `results.csv` y agregación de métricas para reporte.
- PyYAML: lectura/escritura de `data.yaml` (rutas de train/val, nombres de clases y conteos).

## Modelos y variantes
- `yolov8n.pt` (nano): enfoque por defecto en entornos con recursos limitados; rápido y ligero.
- `yolov8s.pt` (small): alternativa con mayor capacidad a costa de más cómputo; recomendable si se dispone de GPU.

Elección: por compatibilidad y tiempos en Colab gratuito o CPU, el flujo usa `yolov8n.pt` por defecto, y sugiere `yolov8s.pt` en caso de GPU.

## Estructura de carpetas relevante
- `Z_ProyectoYolo/datasets/`  
  - `bicycle.v1i.yolov8/` y `Car.v5-car_4.yolov8/`: datasets fuente (formato YOLOv8).
  - `merged_bike_car/`: versión fusionada de ambos datasets (bicicleta→id 0, auto→id 1).
- `Z_ProyectoYolo/runs/`: salidas de entrenamiento (Ultralytics).
- `Z_ProyectoYolo/evaluation/`  
  - `figures/`: figuras de aprendizaje y PR/mAP.
  - `metrics/`: `metrics.json` y/o CSV con métricas finales.
- `Z_ProyectoYolo/inference/`  
  - `images_new/`: imágenes propias para pruebas.
  - `results_images/`: predicciones exportadas.
- `Z_ProyectoYolo/modelo/`: copia de `best.pt` para entrega.
- `Z_ProyectoYolo/informe.md`: informe breve (3–5 páginas).

## Flujo de alto nivel
1. Verificar datasets (estructura YOLOv8 con splits `train` y `val`/`valid`) y contar instancias por clase.
2. Si falta un dataset combinado, fusionar automáticamente los dos conjuntos fuente y remapear ids.
3. Crear/usar `data.yaml` apuntando a `train` y al split de validación detectado.
4. Entrenar (`yolo detect train`) con hiperparámetros básicos.
5. Extraer métricas (Precision, Recall, mAP@0.5), generar gráficos y guardar en `evaluation/`.
6. Ejecutar inferencia sobre `images/val` y `inference/images_new/` y exportar resultados a `inference/results_images/`.
7. Copiar `best.pt` a `modelo/best.pt` y generar `informe.md` con resultados y conclusiones.

## Consideraciones de rendimiento
- En CPU, priorizar `yolov8n.pt`, menor batch y resolución moderada (p. ej., 512). 
- En GPU, se puede escalar a `yolov8s.pt`, `imgsz=640` y batch mayor.
- Early stopping (patience baja) acelera la obtención de un resultado funcional.

## Reproducibilidad
- Se fija una semilla (`RANDOM_SEED`).
- Se registran versiones de `ultralytics` y `torch` al inicio del cuaderno.
- Rutas relativas dentro de `Z_ProyectoYolo` para facilitar replicación en Colab/otros entornos.

## Limitaciones y mejoras
- El desempeño depende de la calidad y el balance del dataset. Si alguna clase tiene <50 instancias, se recomienda ampliar o reanotar.
- Para mejores resultados: más épocas, cambios de backbone (`yolov8m/l`), y más datos.
