# Taller-Repaso-Fundamentos-de-Docker

Ejercicio 1 – Exploración de imágenes y contenedores
1. Liste las imágenes disponibles en el sistema: docker images
<img width="719" height="217" alt="1 1" src="https://github.com/user-attachments/assets/17a503df-7cb9-4bf7-a9ba-dd1420720e48" />

2. Descargue la imagen oficial de Alpine y Ubuntu:
docker pull alpine:3.20
docker pull ubuntu:22.04
<img width="798" height="249" alt="1 2" src="https://github.com/user-attachments/assets/6d9b0688-13a4-4200-a593-ef164888ca4f" />

3. Verifique las imágenes descargadas y compare sus tamaños.
<img width="739" height="226" alt="1 3" src="https://github.com/user-attachments/assets/6bfd58cd-d13c-4094-a925-29b91a71039e" />

alpine:3.20: 7.79 MB

ubuntu:22.04: 77.9 MB

Reflexión: ¿Por qué Alpine es significativamente más ligera que Ubuntu?: Porque Alpine Linux es una distribución minimalista diseñada para ocupar poco espacio

---------------------------------------------------------------------------------------

Ejercicio 2 – Creación y ejecución de contenedores

1. Ejecute un contenedor interactivo de Alpine:
   
docker run -it --name test-alpine alpine:3.20 sh

<img width="535" height="57" alt="2 1" src="https://github.com/user-attachments/assets/e7af93aa-af1b-4ab0-b9d2-df11bc7837b8" />


2. Dentro del contenedor, ejecute ls, pwd y cat /etc/os-release, luego salga con exit.
<img width="719" height="269" alt="2 2" src="https://github.com/user-attachments/assets/9883fe13-04ab-4ea8-878f-5f191c251935" />

3. Liste los contenedores: docker ps -a
<img width="1291" height="389" alt="2 3" src="https://github.com/user-attachments/assets/487f0315-4e93-4d18-b058-69b81ba78224" />

Pregunta: ¿Cuál es la diferencia entre docker ps y docker ps -a?: docker ps muestra solo los contenedores que estén perdidos y docker ps -a muestra todos los contenedores 
