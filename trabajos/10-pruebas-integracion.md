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

Para este trabajo práctico vamos a probar aplicaciones web y rest y para ello utilizaremos Codeceptjs como ejemplo.

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
- En un directorio, por ejemplo **.\proyectos\ut** ejecutar:

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

- Para generar selectores fácilmente utilizamos plugins como (Firefox o Chrome)
  - TruePath https://addons.mozilla.org/en-US/firefox/addon/truepath/
  - ChroPath https://chrome.google.com/webstore/detail/chropath/ljngjbnaijcbncmcnjfhigebomdlkcjo
  
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


- Editar el archivo generado `angular-sample_tests.js`:
```javascript

```

- REVISAR!!!!!!!!! Reemplazar la sección helpers de codecept.conf.js por:

```javascript
	helpers: {
		REST: {
			endpoint: "http://localhost:4200",
			onRequest: () => {
			}
		}
	}
```

- Levantar la aplicación en otra consola :
```bash
ng serve
```
- Ejecutar los tests

```
npx codeceptjs run --steps
```

- Analizar resultados

#### 4- REVISARRR Habilitar reportes para utilizarlos en CICD
- Instalar el módulo para reporting
```bash
npm i mocha-junit-reporter mocha-multi --save
```
- Reemplazar la key mocha en el archivo codecept.conf.js por:

```javascript
	mocha:  {
    "reporterOptions": {
      "codeceptjs-cli-reporter": {
        "stdout": "-",
        "options": {
          "steps": true,
        }
      },
      "mocha-junit-reporter": {
        "stdout": "./output/console.log",
        "options": {
          "mochaFile": "./output/result.xml"
        },
        "attachments": true //add screenshot for a failed test
		  }
		}
	}
```

- Ejecutar los tests nuevamente
```bash
npx codeceptjs run --steps --reporter mocha-multi
```
 
- La salida compatible con Jenkins esta en ./output/results.xml

- Hacemos un push hacia nuestro repo

#### 5- Integrar la ejecución en Jenkins
- En Jenkins configuramos un pipeline para hacer un build de nuestra app Angular y ejecutar nuestros test.
- Creamos una nueva imagen de Jenkins que incluya nodejs para poder correr Angular con  este Dockerfile:
```
FROM jenkins/jenkins:lts

USER root

# Instala dependencias necesarias
RUN apt-get update && apt-get install -y nodejs npm \
    apt-transport-https \
    software-properties-common \
    wget

# Agrega el repositorio de Microsoft y actualiza
RUN wget -q https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    apt-get update

# Instala el SDK de .NET Core
RUN apt-get install -y dotnet-sdk-7.0
```
- Desde DockerDesktop o desde la terminal borramos el volumen jenkins_home si es que existe.
- Creamos la imagen a partir del dockkerfile:
```
docker build -t jenkins-ingsoft3 -f Dockerfile .
```
- Levantamos un contenedor con nuestra imagen:
```
cd  ~/jenkins
rm -rf jenjins
mkdir -p ~/jenkins
docker run -d -p 8080:8080 -p 50000:50000 --name jenkins \
-v jenkins_home:/var/jenkins_home \
jenkins-ingsoft3
```
- Inicializamos Jenkins como se indica en el TP7
- Creamos un pipeline llamado angular-sample reemplazando [MIREPO] :
```
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Print Node.js and npm versions
                    sh 'node --version'
                    sh 'npm --version'

                    // Get some code from a GitHub repository
                    git branch: 'master', url: 'https://github.com/[MIREPO]/angular-sample.git'

                    // Install dependencies using npm
                    def npmInstall = sh(script: 'npm install', returnStatus: true)
                    if (npmInstall != 0) {
                        error "npm install failed"
                    }

                    // Install Angular CLI globally
                    def ngInstall = sh(script: 'npm install -g @angular/cli', returnStatus: true)
                    if (ngInstall != 0) {
                        error "Angular CLI installation failed"
                    }

                    // Build the Angular project
                    def ngBuild = sh(script: 'ng build', returnStatus: true)
                    if (ngBuild != 0) {
                        error "ng build failed"
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Install CodeceptJS globally
                    def codeceptInstall = sh(script: 'npm install -g codeceptjs', returnStatus: true)
                    if (codeceptInstall != 0) {
                        error "CodeceptJS installation failed"
                    }

                    // Install Playwright dependencies
                    def playwrightDeps = sh(script: 'npx playwright install-deps', returnStatus: true)
                    if (playwrightDeps != 0) {
                        error "Playwright dependencies installation failed"
                    }

                    // Install Playwright
                    def playwrightInstall = sh(script: 'npx playwright install', returnStatus: true)
                    if (playwrightInstall != 0) {
                        error "Playwright installation failed"
                    }

                    // Run CodeceptJS tests
                    def codeceptRun = sh(script: 'npx codeceptjs run', returnStatus: true)
                    if (codeceptRun != 0) {
                        error "CodeceptJS tests failed"
                    }
                }
            }
        }
    }
}

```

