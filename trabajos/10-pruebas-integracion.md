# Trabajo Práctico 10 - Pruebas de Integración

### 1- Objetivos de Aprendizaje
 - Adquirir conocimientos sobre conceptos referidos a pruebas de integración (integration tests).
 - Generar y ejecutar pruebas de integración utilizado frameworks de código abierto.

### 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 5 (Libro Ingeniería de Software: Cap 8)

### 3- Consignas a desarrollar en el trabajo práctico:

#### Conceptos generales explicaciones de los mismos

#### Pruebas de integración
Una prueba de integración tiene como objetivo probar el comportamiento de un componente o la integración entre un conjunto de componentes. El término prueba funcional se usa a veces como sinónimo para prueba de integración. Las pruebas de integración comprueban que todo el sistema funciona según lo previsto, por lo que reducen la necesidad de pruebas manuales intensivas.

Este tipo de pruebas le permiten traducir sus historias de usuario en un conjunto de pruebas. La prueba se asemejaría a una interacción esperada del usuario con la aplicación.

#### Frameworks de pruebas 

Existen una gran variedad de herramientas o frameworks disponibles para las pruebas de integración, tanto para componentes del backend como del frontend. Estas pueden ser comerciales, de código abierto o desarrolladas y utilizadas internamente por las compañías de software.

En este trabajo práctico utilizaremos Codeceptjs como ejemplo.

#### Selenium

Selenium es una herramienta de prueba de software automatizada y de código abierto para probar aplicaciones web. Tiene capacidades para operar en diferentes navegadores y sistemas operativos. Selenium es un conjunto de herramientas que ayuda a los testers a automatizar las aplicaciones basadas en la web de manera más eficiente.

Podemos codificar las pruebas directamente en un lenguaje de programación, por ejemplo javascript y ejecutarlas como parte del proceso de CI/CD.

#### Codeceptjs https://codecept.io/

Codeceptjs es un framework end to end para pruebas de integración y de aceptación de usuario, es muy simple de usar y abstrae al que escribe los tests de trabajar directamente con el driver de Selenium o algún otro driver.

## 4- Desarrollo:

#### 1- Familiarizarse con CodeceptJs
  - El objeto **I** y sus funcionalidades básicas: https://codecept.io/basics

#### 2- Testeando la página de GitHub

- Instalar NodeJs v12 o superior: https://nodejs.org/en/download/
- En un directorio, por ejemplo **.\proyectos\tp10** ejecutar:

```bash
npx create-codeceptjs .
```

- Ininicializar un nuevo proyecto CodeceptJS:
```bash
npx codeceptjs init
```
- Elegimos las opciones por defecto, ponemos **sample** cuando se nos pregunte por el nombre del primer test:

<img width="910" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/de7b784f-49c2-40ac-97fb-2ff4dd87e693">


- Editar el archivo **sample_test.js** generado:
```
Feature('My First Test');

Scenario('test something', ({ I }) => {
  I.amOnPage('https://github.com');
  I.see('GitHub');
});
```

- Finalmente correr el test:
```npx codeceptjs run```

<img width="463" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/90911ffb-6882-47c0-bbf3-c40bfafeba13">

- Agregamos otras validaciones
```javascript
Scenario('test something', ({ I }) => {
    I.amOnPage('https://github.com');
    I.see('GitHub');
    I.see('The home for all developers')
    I.scrollPageToBottom()
    I.seeElement("//li[contains(.,'© 2022 GitHub, Inc.')]")
});
```
- En el resultado vemos que falla, dado que la página de github ha cambiado.
- Actualizamos nuestro escenario:

```
Feature('My First Test');

Scenario('test something', ({ I }) => {
    I.amOnPage('https://github.com');
    I.see('GitHub');
    I.see('Let’s build from here')
    I.scrollPageToBottom()
    I.seeElement("//li[contains(.,'© 2023 GitHub, Inc.')]")
});
```
- Volvemos a correr el test:
```npx codeceptjs run```
- Verificamos que el test haya sido exitoso
  
#### 3- Testeando una aplicación Angular

- Clonar repo
```
git clone https://github.com/ingsoft3ucc/angular-sample.git
```
- Instalamos dependencias con npm

```
cd angular-sample
npm install
```
- Corremos el proyecto

```
ng serve
```

- Navegamos a http://localhost:4200

  ![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/bab4c8e4-a151-4bc4-8b82-53105a922b58)

  
- Creamos el proyecto de codeceptjs

```bash
npx create-codeceptjs .
```

 - Inicializar CodeceptJS: ```npx codeceptjs init```


- Responder las preguntas. Aceptar valores por defecto. Cuando pregunte por url colocar `http://localhost:4200` y y el nombre de los tests poner `angular-sample`


- Editar el archivo generado `angular-sample_tests.js` de manera tal que se pruebe la funcionalidad de login en los escenarios login correcto y login incorrecto

- Levantar la aplicación en otra consola :
```bash
ng serve
```

<img width="800" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/e9a6984b-b8ca-4f58-ad1a-9ac2cbd6503f">


- Ejecutar los tests

```
npx codeceptjs run --steps
```
<img width="556" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/789f6036-bed3-4f2c-ae17-2b94b63b6e76">

#### 4- Habilitar reportes
- Instalar el módulo para reporting
```bash
npm i mocha-junit-reporter mocha-multi --save
```
<img width="754" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/755e4412-dbfa-42a6-81cd-cb9012de60b3">

- Reemplazar la key mocha en el archivo codecept.conf.js por:

```javascript
const { setHeadlessWhen, setCommonPlugins } = require('@codeceptjs/configure');
// turn on headless mode when running with HEADLESS=true environment variable
// export HEADLESS=true && npx codeceptjs run
setHeadlessWhen(process.env.HEADLESS);

// enable all common plugins https://github.com/codeceptjs/configure#setcommonplugins
setCommonPlugins();

/** @type {CodeceptJS.MainConfig} */
exports.config = {
  tests: './*_test.js',
  output: './output',
  helpers: {
    Playwright: {
      browser: 'chromium',
      url: 'http://localhost:4200',
      show: false
    }
  },
  include: {
    I: './steps_file.js'
  },
  
  mocha: {
     reporter: 'mochawesome',
     reporterOptions: {
       reportDir: './output',
       reportFilename: 'mochawesome-report',
     },
   },
  
  name: 'angular-sample'
}
```

- Ejecutar los tests nuevamente
```bash
npx codeceptjs run --steps --reporter mochawsome
```
 

- Hacemos un push hacia nuestro repo

#### 5 - Presentación
Subir todo el código, ejemplos y respuestas a una carpeta trabajo-practico-10.

