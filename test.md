# Deteccion de uso de mascarilla en tiempo real usando YOLO V3 

Las instrucciones que se presentan a continuacion son para ejecutar un algoritmo de deteccion si una o varias personas estan usando o no mascarilla. 

Todo el trabajo duro fue ya realizado (no presento aqui la etapa de entrenamiento del sistema el cual me llevo varias semanas) aqui facilito todo los archivo necesarios y las instrucciones para correr el algoritmo de mandera muy facil, solo sigue las instrucciones y tendras un sistema de tiempo real para detecion de mascarillas

>Solo como informacion general este sistema fue entranado con 2839 imagenes, las cuales fueron escogidas  y evaluadas manualmente. Ademas se utilizo labelImg para etiquetar manualamente una a una las imagenes.

## Pre-requisitos

* Ubuntu 18.04.02 (bionic beaver)
* Tarjeta NVIDIA GPU y su driver instalado correctamente
* OpenCV >= 2.4
* CUDA 10.1
* cuDNN >= 7.0 for CUDA 10.1
* Python >= 3.0

## Getting started
- Siempre es una buena idea Update y Upgrade nuestro sistema
 ```
sudo apt-get update 
sudo apt-get upgrade
 ```
## Paso 1: Clonar y compilar darket 
-Los siguientes comandos clonará darknet  del repositorio de AlexeyAB, ademas se realizarán los cambios necesario en el makefile para activar GPU y OPENCV  

```
git clone https://github.com/AlexeyAB/darknet.git
cd darknet
sed -i 's/OPENCV=0/OPENCV=1/' Makefile
sed -i 's/GPU=0/GPU=1/' Makefile
sed -i 's/CUDNN=0/CUDNN=1/' Makefile
make
```

## Paso 2: Descargar los archivos necesarios
Asegurate de descargar y copiar esos archivos en los directorios correctos q se indican a continuacion:

### Paso 2.1: Descargar los weights pre-entrenados

> Este file .weights contiene los parámetros de la red neuronal convolucional (CNN) de los weights pre-entrenados.

- Descarga el archivo **yolov3_face_mask_detection.weights** usando el link:
```
https://drive.google.com/open?id=17jOtOPXNgvYz0vPOpTmhZeQSB843NVIq
```
- Copia este archivo dentro del directorio principal de darketet --> darknet/


### Paso 2.2: Descargar el archivo de configuracion 

> Este file .cfg contiene toda la información relacionada con a la arquitectura y parámetros de YOLOv3.
- Descarga el archivo usando el link:

Descagar el archivo **yolov3_face_mask_detection.cfg** usando el link:
```
https://drive.google.com/open?id=1GNcC5pdh5HRqubKh4AELvJHyuwmf8Q6o
```
Copia este archivo dentro del directorio --> darknet/cfg

### Paso 2.3: Descargar el archivo .names 
>  El file .name contiene toda el nombre de las clases que detecta el sistema.

Descarga el archivo **yolov3_face_mask_detection.names** usando el link:
```
https://drive.google.com/open?id=1hMic2AgVUHc2NjMDaPUYQ1XkBkyz3Fcg
```
Copia este archivo dento del directorio   --> darknet/data

### Paso 2.4: Descargar el archivo .data 
>  El file .data contiene toda el numero clases que detecta el sistema y los direccionamientos necesarios

Descarga el archivo **yolov3_face_mask_detection.data** usando el link:
```
https://drive.google.com/open?id=1uimuJv8zMoYdlhPY80UsRM4sbheNMAGq
```
Copia este archivo dento del directorio   --> darknet/data


- El siguiente diagrama puede ayudar a clarificar donde van estos archivos correctamente:
```
    darknet
        │ 
        └── 3rdparty
        └── backup        
        └── include
        └──.......
        └───yolov3_custom_final.weights
        │ 
        └─── cfg
        │   │
        │   └───yolov3_face_mask_detection.cfg
        │   
        └─── data
            │
            └───yolov3_face_mask_detection.names
            └───yolov3_face_mask_detection.data
```
## Paso 3 Listo ! Ejecutar Darknet y YOLOv3 !
- Asegurate de estar dentro del directorio de darket  tener una camara web operativa y ejectuta la siguiente comando:

```
./darknet detector demo data/yolov3_face_mask_detection.data  cfg/yolov3_face_mask_detection.cfg yolov3_face_mask_detection.weights 
```
- Si colocastes los archivos en la ubicacion correcta, obtendras algo como esto, donde el sistema detectara en tiempo real si una o varias personas estan usando mascarilla:
un gif

para ejecutar en un video 
el comando
un gif

para ejecutar en una imagen 
el comando 
la imagen








