## Trabajo Práctico 8 - Herramientas de construcción de software en la nube
### 1- Objetivos de Aprendizaje
 - Adquirir conocimientos acerca de las herramientas de integración continua en la nube.
 - Configurar este tipo de herramientas.
 - Implementar procesos simples de construcción automatizada.

### 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 3 (Libro Continuous Delivery: Cap 3)

### 3- Consignas a desarrollar en el trabajo práctico:
 - Para una mejor evaluación del trabajo práctico, incluir capturas de pantalla de los pasos donde considere necesario.
 - En este caso existen varias herramientas con funcionalidades similares en la nube:
   - [GitHub Actions](https://github.com/actions)
   - [Gitlab](https://about.gitlab.com/) - Trial de 30 días
   - [Azure DevOps](https://azure.microsoft.com/es-es/products/devops)
      

## 4- Desarrollo:

#### 1- Pros y Contras
Las herramientas de construcción en la nube como GitHub Actions, GitLab CI/CD y Azure Pipelines ofrecen varias ventajas y desventajas en comparación con herramientas locales como Jenkins. A continuación, se presentan algunos pros y contras de las herramientas de construcción en la nube en contraste con Jenkins:

Ventajas de las herramientas de construcción en la nube:

Facilidad de configuración y administración: Las herramientas en la nube generalmente son más fáciles de configurar y administrar que las soluciones locales como Jenkins. No es necesario preocuparse por la gestión de servidores, actualizaciones de software, ni la configuración inicial.

Escalabilidad: Las herramientas en la nube generalmente se escalan automáticamente para manejar la carga según sea necesario. Esto es útil cuando se necesita aumentar o reducir la capacidad de construcción según las demandas del proyecto.

Integración con servicios en la nube: Estas herramientas suelen estar integradas con servicios en la nube como AWS, Azure, Google Cloud, y otros, lo que facilita la implementación y la orquestación de recursos en la nube.

Facilita la colaboración: Las herramientas en la nube suelen proporcionar una plataforma centralizada para que los equipos colaboren en la construcción, pruebas y despliegue de aplicaciones, lo que puede mejorar la eficiencia.

Compatibilidad con control de versiones: Estas herramientas están diseñadas para integrarse fácilmente con sistemas de control de versiones como Git, lo que simplifica la automatización de flujos de trabajo basados en repositorios.

Desventajas de las herramientas de construcción en la nube:

Costos: Aunque algunas de estas herramientas ofrecen planes gratuitos, los proyectos más grandes pueden incurrir en costos significativos en función del uso. Jenkins, al ser de código abierto, generalmente no tiene costos de licencia asociados.

Dependencia de la conectividad a Internet: Las herramientas en la nube requieren una conexión a Internet constante para funcionar. Si la conectividad es un problema, esto puede afectar la continuidad de los flujos de trabajo.

Limitaciones en personalización: Algunas herramientas en la nube pueden no ser tan flexibles en términos de personalización y configuración avanzada en comparación con Jenkins, que permite una amplia gama de complementos y scripts personalizados.

Privacidad y seguridad: Puede haber preocupaciones de seguridad al confiar en herramientas de terceros con datos y código fuente confidenciales. Las organizaciones deben evaluar cuidadosamente las políticas de seguridad y privacidad de estas herramientas.

Posibles restricciones en recursos: En algunas ocasiones, las herramientas en la nube pueden imponer límites en la cantidad de recursos que se pueden utilizar para ejecutar trabajos de construcción, lo que puede ser una limitación en proyectos muy grandes o intensivos en recursos.

En última instancia, la elección entre herramientas de construcción en la nube como GitHub Actions, GitLab CI/CD, Azure Pipelines y herramientas locales como Jenkins dependerá de las necesidades específicas de tu proyecto, los requisitos de seguridad y la infraestructura disponible.

#### 2- Configurando GitHub Actions
  - Workflows, Jobs, Steps, Acciones, Eventos y Runners.

   <img width="1218" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/984508c4-5a89-4fd3-8580-08b49a856d75">
   <img width="659" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/c58571dc-6bc2-4dd5-a635-e8d96390941a">
   <img width="681" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/9e03b293-7be3-4279-808e-a32771361c01">
   <img width="694" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/3d2c541c-92b4-499d-8dd3-0e04c842e574">

   <img width="728" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/0b609878-793f-484e-8164-a98973c17118">
   <img width="733" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/3b578407-57e6-46f7-b6b6-f966cd3d3ca4">

<img width="691" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/9c44dfb6-00f4-46b6-83d7-a5812df3a4e8">




  - Revisión Rápida de la sintaxis yml para los worflows
  - Repetir el ejercicio 6.1 del trabajo práctico [trabajo práctico 7](07-servidor-build.md) para el proyecto SimpleWebAPI, pero utilizando GitHub Actions.
  - En GitHub, en el repositorio donde se encuentra la aplicación **SimpleWebAPI**, ir a la opción **Actions** y crear un nuevo `workflow`.
  - El nombre de archivo puede ser main.yml y tendrá un contenido similar al siguiente:

```yaml
name: Build and Publish

on:
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Setup .NET Core
      uses: actions/setup-dotnet@v3
      with:
        dotnet-version: 7.0.x

    - name: Restore dependencies
      run: dotnet restore

    - name: Build
      run: dotnet build --configuration Release

    - name: Publish
      run: dotnet publish --configuration Release --output ./publish

    - name: Upload Artifacts
      uses: actions/upload-artifact@v3
      with:
        name: app
        path: ./publish
  
  deploy:
    needs: build
    runs-on: ubuntu-latest

    steps:
    - name: Download Artifacts
      uses: actions/download-artifact@v3
      with:
        name: app
    - name: Output contents
      run: ls
    - name: Deploy to Server
      run: |
        echo "Deploy"
   
```
  - Guardar el archivo (hacemos commit directamente en GitHub por ejemplo) y vemos la ejecución del worflow y sus logs.

   <img width="1103" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/c30255a1-fe44-4ea7-b189-775fc8ad795b">

  - Explicar paso a paso que realiza el pipeline anterior.

#### 3- Configurar un worflow en GitHub Actions para generar una imagen de Docker de **SimpleWebApi** y subirla a DockerHub

  - En GitHub Actions generar una acción que genere una imagen de docker con nuestra aplicación **SimpleWebAPI** y la suba a DockerHub
  - Generar `secretos` y los `pasos` necesarios para subir la imagen a Docker Hub. [Referencia](https://github.com/actions/starter-workflows/blob/main/ci/docker-publish.yml)

- Paso 1: Configurar las credenciales de Docker Hub en tu repositorio de GitHub:

En tu repositorio de GitHub, ve a "Settings" (Configuración) > "Secrets" (Secretos).
Haz clic en "New repository secret" (Nuevo secreto del repositorio).
Define dos secretos: uno para el nombre de usuario de Docker Hub y otro para la contraseña de Docker Hub. Puedes nombrar estos secretos como DOCKERHUB_USERNAME y DOCKERHUB_PASSWORD, respectivamente.

<img width="1235" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/6f68fde7-d353-4cb0-9d9c-2db4b7355b49">


- Paso 2: Crear un workflow para construir y subir la imagen de Docker:

```yaml
name: Docker Image CI

on:
  workflow_dispatch:
  push:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v2
    
    - name: Build the Docker image
      run: docker build . --file Dockerfile --tag ${{ secrets.DOCKERHUB_USERNAME }}/simple-web-api-gh:latest
    
    - name: Log in to Docker Hub
      run: docker login -u ${{ secrets.DOCKERHUB_USERNAME }} -p ${{ secrets.DOCKERHUB_PASSWORD }}
    
    - name: Push Docker image to Docker Hub
      run: |
        docker push ${{ secrets.DOCKERHUB_USERNAME }}/simple-web-api-gh:latest
      
    - name: Clean up
      run: docker logout
      if: always() # Se ejecutará incluso si un paso anterior falla

 
   
```
  
- Paso 3: Verificar en DockerHub que la imagen ha sido subida
- Paso 4: Descargar la imagen
```bash
docker pull <dockerhub-username>/simple-web-api-gh:latest 
```
- Paso 5: Crear el contenedor
```bash
docker run --name myapi -d -p 8080:80 <dockerhub-username>/simple-web-api-gh
```
- Paso 6: Navegar a http://localhost:8080/weatherforecast

<img width="1332" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/bd1fbf39-bbfb-448a-a59a-07265e100ddd">


#### 4- Crear una GitHub Action que genere los artefactos para el proyecto React
  - En GitHub Actions generar una acción que genere los artefactos para el Ejercicio 2 del TP 5

#### 5- Crear una GitHub Action que genere una imagen de Docker para el proyecto React y lo suba a DockerHub
  - En GitHub Actions generar una acción que genere una imagen de Docker para para el Ejercicio 2 del TP 5 y la suba a DockerHub

#### 6- Opcional: Configurando Gitlab
  - Configurar en GitLab lo indicado en los puntos 2,3,4 y 5.

#### 7- Opcional: Configurando Pipelines en Azure
  - Configurar en Azure lo indicado en los puntos 2,3,4 y 5.

#### 8- Presentación
Subir todo el código, ejemplos y respuestas a una carpeta trabajo-practico-08.
