## Trabajo Práctico 5 - Herramientas de construcción de software

### 1- Objetivos de Aprendizaje
 - Utilizar herramientas de construcción de software y manejo de paquetes y dependencias

### 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 3 (Libro Continuous Delivery: Cap 6 y 13)

### 3- Consignas a desarrollar en el trabajo práctico:
  - Las aplicaciones utilizadas son del tipo "Hello World", dado que el foco del trabajo práctico es como construirlas y no el funcionamiento de la aplicación en sí.
  - En los puntos en los que se pida alguna descripción, realizarlo de la manera más clara posible.

### 4- Desarrollo:
Un software administrador de paquetes es una herramienta esencial en el desarrollo de software que permite a los programadores gestionar eficientemente las bibliotecas, módulos y componentes de código reutilizable que se utilizan en un proyecto. En esencia, actúa como un intermediario que simplifica la incorporación, actualización y eliminación de estas piezas de software en una aplicación.

Su funcionalidad principal abarca desde la descarga automatizada de las bibliotecas necesarias hasta la resolución de conflictos y la garantía de coherencia en las versiones. Los administradores de paquetes también facilitan la especificación de las dependencias exactas o los rangos de versiones que un proyecto requiere, asegurando así que el software funcione de manera predecible y estable.

Estos sistemas, como npm para el ecosistema JavaScript o NuGet para el ecosistema .NET, reducen la carga de trabajo manual al automatizar tareas tediosas y propensas a errores. Al hacerlo, fomentan la reutilización de código, la colaboración entre desarrolladores y la creación eficiente de aplicaciones sólidas y escalables.

En resumen, un software administrador de paquetes es una herramienta esencial para la gestión eficiente de bibliotecas y componentes de código en proyectos de desarrollo de software. Proporciona una estructura organizada para incorporar, gestionar y mantener estas dependencias, lo que contribuye a la eficiencia, la coherencia y la calidad en el proceso de desarrollo.

Utilizar administradores de paquetes como npm (Node Package Manager) y NuGet en lugar de no hacerlo ofrece varias ventajas significativas en el desarrollo de software:

**Gestión de dependencias eficiente:**
En el desarrollo de software, es común utilizar bibliotecas y módulos externos para agilizar el proceso de programación. Sin embargo, manejar manualmente las dependencias puede ser complicado y propenso a errores. Los administradores de paquetes resuelven este problema al automatizar la gestión de dependencias. Te permiten definir las bibliotecas que tu proyecto necesita y aseguran que se instalen correctamente, eliminando la necesidad de descargar y configurar cada componente individualmente.

**Coherencia y estabilidad:**
Los administradores de paquetes garantizan que todas las versiones de las bibliotecas utilizadas en tu proyecto sean coherentes y compatibles entre sí. Esto previene problemas de incompatibilidad y conflictos que podrían surgir al mezclar diferentes versiones de bibliotecas manualmente. Además, la capacidad de especificar versiones exactas o rangos de versiones en los administradores de paquetes asegura que tu proyecto funcione de manera predecible y estable en todo momento.

**Reutilización de código y colaboración:**
Los administradores de paquetes fomentan la reutilización de código al permitir a los desarrolladores compartir sus bibliotecas y componentes con otros. Esto significa que puedes aprovechar el trabajo de otros y no tienes que reinventar la rueda en cada proyecto. La comunidad de desarrolladores contribuye con una amplia gama de paquetes, lo que acelera el desarrollo y mejora la calidad del software.

**Simplificación del proceso de desarrollo:**
Al utilizar administradores de paquetes, te liberas de la carga de tener que rastrear manualmente las actualizaciones de las bibliotecas, buscar nuevas versiones y realizar descargas manuales. Esto simplifica significativamente el proceso de desarrollo y te permite concentrarte en la lógica de tu aplicación en lugar de gestionar las dependencias.

**Mantenimiento y escalabilidad:**
Los proyectos de software tienden a crecer con el tiempo y pueden volverse complejos. Los administradores de paquetes facilitan el mantenimiento y la escalabilidad al proporcionar una forma ordenada de incorporar y gestionar nuevos componentes. Esto ayuda a mantener el código más limpio y facilita la adición de nuevas características y mejoras.

En resumen, utilizar administradores de paquetes como npm y NuGet es esencial en el desarrollo moderno debido a su capacidad para gestionar dependencias, garantizar la coherencia, fomentar la colaboración y simplificar el proceso de desarrollo. Estas herramientas ahorran tiempo, reducen errores y contribuyen a la creación de software más robusto y eficiente.

#### 1- Ejemplo con C# y .NET Core

- Instalar el SDK de .NET Core: Asegúrate de tener el SDK de .NET Core instalado en tu sistema. Puedes descargarlo desde el sitio web oficial de .NET: https://dotnet.microsoft.com/download
- Crear un Proyecto de Web API:
 - Abre una terminal y navega hasta la ubicación donde deseas crear tu proyecto. Luego, ejecuta el siguiente comando para crear un nuevo proyecto de Web API:
```bash
dotnet new webapi -n MiProyectoWebAPI
```
Esto creará un nuevo proyecto de Web API llamado "MiProyectoWebAPI" en un directorio con el mismo nombre.

Navegar al Directorio del Proyecto:
Ve al directorio del proyecto que acabas de crear:
```bash
cd MiProyectoWebAPI
```
Ejecutar la Aplicación:
Para ejecutar la aplicación de Web API, ejecuta el siguiente comando:

```bash
dotnet run
```
Esto iniciará la aplicación y la hará disponible en una URL local. Navegar a la url indicada en el mensaje recibido por consola añadiendo /weatherforecast
![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/e4fc5c40-8d78-47be-adcf-934b632b24ae)
![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/6906850e-0933-4f0d-ae92-adb749374a97)

- Revisar el archivo MiProyectoWebAPI.csproj:
- ![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/5d662d70-ac82-443e-9fba-af37fb191641)
- Revisar el archivo obj/debug/project.assets.json
- Borrar directorios bin y obj
- Agregar una nueva referencia a librería NewtonSoft:
```bash
dotnet add package Newtonsoft.Json
```
- Revisar nuevamente los archivos MiProyectoWebAPI.csproj y obj/debug/project.assets.json
- Borrar directorios bin y obj
- Ejecutar nuevamente:
```bash
dotnet run
```
- Revisar contenido de directorio bin/debug/net7.0



#### 2- Ejemplo con nodejs

- Instalar Nodejs: https://nodejs.org/en/

- Crear una nueva aplicación
```bash
npx create-react-app my-app
```

- Ejecutar la aplicación
```bash
cd my-app
npm start
```

- La aplicación web estará disponible en http://localhost:3000

- Analizar el manejo de paquetes y dependencias realizado por npm.



#### 3- Build tools para otros lenguajes
- Hacer una lista de herramientas de build (una o varias) para distintos lenguajes, por ejemplo (Rust -> cargo)
- Elegir al menos 10 lenguajes de la lista de top 20 o top 50 de tiobe: https://www.tiobe.com/tiobe-index/


#### 4- Presentación

- Subir todo el código, ejemplos y respuestas a una carpeta trabajo-practico-05.

> Tip: Agregar un archivo .gitignore al repositorio para evitar que se agreguen archivos que son resultado de la compilación u otros binarios, que no son necesarios, al mismo.
