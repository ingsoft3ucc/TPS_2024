## Trabajo Práctico 8 - Implementación de Contenedores en Azure y Automatización con Azure CLI

### 1- Objetivos de Aprendizaje

Al finalizar esta sesión, los estudiantes serán capaces de:

1. **Seleccionar el servicio de contenedores más adecuado para diferentes escenarios de despliegue en la nube.**
2. **Configurar y utilizar Azure Container Registry (ACR) para almacenar imágenes Docker de manera segura.**
3. **Automatizar la creación y gestión de recursos en Azure mediante scripts y comandos de Azure CLI.**
4. **Utilizar variables y secretos de manera eficiente y segura en los pipelines de Azure DevOps.**
5. **Desarrollar y ejecutar un pipeline CI/CD completo que incluya la construcción y despliegue de contenedores en Azure.**

### 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 2 (Libro Ingeniería de Software: Unidad 18)

### 3- Consignas a desarrollar en el trabajo práctico:

#### Conceptos generales y explicaciones de los mismos
##### Servicios de Contenedores en Azure

Azure ofrece una amplia variedad de servicios para desplegar y gestionar aplicaciones basadas en contenedores, cada uno adecuado para diferentes escenarios y niveles de complejidad. A continuación se detallan los principales servicios de contenedores que ofrece Azure:

---

##### Azure Container Instances (ACI)
- **Despliegue Rápido y Sencillo de Contenedores**  
  Azure Container Instances es la opción más sencilla y rápida para desplegar contenedores en Azure. ACI permite ejecutar contenedores sin necesidad de gestionar servidores o infraestructuras complejas, lo que lo convierte en una excelente opción para tareas puntuales, desarrollo y pruebas. Además, ACI ofrece facturación por segundo, lo que lo hace muy rentable para cargas de trabajo de corta duración.

**Caso de uso:**  
Es ideal para procesamiento por lotes, cargas de trabajo eventuales o aplicaciones que no requieren orquestación avanzada ni alta disponibilidad.

---

##### Azure App Services con Soporte para Contenedores
- **Plataforma Gestionada para Aplicaciones Web y APIs en Contenedores**  
  Azure App Services es una plataforma gestionada para aplicaciones web y APIs que soporta contenedores Docker. Este servicio permite desplegar aplicaciones con alta disponibilidad sin necesidad de gestionar la infraestructura subyacente. Además, App Services ofrece escalabilidad automática, integración con pipelines de CI/CD y soporte para múltiples lenguajes de programación.

**Caso de uso:**  
Es ideal para aplicaciones web y APIs que requieren integración con otros servicios de Azure y que necesitan escalabilidad y alta disponibilidad sin preocuparse por la gestión de servidores.

---

##### Azure Kubernetes Service (AKS)
- **Orquestación Completa de Contenedores**  
  Azure Kubernetes Service es la opción gestionada de Kubernetes en Azure, diseñada para proyectos que requieren una orquestación completa de contenedores. AKS permite gestionar clústeres de Kubernetes de manera simplificada, proporcionando escalabilidad automática, distribución de carga y recuperación ante fallos. A pesar de que Azure gestiona la infraestructura subyacente, los usuarios tienen control total sobre el clúster y las configuraciones de Kubernetes.

**Caso de uso:**  
AKS es ideal para aplicaciones a gran escala, microservicios y cargas de trabajo críticas que necesitan una orquestación avanzada, alta disponibilidad y flexibilidad en la gestión de contenedores.

---

##### Azure Container Apps
- **Orquestación Simplificada con Kubernetes**  
  Azure Container Apps es una plataforma basada en Kubernetes, pero que abstrae la complejidad de gestionar el clúster. Azure Container Apps permite desplegar y escalar automáticamente aplicaciones basadas en contenedores, ofreciendo escalabilidad basada en eventos y microservicios. Además, se integra con KEDA para escalado automático basado en eventos y con Dapr para facilitar patrones de microservicios.

