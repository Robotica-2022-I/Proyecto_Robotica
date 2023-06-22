# Proyecto_Robotica
Descripción, códigos y video de implementación del proyecto de robótica 


Daniel Felipe Cantor Santana

Juan David Morales Restrepo

David Leonardo Cocoma Reyes 



# 1) Requisitos

- Robot Studio versión 2021 o superior INSTALADO y activo.
- Manipulador industrial ABB IRB 140.
- Herramienta personalizada con ventosas y gancho para el brazo IRB 140.
- Banda transportadora del LabSIR, apagada.
- Estantería de madera y balde metálico.

# 2) Descripción

Con el proyecto se busco tomar 3 de 6 piezas de una la estantería para ser ubicadas en el balde. De la misma manera el bande debe variar su posición, salir de una posición inicial y volver tras un tiempo.

## Proceso de alistamiento
Se cuenta en el laboratorio con robot ABB IBR 140, una banda transpostadora y una estanteria, junto algunas cajas que pueden servir como apoyo en caso de que se requiera. El robot y la banda ya poseen posiciones fijas que se recomiendan no cambiar (ya que esto podria perjudicar el trabajo de los demas equipos de trabajo), por otro lado las estanterias pueden tener la ubicación que se desea. La disposición empleada se presenta en la siguiente figura:

![Imagen 1](https://github.com/Robotica-2022-I/Proyecto_Robotica/blob/main/Imagenes%20proyecto/Brazo%20armado.jpg)
Ademas como se logra ver, la "planta de trabajo" debe poseer un testigo que demuestre el funcionamiento del proceso (el LED en verde de la foto).

## Herramientas
Entre las herramientas empleadas en el laboratorio se tienen:

  - Una ventosa
  - Un suministro de aire comprimido
  - Un gancho

## Piezas
Las piezas se diseñaron como circunferencias de 7cm con apoyos para darles un ángulo de 45° respecto a la horizontal.

--------------------------------------------------FIGURA DE LAS PEIZAS--------------------------------------------------------------------------------------

# 3) Planos y fotografias herramienta
La herramienta se construyó buscando que esta sostuviese tanto el gancho como la válvula. Se diseñó con inventor para posteriormente ser impresa.A continuación se presenta el modelado de la herramienta y el resultado en físico.


------------------------------------------------------FOTOS HERRAMIENTA E INVENTOR XD-------------------------------------------------------------------

# 4) RobotStudio
En el código de robostudio se tiene una estanteria, con medidas reales, las piezas fabricadas (ya con su inclinación), la banda transportadora, el balde y el brazo robot, como se aprecia en la siguiente imagen:


----------------------------------------------------------PANTALLAZO ROBOSTUDIO------------------------------------------------

# 5) Código de RAPID
El código RAPID empleado se encuentra adjunto a este repositorio. Dicho código contienen una rutina por pieza, una para tomar el balde y otra para dejarlo en su posición original.

---------------------------------------------------------Explicar mejor------------------------------------------


# 6) Comparación de tiempos


------------------------------------------------------TOMAR TIMEPO MAÑANA---------------------------------------------------------

# 7) Video de sustentanción

---------------------------------------------------------Hacer video de sustentanción------------------------------------------------------------------

