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

------------------------------------------------------------------------------------------------------

Ejercicio 5 – Imágenes slim vs alpine
1. Descargue dos imágenes de Python: docker pull python:3.12-slim
docker pull python:3.12-alpine
<img width="839" height="405" alt="5 1" src="https://github.com/user-attachments/assets/9ede9dad-7894-4b35-983d-73ee5d470a5b" />

2. Compare los tamaños de ambas (docker images).
<img width="792" height="294" alt="5 2" src="https://github.com/user-attachments/assets/205c6227-bb8b-4986-949c-0005cf31f385" />

3. Ejecute un contenedor con cada una y verifique el sistema base: docker run --rm -it python:3.12-slim bash
docker run --rm -it python:3.12-alpine sh
<img width="732" height="475" alt="5 3" src="https://github.com/user-attachments/assets/4d2588af-eb55-4015-af9b-304b2b69da4f" />

Reflexión:

● slim: más ligera que la versión completa, pero mantiene compatibilidad con librerías clásicas.

● alpine: mucho más pequeña, pero puede requerir ajustes adicionales porque carece de ciertas librerías por defecto.


-------------------------------------------------------------------------------------------------------
Preguntas de repaso
1. ¿Cuál es la diferencia principal entre una imagen y un contenedor?: La imagen es como una plantilla y el contenedor es la instancia de ejecución de esa imagen.
2. ¿Qué comando se utiliza para eliminar un contenedor que ya no se requiere?: docker rm "nombre".
3. ¿Qué ventajas tiene usar imágenes Alpine en proyectos reales?: Son más ligeras y rápidas.
4. ¿Qué sucede si no se exponen puertos al ejecutar un contenedor? El contenedor corre normal pero los servicios internos no pueden ser accesibles desde afuera.
5. ¿Qué rol cumple un Dockerfile dentro de un proyecto? Define cómo contruir la imagen.

--------------------------------------------------------------------------------------------------------
Ejercicio 5 – API con archivo copiado desde el host
Construya una imagen personalizada que copie un archivo JSON desde el host hacia el contenedor, levante una API sencilla y exponga endpoints que permitan interactuar con dicho archivo mediante métodos HTTP.

Pasos a desarrollar:

1. En el host, cree un archivo students.json con registros iniciales [
{"id": 1, "nombre": "Ana"},
{"id": 2, "nombre": "Carlos"}
]

<img width="332" height="231" alt="55 1" src="https://github.com/user-attachments/assets/e94e1e85-da12-47ec-a798-42bc687a75a2" />

2. Implemente un archivo app.py con Flask que permita:

○ Listar estudiantes (GET /students).

○ Agregar un estudiante (POST /students).

○ Actualizar un estudiante (PATCH /students/<id>).

<img width="389" height="541" alt="55 2" src="https://github.com/user-attachments/assets/570149a0-4d2d-4449-9899-3ef8e8a1c06f" />

3. Defina un Dockerfile que:

● Use como base cualquier imagen base de Python slim que le permita que funcione FastAPI.

● Copie app.py y students.json al directorio /app.

● Instale FastAPI.

● Ejecute la aplicación con CMD ["tu_comando", "archivo.py"].

<img width="338" height="164" alt="55 3" src="https://github.com/user-attachments/assets/0eecd7a8-4bc4-4096-a6b8-a3a62579d455" />

4. Construya la imagen con: docker build -t api-students .
   
<img width="1286" height="378" alt="55 4" src="https://github.com/user-attachments/assets/c19f12eb-326d-41b5-88a5-063c3461e31a" />

5. Levante un contenedor en segundo plano: docker run -d --name api -p 5000:5000 api-students
   
<img width="654" height="81" alt="55 5" src="https://github.com/user-attachments/assets/cae10488-87eb-48cf-aa46-8f5ee74b91c2" />

6. Realice pruebas desde el host con curl:
    
● GET

● POST

<img width="1295" height="157" alt="55 6" src="https://github.com/user-attachments/assets/777ffcfc-d43e-468a-80ee-6d2b3cf5311c" />

-----------------------------------------------------------------------------------------------------------------

Ejercicio 6 – Repaso: Volúmenes vs Bind Mounts

Parte A – Named Volume

1. Cree un volumen: docker volume create mysqldata
<img width="353" height="70" alt="6 1" src="https://github.com/user-attachments/assets/b7466c1d-a03b-46dc-8fa4-bd1d60900aa9" />

2. Levante un contenedor con MySQL que use este volumen: docker run -d --name db -e MYSQL_ROOT_PASSWORD=pass \
-v mysqldata:/var/lib/mysql mysql:8
<img width="602" height="342" alt="6 2" src="https://github.com/user-attachments/assets/431f44ff-3417-4b3c-be2f-e5791c5717e2" />

3. Dentro de la base de datos, cree una tabla de prueba con algunos registros.
<img width="831" height="427" alt="6 3" src="https://github.com/user-attachments/assets/a1c53f2f-54e1-4c54-94ae-35759babfcb0" />

4. Elimine el contenedor y levante uno nuevo con el mismo volumen.
<img width="209" height="45" alt="6 4" src="https://github.com/user-attachments/assets/d2b7ded6-304e-490b-9917-094a2a95e8ed" />
<img width="657" height="86" alt="6 5" src="https://github.com/user-attachments/assets/08265def-d7e0-4de9-963b-3c0e743d6ef5" />

5. Verifique que los datos persisten.
<img width="810" height="553" alt="6 6" src="https://github.com/user-attachments/assets/37eecd1a-ec31-4890-bf65-238d599adf41" />

Parte B – Bind Mount

En el host, cree un directorio: mkdir ~/bindtest && echo "Linea inicial" > ~/bindtest/info.txt
<img width="465" height="77" alt="7 1" src="https://github.com/user-attachments/assets/bc726762-41e2-4331-9a25-7a43fe3adc69" />

1. Levante un contenedor de Alpine montando el directorio: docker run -it --rm -v ~/bindtest:/data alpine sh
<img width="821" height="123" alt="7 2" src="https://github.com/user-attachments/assets/376d3c36-c37d-4546-a40d-7bfcefa75d80" />

2. Dentro del contenedor, agregue una línea a info.txt y cree un archivo nuevo.
<img width="821" height="90" alt="7 2 copia" src="https://github.com/user-attachments/assets/591d559e-f781-45d0-b146-89c5f23569b6" />
 
3. Desde el host, confirme que los cambios están reflejados en ~/bindtest.
<img width="532" height="184" alt="7 3" src="https://github.com/user-attachments/assets/2baee152-fde7-4a7c-8fe7-d9b3fcbcd868" />

Reflexión:

● ¿Qué diferencia observa entre usar volúmenes y bind mounts?: Los volúmenes los maneja Docker y se guardan en /var/lib/docker/volumes y bind mounts usan carpetas y archivos del host.

● ¿En qué casos resulta preferible usar uno u otro? Los volúmenes son buenos para bases de datos y bind mount es bueno para pruebas o compartir archivos con el host.