**Caso de uso:**  
Es ideal para microservicios, aplicaciones sin servidor (serverless) y despliegues basados en eventos que requieren escalabilidad, pero sin la necesidad de gestionar Kubernetes directamente.

---

##### Azure Container Registry (ACR)
- **Servicio de Azure para Almacenamiento y Gestión de Imágenes de Contenedores**  
  Azure Container Registry es un servicio seguro y escalable que permite almacenar y gestionar imágenes de contenedores. ACR está diseñado para integrarse fácilmente con otros servicios de Azure, como AKS, ACI, y App Services, proporcionando una solución privada para almacenar y distribuir imágenes Docker. ACR también soporta características avanzadas como la replicación geográfica y políticas de seguridad robustas.

- **No es Obligatorio Usar ACR**  
  Aunque ACR es una opción poderosa y bien integrada en el ecosistema de Azure, no es obligatorio. Es posible desplegar contenedores en Azure utilizando otros registros como Docker Hub o registros privados de terceros. Sin embargo, ACR ofrece mayor seguridad y control en entornos de producción que requieren un manejo más estricto de las imágenes de contenedores.

**Caso de uso:**  
ACR es ideal para organizaciones que buscan una solución privada y segura para gestionar imágenes de contenedores dentro de sus entornos de Azure.

---

##### Azure Command Line Interface (Azure CLI)
- **Interfaz de Línea de Comandos Unificada**  
  Azure CLI es una interfaz de línea de comandos que permite interactuar con todos los servicios de Azure. Esta herramienta está diseñada para ser utilizada en scripts y pipelines de CI/CD, facilitando la automatización de tareas como la creación, actualización y eliminación de recursos en Azure. Azure CLI es compatible con Windows, macOS y Linux, y también está disponible en el portal de Azure a través de **Azure Cloud Shell**.

**Ejemplo:**  
Con comandos simples como `az group create` o `az container create`, es posible gestionar recursos de Azure como grupos de recursos y contenedores desde cualquier entorno de línea de comandos.

**Caso de uso:**  
Azure CLI es ideal para desarrolladores y equipos DevOps que buscan automatizar tareas en Azure de manera rápida y eficiente.

---

##### Variables en Pipelines de Azure DevOps
- **Parametrización y Reutilización en Pipelines**  
  Las variables en los pipelines de Azure DevOps permiten parametrizar y reutilizar información a lo largo del pipeline. Esto facilita la configuración de diferentes entornos (como QA, Staging y Producción) sin necesidad de cambiar el código fuente. Las variables pueden definirse directamente en el archivo YAML del pipeline o en la interfaz de usuario de Azure DevOps.

- **Secretos y Seguridad:**  
  Para manejar información sensible como contraseñas o claves API, se pueden definir variables como secretas, lo que garantiza que no sean expuestas en los logs. También es posible integrar **Azure Key Vault** para gestionar secretos de manera más segura.

**Caso de uso:**  
Las variables son esenciales para construir pipelines flexibles y adaptables que puedan desplegarse en múltiples entornos, mientras que los secretos garantizan que la información confidencial esté protegida durante todo el proceso de despliegue.

---

### 4- Desarrollo:
#### Prerequisitos:

