
## Trabajo Práctico 7 - Servidor de Build (de integración continua).
### 1- Objetivos de Aprendizaje
 - Adquirir conocimientos acerca de las herramientas de integración continua.
 - Configurar este tipo de herramientas.
 - Implementar procesos de construcción automatizado simples.

### 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 3 (Libro Continuous Delivery: Cap 3)


CI (Continuous Integration), Continuous Deployment y Continuous Delivery son tres prácticas clave en la ingeniería de software que se utilizan para mejorar la calidad del software y acelerar el proceso de desarrollo. Aunque están relacionadas y a menudo se utilizan juntas, tienen diferencias clave:

**Continuous Integration (CI):**

CI es una práctica que implica la integración constante de cambios de código en un repositorio compartido por parte de varios desarrolladores.
Los desarrolladores envían regularmente su código al repositorio compartido (a menudo varias veces al día).
Cada vez que se envía código, se activan pruebas automáticas para verificar la calidad y la compatibilidad del código.
El objetivo principal de CI es detectar y resolver problemas de integración de código de manera temprana y continua, lo que evita la acumulación de errores.

**Continuous Delivery** 
En Continuous Delivery, después de que el código pasa por CI y se considera estable, se automatiza el proceso de empaquetado y preparación para la entrega.
Sin embargo, la entrega real al entorno de producción se realiza manualmente después de una revisión y aprobación humanas.

**Continuous Deployment (CD)**
Se refiere a la práctica de automatizar y acelerar el proceso de entrega de software al entorno de producción.
En Continuous Development, una vez que el código pasa por el proceso de CI y se considera estable, se automatiza la entrega del software al entorno de producción sin intervención manual adicional.
Esto implica la automatización de tareas como pruebas adicionales, empaquetado, despliegue y configuración en el entorno de producción.

En resumen, CI se centra en la integración continua de cambios de código y pruebas automáticas, mientras que Continuous Delivery y Continuous Deployment se centran en la automatización del proceso de entrega de software al entorno de producción, con Continuous Delivery deteniéndose antes de la entrega real y Continuous Deployment automatizando todo el proceso hasta la entrega al entorno de producción. 
Estas prácticas son esenciales en el desarrollo de software ágil y permiten la entrega rápida y confiable de software de alta calidad.

**JENKINS**

Jenkins es un servidor de integración continua (CI). Jenkins se utiliza principalmente para automatizar y gestionar el proceso de integración continua, lo que significa que se enfoca en la integración constante de cambios de código en un repositorio compartido y en la ejecución de pruebas automáticas para garantizar la calidad del software.

Si bien Jenkins es una herramienta muy versátil y extensible, puede ser parte de un flujo de trabajo más amplio que incluye Continuous Delivery (CD) o Continuous Deployment (CD), pero por sí mismo, Jenkins se centra en la CI.

Para implementar Continuous Delivery o Continuous Deployment, Jenkins se utiliza en combinación con otras herramientas y prácticas para automatizar el proceso de empaquetado, despliegue y entrega de software en entornos de producción. Estas prácticas más amplias involucran la automatización de todo el proceso de desarrollo y entrega de software, y Jenkins puede ser una pieza importante de esa automatización, pero su función principal sigue siendo la de un servidor de integración continua.

### 3- Consignas a desarrollar en el trabajo práctico:
 - Para una mejor evaluación del trabajo práctico, incluir capturas de pantalla de los pasos donde considere necesario.

### 4- Desarrollo:

#### 1- Poniendo en funcionamiento Jenkins
  - Crear una imagen de Docker que se base en la imagen oficial de Jenkins y que tenga instalado .NET Core. Crear un archivo llamado Dockerfile.jenkins con el siguiente contenido:
  
