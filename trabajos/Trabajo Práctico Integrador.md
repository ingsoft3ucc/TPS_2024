## Trabajo Práctico Integrador

La presentación de este trabajo práctico es **condición necesaria** para rendir el final teórico.


### 1- Lo que debe contemplar el proyecto integrador

-	Utilizar una aplicación (desarrollo propio o de un proyecto en github) que tenga al menos un servicio de backend, otro de frontend e interacción con base(s) de datos.
-	La aplicación debe estar en un repositorio de Git público.
-	Tener la construcción de la salida automatizada, utilizando alguna de las herramientas vistas en clase (Jenkins, GitHub Actions o alguna similar)
-	Cada commit a master deberá construir la aplicación
-	Se deberán correr los test de unidad y eventualmente recolectar y mostrar los resultados.
-	La salida de la construcción deberá ser una Imagen de Docker.
-	Esta imagen deberá ser almacenada en DockerHub
-	Desplegar la aplicación (Docker) en un entorno:	Puede ser Cloud (AWS, GCloud, Heroku):	Esto debe estar automatizado y ser parte del pipeline como por ejemplo otro job en Jenkins o alguna herramienta de las anteriormente mencionadas
-	Una vez desplegado, correr test de integración (codeceptjs). Se puede correr desde un Job o step en Jenkins. 
-	Mostrar alguna mejora o cambio en el código que se haya realizado (en el caso de usar un proyecto de github en lugar de un desarrollo propio)
-	Mostrar los test cases escritos (tests de integración e2e)
-	Cualquier agregado y/o mejora de lo antes descrito se tendrá en consideración para la nota del mismo.

### 2- Validación

- Se correrán Tests de Aceptación de Usuario automatizados contra la versión de producción.
- El profesor requerirá un pequeño cambio de código y se validará que la nueva versión en producción tenga dicha modificación.