#### 4.1 Modificar nuestro pipeline para construir imágenes Docker de back y front y subirlas a ACR
- Desarrollo del punto 4.1: 
	- ##### 4.1.1 Crear archivos DockerFile para nuestros proyectos de Back y Front
   	  - En la raiz de nuestro repo crear una carpeta docker con dos subcarpetas api y front, dentro de cada una de ellas colocar los dockerfiles correspondientes para la creación de imágenes docker en función de la salida de nuestra etapa de Build y Test
        	![image](https://github.com/user-attachments/assets/2debb92f-9d69-47f1-a85b-72abbc381035)

          - DockerFile Back:
			```yaml
			 # Imagen base para ejecutar la aplicación
			FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
			WORKDIR /app
			
			# Copiar los binarios preconstruidos de la API al contenedor
			# Espera que los binarios estén en la carpeta "api" en el contexto de construcción
			COPY ./api/ ./
			
			# Exponer los puertos 80 (HTTP) y 443 (HTTPS)
			EXPOSE 80
			EXPOSE 443
			
			# Configurar las URLs para que la aplicación escuche en HTTP y HTTPS
			ENV ASPNETCORE_URLS="http://+:80" 
			#;https://+:443"
			
			# Comando para ejecutar la aplicación
			ENTRYPOINT ["dotnet", "EmployeeCrudApi.dll"]
			#CMD ["/bin/bash"]
			```
          - DockerFile Front:
			```yaml
			# Utilizar la imagen base de nginx
			FROM nginx:alpine
			
			# Establecer el directorio de trabajo en el contenedor
			WORKDIR /usr/share/nginx/html
			
			# Eliminar los archivos existentes de la imagen base de nginx
			RUN rm -rf ./*
			
			# Copiar los archivos compilados de Angular al directorio de nginx
			COPY ./ .
			
			# Exponer el puerto 80 para servir la aplicación Angular
			EXPOSE 80
			```
   	- ##### 4.1.2 Crear un recurso ACR en Azure Portal siguiendo el instructivo 5.1
  	- ##### 4.1.3 Modificar nuestro pipeline en la etapa de Build y Test
   	  - Luego de la tarea de publicación de los artefactos de Back agregar la tarea de publicación de nuestro dockerfile de back para que esté disponible en etapas posteriores:
   	     ```yaml
	     - task: PublishPipelineArtifact@1
   	       displayName: 'Publicar Dockerfile de Back'
   	         inputs:
		   targetPath: '$(Build.SourcesDirectory)/docker/api/dockerfile'
		   artifact: 'dockerfile-back'
   	     ```
   	  - Luego de la tarea de publicación de los artefactos de Front agregar la tarea de publicación de nuestro dockerfile de front para que esté disponible en etapas posteriores:
   	     ```yaml
	     - task: PublishPipelineArtifact@1
   	       displayName: 'Publicar Dockerfile de Back'
   	         inputs:
		   targetPath: '$(Build.SourcesDirectory)/docker/front/dockerfile'
		   artifact: 'dockerfile-front'
   	     ```
	- ##### 4.1.4 Agregar a nuestro pipeline variables 
   	
  	- ##### 4.1.5 Agregar a nuestro pipeline una nueva etapa que dependa de nuestra etapa de Build y Test
   	     ```yaml
		# #----------------------------------------------------------
		# ### STAGE BUILD DOCKER IMAGES Y PUSH A AZURE CONTAINER REGISTRY
		# #----------------------------------------------------------
		
		- stage: DockerBuildAndPush
		  displayName: 'Construir y Subir Imágenes Docker a ACR'
		  dependsOn: BuildAndTestBackAndFront
		  jobs:
		    - job: docker_build_and_push
		      displayName: 'Construir y Subir Imágenes Docker a ACR'
		      pool:
		        vmImage: 'ubuntu-latest'
		
		      steps:
		        - checkout: self
		
		        #----------------------------------------------------------
		        # BUILD DOCKER BACK IMAGE Y PUSH A AZURE CONTAINER REGISTRY
		        #----------------------------------------------------------
		
		        - task: DownloadPipelineArtifact@2
		          displayName: 'Descargar Artefactos de Back'
		          inputs:
		            buildType: 'current'
		            artifactName: 'drop-back'
		            targetPath: '$(Pipeline.Workspace)/drop-back'
		        
		        - task: DownloadPipelineArtifact@2
		          displayName: 'Descargar Dockerfile de Back'
		          inputs:
		            buildType: 'current'
		            artifactName: 'dockerfile-back'
		            targetPath: '$(Pipeline.Workspace)/dockerfile-back'
		
		        - task: AzureCLI@2
		          displayName: 'Iniciar Sesión en Azure Container Registry (ACR)'
		          inputs:
		            azureSubscription: '$(ConnectedServiceName)'
		            scriptType: bash
		            scriptLocation: inlineScript
		            inlineScript: |
		              az acr login --name $(acrLoginServer)
		    
		        - task: Docker@2
		          displayName: 'Construir Imagen Docker para Back'
		          inputs:
		            command: build
		            repository: $(acrLoginServer)/$(backImageName)
		            dockerfile: $(Pipeline.Workspace)/dockerfile-back/dockerfile
		            buildContext: $(Pipeline.Workspace)/drop-back
		            tags: 'latest'
		
		        - task: Docker@2
		          displayName: 'Subir Imagen Docker de Back a ACR'
		          inputs:
		            command: push
		            repository: $(acrLoginServer)/$(backImageName)
		            tags: 'latest'
	```yaml          
  	

#### 4.4 Desafíos:


### 5- Instructivos:
### 5.1 Crear un recurso Azure Container Registry

1\. Crear un nuevo recurso en nuestro grupo de recursos

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-22/b9a2ff13-8768-41a9-b94a-e051fdd7fb4d/ascreenshot.jpeg?tl_px=0,0&br_px=859,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=309,124)


