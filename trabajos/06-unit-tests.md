## Trabajo Práctico 6 - 

### 1- Objetivos de Aprendizaje
 - Adquirir conocimientos acerca de las herramientas de despliegue y releases de aplicaciones.
 - Configurar este tipo de herramientas.
 - Comprender el concepto de recurso en Azure
 - Comprender los conceptos básicos de Release Pipelines en Azure DevOps.
 - Configurar un Release Pipeline para automatizar despliegues en diferentes entornos-

### 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 3 (Libro Continuous Delivery: Cap 10)

### 3- Consignas a desarrollar en el trabajo práctico:
 - Los despliegues (deployments) de aplicaciones se pueden realizar en diferentes tipos de entornos
   - On-Premise (internos) es decir en servidores propios.
   - Nubes Públicas, ejemplo AWS, Azure, Gcloud, etc.
   - Plataformas como servicios (PaaS), ejemplo Heroku, Google App Engine, AWS, Azure WebApp, etc
 - En este práctico haremos despliegue a Plataforma como Servicio utilizando Azure Web Apps

### 4- Desarrollo:
4.1\. Crear una cuenta en Azure

4.2\. Crear un recurso Web App en Azure Portal y navegar a la url provista

4.3\. Actualizar Pipeline de Build para que use tareas de DotNetCoreCLI@2 como en el pipeline clásico, luego crear un Pipeline de Release en Azure DevOps con CD habilitada

4.4\. Optimizar Pipeline de Build

4.5\. Verificar el deploy en la url de la WebApp /weatherforecast

4.6\. Realizar un cambio al código del controlador para que devuelva 7 pronósticos, realizar commit, evaluar ejecución de pipelines de build y release, navegar a la url de la webapp/weatherforecast y corroborar cambio

4.7\. Clonar la Web App de QA para que contar con una WebApp de PROD a partir de un Template Deployment en Azure Portal y navegar a la url provista para la WebApp de PROD.

4.8\. Agregar una etapa de Deploy a Prod en Azure Release Pipelines 

4.9\.  Realizar un cambio al código del controlador para que devuelva 10 pronósticos, realizar commit, evaluar ejecución de pipelines de build y release, navegar a la url de la webapp/weatherforecast y corroborar cambio, verificar que en la url de la webapp_prod/weatherforecast se muestra lo mismo.

4.10\. Modificar pipeline de release para colocar una aprobación manual para el paso a Producción.

4.11\. Realizar un cambio al código del controlador para que devuelva 5 pronósticos, realizar commit, evaluar ejecución de pipelines de build y release, navegar a la url de la webapp/weatherforecast y corroborar cambio, verificar que en la url de la webapp_prod/weatherforecast aun se muestra la versión anterior.

4.12\. Aprobar el pase ya sea desde el release o desde el mail recibido. 
<img width="1197" alt="image" src="https://github.com/user-attachments/assets/05e8d1a1-ae06-4824-91d7-1a6e0162e859">

<img width="1221" alt="image" src="https://github.com/user-attachments/assets/33710115-a5c3-43ee-a208-5879331c7a8d">

<img width="1466" alt="image" src="https://github.com/user-attachments/assets/9655c548-d3da-4d29-8080-8324d711c18f">

4.12.1\. Notar que se puede dar la aprobación pero posponer su aplicación hasta una determinada fecha


<img width="1222" alt="image" src="https://github.com/user-attachments/assets/11f710b9-4ac1-4e2c-a560-7714835b2ce6">

4.13\. Esperar a la finalización de la etapa de Pase a Prod y luego corroborar que en la url de la webapp_prod/weatherforecast se muestra la nueva versión coinicidente con la de QA.
<img width="1465" alt="image" src="https://github.com/user-attachments/assets/533ac589-58e1-4f36-9356-d37a0da58220">

<img width="1125" alt="image" src="https://github.com/user-attachments/assets/26256e9d-28c5-41d7-97cb-e86df429e817">

4.14\. Realizar un pipeline (no release) que incluya el deploy a QA y a PROD con una aprobación manual. El pipeline debe estar construido en YAML sin utilizar el editor clásico de pipelines ni el editor clásico de pipelines de release.
 
### 5- Instructivos:
#### 5.1 Crear una Base de Datos SQL en Azure

