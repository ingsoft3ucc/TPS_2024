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
 - Para este práctico utilizaremos como ejemplo a Azure

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
``

```
docker tag miang <mi_usuario>/miang:latest
docker push <mi_usuario>/miang:latest

```
