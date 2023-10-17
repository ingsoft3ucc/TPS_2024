## Trabajo Práctico 11 - Despliegue de aplicaciones

### 1- Objetivos de Aprendizaje
 - Adquirir conocimientos acerca de las herramientas de despliegue y releases de aplicaciones.
 - Configurar este tipo de herramientas.

### 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 3 (Libro Continuous Delivery: Cap 10)

### 3- Consignas a desarrollar en el trabajo práctico:
 - Los despliegues (deployments) de aplicaciones se pueden realizar en diferentes tipos de entornos
   - On-Premise (internos) es decir en servidores propios.
   - Nubes Públicas, ejemplo AWS, Azure, Gcloud, etc.
   - Plataformas como servicios (PaaS), ejemplo Heroku, Google App Engine, AWS, Azure, etc
 - Para este práctico utilizaremos como ejemplo a Google Cloud

### 4- Desarrollo:

- Sobre la aplicación angular que se realizo en el punto 3, 4 y 5 del TP10 construimos un Dockerfile

```
# Stage 1
FROM node:14.15.4 as node
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build --prod
# Stage 2
FROM nginx:alpine
COPY --from=node /app/dist/angular-registration-login-example /usr/share/nginx/html

EXPOSE 80
```

- Construimos la imagen

```
docker build -t miang .         
```

- Subimos la imagen a DockeHub

```
docker login
docker tag miang <mi_usuario>/miang:latest
docker push <mi_usuario>/miang:latest

```

- Crear una cuenta Google Cloud
- Crear un proyecto TP11

 ![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/cd2e0fce-0510-43fe-8132-cb65b07410d8)
 ![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/d1b9bb13-7f35-4f76-8e05-e560cc390da4)

- Activar Cloud Shell 
![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/9801fc96-ff88-487b-98ec-9b4f3e6ad296)

- Hacemos un pull de nuestra imagen de DockerHub
```
docker pull <nombre_usuario>/<nombre_imagen>
```

![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/74a0d2fa-1d8f-446a-8f0f-8c168f793fbb)



- Una vez descargada de DockerHub, tagueamos nuestra imagen para subirla a Google Cloud Registry
```
docker images
docker tag <nombre_usuario>/<nombre_imagen> gcr.io/<id_proyecto>/<nombre_imagen_en_google_cloud>
docker images
```
![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/180e1942-3728-4a40-bfd5-4b31f2a9f0e7)


- Hacemos un push de nuestra imagen tagueada hacia Google Cloud Registry

```
docker push gcr.io/<id_proyecto>/<nombre_imagen_en_google_cloud>
```

![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/b9a53505-79a4-4fa1-ae5a-d472e1e33aa6)


- No esta habilitada una API, por eso reintenta, vamos a Container Registry y habilitamos la API

 ![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/ff10010c-0a50-4750-bcff-d0a7a4994374)
 ![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/4005cee8-f617-46d2-9aea-ae2a520b5183)

- Reintentamos el push

```
docker push gcr.io/<id_proyecto>/<nombre_imagen_en_google_cloud>
```
- Si nos pide autenticación hacemos:

```
gcloud auth login
```
Eso nos da un link para que nos autentiquemos y copiemos el token que pegaremos en la consola que nos lo pida

y luego 

```
gcloud auth configure-docker
```

- Vamos a Cloud Run y le damos Crear Servicio

![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/e3fc8cfe-11c7-4e2d-b29b-d9e347832a3b)
![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/2a9fae3b-737d-4673-9066-244190bfa922)

- Seleccionamos nuestra imagen:

![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/4a5e035c-b19d-4b5e-9567-dbcb23a7641b)

- Configuramos max 15 instancias:
  
 ![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/4f08718a-1108-46c2-a559-2916e72dac1b)

- Configuramos acceso público:

![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/c5f28963-3feb-4216-8c8e-7efba2963044)

- Configuramos puerto 80 q es donde escucha nuestra imagen/contenedor:

![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/9eb32074-0299-4c9c-8ea7-0319ebe2a42a)

- Le damos Crear:

![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/182f1363-0c82-4e20-8b12-b6ba47347a3e)

- Luego de unos segundos nos disponibiliza la url:

<img width="698" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/b8aa42ab-f8e9-41c9-98d5-249786c3cb32">

<img width="1207" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/2cfc5a68-6f44-499e-ba36-474773471ea2">













