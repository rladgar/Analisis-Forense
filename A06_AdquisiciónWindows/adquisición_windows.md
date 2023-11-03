# A06. Realizar la adquisición forense (en vivo) de una máquina windows (memoria volátil y no volátil) usando las herramientas que estimes pertinentes.

## Índice

1. [Introducción](#introducción)
2. [Memoria volátil](#memoria-volátil)
3. [Memoria no volátil](#memoria-no-volátil)
4. [Conclusión](#conclusión)

## Introducción

En esta actividad llevaré a cabo la adquisición forense de una máquina virtual con el sistema operativo Windows 10 aplicando la fase de adquisición de mi metodología propia que he creado junto a mi grupo (Grupo 3). Mi enfoque será garantizar la integridad de las evidencias, considerando el orden de volatilidad de las mismas y realizando triage para identificar todas las posibles evidencias existentes.

Para ello, como no dispongo de disco duro externo, he creado una carpeta compartida en Virtual Box de forma que me permita almacenar las evidencias en mi máquina local.

Antes de empezar, he desactivado el antivirus de la máquina virtual en la que voy a realizar la adquisición forense para evitar posibles errores durante el proceso.


![Alt text](img/1.png)

## Memoria volátil

La primera adquisición que he realizado es de la información del sistema (hora,fecha, hora de inicio del sistema y procesos) y de la red (interfaces, tablas de enrutamiento y caché). Para ello, utilizando un terminal los capturo directamente a mi disco externo:

- La información del sistema:

![Alt text](img/4.png)

- La información de la red:

![Alt text](img/5.png)

Registros en el disco duro externo:

![Alt text](img/6.png)

Seguidamente he realizado la adquisición de la memoria *ram* para respetar el orden de volatilidad de las evidencias y mantener la mayor integridad posible de las mismas. 
Procedo a capturar la **memoria ***ram***** con la ayuda de la herramienta ***"DumpIT"*** ejecutándola directamente desde el ejecutable como administrador ya que según el estudio realizado por el usuario @_N4rr34n6_ (https://unminioncurioso.blogspot.com/2020/10/impacto-de-las-herramientas-en-la.html) es la herramienta que menos espacio ocupa en memoria por lo que podré capturar una mayor cantidad de información:

![Alt text](img/2.png)

Una vez finalizado el proceso, obtengo la imagen de la memoria *ram*:

![Alt text](img/3.png)


Tras adquirir la memoria, procedo a realizar triage con la ayuda de la herramienta ***WINTRIAGE*** para identificar todas las posibles evidencias, obtener informes de los registros, eventos, información de usuarios en el sistema, una segunda adquisición de ram con RawCopy, etc.. :

En cuento a los módulos utilizados, los he marcado todos menos el de la imagen del disco duro ya que esa adquisición la realizaré después:

![Alt text](img/7.png)

Y en cuanto al destino, le indico que se almacene en mi disco duro externo.

Ya configurada la herramienta, inicio el proceso:

![Alt text](img/8.png)


Una vez terminado el proceso, he obtenido todos datos del triage realizado en mi disco duro externo:

![Alt text](img/9.png)


## Memoria no volátil

Por último, he realizado la adquisición de la memoria no volátil, en este caso, la máquina virtual solo dispone de un disco duro. Para realizar dicha adquisición he utilizado la herramienta ***FTK IMAGER***.

La configuración que he realizado es la siguiente:

He establecido el tipo de imagen como raw (dd):

![Alt text](img/11.png)

Le he indicado que se almacene en el disco duro externo y también que la imagen no se divida:

![Alt text](img/13.png)

Le he marcado las dos opciones mostradas en la captura para que realice una verificación de la imagen después de crearla y me muestre información sobre el proceso:

![Alt text](img/14.png)

Inicio el proceso de creación de la imagen:

![Alt text](img/17.png)

Una vez finalizado el proceso, empieza el proceso de verificación de la imagen:

![Alt text](img/18.png)

Como se puede ver en la captura los hashes coinciden y no hay ningún bloque defectuoso:

![Alt text](img/20.png)

Y en el disco externo ya se encuentra la imagen y el informe:

![Alt text](img/22.png)

## Conclusión

Tras realizar la adquisición forense completa de la máquina virtual de Windows 10, he obtenido una gran cantidad de información relevante. Durante este proceso, he adquirido la memoria ram con ***DumpIT***, he capturado algunos registros del sistema y de red con ayuda de comandos, he realizado triage con la herramienta ***WINTRIAGE*** y, por último, he adquirido el disco duro de la maquina con la ayuda de ***FTK Imager***, en todo momento manteniendo la integridad de las evidencias siguiendo paso a paso nuestra metodología. Esto me ha ayudado a ampliar mi conocimiento sobre la adquisición forense completa de un dispositivo.