```bash
FROM jenkins/jenkins:lts

USER root

# Instala dependencias necesarias
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    software-properties-common \
    wget

# Agrega el repositorio de Microsoft y actualiza
RUN wget -q https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    apt-get update

# Instala el SDK de .NET Core
RUN apt-get install -y dotnet-sdk-7.0

USER jenkins
```

- Desde la misma ubicación donde tengas el archivo Dockerfile personalizado, ejecuta el siguiente comando para construir una nueva imagen de Docker con .NET Core y Jenkins. Esto creará una nueva imagen de Docker llamada jenkins-with-dotnetcore:
```bash
docker build -t jenkins-with-dotnetcore -f Dockerfile.jenkins .
```
- Ejecuta un Contenedor con la Nueva Imagen. Ahora, puedes ejecutar un contenedor utilizando la imagen que acabas de crear:
```bash
# Linux / Mac OS

mkdir -p ~/jenkins
docker run -d -p 8080:8080 -p 50000:50000 --name jenkins \
-v jenkins_home:/var/jenkins_home \
jenkins-with-dotnetcore

```

```bash
# windows

mkdir -p c:\jenkins
docker run -d -p 8080:8080 -p 50000:50000 --name jenkins -v c:\jenkins:/var/jenkins_home jenkins-with-dotnetcore
```




  - Una vez en ejecución, abrir http://localhost:8080
  - Inicialmente deberá especificar el texto que se encuentra dentro del archivo ~/jenkins/secrets/initialAdminPassword **en el contenedor**
```bash
cat ~/jenkins/secrets/initialAdminPassword
```
  - Instalar los plugins por defecto
![alt text][imagen]

[imagen]:  jenkins-plugins.png  
  - Crear el usuario admin inicial. Colocar cualquier valor que considere adecuado.
![alt text][imagen1]

[imagen1]:  jenkins-admin.png    


#### 2- Instalando Plugins y configurando herramientas
  - En Administrar Jenkins vamos a la sección de Administrar Plugins
  - De la lista de plugins disponibles instalamos .NET SDK Support
  - Reiniciamos el servidor
  - Abrir nuevamente página de Plugins y explorar la lista, para familiarizarse qué tipo de plugins hay disponibles.

**Tipos de Jobs**

En Jenkins, los proyectos de estilo libre (también conocidos como proyectos de construcción de estilo libre o freestyle projects) y los pipelines son dos enfoques diferentes para crear y configurar trabajos de automatización. 
**Proyecto de Estilo Libre (Freestyle Project):**

-Interfaz Gráfica Amigable: Los proyectos de estilo libre utilizan una interfaz gráfica basada en formularios y menús desplegables que facilita la configuración del trabajo sin necesidad de escribir código o scripts.

-Configuración Basada en Pasos: En un proyecto de estilo libre, configuras el trabajo mediante una serie de pasos predefinidos, como "Construir", "Publicar", "Notificar", etc. Cada paso se configura utilizando opciones y campos específicos.

-Facilidad para Usuarios No Técnicos: Los proyectos de estilo libre son ideales para usuarios que no están familiarizados con la creación de scripts o que desean una configuración rápida y simple.

-Limitaciones en la Lógica de Flujo: Pueden resultar limitados para implementar flujos de trabajo más complejos y condicionales, ya que la lógica de ejecución se basa principalmente en la configuración de pasos secuenciales.

**Pipeline:**

-Definición como Código: Los pipelines se definen como código en un DSL (lenguaje específico de dominio) llamado "Pipeline DSL". Esto significa que defines tu flujo de trabajo como un script de Jenkinsfile, generalmente escrito en Groovy.

-Mayor Flexibilidad: Los pipelines ofrecen una mayor flexibilidad y capacidad para crear flujos de trabajo altamente personalizados y condicionales. Puedes utilizar lógica de programación y estructuras de control en tu Jenkinsfile.

-Gestión de Versiones: Los Jenkinsfiles se pueden gestionar en sistemas de control de versiones (como Git), lo que permite un control de versiones completo y seguimiento de cambios en tus flujos de trabajo.

