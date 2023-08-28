## Trabajo Práctico 5 - Herramientas de construcción de software

### 1- Objetivos de Aprendizaje
 - Utilizar herramientas de construcción de software y manejo de paquetes y dependencias

### 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 3 (Libro Continuous Delivery: Cap 6 y 13)

### 3- Consignas a desarrollar en el trabajo práctico:
  - Las aplicaciones utilizadas son del tipo "Hello World", dado que el foco del trabajo práctico es como construirlas y no el funcionamiento de la aplicación en sí.
  - En los puntos en los que se pida alguna descripción, realizarlo de la manera más clara posible.

### 4- Desarrollo:

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
