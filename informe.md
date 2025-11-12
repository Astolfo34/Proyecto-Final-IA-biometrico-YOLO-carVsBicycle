# Informe: Detección Bicicleta vs Auto (YOLOv8)

## 1. Problema y justificación
- Detectar y clasificar bicicletas y autos en imágenes para aplicaciones de tráfico y seguridad.

## 2. Dataset (formato YOLOv8)
- Ruta base: `./datasets`; usando: `./datasets/merged_bike_car`.
- Estructura: images/{train,val}, labels/{train,val}.
- Anotación: archivos .txt por imagen con (class cx cy w h).

## 3. Entrenamiento (configuración)
- Modelo: `yolov8n.pt` | IMGSZ=512 | EPOCHS=12 | BATCH≈4 | DEVICE=cpu.
- Optimizaciones: AdamW, cos_lr, early stopping (patience=3).

## 4. Resultados (métricas y figuras)
- precision: 0.8964
- recall: 0.7957
- mAP50: 0.8505
- mAP50-95: 0.6074
- Figuras en `./evaluation/figures`.
- Ejemplos cualitativos en `./inference/results_images`.

## 5. Conclusiones y mejoras
- Aumentar datos de la clase minoritaria si hay desbalance.
- Revisar anotaciones dudosas y homogeneizar criterios.
- Probar `yolov8s.pt` y más épocas si se dispone de GPU dedicada.