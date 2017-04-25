# Open Hardware Day

#  Kicad: diseñando electrónica con software libre

## José Antonio Vacas @javacasm

![Licencia CC](./images/Licencia_CC.png)

### ¡¡Este tutorial está sin terminar!! es un trabajo en continuo progreso...

## ¿Qué es [Kicad](http://kicad-pcb.org) (http://kicad-pcb.org)?

Es un paquete de aplicaciones open-source formado por diferentes componentes pensados para trabajar las distintas fases de la creación y desarrollo de circuitos electrónicos.


![Alhambra en kicad](./images/Alhambra_kicad.png)

Actualmente [recibe apoyo](http://kicad-pcb.org/about/kicad/) de entidades tan importantes como el CERN, la fundación Raspberry o Arduino.

## Documentación

Existe mucha [documentación](http://kicad-pcb.org/help/documentation/) y traducida a varios idiomas

También disponemos de [diferentes tutoriales](http://kicad-pcb.org/help/tutorials/) y [videotutoriales](http://kicad-pcb.org/help/tutorials/#_video_tutorials) desde un nivel básico hasta uno tan avanzado que nos enseña a [diseñar una placa compatible con Arduino UNO](https://www.youtube.com/user/XploreLabz/videos)

Personalmente estoy siguiendo la serie [8 vídeos de Applied Electronics](https://www.youtube.com/playlist?list=PLasv3NGTWxRtv5-lh-6zYzKbRS5hVgy1C), que aunque va algo lenta empieza por el orden que a mi me parece más lógico. También tengo apuntado para ver el [vídeo de Windsor Schmidt](https://www.youtube.com/watch?v=zK3rDhJqMu0)

## Instalación en Ubuntu

(La instalación en Windows o mac no parece complicada: en la [página de descargas](http://kicad-pcb.org/download/) tienes los enlaces )

Para instalar la versión stable

    sudo add-apt-repository --yes ppa:js-reynaud/kicad-4
    sudo apt update
    sudo apt install kicad

Si nos gusta estar a la última (aunque con su riesgo...) podemos instalar las build que se generan día a día con la última funcionalidad

    sudo add-apt-repository --yes ppa:js-reynaud/ppa-kicad
    sudo apt update
    sudo apt install kicad

## Componentes

Desde la pantalla inicial donde vemos el proyecto podemos abrir las distintas herramientas que se corresponden con las diferentes fases y resultados

![Pantalla inicial de Kicad](./images/PantallaInicialKicad.png)

|Componente|Icono|Utilidad|Formato|
|---|---|---|---|
|Kicad | ![Kicad](./images/kicad.png)|Gestor de proyectos| *.pro|
|Eeschema|![Create schema.png](./images/Create schema.png)| Editor de los esquemas electrónicos |*.sch, *.lib, *.net|
|Pcbnew| ![PcbNew](./images/PCBNew.png)|Adaptamos el circuito a una placa|*.pcb, *.kicad_pcb|
|Schematic Library Editor| ![Schematic Library Editor](images/SchematicLibraryEditor.png)||
|PCB Footprint Editor| ![PCB Footprint Editor](./images/PCBFootprintEditor.png)|Editor de los formatos de los distintos componentes|
|CvPCB |![CvPCB](./images/CVPCB.png)|Asocia los componentes y su huella (footprint)|*.cmp, *.net|
|Gerber Viewer| ![Gerber Viewer](./images/GerberViewer.png)|Visor de formato Gerber|(formatos gerber)|
|Bitmap To Component|![Bitmap 2 Component](./images/Bitmap2Component.png)|Convierte imágenes a componentes|*.kicad_wks,*.lib, kicad_mod|
|PCB Calculator| ![PCB Calculator](./images/PCBCalculator.png)|Diferentes calculadoras sobre temas de electrónica||
|PL Editor| ![PL Editor](./images/PLEditor.png)|Editor de la plantilla para diseño|*.kicad_wks|



#### [¿Qué es una PCB?](./PCBs.md)

Viendo la complejidad de una PCB, ahora vemos que son muchas las distintas "capas" que tenemos que diseñar, con el objetivo de que todas interaccionen adecuadamente.


## Creación de un circuito

![flujo de trabajo](http://docs.kicad-pcb.org/4.0.6/es/images/es/kicad_flowchart.png)

### ¿Cuáles son los pasos del desarrollo de la placa de un circuito electrónico?

* Creamos el schema ![Create schema](./images/CreateSchema.png)

  * Seleccionamos los componentes  y los conectamos entre si.
  * Definir un conjunto de reglas que tiene que cumplir nuestro circuito
  * Definimos el formato/huella de los componentes
  * Suele ocurre que no existe el que buscamos, lo que podemos resolver con CvPCB
![](https://github.com/javacasm/CharlaKicad/raw/master/images/CVPCB.png)

  * Con PCBNew definimos cómo se disponen y conectan los componentes en la placa ![PCBNew](https://github.com/javacasm/CharlaKicad/raw/master/images/PCBNew.png)
  * Definimos más reglas (por ejemplo la distancia entre componentes y las pistas)



Todos estos procesos son iterativos y vamos mejorando el resultado

Cuando hemos terminado generamos los ficheros Gerber, que podemos ver con GerberViewer ![GerberViewer](https://github.com/javacasm/CharlaKicad/raw/master/images/GerberViewer.png)

A partir de los ficheros Gerber, iniciamos el proceso de fabricación, por ejemplo con [DirtyPCBs](http://dirtypcbs.com/store/pcbs)

### ¿Cuanto cuesta un tirada de pcbs?

Los fabricantes  piden que las placas cumplan determinadas reglas de diseño (relacionadas con sus tolerancias y calidades) que deberemos incluir en el diseño.

Para encargarla sólo tendremos que subir los diferentes ficheros de las diferentes capas: pistas, agujeros, cortes, serigrafía, ....

## Hagamos un ejemplo .....

Shift+? Hotkeys

* Abrimos Eeschema
* Configuramos la página con nuestros datos
* Seleccionamos los componentes "a"
* Editamos el componente con  "e"
* Si no existe lo creamos con el Library Editor ![LE](https://github.com/javacasm/CharlaKicad/raw/master/images/SchematicLibraryEditor.png)
* Para conectar hacemos click entre los componentes
* En cualquier momento podemos revisar cómo va el diseño, validando las reglas
* Anotamos los componentes dándoles nombre
* Vamos a asociar las huellas (por defecto se sacan de github) de nuestros componentes. ![CvPCB](https://github.com/javacasm/CharlaKicad/raw/master/images/CVPCB.png)
* Si no existe lo podemos crear ![](https://github.com/javacasm/CharlaKicad/raw/master/images/PCBFootprintEditor.png)
* Generamos la red de conexiones
* Y la importanmos desde PCBNew
* Colocamos los componentes
* Comenzamos el enrutados
* Podemos usar herramientas externas FreeRoute




## Referencias

[Creating a pcb with Kicad (1/3)](https://hackaday.com/2016/11/17/creating-a-pcb-in-everything-kicad-part-1)

[Creating a pcb with Kicad (2/3)](http://hackaday.com/2016/12/09/creating-a-pcb-in-everything-kicad-part-2/)

[Creating a pcb with Kicad (3/3)](http://hackaday.com/2016/12/23/creating-a-pcb-in-everything-kicad-part-3/)
