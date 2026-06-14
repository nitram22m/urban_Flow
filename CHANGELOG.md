# Changelog

## [Sprint 1] - Ejercicio 01
### Added
- Inicializacion del repositorio Git en rama Sprint_1.
- Creacion de la estructura de directorios del proyecto.
- Creacion de README.md con objetivo e introduccion.
- Creacion de CHANGELOG.md.

## [Sprint 1] - Ejercicio 04
### Added
- Clase FineAnalyzer con encapsulamiento del DataFrame limpio.
- Metodo ranking_patentes: top 5 patentes mas multadas.
- Metodo ranking_horarios: top 5 horarios con mas multas.
- Metodo exceso_promedio: exceso medio como % sobre velocidad maxima.
- Metodo exceso_real_promedio: exceso medio en km/h.
- Metodo multas_por_ubicacion: conteo de multas por ubicacion.

## [Sprint 1] - Punto 07
### Added
- Redaccion de la conclusion del analisis en README.md.

## [Sprint 2] - Ejercicio 01
### Added
- Rama Sprint_2 creada desde Sprint_1.
- Estructura de directorios Sprint 2.
- Descarga y descompresión de urban_flow_plates.zip.
- README.md actualizado con objetivo Sprint 2.

## [Sprint 2] - Ejercicio 02
### Added
- Listado de imágenes con nombre y tamaño en KB.
- Separación en grupos 'plates' y 'completes'.
- Guardado de group_images.json en data/interim/.
- Función mostrar_muestras reutilizable.

## [Sprint 2] - Ejercicio 03
### Added
- Conversión a grises en 03_01_gray_scale/.
- Suavizado gaussiano en 03_02_blur/.
- Detección de bordes Canny en 03_03_canny/.
- Grillas de muestras por etapa de procesamiento.

## [Sprint 2] - Ejercicio 04
### Added
- Pipeline OCR: denoising, sharpening, cierre morfologico.
- 7 variantes de preprocesamiento por imagen.
- Seleccion por rango 4-10 chars alfanumericos.
- Filtrado geometrico con margen asimetrico en completes.
- Cruce LCS con ratio >= 0.80 soportando multas REINCIDENTES (1 imagen -> N multas).
- speeding_fines_image.csv en data/processed/.

## [Sprint 2] - Ejercicio 05
### Added
- Métricas: multas sin/con imagen e imgs sin match.
- Métricas: multas pendientes totales y con imagen.
- multas_imagen.jpg: distribución con/sin evidencia.
- top10_patentes_imagen.jpg: top 10 con match.

## [Sprint 2] - Ejercicio 06
### Added
- Conclusión del Sprint 2 agregada al README.md principal.
- Análisis de reincidentes (relación 1 a N entre imágenes y multas).
- Análisis impacto datos inválidos 00:00 y 1932-01-01.

## [Sprint 3] - Ejercicio 01
### Added
- Creé la rama Sprint_3 a partir de la 2.
- Chequeé que los datasets viejos sigan ahí.
- Actualicé el README con lo que vamos a hacer en este sprint.