2\. Type "azure container registry [[enter]]"


3\. Click en Crear Container registry

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-22/7a92bebc-a386-4455-b6ef-32e6d5f2c14a/ascreenshot.jpeg?tl_px=83,356&br_px=1066,905&force_format=jpeg&q=100&width=983&wat_scale=87&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=153,345)


4\. Click the "Nombre del Registro" field.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-22/9e737759-10f4-442d-b7c6-20fbbe7f83cd/ascreenshot.jpeg?tl_px=41,98&br_px=1417,867&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=243,276)


5\. Ingresar un nombre unico para nuestro ACR, como &lt;iniciales&gt;IngSoft3UCCACR


6\. En el combo Plan de Precios seleccionar "Básico"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-22/2aac180a-ae02-4e48-93fa-b2438069feef/ascreenshot.jpeg?tl_px=78,261&br_px=1225,902&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=250,405)


7\. Click "Siguiente: Redes >"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-22/a061f990-29b5-4cfd-8b57-9ead220e0f4b/ascreenshot.jpeg?tl_px=41,149&br_px=1417,918&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=295,600)


8\. Click "Siguiente: Cifrado >"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-22/12d0b212-01d9-4967-84b6-009d2e0e6a22/ascreenshot.jpeg?tl_px=41,149&br_px=1417,918&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=295,600)


9\. Click "Siguiente: Etiquetas >"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-22/b16d170c-d16c-4157-a07f-46353f789e8a/ascreenshot.jpeg?tl_px=41,149&br_px=1417,918&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=295,600)


10\. Click "Siguiente: Revisar y crear >"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-22/1aa47fd4-b7af-4098-890f-5f0cff1034a6/ascreenshot.jpeg?tl_px=39,145&br_px=1424,919&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=294,600)


11\. Click "Crear"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-22/9897db3f-a47a-45f5-8308-54b198446b9a/ascreenshot.jpeg?tl_px=0,4&br_px=1541,966&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=10,632)


12\. Click "Ir al recurso"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-22/c68f069c-652e-454c-9cc0-06cdbaee683e/ascreenshot.jpeg?tl_px=78,65&br_px=1225,706&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=1,182)


13\. Copiar la url de nuestro recurso ACR

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-22/ce058583-1cf6-4e1f-9bb6-e18bb1b4eb35/ascreenshot.jpeg?tl_px=474,62&br_px=1457,611&force_format=jpeg&q=100&width=983&wat_scale=87&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=744,121)





### 6-  Presentación del trabajo práctico.
- Subir un doc al repo de GitHub con las capturas de pantalla de los pasos realizados. Debe ser un documento (md, word, o pdf), no videos. Y el documento debe seguir los pasos indicados en el Desarrollo del TP.
- Acceso al repo de Azure Devops para revisar el trabajo realizado.

### 7-  Criterio de Calificación
Los pasos 4.1 al 4.X representan un 60% de la nota total, los pasos 4.X y subsiguientes representan el 40% restante.

### 8-  Recursos Adicionales