# Create an Azure SQL Database Step-by-Step Guide
#### [Made by Ariel Schwindt with Scribe](https://scribehow.com/shared/Create_an_Azure_SQL_Database_Step-by-Step_Guide__qb46OueOQau-h-Z7rSw3pA)


1\. Navigate to [https://portal.azure.com/#home](https://portal.azure.com/#home)


2\. Seleccionar Grupo de Recursos

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/6b4af0eb-94ff-4d73-8462-bc46d37150ea/ascreenshot.jpeg?tl_px=0,0&br_px=1376,769&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=250,270)


3\. Click en Crear

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/d848857e-de1f-482c-9b7f-1cb5ec094747/ascreenshot.jpeg?tl_px=0,0&br_px=859,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=297,131)


4\. Buscar "sql database"


5\. Click "sql database"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/9de63352-364e-4f73-9aa6-1a6b48b17beb/ascreenshot.jpeg?tl_px=0,0&br_px=859,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=350,177)


6\. Click en Crear

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/ae6e9368-9d55-4fec-910d-65bd60e68699/ascreenshot.jpeg?tl_px=68,487&br_px=928,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,213)


7\. Ingresar &lt;Sus-Iniciales&gt;-sql-db" como nombre de la base de datos"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/e1ec24d7-ddcf-41db-8430-60856f9d67f1/ascreenshot.jpeg?tl_px=0,418&br_px=982,968&force_format=jpeg&q=100&width=983&wat_scale=87&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=387,346)


8\. Click "Crear nuevo"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/d1c9ab83-8de5-4218-ac79-8102cbed7ce3/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=309,346)


9\. Ingresas "&lt;sus-iniciales&gt;-sql-server01" como nombre del servidor


10\. Click "(US) East US"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/1b6df987-2a35-49d9-9068-8ee166934aee/ascreenshot.jpeg?tl_px=0,111&br_px=859,592&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=398,212)


11\. Click en el combo de Ubicación y buscar una Ubicación Disponible

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/1b1774ff-c8a7-4aca-841b-97220f7f1dee/ascreenshot.jpeg?tl_px=0,102&br_px=859,583&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=376,212)


12\. Click "(US) South Central US"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/ebdf1e76-cee4-4f70-b0f7-cd74764534a6/ascreenshot.jpeg?tl_px=0,109&br_px=859,590&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


13\. Click "Uso de la autenticación de SQL"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/2de48b5b-6dba-4da2-be76-58b13dd96acc/ascreenshot.jpeg?tl_px=0,469&br_px=859,950&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=327,212)


14\. Click the "Inicio de sesión del administrador del servidor" field.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/dcb5feab-afdc-4b48-8d9b-e2e7a7564b3f/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=329,230)


15\. Type "sqladmin [[tab]]"


16\. Ingresar contraseña deseada, por ejemplo Azure@456, repetirla y dar click en Aceptar

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/25848ed9-de32-4478-8312-b83766d713a5/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=64,414)


17\. Click en Implementación.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/7cf6b6f0-3735-4bfb-bee6-08b85bb8e824/ascreenshot.jpeg?tl_px=0,426&br_px=859,907&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=267,212)


18\. Click "Configurar base de datos"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/01966464-a4f2-4869-a6a5-1eaf98afe3e0/ascreenshot.jpeg?tl_px=0,470&br_px=859,951&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=325,212)


19\. Click "Básico (Para cargas de trabajo menos exigentes.)"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/294357c6-f9fd-407c-8ec5-d17881a0a32d/ascreenshot.jpeg?tl_px=69,145&br_px=928,626&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


20\. Click "Aplicar"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/92ecf786-cc63-460e-be22-ef40bf11fb3e/ascreenshot.jpeg?tl_px=0,6&br_px=1541,968&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=9,642)


21\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/c3dd8e15-9643-4804-9de7-ae8f47eb98d7/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=230,428)


22\. Click "Punto de conexión público"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/b4445028-1e4f-466d-83e1-55a810ea0275/ascreenshot.jpeg?tl_px=0,144&br_px=859,625&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=305,212)


23\. Click "Sí"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/135ebcbf-6416-4c95-96ea-57587cf909a6/ascreenshot.jpeg?tl_px=0,350&br_px=859,831&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=348,212)


