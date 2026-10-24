# Procedencia y fidelidad de la recuperación

Los tres cuadernos se recuperaron mediante la opción **Copy All Cells** de Colab. Se recibió un array JSON por cuaderno con sus celdas, fuentes, salidas y metadatos internos.

| Archivo del repositorio | Nombre de origen | Fuente |
| --- | --- | --- |
| `01-deteccion-manos-tiempo-real.ipynb` | `Untitled11.ipynb` | [Colab](https://colab.research.google.com/drive/1B1sKqviVwU1P4QfECw_5873DTu4n0cQJ) |
| `02-seguimiento-manos-diagnostico.ipynb` | `Untitled13.ipynb` | [Colab](https://colab.research.google.com/drive/11PojJsvWJWT3xuT4o0YFJiko2lRUxLJD) |
| `03-control-brazo-robotico-gestos.ipynb` | `Untitled15.ipynb` | [Colab](https://colab.research.google.com/drive/1FIJBkN0xG1JSir5UB3ugNX7QYCgzndC2) |

El envoltorio de cada archivo `.ipynb` se reconstruyó como `nbformat=4`, `nbformat_minor=0` y `metadata={}`. Las celdas se compararon mediante igualdad estructural exacta con los arrays exportados. Los archivos resultantes se copiaron al repositorio sin reserializarlos ni modificar su código.

No se obtuvo la descarga completa original de Drive. Por tanto, no se afirma que el hash del archivo reconstruido sea el del archivo original, ni que se hayan recuperado sus metadatos de raíz. Las celdas sí conservan sus metadatos originales disponibles, sus fuentes y sus salidas.

El inventario [originales.json](originales.json) registra el tamaño y SHA256 de cada exportación reconstruida, el SHA256 del array recibido desde la interfaz y un hash canónico de su estructura de celdas. Distingue explícitamente:

- `original_bytes_preserved=false`: no se dispone del archivo original completo.
- `export_file_bytes_preserved=true`: la copia del repositorio coincide byte por byte con la exportación reconstruida.
- `cells_preserved=true`: las celdas coinciden con el array exportado desde Colab.

Se analizaron las fuentes de las diez celdas sin ejecutarlas. Cuatro contienen Python sintácticamente válido y seis contienen comandos de instalación de IPython. Los mensajes de error y de instalación que aparecen son históricos; no son resultados generados durante la recuperación del 24 de octubre de 2026.

Los nombres descriptivos y la numeración facilitan la lectura del proyecto. No se utiliza el número de un cuaderno sin título como prueba de cronología.

## Fragmento no incorporado

[Untitled14.ipynb](https://colab.research.google.com/drive/107aF8ruNvLiTwLylgI3GsQqD9hxysQ9_) tiene una única celda con `python seguimiento_mano.py`. No contiene la implementación de ese archivo ni salidas. Se documenta su relación temática y se conserva en la copia de recuperación local, pero no se presenta como otro proyecto o variante funcional.

## Autoría y archivos externos

Las celdas no declaran autores, coautores, licencia o un enlace al código de un tercero. Los nombres de las bibliotecas identifican dependencias, no la autoría de los cuadernos. No hay firmware de Arduino, planos del brazo, archivos de entrenamiento ni datos privados de cámara añadidos al repositorio.
