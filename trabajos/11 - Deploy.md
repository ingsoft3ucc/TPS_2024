

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

- Subimos la imagen a DockeHub

```
docker login
``

```
docker tag miang <mi_usuario>/miang:latest
docker push <mi_usuario>/miang:latest

```
