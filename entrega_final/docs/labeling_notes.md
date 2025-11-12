# Notas de Etiquetado

Este archivo recoge inconsistencias detectadas entre imágenes y archivos de etiquetas YOLO.

## Procedimiento de Verificación Automática
El notebook verifica:
1. Que cada imagen en `datasets/images/train` y `datasets/images/val` tenga su archivo `.txt` correspondiente en `datasets/labels/train` y `datasets/labels/val`.
2. Formato YOLO correcto por línea: `class x_center y_center width height` con 5 valores numéricos.
3. Clases válidas: 0 = bicicleta, 1 = auto.

## Imágenes sin etiqueta
(Pendiente de rellenar automáticamente por el notebook.)

## Archivos de etiqueta vacíos
(Pendiente de rellenar automáticamente por el notebook.)

## Recomendaciones
- Mantener consistencia en la iluminación y ángulo de captura.
- Evitar bounding boxes excesivamente grandes que cubran áreas irrelevantes.
- Verificar casos de oclusión parcial para mejorar robustez.


## Verificación automática

Fecha: 2025-11-11 17:06:08


## Verificación automática

Fecha: 2025-11-11 17:16:38


## Verificación automática

Fecha: 2025-11-12 08:38:32
