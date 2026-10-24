# Limitaciones del prototipo conservado

## Entorno original con errores

Las salidas registran instalaciones de MediaPipe 0.10.21 que requieren NumPy menor que 2, junto con otras bibliotecas del entorno que esperan versiones diferentes. En `01`, una celda actualiza NumPy a 2.2.5 y otra instalación vuelve a 1.26.4. En `02` se imprime 2.0.2 antes de un fallo de importación. Los conflictos y los errores de compatibilidad binaria se mantienen en los originales.

Estas salidas no permiten afirmar que la combinación instalada llegara a ejecutar el seguimiento de manos o a controlar un brazo. No se corrigieron dependencias dentro de los cuadernos. El archivo de requisitos es un inventario de dependencias directas, no una garantía de compatibilidad actual.

Los comandos `!pip install` y `pip install` se interpretan en el entorno de cuadernos mediante IPython; no son sentencias de Python estándar para copiar sin cambios a un archivo `.py`.

## Cámara, ventanas y hardware local

Los tres programas abren `cv2.VideoCapture(0)` y muestran una ventana con `cv2.imshow`. Necesitan una cámara accesible desde el proceso y un entorno gráfico compatible. El código no incluye captura de cámara a través de JavaScript del navegador.

El cuaderno `03` intenta abrir `COM46` a 9600 baudios antes de capturar vídeo. No comprueba si ese puerto existe ni permite seleccionarlo mediante una interfaz. No incluye el firmware que interpreta las líneas de texto enviadas, el mapa de pines o las características mecánicas del brazo.

## Conversión de coordenadas

La base utiliza la coordenada X del punto 0. La extensión transforma directamente la coordenada Z de ese punto a un intervalo de ángulos. El código no incluye una calibración que relacione esa coordenada con la distancia física de la mano o con el recorrido mecánico del brazo.

La pinza utiliza la distancia entre los puntos 4 y 8. Los límites de distancia y ángulo están fijados en el código. No se documenta una calibración del montaje para determinar la posición física correspondiente a cada ángulo.

## Envío serial y recursos

Cada mano detectada produce tres escrituras seriales por fotograma. No hay selección persistente de una mano controladora, filtrado temporal de los ángulos, límite explícito de frecuencia de órdenes, lectura de confirmaciones del Arduino ni protocolo de recuperación de la conexión.

Cuando se dejan de detectar manos, el programa no envía una instrucción nueva para ese caso. El comportamiento resultante del hardware depende del firmware externo, que falta.

El cierre de cámara, ventanas y puerto aparece al final del programa, sin un bloque `try/finally` que garantice ese cierre ante una excepción. Estas observaciones describen el código archivado; no se han aplicado cambios a sus celdas.