24\. Click "Sí"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/fec30783-8133-456e-8b57-ecb94617f268/user_cropped_screenshot.jpeg?tl_px=0,163&br_px=982,712&force_format=jpeg&q=100&width=983&wat_scale=87&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=342,243)


25\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/e1c050da-1b6c-4aab-8443-c2d71cbd119e/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=325,429)


26\. Click "Siguiente: Configuración adicional >"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/3abe0aa9-a898-4662-b043-f2144482c761/ascreenshot.jpeg?tl_px=0,198&br_px=1376,968&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=271,561)


27\. Click "Siguiente: Revisar y crear >"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/64ddf80f-4816-4fa4-91ee-cf583d36e5c2/ascreenshot.jpeg?tl_px=0,6&br_px=1541,968&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=258,632)


28\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/07814b9b-1d6a-44db-b1c2-b582059a9540/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=57,419)


29\. Click "Ir al recurso"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/576067e4-6ed7-443e-8b01-59a37d9e72a8/ascreenshot.jpeg?tl_px=0,176&br_px=859,657&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=356,212)


30\. Click "Editor de consultas (versión preliminar)"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/379cc073-f83a-4c7d-a750-9421a52f63e9/ascreenshot.jpeg?tl_px=0,100&br_px=859,581&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=149,212)


31\. Click the "Inicio de sesión" field.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/aad2e638-d236-4285-9d78-a1e52acbd72b/ascreenshot.jpeg?tl_px=244,235&br_px=1104,716&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


32\. Ingresar usuario y contraseña, por ejemplo sqladmin y Azure@456


33\. Click "Aceptar"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/ccbcf84a-79a4-4669-bb0e-d06520c29d52/ascreenshot.jpeg?tl_px=283,343&br_px=1143,824&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


34\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/5e2fe0cc-9b57-4a55-9d2c-89ed5902f586/File.jpeg?tl_px=543,148&br_px=1403,629&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


35\. Ingresar el siguiente script de creacion de Tabla y registros


36\. Click en Ejecutar

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/da63790b-83e9-4548-9deb-3a1f29168443/ascreenshot.jpeg?tl_px=0,0&br_px=1376,769&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=479,156)


37\. Borrar el script

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/eece78cd-d480-44a5-b05a-d63bc5e3807a/ascreenshot.jpeg?tl_px=164,4&br_px=1541,773&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=621,276)


38\. Type "Select * from Employees"


39\. Click En Ejecutar.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/89d8081a-6c21-431d-aa23-53534bf0dd38/ascreenshot.jpeg?tl_px=0,0&br_px=1376,769&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=479,163)


40\. Click "Información general"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/4b5b1030-256a-4007-8f07-d17f322513f3/ascreenshot.jpeg?tl_px=0,0&br_px=1541,961&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=22,95)


41\. Click "Mostrar las cadenas de conexión de la base de datos"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/46644253-df61-4dfb-8977-82afc2cab377/ascreenshot.jpeg?tl_px=164,0&br_px=1541,769&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=837,244)


42\. Copiar

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/d3f34801-ac57-42d3-800f-ab27ff258a15/ascreenshot.jpeg?tl_px=164,120&br_px=1541,889&force_format=jpeg&q=100&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=644,277)


43\. Click this icon.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-06/5bcf3d84-707a-4e79-8995-90c17dc413b3/ascreenshot.jpeg?tl_px=681,321&br_px=1541,802&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=798,212)



### 6-  Presentación del trabajo práctico.
- Subir un doc al repo con las capturas de pantalla de los pasos realizados y tener en el excel de repos (https://docs.google.com/spreadsheets/d/1mZKJ8FH390QHjwkABokh3Ys6kMOFZGzZJ3-kg5ziELc/edit?gid=0#gid=0) la url del proyecto de AzureDevops.
- Aclarar los nombres de los pipelines que se deben evaluar.

### 7-  Criterio de Calificación
Los pasos 4.1 al 4.13 representan un 60% de la nota total, los pasos 4.13 y subsiguientes representan el 40% restante.

### 8-  Documentación y Recursos Adicionales
- https://learn.microsoft.com/en-us/azure/devops/?view=azure-devops

- https://learn.microsoft.com/en-us/azure/devops/pipelines/?view=azure-devops

- https://learn.microsoft.com/en-us/azure/devops/pipelines/yaml-schema/?view=azure-pipelines

- https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview

- https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/overview


