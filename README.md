# Control de brazo robótico mediante gestos

Prototipo de visión por computador que transforma los puntos de una mano capturada por webcam en comandos para tres servos de un brazo robótico. Utiliza OpenCV para el vídeo, MediaPipe Hands para los puntos de la mano y PySerial para enviar las órdenes a Arduino.

El repositorio conserva tres cuadernos relacionados: dos pruebas de detección de manos y una versión que incorpora el control del brazo. Sus celdas, comentarios y salidas se recuperaron desde Colab sin modificar el código. Los archivos `.ipynb` tienen un envoltorio reconstruido, con metadatos de raíz vacíos; no se dispone de la descarga original completa. La procedencia y los hashes están en [ORIGEN.md](docs/ORIGEN.md).

## Cuaderno principal

Abre [03-control-brazo-robotico-gestos.ipynb](notebooks/03-control-brazo-robotico-gestos.ipynb) para leer el prototipo completo.

La lectura de su código muestra este recorrido:

1. Abrir el puerto serial `COM46` a 9600 baudios y esperar dos segundos.
2. Capturar la cámara `0` y reflejar horizontalmente cada fotograma.
3. Detectar los puntos de la mano con MediaPipe Hands y dibujarlos.
4. Calcular los ángulos de la base, la extensión y la pinza.
5. Enviar tres líneas de texto por cada mano detectada y mostrar las coordenadas y los ángulos en una ventana de OpenCV.
6. Terminar con la tecla Escape y cerrar los recursos cuando se llega al final del bucle.

## Cuadernos conservados

| Archivo | Contenido | Nombre de origen |
| --- | --- | --- |
| [01-deteccion-manos-tiempo-real.ipynb](notebooks/01-deteccion-manos-tiempo-real.ipynb) | Detección de hasta dos manos, dibujo de puntos y conexiones, y pruebas de instalación. | `Untitled11.ipynb` |
| [02-seguimiento-manos-diagnostico.ipynb](notebooks/02-seguimiento-manos-diagnostico.ipynb) | Otra configuración de detección de manos y comprobación de versiones de NumPy y MediaPipe. | `Untitled13.ipynb` |
| [03-control-brazo-robotico-gestos.ipynb](notebooks/03-control-brazo-robotico-gestos.ipynb) | Seguimiento de palma, índice y pulgar; conversión a ángulos y envío serial a tres servos. | `Untitled15.ipynb` |

La numeración organiza la lectura de las pruebas al prototipo; no acredita una cronología de desarrollo. Los tres archivos contienen código diferente y pertenecen al mismo tema. No se incluyó como proyecto independiente `Untitled14.ipynb`, que solo contenía `python seguimiento_mano.py` sin el archivo mencionado.

## Conversión de gestos a comandos

| Elemento | Entrada utilizada por el código | Ángulo limitado | Línea enviada |
| --- | --- | --- | --- |
| Base | Coordenada X de la muñeca, punto 0 denominado palma en el código. | 0 a 180 grados | `1 <angulo>` |
| Extensión | Coordenada Z del mismo punto, acotada al intervalo -0.2 a 0.1. | 90 a 180 grados | `3 <angulo>` |
| Pinza | Distancia euclidiana entre las puntas del pulgar y el índice, puntos 4 y 8. | 50 a 110 grados | `2 <angulo>` |

Cada orden termina en un salto de línea. El significado mecánico de esos identificadores y la posición de apertura o cierre dependen del firmware y del montaje, que no están incluidos. El código no documenta una calibración de distancia física para la coordenada Z.

## Tecnologías y dependencias

- Python.
- OpenCV: captura de cámara, conversión de color, ventanas y anotaciones.
- MediaPipe Hands: detección y seguimiento de puntos de la mano mediante `mp.solutions.hands`.
- PySerial: comunicación con Arduino.
- NumPy: dependencia de la pila de visión y comprobación de versión en el cuaderno `02`.

[requirements.txt](requirements.txt) enumera las dependencias directas como referencia. No es un entorno bloqueado ni una combinación validada. Las salidas históricas registran, entre otras versiones, MediaPipe 0.10.21, OpenCV 4.11.0.86 y PySerial 3.5; también registran instalaciones incompatibles de NumPy.

## Qué hace falta para retomarlo

El código de cámara y puerto serial requiere un entorno local con webcam accesible y ventanas de OpenCV. Una sesión remota estándar de Colab no proporciona directamente la cámara `0` ni el puerto `COM46` de un ordenador personal.

Para trabajar sobre una copia de los cuadernos hace falta:

1. Preparar un entorno local compatible con la API de MediaPipe utilizada y revisar las instalaciones históricas antes de repetirlas.
2. Aportar el Arduino, el brazo y su firmware; el repositorio no contiene un programa `.ino`, esquema de conexiones ni asignación de pines.
3. Ajustar en la copia de trabajo el puerto serial, la cámara y la conversión de ángulos al montaje real. La primera celda del cuaderno principal abre el puerto y comienza a enviar órdenes cuando detecta una mano.
4. Revisar el orden de ejecución: las celdas de instalación del cuaderno principal aparecen después de la celda que importa las bibliotecas y controla el hardware.

Las pruebas `01` y `02` se limitan a la cámara y no envían órdenes seriales. En ellas, la tecla de salida es `q`.

## Estado de los experimentos

Este repositorio documenta un prototipo recuperado. Las salidas guardadas no demuestran una sesión de control del brazo funcionando:

| Cuaderno | Evidencia guardada |
| --- | --- |
| `01` | Instalaciones con conflictos de dependencias y un `NameError` relacionado con `audio_classifier`. |
| `02` | Incompatibilidad binaria de NumPy al importar la pila de visión y un `NameError` relacionado con `core`. |
| `03` | Incompatibilidad binaria de NumPy en la celda principal; instalación posterior de MediaPipe y PySerial. |

No se añadieron capturas de una ejecución nueva ni se afirmó que el hardware haya sido probado. Los errores históricos se conservan dentro de los cuadernos. [LIMITACIONES.md](docs/LIMITACIONES.md) recoge los detalles de entorno y del control serial.

## Conservación y validación

Los tres archivos publicados son copias exactas de los archivos reconstruidos durante la recuperación. Se compararon estructuralmente sus diez celdas con los arrays exportados mediante **Copy All Cells** de Colab. Se conservaron las once salidas guardadas y los metadatos internos de las celdas. Los metadatos de raíz originales no estaban disponibles y no se inventaron.

Cuatro celdas contienen Python válido según un análisis estático de sintaxis. Las otras seis contienen comandos de instalación propios del entorno de cuadernos; no se trataron como errores del algoritmo. No se ejecutaron celdas, no se instaló software y no se accedió a la cámara ni al puerto serial durante esta recuperación.

## Autoría

Los cuadernos fueron proporcionados por el propietario de esta cuenta. Sus celdas no incluyen una declaración explícita de autores, coautores o licencia. Este repositorio no añade una licencia de redistribución ni atribuye el código a una fuente que no figure en los archivos.

La IA se utilizó como herramienta de aceleración de procesos para la organización y documentación del repositorio.
