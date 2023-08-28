## Trabajo Práctico 6 - Construcción de Imágenes de Docker

### 1- Objetivos de Aprendizaje
 - Adquirir conocimientos para construir y publicar imágenes de Docker.
 - Familiarizarse con el vocabulario.

### 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 3

### 3- Consignas a desarrollar en el trabajo práctico:
 - En los puntos en los que se pida alguna descripción, realizarlo de la manera más clara posible.

### 4- Desarrollo:

#### 1- Conceptos de Dockerfiles
  - Leer https://docs.docker.com/engine/reference/builder/ (tiempo estimado 2 horas)
  - Describir las instrucciones
     - FROM
     - RUN
     - ADD
     - COPY
     - EXPOSE
     - CMD
     - ENTRYPOINT

#### 2- Generar imagen de docker
   - Utilizar el resultado del paso 1 del TP 5
   - Agregar un archivo llamado **Dockerfile** (en el directorio raiz donde se encuentran todos los archivos y directorios)
```Dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80


FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["MiProyectoWebAPI.csproj", "."]
RUN dotnet restore "./MiProyectoWebAPI.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "MiProyectoWebAPI.csproj" -c Release -o /app/build
RUN dotnet publish "MiProyectoWebAPI.csproj" -c Release -o /app/publish /p:UseAppHost=false
ENTRYPOINT ["dotnet", "bin/Debug/net7.0/MiProyectoWebAPI.dll"]

```
   - Generar la imagen de docker con el comando build
```bash
docker build -t miproyectowebapi .
```
  - Ejecutar el contenedor
```bash
docker run -p 8080:80 -it --rm miproyectowebapi
```
  - Capturar y mostrar la salida.
  - Entrar a la terminal del contenedor y ver directorios src, app/build y app/publish


#### 3- Dockerfiles Multi Etapas
Se recomienda crear compilaciones de varias etapas para todas las aplicaciones (incluso las heredadas). En resumen, las compilaciones de múltiples etapas:

- Son independientes y auto descriptibles
- Resultan en una imagen de Docker muy pequeña
- Puede ser construido fácilmente por todas las partes interesadas del proyecto (incluso los no desarrolladores)
- Son muy fáciles de entender y mantener.
- No requiere un entorno de desarrollo (aparte del código fuente en sí)
- Se puede empaquetar con pipelines muy simples

Las compilaciones de múltiples etapas también son esenciales en organizaciones que emplean múltiples lenguajes de programación. La facilidad de crear una imagen de Docker por cualquier persona sin la necesidad de JDK / Node / Python / etc. no puede ser sobrestimado.

- Modificar el dockerfile para el proyecto anterior de la siguiente forma
```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80


FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["MiProyectoWebAPI.csproj", "."]
RUN dotnet restore "./MiProyectoWebAPI.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "MiProyectoWebAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MiProyectoWebAPI.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MiProyectoWebAPI.dll"]

```
- Construir nuevamente la imagen
```bash
docker build -t miproyectowebapi .
```
- Analizar y explicar el nuevo Dockerfile, incluyendo las nuevas instrucciones.
- Entrar a la terminal del contenedor y ver directorios src, app/build y app/publish


#### 4- Imagen para aplicación web en Nodejs
  - Crear una la carpeta `trabajo-practico-06/nodejs-docker`
  - Generar un proyecto siguiendo los pasos descriptos en el trabajo práctico 5 para Nodejs
  - Escribir un Dockerfile para ejecutar la aplicación web localizada en ese directorio
    - Idealmente que sea multistage, con una imagen de build y otra de producción.
    - Usar como imagen base **node:13.12.0-alpine**
    - Ejecutar **npm install** dentro durante el build.
    - Exponer el puerto 3000
  - Hacer un build de la imagen, nombrar la imagen **test-node**.
  - Ejecutar la imagen **test-node** publicando el puerto 3000.
  - Verificar en http://localhost:3000 que la aplicación está funcionando.
  - Proveer el Dockerfile y los comandos ejecutados como resultado de este ejercicio.

#### 5- Publicar la imagen en Docker Hub.
  - Crear una cuenta en Docker Hub si no se dispone de una.
  - Registrase localmente a la cuenta de Docker Hub:
```bash
docker login
```
  - Crear un tag de la imagen generada en el ejercicio 3. Reemplazar <mi_usuario> por el creado en el punto anterior.
```bash
docker tag test-node <mi_usuario>/test-node:latest
```
  - Subir la imagen a Docker Hub con el comando
```bash
docker push <mi_usuario>/test-node:latest
``` 
  - Como resultado de este ejercicio mostrar la salida de consola, o una captura de pantalla de la imagen disponible en Docker Hub.
