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

Reflexión: ¿Por qué Alpine es significativamente más ligera que Ubuntu?: Porque Alpine Linux es una distribución minimalista diseñada para ocupar poco espacio.

---------------------------------------------------------------------------------------

Ejercicio 2 – Creación y ejecución de contenedores

1. Ejecute un contenedor interactivo de Alpine:
   
docker run -it --name test-alpine alpine:3.20 sh

<img width="535" height="57" alt="2 1" src="https://github.com/user-attachments/assets/e7af93aa-af1b-4ab0-b9d2-df11bc7837b8" />


2. Dentro del contenedor, ejecute ls, pwd y cat /etc/os-release, luego salga con exit.
<img width="719" height="269" alt="2 2" src="https://github.com/user-attachments/assets/9883fe13-04ab-4ea8-878f-5f191c251935" />

3. Liste los contenedores: docker ps -a
<img width="1291" height="389" alt="2 3" src="https://github.com/user-attachments/assets/487f0315-4e93-4d18-b058-69b81ba78224" />

Pregunta: ¿Cuál es la diferencia entre docker ps y docker ps -a?: docker ps muestra solo los contenedores que estén perdidos y docker ps -a muestra todos los contenedores.

--------------------------------------------------------------------------------------------

Ejercicio 3 – Construcción de una imagen propia
Cree un archivo Dockerfile:

FROM alpine:3.20

RUN apk add --no-cache curl

CMD ["curl", "--version"]

<img width="870" height="98" alt="3 0" src="https://github.com/user-attachments/assets/5958bbbf-c3a4-42d4-89f7-f75a9f5f9234" />


1. Construya la imagen: docker build -t mi-alpine-curl .
   
<img width="1299" height="296" alt="3 1" src="https://github.com/user-attachments/assets/db699ae2-1efa-4d3b-90a6-f37c5bf69cd7" />

2. Ejecute un contenedor desde su nueva imagen: docker run --rm mi-alpine-curl

<img width="1292" height="231" alt="3 2" src="https://github.com/user-attachments/assets/c24ff27a-3c3f-4888-b1c7-5810577e335f" />

Pregunta: ¿Qué sucede con el contenedor cuando se utiliza la opción --rm?: Se elimina automáticamente cuando el proceso principal dentro del contenedor termine.

------------------------------------------------------------------------------------------------
Ejercicio 4 – Puertos internos vs externos

1. Cree un archivo index.html en el host: <h1>Hola Docker</h1>
<img width="485" height="95" alt="4 1" src="https://github.com/user-attachments/assets/9454002e-0451-48c8-b80f-42695d992923" />

2. Levante un contenedor de Nginx sirviendo ese archivo con un bind mount: docker run -d --name web -p 8080:80 -v $(pwd)/index.html:/usr/share/nginx/html/index.html:ro nginx:alpine
<img width="1088" height="72" alt="4 2" src="https://github.com/user-attachments/assets/3ccb49d6-112d-41f0-87e8-a695fe9cb130" />


3. Abra http://localhost:8080 en el navegador
<img width="458" height="139" alt="4 3" src="https://github.com/user-attachments/assets/3a29fd14-12f0-4e75-ad78-c68eb51bd6a6" />

Explicación:
● 80 es el puerto interno del contenedor (donde escucha Nginx).
● 8080 es el puerto externo en el host (desde donde se accede al servicio).
