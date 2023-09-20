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
   - [CircleCI](https://circleci.com/)
   - [Travis CI](https://travis-ci.com/)
   - [Codefresh](https://codefresh.io/)
   - [Gitlab](https://about.gitlab.com/) - Trial de 30 días

## 4- Desarrollo:

#### 1- Pros y Contras
  - Listar los pros y contras de este tipo de herramientas
  - Sacar conclusiones

#### 2- Configurando GitHub Actions
  - Repetir el ejercicio 6 del trabajo práctico [trabajo práctico 7](07-servidor-build.md) para el proyecto SimpleWebAPI, pero utilizando GitHub Actions.
  - En GitHub, en el repositorio donde se encuentra la aplicación **SimpleWebAPI**, ir a la opción **Actions** y crear un nuevo `workflow`.
  - El nombre de archivo puede ser main.xml y tendrá un contenido similar al siguiente (el path donde se encuentra el código puede ser diferente):

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
  - Guardar el archivo (hacemos commit directamente en GitHub por ejemplo) y ejecutamos manualmente el pipeline.
  - Explicar que realiza el pipeline anterior.

#### 3- Utilizando nuestros proyectos con Docker
  - Repetir el ejercicio 7 del trabajo práctico [trabajo práctico 7](07-servidor-build.md), pero utilizando GitHub Actions.
  - Generar `secretos` y los `pasos` necesarios para subir la imagen a Docker Hub. [Referencia](https://github.com/actions/starter-workflows/blob/main/ci/docker-publish.yml)

#### 4- Opcional: Configurando CircleCI
  - De manera similar al ejercicio 2, configurar un build job para el mismo proyecto, pero utilizando CircleCI
  - Para capturar artefactos, utilizar esta referencia: https://circleci.com/docs/2.0/artifacts/
  - Como resultado de este ejercicio, subir el config.yml a la carpeta **spring-boot**

#### 5- Opcional: Configurando TravisCI
  - Configurar el mismo proyecto, pero para TravisCI. No es necesario publicar los artefactos porque TravisCI no dispone de esta funcionalidad.
  - Como resultado de este ejercicio subir el archivo .travis.yml a la carpeta **spring-boot**

#### 6- Opcional: Configurando Codefresh
  - Configurar el mismo proyecto, pero para Codefresh. 
  - Como resultado de este ejercicio subir el archivo codefresh.yml a la carpeta **spring-boot**

#### 7- Opcional: Configurando Gitlab
  - Configurar el mismo proyecto, pero para Gitlab. 
  - Como resultado de este ejercicio subir el archivo .gitlab-ci.yml a la carpeta **spring-boot**