-Reutilización y Modularidad: Puedes reutilizar secciones de código en múltiples trabajos de Jenkins al utilizar funciones y definiciones compartidas en tus Jenkinsfiles.

-Mayor Escalabilidad: Los pipelines son más adecuados para proyectos grandes y complejos, donde se requiere una gestión más avanzada de flujos de trabajo, paralelismo y manejo de errores.

-En resumen, la principal diferencia radica en la forma en que se configuran y gestionan los trabajos de Jenkins. Los proyectos de estilo libre son más simples y se basan en una configuración gráfica, mientras que los pipelines son más flexibles, versátiles y se definen como código, lo que los hace ideales para flujos de trabajo más complejos y para equipos de desarrollo que prefieren la gestión de código fuente para sus flujos de trabajo de Jenkins. La elección entre uno u otro dependerá de tus necesidades y preferencias específicas.

#### 3- Creando el primer Job de estilo libre
  - Crear un nuevo item, del tipo estilo libre con nombre **first-job**
    ![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/b7ba3848-4cb4-419e-8116-924ecd59d538)

  - Una vez creado el job, en la sección Build Steps seleccionamos **Ejecutar linea de comandos (shell)** y escribimos:
    ![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/ff7660e5-5887-4a2c-8be7-dfb98357fdc5)

    ![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/b086b436-c41f-4d9b-be65-e8649b4a85e1)


```bash
current_datetime=$(date +"%Y-%m-%d %H:%M:%S")
Imprime la fecha y hora actual utilizando el comando echo
echo "La fecha y hora actual es: $current_datetime"
```

  - Guardamos y ejecutamos el Job
  - Analizar la salida del mismo

#### 4- Creando el primer Pipeline Job
  - Crear un nuevo item, del tipo Pipeline con nombre **hello-world**
  - Una vez creado el job, en la sección Pipeline seleccionamos **try sample Pipeline** y luego **Hello World**
  - Guardamos y ejecutamos el Job
  - Analizar la salida del mismo


#### 5- Creando un Pipeline Job con Git
  - Similar al paso anterior creamos un ítem con el nombre **github-job**
  - En script escibir:
```bash
  pipeline {
    agent any

   
    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/ingsoft3ucc/SimpleWebAPI'

            }
        }
    }
 }  
```
    
  ![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/6724bc06-44fa-4e88-85d5-13a3f95938b6)

  - Guardar y ejecutar el Job
  - Analizar el script, para identificar los diferentes pasos definidos y correlacionarlos con lo que se ejecuta en el Job y se visualiza en la página del Job.

#### 6- Utilizando nuestros proyectos. 
#### 6.1- .NET Core

  - Crear un Job de estilo libre llamado "**git-netcore-job**" que construya el proyecto en .NET Core del ejercicio 1 del TP 05.
  - Configurar el Job para obtener el código desde el repositorio de cada alumno:
 ![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/832cc713-ca04-4baa-9e19-b9d66b880412)

  - Agregar las credenciales correspondientes:
     
![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/bf2a9b63-321e-4904-8b20-74291cc43785)

![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/afd7a315-c3db-4913-bdf8-a874ab31508a)

- Indicar la rama desde la cual se construira:

![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/e08d13b5-a25b-433d-b2a0-0f7cf4b8f01a)
- Configurar las etapas de Build y Publish del proyecto

![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/825c9d07-2302-4656-9808-5deeb54994ea)

  - Corremos el Job y revisamos la salida.

#### 6.2- Monitorear Cambios en el repo de GitHub
 - Configurar Poll cada 1 minuto
 - Verificar su funcionamiento al hacer un commit y cuando no se hizo commit
 - Explicar por que no es posible tener un WebHook en nuestro TP
   
#### 6.3- Node.js
 - Repetir el ejercicio 6.1 para construir el proyecto del ejercicio 2 del TP 05.


