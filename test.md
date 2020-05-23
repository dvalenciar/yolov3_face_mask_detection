# Deteccion de uso de mascarilla en tiempo real usando YOLO V3 
  ![](https://github.com/dvalenciar/yolov3_face_mask_detection/blob/master/video_out.gif)

Las instrucciones que se presentan a continuación son para ejecutar un algoritmo de detección si una o varias personas están usando o no mascarilla. 

Todo el trabajo duro fue ya realizado (no presento aquí la etapa de entrenamiento del sistema el cual me llevo varias semanas) aquí facilito todo los archivo necesarios ya entranados y las instrucciones para correr el algoritmo de manera muy fácil, solo sigue las instrucciones y tendrás un sistema de tiempo real para detección de mascarillas.

> Solo como información general este sistema fue entrenado con 2839 imágenes, las cuales fueron escogidas  y evaluadas manualmente. Ademas se utilizo labelImg para etiquetar manualmente una a una las imágenes.

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
-Los siguientes comandos clonará darknet del repositorio de AlexeyAB, ademas se realizarán los cambios necesario en el makefile para activar GPU y OPENCV  

```
git clone https://github.com/AlexeyAB/darknet.git
cd darknet
sed -i 's/OPENCV=0/OPENCV=1/' Makefile
sed -i 's/GPU=0/GPU=1/' Makefile
sed -i 's/CUDNN=0/CUDNN=1/' Makefile
make
```

## Paso 2: Descargar los archivos necesarios
Asegurate de descargar y copiar estos archivos en los directorios correctos que se indican a continuación:

### Paso 2.1: Descargar los weights pre-entrenados

> Este archivo .weights contiene los parámetros de la red neuronal convolucional (CNN) de los weights pre-entrenados.

- Descarga el archivo **yolov3_face_mask_detection.weights** usando el link:
```
https://drive.google.com/open?id=17jOtOPXNgvYz0vPOpTmhZeQSB843NVIq
```
- Copia este archivo dentro del directorio principal de darknet --> darknet/


### Paso 2.2: Descargar el archivo de configuracion 

> Este archivo .cfg contiene toda la información relacionada con a la arquitectura y parámetros de YOLOv3.

- Descagar el archivo **yolov3_face_mask_detection.cfg** usando el link:
```
https://drive.google.com/open?id=1GNcC5pdh5HRqubKh4AELvJHyuwmf8Q6o
```
- Copia este archivo dentro del directorio --> darknet/cfg/


### Paso 2.3: Descargar el archivo .names 
>  Este archivo .name contiene el nombre de las clases que detecta el sistema.

- Descarga el archivo **yolov3_face_mask_detection.names** usando el link:
```
https://drive.google.com/open?id=1hMic2AgVUHc2NjMDaPUYQ1XkBkyz3Fcg
```
- Copia este archivo dentro del directorio   --> darknet/data/

### Paso 2.4: Descargar el archivo .data 
>  Ese archivo .data contiene el numero clases que detecta el sistema y los direccionamientos necesarios

- Descarga el archivo **yolov3_face_mask_detection.data** usando el link:
```
https://drive.google.com/open?id=1uimuJv8zMoYdlhPY80UsRM4sbheNMAGq
```
- Copia este archivo dentro del directorio --> darknet/data/

## 


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

- Asegurate de estar dentro del directorio de darknet y tener una camara web operativa. Si colocaste los archivos en la ubicacion correcta,  ejecuta el siguiente comando, la camara web comenzara a operar y el sistema detectara en tiempo real si una o varias personas estan usando mascarilla
```
./darknet detector demo data/yolov3_face_mask_detection.data  cfg/yolov3_face_mask_detection.cfg yolov3_face_mask_detection.weights 
```

- Si deseas aplicar la deteccion a una imagen ejecuta el siguiente comando:
```
./darknet detector test data/yolov3_face_mask_detection.data  cfg/yolov3_face_mask_detection.cfg yolov3_face_mask_detection.weights  <image_path>
```
Por ejemplo, tengo mi imagen "image_test.jpg" en la carpeta data, el comando seria:
```
./darknet detector test data/yolov3_face_mask_detection.data  cfg/yolov3_face_mask_detection.cfg yolov3_face_mask_detection.weights  data/image_test.jpg 
```
![](https://github.com/dvalenciar/yolov3_face_mask_detection/blob/master/predictions.jpg)

- Si deseas aplicar la deteccion a un video ejecuta el siguiente comando:
```
./darknet detector demo data/yolov3_face_mask_detection.data cfg/yolov3_face_mask_detection.cfg yolov3_face_mask_detection.weights <video_path.mp4> 
```

- Si deseas aplicar la deteccion a un video y guardar el resultado con la deteccion, ejecuta el siguiente comando:

```
./darknet detector demo data/yolov3_face_mask_detection.data cfg/yolov3_face_mask_detection.cfg yolov3_face_mask_detection.weights -dont_show <video_path.mp4> -i 0 -out_filename out_face_mask_2.avi
```
Encontras un video llamado face_mask_2.avi en el directorio principal ---> darknet/
![](https://github.com/dvalenciar/yolov3_face_mask_detection/blob/master/video_out_2.gif)





