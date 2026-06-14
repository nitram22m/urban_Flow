# Urban Flow - Sprint 1

## Sprint actual: Sprint 1

## Objetivo
Aplicar conocimientos de versionado de codigo, organizacion,
limpieza del codigo y utilizacion de pandas para analizar
infracciones de velocidad en la localidad de Vaalserberg.

## Introduccion y contexto
La localidad de Vaalserberg (Belgica), en zona fronteriza
con Paises Bajos y Alemania, cuenta con radares urbanos
para deteccion de infracciones por exceso de velocidad.
Los registros historicos provienen de sistemas heredados
con errores de formato y datos faltantes que generan
inconsistencias en el nuevo sistema.
El objetivo es analizar y depurar los datos del viejo
sistema para incorporarlos al nuevo sin inconsistencias.


## Conclusion del analisis - Sprint 1

El dataset original contenia alrededor de 4000 registros de infracciones
de velocidad provenientes de un sistema heredado. Tras la normalizacion
y limpieza, se obtuvieron los registros que efectivamente representan
una infraccion (velocidad registrada superior al limite con tolerancia
del 5%).

Los principales hallazgos son:

- Las ubicaciones con mayor cantidad de infracciones son avenidas
  principales, lo que sugiere que los radares estan correctamente
  ubicados en zonas de alto flujo vehicular.

- Una fraccion significativa de los registros presentaba fechas
  invalidas que fueron normalizadas a 1932-01-01, lo que indica
  problemas de calidad en el sistema heredado.

- La hora 00:00 agrupa tanto capturas reales de medianoche como
  todas aquellas horas que no pudieron ser interpretadas. Por
  consigna, las horas invalidas se procesan como 00:00, por lo
  que este valor no puede tomarse como referencia horaria
  confiable sin un analisis adicional de la fuente original.

- Aproximadamente la mitad de los registros del dataset original
  carecian de velocidad_registrada o de patente, lo que evidencia
  problemas serios de captura en el sistema viejo y refuerza la
  necesidad de migrar al nuevo sistema.

- El exceso de velocidad real promedio entre los infractores
  supera ampliamente el limite permitido, lo que representa un
  riesgo significativo para la seguridad vial de la localidad.

# Urban Flow - Sprint 2

## Objetivo
Determinar qué multas de velocidad cuentan con evidencia visual válida mediante OCR sobre imágenes de radares urbanos.

## Introducción y contexto
Los radares urbanos generan registros administrativos automáticos y las cámaras asociadas registran la evidencia visual. No todas las multas tienen imagen asociada, no todas las imágenes corresponden a una infracción y puede haber errores de detección OCR.

## Sprint actual
Sprint 2: procesamiento de imágenes con OpenCV y extracción de patentes con Tesseract OCR.

## Conclusión - Sprint 2

### Relación entre imágenes y datos tabulares (Reincidentes)

En este sprint integramos dos fuentes de datos: el dataset de multas del Sprint 1 y las imágenes de los radares.
Cruzamos ambas usando OCR para determinar qué multas tienen evidencia visual válida.
Descubrimos que la relación es de **1 a N** (una imagen puede corresponder a múltiples multas) dado que existen vehículos reincidentes que cometieron varias infracciones de velocidad. Por lo tanto, el cruce itera sobre el listado de multas y le asigna la imagen que mejor coincida con su patente.

### Pipeline de procesamiento implementado

Construimos un pipeline de cuatro etapas con OpenCV: conversión a grises, suavizado bilateral, detección de bordes con Canny adaptativo y extracción OCR con Tesseract.
Para mejorar la lectura de patentes agregamos cierre morfológico rectangular, sharpening con kernel 3x3, umbralización OTSU en múltiples variantes y filtrado geométrico por área y relación de aspecto (2.0 a 6.5).

### Impacto de los registros con hora 00:00 y fecha 1932-01-01

Decidimos conservar estas filas porque representan multas reales cuyo valor temporal no pudo parsearse en el Sprint 1. Participan del cruce con imágenes y pueden tener coincidencia visual, pero sus fechas y horas no son confiables para análisis cronológico. Cualquier métrica por franja horaria o período que las incluya debe interpretarse con precaución.

### Resultados y Multas sin evidencia visual

Una parte del dataset no obtuvo coincidencia con ninguna imagen (851 multas). Las causas pueden ser: que la patente no figure en el set de fotos, o que el OCR no haya podido extraer el texto correctamente.
Sin embargo, al soportar reincidentes, logramos asignar imágenes válidas a 834 multas (usando las 31 fotografías que superaron el umbral de similitud del 80% mediante LCS de izquierda a derecha).

### Conclusión general

El trabajo de este sprint nos permitió vincular la evidencia fotográfica con los registros administrativos contemplando la reincidencia vehicular. La arquitectura de pipeline por etapas que desarrollamos facilita iteraciones futuras para mejorar el porcentaje de extracción OCR.

# Urban Flow - Sprint 3

## Sprint actual: Sprint 3

## Objetivo
Profesionalizar la solución incorporando persistencia relacional (SQLAlchemy), control de versiones de datos (DVC) y búsqueda vectorial por similitud (ChromaDB + OpenCLIP).

## Introducción y contexto
El volumen de datos creció bastante, así que pasamos de usar archivos CSV a una base de datos SQLite llamada `transito` usando SQLAlchemy. También metimos DVC para no subir archivos pesados a Git, y armamos un buscador de patentes por imágenes con ChromaDB.
