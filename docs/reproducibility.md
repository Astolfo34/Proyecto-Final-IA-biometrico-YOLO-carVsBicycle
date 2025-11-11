# Reproducibilidad

Este documento describe los pasos y la configuración para reproducir resultados del proyecto.

## Semillas Aleatorias
- RANDOM_SEED: 42 (por defecto)

## Entorno
- Ejecución prevista: Google Colab.
- Instalar dependencias:
  - Ver `Z_ProyectoYolo/requirements.txt`.
- Versiones recomendadas:
  - ultralytics >= 8.x
  - Python 3.10+
  - torch (preinstalado en Colab)

## Estructura de Carpetas
Consultar el README del notebook y la estructura definida en el propio cuaderno. Todas las rutas relativas parten de `Z_ProyectoYolo/`.

## Pasos Básicos
1. Abrir `Z_ProyectoYolo/notebook.ipynb` en Colab.
2. Ejecutar las celdas en orden.
3. Ajustar `MODEL_BACKBONE`, `epochs`, `batch` según GPU disponible.
4. Al finalizar, descargar `entrega_final/entrega_final.zip`.

## Notas
- Si el dataset está desbalanceado, considerar técnicas de aumento de datos o recolección adicional.
- Documentar cualquier cambio de hiperparámetros en el informe final.
