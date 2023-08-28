## Trabajo Práctico 5 - Herramientas de construcción de software

### 1- Objetivos de Aprendizaje
 - Utilizar herramientas de construcción de software y manejo de paquetes y dependencias

### 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 3 (Libro Continuous Delivery: Cap 6 y 13)

### 3- Consignas a desarrollar en el trabajo práctico:
  - Las aplicaciones utilizadas son del tipo "Hello World", dado que el foco del trabajo práctico es como construirlas y no el funcionamiento de la aplicación en sí.
  - En los puntos en los que se pida alguna descripción, realizarlo de la manera más clara posible.

### 4- Desarrollo:



#### 8- Ejemplo con nodejs

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


#### 9- Ejemplo con python
- Instalar dependencias (Ejemplo Ubuntu) varía según el OS:
```
sudo apt install build-essential python3-dev
pip3 install cookiecutter
```
- Correr el scaffold
```bash
$ cookiecutter https://github.com/candidtim/cookiecutter-flask-minimal.git
application_name [Your Application]: test
package_name [yourapplication]: test
$
```
- Ejecutar la aplicación
```bash
cd test
make run
```
- Acceder a la aplicación en: http://localhost:5000/
- Explicar que hace una tool como cookiecutter, make y pip.

#### 10- Build tools para otros lenguajes
- Hacer una lista de herramientas de build (una o varias) para distintos lenguajes, por ejemplo (Rust -> cargo)
- Elegir al menos 10 lenguajes de la lista de top 20 o top 50 de tiobe: https://www.tiobe.com/tiobe-index/


#### 11- Presentación

- Subir todo el código, ejemplos y respuestas a una carpeta trabajo-practico-05.

> Tip: Agregar un archivo .gitignore al repositorio para evitar que se agreguen archivos que son resultado de la compilación u otros binarios, que no son necesarios, al mismo.
