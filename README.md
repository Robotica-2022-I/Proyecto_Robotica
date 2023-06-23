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

El objetivo de este proyecto es tomar un balde de una banda transportadora ubicada cerca del manipulador, dejarlo en algún lugar en el espacio de trabajo y tomar 3 de 6 posibles piezas de una estantería para depositarlas en el balde, volver a tomarlo y llevarlo devuelta a la banda transportadora.

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
Las piezas se diseñaron como circunferencias de 7cm con apoyos para darles un ángulo de 55° respecto a la horizontal. Esto con el objetivo de que se tuviera un área suficiente para que la ventosa no presentara problemas en el agarre y la inclinación para que la herramienta pueda acceder de forma sencilla a la mismas.

![Imagen 2](https://github.com/Robotica-2022-I/Proyecto_Robotica/blob/main/Imagenes%20proyecto/Piezas.jpg)

# 3) Planos y fotografias herramienta
La herramienta se construyó buscando que esta sostuviese tanto el gancho como la válvula. Se diseñó con inventor para posteriormente ser impresa en 3D. A continuación se presenta el modelado de la herramienta y el resultado en físico.

![Imagen 2](https://github.com/Robotica-2022-I/Proyecto_Robotica/blob/main/Imagenes%20proyecto/medidaspng.png)

La herramienta fue diseñada en 3 partes de forma que en caso de que alguna llegara a dañarse se pudiera reemplazar de forma sencilla y económica. 
1. La base de la herramienta que tiene el acople para conectarese al ABB.
2. El cilindro donde se instala el gancho.
3. La abrazadera en forma de T la cual se encarga de sostener la ventosa.

El modelo en inventor con el gancho y la ventosa queda de la siguiente forma:
![Imagen 3](https://github.com/Robotica-2022-I/Proyecto_Robotica/blob/main/Imagenes%20proyecto/ensamble.png)

El resultado en físico de la herramienta se aprecia en las siguientes imágenes (sin gancho-ventosa y con ellos):
![Imagen 4](https://github.com/Robotica-2022-I/Proyecto_Robotica/blob/main/Imagenes%20proyecto/Herramienta%20en%20físico.jpg)
![Imagen 5](https://github.com/Robotica-2022-I/Proyecto_Robotica/blob/main/Imagenes%20proyecto/Herramienta_gancho.jpg)


# 4) RobotStudio
En el código de robostudio se tiene una estanteria, con medidas reales, las piezas fabricadas (ya con su inclinación), la banda transportadora, el balde y el brazo robot, como se puede apreciar en las siguientes imagenes:

![Imagen 6](https://github.com/Robotica-2022-I/Proyecto_Robotica/blob/main/Imagenes%20proyecto/inventor.png)

![Imagen 7](https://github.com/Robotica-2022-I/Proyecto_Robotica/blob/main/Imagenes%20proyecto/estanteria.png)

![Imagen 8](https://github.com/Robotica-2022-I/Proyecto_Robotica/blob/main/Imagenes%20proyecto/banda.png)

En este software se hace la programación de todas las rutinas y trayectorias para el desarrollo del proyecto, se habla en detalle en el apartado del código en RAPID.

# 5) Código de RAPID
El código RAPID empleado se encuentra adjunto a este repositorio, en la carpeta "Proyecto_rob". El código que se sube al ABB  se llama "Proyecto_rob.pgf"

Al inicio del código podemos encontrar la ubicación de todos los puntos necesarios para el desarrollo de las rutinas, las cuales son 14, 6 Para tomar cada pieza de la estantería, 6 para depositarlas en el balde, 1 para tomar el balde de la banda y llevarlo a un punto cercano y 1 última para tomar el balde en ese punto y devolverlo a la banda. Un ejemplo de proceso  de la pieza 1, se presenta a continuación:

```
    PROC Pieza_1B()
        MoveJ Target_23,v100,z100,Ventosa\WObj:=WorkEstante;
        MoveJ Target_183,v300,z100,Ventosa\WObj:=WorkBanda;
    ENDPROC
```
Cabe aclarar que, este código es resultante de la rutina creada en RoboStudio.


Dentro del main se encuentra toda la lógica para realizar las acciones en orden, las condiciones de entradas y salidas para iniciar las secuencias y evidenciar cuál se está trabajando, así como el accionamiento de la válvula que permite el funcionamiento de la ventosa. Un ejemplo de lógica del Main, en este caso para la pieza 1, se presenta a continuación: 

```
            Pieza_1;
            WAITTIME 0.25;
            SetDO DO_02,1;
            WAITTIME 2;
            SetDO DO_02,0;
            Pieza_1B;
            WAITTIME 2;
            SetDO DO_01,1;
            WAITTIME 2;
            SetDO DO_01,0;
```

Esta rutina sigue los siguientes pasos:

  -  Llama los puntos para ir a la pieza 1 
  -  Espera 0.25s y activa la válvula de succión (DO_02,0)
  -  Se desactiva dicha válvula, ya que el robot ya se encuentra succionando la pieza
  -  Se llaman los puntos para desplazar y dejar las piezas en el balde
  -  Se envia la señal para detener el aire
  -  Se esperan 2s para que la pieza caiga en el balde
      
# 6) Comparación de tiempos
Se midió el tiempo para una rutina completa y para la ubicación de las piezas a mano:

  - Una rutina completa en promedio dura 1:25 min
  - Una rutina de selección a mano dura alrededor de 2:00 min 

Inicialmente no se llegaria a la conclusión de  35s de diferencia fuese un tiempo significativo, sin embargo si la selección de píezas se lleva a escala industrial la cantidad vez en que puede repetirse este proceso pasa de 30 a 48 veces en una hora. Esto sin contar que una persona siente los efectos del cansancio.


# 7) Video de sustentanción

[![Alt text](https://img.youtube.com/vi/2l879iaXXKw/0.jpg)](https://www.youtube.com/watch?v=2l879iaXXKw)

