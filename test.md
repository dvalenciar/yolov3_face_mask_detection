# Deteccion de mascarillas en tiempo real  usando YOLO V3 

## Pre-requisitos
* Tarjeta NVIDIA GPU y su driver instalado correctamente
* OpenCV >= 2.4
* CUDA 10.1
* cuDNN >= 7.0 for CUDA 10.1

fue entranado con # tod ya fue entrando ahora para ti e mas facil solo tienes que seguir estos pasos 
y ya 

Abrir una nueva terminal:
git clone https://github.com/AlexeyAB/darknet.git

Modificar makefile para activar GPU y  OPENCV  

cd darknet
sed -i 's/OPENCV=0/OPENCV=1/' Makefile
sed -i 's/GPU=0/GPU=1/' Makefile
sed -i 's/CUDNN=0/CUDNN=1/' Makefile

Compilar darknet
make

Descagar el archivo cfg. disponible aqui
El archivo yolov3.cfg contiene toda la información relacionada con a la arquitectura y parámetros de YOLOv3.
Copia este archivo dento del directorio   --> darknet/cfg

Descarga el archivo .data disponible aqui
Copia este archivo dento del directorio   --> darknet/data

Descarga el archivo .names disponible aqui
Copia este archivo dento del directorio   --> darknet/data

Descarga los pesos 
contiene los parámetros de la red neuronal convolucional (CNN) de los pesos pre-entrenados .

Copia este archivo dento del directorio principal  --> darknet/

el siguiente diagrama puede ayudar a clarificar donde iran estos archivos:

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

Asegurate de estar dentro del directorio de darket y ejectuta la siguiente comando:


./darknet detector demo data/yolov3_face_mask_detection.data  cfg/yolov3_face_mask_detection.cfg yolov3_face_mask_detection.weights 






