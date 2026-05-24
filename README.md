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
