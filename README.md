# Ingeniería del Software 3 - Práctico

Repositorio Git de Ingeniería de Software 3 - 2024

# Agenda

Durante este curso, exploraremos una variedad de herramientas y conceptos esenciales que son fundamentales para el desarrollo y la gestión de sistemas modernos

* **Git Básico:** Comenzaremos con una introducción a Git, la herramienta de control de versiones más utilizada. Aprenderemos los conceptos fundamentales y las operaciones básicas para gestionar y colaborar en proyectos de software de manera eficiente.

* **Docker**: Nos adentraremos en Docker, una plataforma que permite desarrollar, enviar y ejecutar aplicaciones en contenedores. Veremos cómo crear y gestionar contenedores, así como las mejores prácticas para su uso en entornos de desarrollo y producción.

* **Azure y Azure DevOps**: Exploraremos los servicios de Microsoft Azure y Azure DevOps, enfocándonos en cómo desplegar y gestionar aplicaciones en la nube. Aprenderemos a utilizar herramientas de integración continua y entrega continua para automatizar procesos de desarrollo y despliegue.

* **Introducción a Sistemas Distribuidos y Arquitectura de Microservicios**: Exploraremos cómo utilizar los servicios de Azure para implementar soluciones distribuidas y contenerizadas aprovechando sus capacidades para crear aplicaciones escalables y resilientes.

* **Administración de Dependencias:** Revisaremos herramientas como NuGet y npm para la administración de dependencias en nuestros proyectos. Aprenderemos cómo gestionar bibliotecas y paquetes de manera eficiente, asegurando que nuestras aplicaciones estén siempre actualizadas y libres de conflictos.

* **Pipelines de Build y Deploy**: Aprenderemos a configurar y gestionar pipelines de construcción y despliegue, los cuales son esenciales para mantener la calidad y la consistencia en el desarrollo de software. Veremos cómo automatizar estos procesos para mejorar la eficiencia y reducir errores humanos.

* **Pruebas Unitarias y Pruebas de Integración:** Finalizaremos con una exploración de las pruebas unitarias y de integración, dos tipos cruciales de pruebas en el desarrollo de software. Aprenderemos a escribir y ejecutar pruebas automatizadas para asegurar que nuestro código sea robusto y funcione según lo esperado.

Estos temas nos proporcionarán una base sólida en las prácticas modernas de desarrollo y operaciones en ingeniería de sistemas, preparándonos para enfrentar los desafíos del mundo real con confianza y habilidad. 

**¡Esperamos que disfruten y aprovechen al máximo este semestre!**

# Condiciones para la Presentación de Trabajos Prácticos

A continuación, se detallan las condiciones para la presentación de los trabajos prácticos:

* **Formato de Entrega:** La entrega del trabajo se realizará directamente en un repositorio de Git generado por cada alumno. Asegúrense de que el repositorio esté correctamente configurado y accesible.

* **Tiempo de Entrega:** Cada trabajo práctico debe ser entregado en un plazo de 2 semanas a partir de la fecha de asignación. Los trabajos presentados fuera de plazo se considerarán no entregados.

* **Criterios de Evaluación:** Se evaluará tanto la completitud del trabajo como la presentación del mismo. Asegúrense de que su trabajo esté completo y presentado de una manera clara y ordenada. 

* **Parciales:** No habrá parciales, el promedio final de notas de cada Trabajo Práctico se considerará como nota de Parcial.

# Condiciones para la regularidad

* Asistencia a un mínimo del 70% de las clases prácticas

* Nota de Parcial mayor a 4

* No se promociona, se debe presentar un TP Integrador

# Trabajo Práctico Integrador: Requisitos y Validación

El Trabajo Práctico Integrador es un componente esencial para la aprobación del examen final teórico de esta materia. Se presenta el día que se rinde el final de la materia.

El Trabajo Práctico Integrador es un componente esencial para la aprobación del examen final teórico de esta materia. Se presenta el día que se rinde el final de la materia.

* **Requisitos del Proyecto Integrador**:

  * **Aplicación Completa:** Utilicen una aplicación, ya sea desarrollada por ustedes o un proyecto existente en GitHub, que incluya:
    - Un servicio de frontend.
    - Un servicio de backend.
    - Interacción con base(s) de datos.
    - Repositorio en Git: La aplicación debe estar alojada en un repositorio público Git.

  * **Build y Deploy Automatizados:** Configuren la construcción y el deploy de la aplicación de manera automatizada utilizando herramientas vistas en clase, como Azure Devops Pipelines o GitHub Actions
    - Cada pull request aprobado a la rama master debe construir la aplicación automáticamente.
    - Deben ejecutar los tests de unidad, recolectar y mostrar los resultados.
    - Superados los test de unidad, el pipeline debe realizar el deploy automáticamente al entorno de QA ejecutando además pruebas de integración.
    - Debe existir una aprobación manual para aprobar el pase al entorno de Producción
    - Test Cases: Presenten los test cases escritos, incluyendo los tests de integración.
   
  * **Validación**

    Para validar su proyecto, se realizará lo siguiente:

   * El profesor pedirá un pequeño cambio en el código para validar que:
     - Se corren las pruebas unitarias, se deberá visualizar un informe/reporte
     - Se corre correctamente el proceso automatizado de Build
     - Se corre correctamente el proceso automatizado de Deploy
     - La versión en QA refleja dicha modificación.
     - Se corren las pruebas de integración, se deberá visualizar un informe/reporte
     - Se realiza la aprobación manual para el pase al entorno de PROD.

  * El profesor pedirá un pedirá un pequeño cambio en un test unitario para validar que:
    - El fallo de un test unitario aborta el proceso automatizado de Build y pasos subsiguientes.

Asegúrense de cumplir con todos los requisitos y procedimientos establecidos para asegurar una evaluación satisfactoria. Cualquier mejora o agregado se tendrá en cuenta para la nota final del proyecto.


# Tabla de contenidos


  * [Trabajo Práctico 1 - Git Básico](trabajos/01-git-basico.md)
  * [Trabajo Práctico 2 - Introducción a Docker](trabajos/02-introduccion-docker.md)
  * [Trabajo Práctico 3 - Introducción a Azure DevOps](trabajos/03-introduccion-azuredevops.md)
  * [Trabajo Práctico 4 - Azure DevOps Build Pipelines](trabajos/04-ado-pipelines.md)
  * [Trabajo Práctico 5 - Azure DevOps Release Pipelines](trabajos/05-ado-release-pipelines.md)
  * [Trabajo Práctico 6 - Pruebas Unitarias](trabajos/06-unit-tests.md)
  * [Trabajo Práctico 7 - Code Coverage, Análisis Estático de Código y Pruebas de Integración](trabajos/07-code-coverage_integration-tests.md)
  * [Trabajo Práctico 8 - Implementación de Contenedores en Azure y Automatización con Azure CLI](trabajos/08-contenedores-azure-automatizacion-azcli.md)
  * [Trabajo Práctico 9 - Implementación de Contenedores en Azure Parte 2](trabajos/09-contenedores-azure-automatizacion-Parte2.md)

