## Trabajo Práctico 9 - Implementación de Contenedores en Azure Parte 2

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

### 4- Desarrollo:

#### 4.1 Modificar nuestro pipeline para incluir el deploy en QA y PROD de Imagenes Docker en Servicio Azure App Services con Soporte para Contenedores
- Desarrollo del punto 4.1: 
	
  	- ##### 4.1.1 - Agregar a nuestro pipeline una nueva etapa que dependa de nuestra etapa de Construcción y Pruebas y de la etapa de Construcción de Imagenes Docker y subida a ACR realizada en el TP08
  	    
  	  - Agregar tareas para crear un recurso Azure Container Instances que levante un contenedor con nuestra imagen de back utilizando un AppServicePlan en Linux
  	  ```yaml
		#---------------------------------------
		### STAGE DEPLOY TO AZURE APP SERVICE QA
		#---------------------------------------
		- stage: DeployImagesToAppServiceQA
		  displayName: 'Desplegar Imagenes en Azure App Service (QA)'
		  dependsOn: 
		  - BuildAndTestBackAndFront
		  - DockerBuildAndPush
		  condition: succeeded()
		  jobs:
		    - job: DeployImagesToAppServiceQA
		      displayName: 'Desplegar Imagenes de API y Front en Azure App Service (QA)'
		      pool:
		        vmImage: 'ubuntu-latest'
		      steps:
		        #------------------------------------------------------
		        # DEPLOY DOCKER API IMAGE TO AZURE APP SERVICE (QA)
		        #------------------------------------------------------
		        - task: AzureCLI@2
		          displayName: 'Verificar y crear el recurso Azure App Service para API (QA) si no existe'
		          inputs:
		            azureSubscription: '$(ConnectedServiceName)'
		            scriptType: 'bash'
		            scriptLocation: 'inlineScript'
		            inlineScript: |
		              # Verificar si el App Service para la API ya existe
		              if ! az webapp list --query "[?name=='$(WebAppApiNameContainersQA)' && resourceGroup=='$(ResourceGroupName)'] | length(@)" -o tsv | grep -q '^1$'; then
		                echo "El App Service para API QA no existe. Creando..."
		                # Crear el App Service sin especificar la imagen del contenedor
		                az webapp create --resource-group $(ResourceGroupName) --plan $(AppServicePlanLinux) --name $(WebAppApiNameContainersQA) --deployment-container-image-name "nginx"  # Especifica una imagen temporal para permitir la creación
		              else
		                echo "El App Service para API QA ya existe. Actualizando la imagen..."
		              fi
		
		              # Configurar el App Service para usar Azure Container Registry (ACR)
		              az webapp config container set --name $(WebAppApiNameContainersQA) --resource-group $(ResourceGroupName) \
		                --container-image-name $(acrLoginServer)/$(backImageName):$(backImageTag) \
		                --container-registry-url https://$(acrLoginServer) \
		                --container-registry-user $(acrName) \
		                --container-registry-password $(az acr credential show --name $(acrName) --query "passwords[0].value" -o tsv)
		              # Establecer variables de entorno
		              az webapp config appsettings set --name $(WebAppApiNameContainersQA) --resource-group $(ResourceGroupName) \
		                --settings ConnectionStrings__DefaultConnection="$(cnn-string-qa)" \
	
  	  ```
  	     
#### 4.2 Desafíos:
- 4.2.1 Agregar tareas para generar Front en Azure App Service con Soporte para Contenedores
- 4.2.2 Agregar variables necesarias para el funcionamiento de la nueva etapa considerando que debe haber 2 entornos QA y PROD para Back y Front.
- 4.2.3 Agregar tareas para correr pruebas de integración en el entorno de QA de Back y Front creado en Azure App Services con Soporte para Contenedores. 
- 4.2.4 Agregar etapa que dependa de la etapa de Deploy en QA que genere un entorno de PROD.
- 4.2.5 Entregar un pipeline que incluya:
  - A) Etapa Construcción y Pruebas Unitarias y Code Coverage Back y Front
  - B) Construcción de Imágenes Docker y subida a ACR
  - C) Deploy Back y Front en QA con pruebas de integración para Azure Web Apps
  - D) Deploy Back y Front en QA con pruebas de integración para ACI
  - E) Deploy Back y Front en QA con pruebas de integración para Azure Web Apps con Soporte para contenedores
  - F) Aprobación manual de QA para los puntos C,D,E
  - G) Deploy Back y Front en PROD para Azure Web Apps
  - H) Deploy Back y Front en PROD para ACI
  - I) Deploy Back y Front en PROD para Azure Web Apps con Soporte para contenedores

### 6-  Presentación del trabajo práctico.
- Subir un doc al repo de GitHub con las capturas de pantalla de los pasos realizados. Debe ser un documento (md, word, o pdf), no videos. Y el documento debe seguir los pasos indicados en el Desarrollo del TP.
- Acceso al repo de Azure Devops para revisar el trabajo realizado.

### 7-  Criterio de Calificación
El paso 4.1 representa un 20% de la nota total, el paso 4.2 representa el 80% restante.




