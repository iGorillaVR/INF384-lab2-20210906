============= 1.1============================
-PRIMER DEFECTO:
-¿Qué está mal? -> Duplicidad de código, 
-Archivo -> pipeline.yml
-Línea -> Para el paso "Descargar el codigo" (linea 14 y 47), "Preparar Python" (linea 20 y 50) e "Instalar dependencias" (linea 24 y 55)

-SEGUNDO DEFECTO:
-¿Qué está mal? -> Falta de caché en las dependencias de Python
-Archivo -> pipeline.yml
-Línea -> En ninguna de las dos ejecuciones se usa 'pip'. (linea 20 y 51)


-TERCER DEFECTO:
-¿Qué está mal? -> Falta de dependencia explícita entre los trabajos (needs)
Defecto: Los jobs validar y publicar se ejecutan en paralelo. El job publicar no tiene la propiedad needs: validar.
-Archivo -> pipeline.yml
-Línea -> "validar" y "publicar" se ejecutan en paralelo. Para que tenga sentido, debería haber un "needs" relacionado a "validar".

-CUARTO DEFECTO:
-¿Qué está mal? -> Falta de comillas en versión de Python
-Archivo -> pipeline.yml
-Línea -> (linea 22 y 53)

============= 1.2============================
En este caso el defecto relacionado con el tiempo registrado en la línea base esta directamente relacionado al PRIMER
DEFECTO. Porque se esta consumiendo tiempo repitiendo código.
Por ejemplo en mi linea base los tiempos finales de las 3 ejecuciones fueron: 1m 6s, 1m 29s y 54s

============= 1.3============================
En este caso relacionado al VSM se ve afecta la eficiencia del flujo debido a la "demora" adicional del pipeline por el 
código duplicado
============= 1.4============================
La métrica que se movería tras "arreglar" el código del pipeline sería: "Lead time para cambios" puesto que reduciríamos el tiempo
que demora en ejecutarse el pipeline,

============= 1.5============================
Vamos a medir el tiempo de ejecución del pipeline (basicamente lo que hemos registrado en el trabajo previo del laboratorio)


--------------------------------------------------------
4.1 Medición posterior
Se utilizó como proxy el tiempo total de ejecución del pipeline.

En la línea base se registraron las siguientes ejecuciones:

1m 6s = 66 segundos
1m 29s = 89 segundos
54s = 54 segundos
El promedio de la línea base fue de aproximadamente 69,67 segundos (1m 10s).

Después de la intervención, las ejecuciones registradas fueron:

-
-
-


La caché de dependencias reduce el trabajo necesario en ejecuciones posteriores.

4.2 Justificación de la versión
Se declaró la versión 1.3.0.

Esta versión corresponde a un incremento MINOR respecto de v1.2.0, debido a que los commits realizados después de ese tag incorporan nueva funcionalidad compatible con la versión anterior y no introducen cambios incompatibles que justifiquen un incremento MAJOR.

4.3 Lo que no se resolvió
El pipeline todavía presenta limitaciones. Una de ellas es la duplicación de pasos entre los jobs validar y publicar, como el checkout, la preparación de Python y la instalación de dependencias.

4.4 Declaración de uso de IA generativa
Se utilizó IA generativa como herramienta de apoyo durante el laboratorio, principalmente para comprender los requisitos del pipeline, identificar posibles problemas de configuración y orientar la corrección del workflow. Las decisiones finales, modificaciones realizadas en el repositorio, revisión de los commits, ejecución del pipeline y verificación de los resultados fueron realizadas y comprobadas por el estudiante.
