## Trabajo Práctico 6 - Pruebas Unitarias

### 1- Objetivos de Aprendizaje
 - Adquirir conocimientos sobre conceptos referidos a pruebas unitarias (unit tests).
 - Generar y ejecutar pruebas unitarias utilizando frameworks disponibles.

### 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 5 (Libro Ingeniería de Software: Cap 8)

### 3- Consignas a desarrollar en el trabajo práctico:
#### ¿Qué son las pruebas de software?
Una prueba de software es una pieza de software que ejecuta otra pieza de software. Valida si ese código da como resultado el estado esperado (prueba de estado) o ejecuta la secuencia de eventos esperados (prueba de comportamiento).

#### ¿Por qué son útiles las pruebas de software?
Las pruebas unitarias de software ayudan al desarrollador a verificar que la lógica de una parte del programa sea correcta.

Ejecutar pruebas automáticamente ayuda a identificar regresiones de software introducidas por cambios en el código fuente. Tener una cobertura de prueba alta de su código le permite continuar desarrollando características sin tener que realizar muchas pruebas manuales.

#### Código (o aplicación) bajo prueba
El código que se prueba generalmente se llama código bajo prueba . Si está probando una aplicación, esto se llama la aplicación bajo prueba .

#### Prueba unitarias (Unit Tests)
Una prueba de unidad es una pieza de código escrita por un desarrollador que ejecuta una funcionalidad específica en el código que se probará y afirma cierto comportamiento o estado.

El porcentaje de código que se prueba mediante pruebas unitarias generalmente se llama cobertura de prueba.

Una prueba unitaria se dirige a una pequeña unidad de código, por ejemplo, un método o una clase. 

**Las dependencias externas deben eliminarse de las pruebas unitarias**, por ejemplo, reemplazando la dependencia con una  implementación de prueba o un objeto (mock) creado por un framework de prueba.

Las pruebas unitarias no son adecuadas para probar la interfaz de usuario compleja o la interacción de componentes. Para esto, es necesario desarrollar pruebas de integración.

#### Frameworks de pruebas unitarias
Hay varios frameworks de prueba disponibles para distintos entornos de programación como NUnit, JUnit,  XUnit, MSTest. En este práctico nos enfocaremos en Jasmine para Angular y XUnit para .NET Core.
- https://xunit.net/
- https://jasmine.github.io/

#### ¿Qué parte del software debería probarse?
Funcionalidad específica de una unidad de código: Una prueba unitaria debe evaluar una única unidad de código, como una función, método o clase. Debe centrarte en probar su funcionalidad específica y sus resultados esperados.

Caminos de ejecución: Asegurarse de probar todos los caminos de ejecución posibles dentro de la unidad de código. Esto incluye casos de éxito y casos de error.

Entradas y salidas: Verificar que la unidad de código maneje correctamente las entradas proporcionadas y produzca las salidas esperadas. Esto implica probar con una variedad de valores de entrada, incluyendo valores límite y casos extremos.

Manejo de excepciones: Si la unidad de código maneja excepciones, asegurarse de probar los casos en los que se lanzan excepciones y verifica que se manejen adecuadamente.

#### Convenciones de nombre:

Por lo general se utiliza la siguiente convención para nombrar a los tests unitarios: 

**Metodo a probar** _ **escenario** _ **resultadoEsperado**

Ejemplo:

**CanBeCancelledBy** _ **UserIsAdmin** _ **ReturnsTrue**

Dentro del código del test se debe utilizar el patrón Arrange, Act y Assert. Ejemplo:

**Arrange:** Crear el objeto o función a probar.

**Act**: Llamar al metodo con  sus parámetros

**Assert**: Evaluar el resultado

#### Familiarizarse con algunos Decoradores y Assert más comunes:

En el contexto de **xUnit** en C#, los "decoradores" o "atributos" son metadatos que se utilizan para proporcionar información adicional sobre las pruebas. Estos atributos permiten a xUnit realizar acciones específicas, como ejecutar pruebas unitarias o gestionar datos y el contexto compartido entre varias pruebas.

| Atributo                | Objetivo                                                                                           |
| ----------------------- | -------------------------------------------------------------------------------------------------- |
| `[Fact]`                | Marca un método como una prueba unitaria básica que no toma parámetros de entrada.                  |
| `[Theory]`              | Marca un método de prueba que se ejecuta varias veces con diferentes parámetros.                    |
| `[InlineData]`          | Proporciona valores de entrada para un método de prueba con `[Theory]`.                            |
| `[ClassData]`           | Proporciona una clase completa como fuente de datos para un método con `[Theory]`.                 |
| `[MemberData]`          | Proporciona datos de una propiedad o método para alimentar un `[Theory]`.                           |
| `[Collection]`          | Agrupa pruebas para que compartan contexto o recursos comunes.                                      |
| `[Trait]`               | Permite categorizar las pruebas con claves y valores (similar a `[Category]` en NUnit).             |
| `[Skip]`                | Omite una prueba, especificando opcionalmente una razón para saltarla.                             |
| `[CollectionDefinition]`| Define una colección de pruebas para que se ejecuten juntas, permitiendo compartir contextos.       |
| `[ClassFixture]`        | Ejecuta código de inicialización compartido para todas las pruebas en una clase.                    |
| `[CollectionFixture]`   | Ejecuta código de inicialización compartido entre varias clases de prueba.                          |
| `[BeforeAfterTest]`     | Marca un atributo para ejecutar código antes y después de cada prueba en un método.                 |
| `[Data]`                | Fuente de datos personalizada para un `[Theory]`.                                                  |
| `[IClassFixture]`       | Define un constructor para instanciar un fixture de clase que será compartido entre todas las pruebas de la clase. |
| `[Output]`              | Permite la inyección de salida de pruebas, como escribir información de diagnóstico.               |

En **Jasmine**, los "decoradores" equivalen a diferentes estructuras y funciones que permiten definir y gestionar pruebas unitarias de manera declarativa. Estas funciones permiten describir el comportamiento esperado de tu código y realizar aserciones.

| Decorador/Matcher        | Objetivo                                                                                           |
| ------------------------ | -------------------------------------------------------------------------------------------------- |
| `describe()`             | Agrupa varias pruebas bajo una misma suite o conjunto lógico de pruebas.                            |
| `it()`                   | Define una prueba individual.                                                                      |
| `beforeEach()`           | Ejecuta código antes de cada prueba dentro de un bloque `describe`.                                 |
| `afterEach()`            | Ejecuta código después de cada prueba dentro de un bloque `describe`.                               |
| `beforeAll()`            | Ejecuta código una vez, antes de todas las pruebas en el bloque `describe`.                         |
| `afterAll()`             | Ejecuta código una vez, después de todas las pruebas en el bloque `describe`.                       |
| `expect()`               | Realiza una aserción o verificación sobre un valor esperado.                                        |
| `toBe()`                 | Verifica si dos valores son exactamente iguales.                                                    |
| `toEqual()`              | Verifica si dos objetos son equivalentes en valor, comparando propiedades.                          |
| `toBeTruthy()`           | Verifica si un valor es verdadero (truthy).                                                         |
| `toBeFalsy()`            | Verifica si un valor es falso (falsy).                                                              |
| `toBeNull()`             | Verifica si un valor es `null`.                                                                     |
| `toBeUndefined()`        | Verifica si un valor es `undefined`.                                                                |
| `toContain()`            | Verifica si una colección o cadena contiene un elemento o subcadena en particular.                  |
| `toThrow()`              | Verifica si una función lanza una excepción al ejecutarse.                                          |
| `toThrowError()`         | Verifica si una función lanza un error en particular.                                               |
| `spyOn()`                | Crea un espía para observar y modificar el comportamiento de funciones o métodos.                   |
| `jasmine.createSpy()`    | Crea un espía que simula el comportamiento de una función.                                          |
| `jasmine.any()`          | Verifica si un valor es de un tipo en particular (como `string`, `number`, etc.).                   |
| `jasmine.objectContaining()` | Verifica si un objeto contiene una propiedad con un valor específico.                          |
| `pending()`              | Marca una prueba como pendiente (todavía no implementada).                                          |
| `fail()`                 | Fuerza que una prueba falle intencionalmente.                                                       |


En xUnit, los comandos Assert se utilizan para verificar las condiciones y resultados de las pruebas unitarias. A continuación, se muestra una lista de algunos de los comandos `Assert` más comúnmente utilizados en xUnit:

| Comando                                     | Descripción                                                                                       |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `Assert.Equal(expected, actual)`            | Verifica si el valor `actual` es igual al valor `expected`.                                        |
| `Assert.NotEqual(notExpected, actual)`      | Verifica si el valor `actual` no es igual al valor `notExpected`.                                  |
| `Assert.True(condition)`                    | Verifica si la condición especificada es `true`.                                                   |
| `Assert.False(condition)`                   | Verifica si la condición especificada es `false`.                                                  |
| `Assert.Null(object)`                       | Verifica si el objeto especificado es `null`.                                                      |
| `Assert.NotNull(object)`                    | Verifica si el objeto especificado no es `null`.                                                   |
| `Assert.Throws<ExceptionType>(() => ...)`   | Verifica si se produce una excepción del tipo `ExceptionType` al ejecutar la acción especificada.   |
| `Assert.ThrowsAny<ExceptionType>(() => ...)`| Verifica si se produce cualquier excepción del tipo `ExceptionType`.                               |
| `Assert.Empty(collection)`                  | Verifica si una colección está vacía.                                                              |
| `Assert.NotEmpty(collection)`               | Verifica si una colección no está vacía.                                                           |
| `Assert.Contains(expectedItem, collection)` | Verifica si una colección contiene un elemento específico.                                         |
| `Assert.DoesNotContain(notExpected, collection)`| Verifica si una colección no contiene un elemento específico.                                      |
| `Assert.Same(expected, actual)`             | Verifica si dos objetos hacen referencia al mismo objeto (misma instancia).                        |
| `Assert.NotSame(notExpected, actual)`       | Verifica si dos objetos no hacen referencia al mismo objeto.                                       |
| `Assert.InRange(actual, low, high)`         | Verifica si un valor está dentro de un rango específico.                                           |
| `Assert.NotInRange(actual, low, high)`      | Verifica si un valor no está dentro de un rango específico.                                        |
| `Assert.Collection(collection, params Action<object>[])` | Verifica que cada elemento en la colección cumple con un conjunto de acciones de validación.      |
| `Assert.Equal(expectedCollection, actualCollection)` | Compara dos colecciones para verificar si son iguales en términos de contenido y orden.            |

En Jasmine, los comandos de `expect` se utilizan para verificar las condiciones y resultados de las pruebas unitarias. A continuación, se muestra una lista de algunos de los comandos `expect` más comúnmente utilizados en Jasmine:

| Comando                                         | Descripción                                                                                         |
| ----------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| `expect(actual).toEqual(expected)`              | Verifica si el valor `actual` es igual al valor `expected` (comparación de igualdad profunda).       |
| `expect(actual).not.toEqual(expected)`          | Verifica si el valor `actual` no es igual al valor `expected`.                                       |
| `expect(actual).toBe(expected)`                 | Verifica si el valor `actual` es exactamente igual al valor `expected` (comparación estricta).       |
| `expect(actual).not.toBe(expected)`             | Verifica si el valor `actual` no es exactamente igual al valor `expected`.                           |
| `expect(actual).toBeTrue()`                     | Verifica si el valor `actual` es `true`.                                                            |
| `expect(actual).toBeFalse()`                    | Verifica si el valor `actual` es `false`.                                                           |
| `expect(actual).toBeNull()`                     | Verifica si el valor `actual` es `null`.                                                            |
| `expect(actual).not.toBeNull()`                 | Verifica si el valor `actual` no es `null`.                                                         |
| `expect(actual).toBeUndefined()`                | Verifica si el valor `actual` es `undefined`.                                                       |
| `expect(actual).not.toBeUndefined()`            | Verifica si el valor `actual` no es `undefined`.                                                    |
| `expect(actual).toContain(expected)`            | Verifica si una colección o cadena contiene el valor `expected`.                                     |
| `expect(actual).not.toContain(expected)`        | Verifica si una colección o cadena no contiene el valor `expected`.                                  |
| `expect(actual).toBeGreaterThan(expected)`      | Verifica si el valor `actual` es mayor que el valor `expected`.                                      |
| `expect(actual).toBeLessThan(expected)`         | Verifica si el valor `actual` es menor que el valor `expected`.                                      |
| `expect(actual).toThrow()`                      | Verifica si se lanza una excepción cuando se ejecuta una función.                                    |
| `expect(actual).toThrowError()`                 | Verifica si se lanza un error cuando se ejecuta una función.                                         |
| `expect(actual).toBeCloseTo(expected, precision)`| Verifica si el valor `actual` está cerca del valor `expected` dentro de un cierto nivel de precisión. |
| `expect(actual).toBeDefined()`                  | Verifica si el valor `actual` está definido.                                                         |
| `expect(actual).not.toBeDefined()`              | Verifica si el valor `actual` no está definido.                                                      |
| `expect(actual).toMatch(regexp)`                | Verifica si una cadena coincide con una expresión regular.                                           |
| `expect(array).toHaveSize(size)`                | Verifica si una colección tiene el tamaño especificado.                                              |

#### Introducción a Mock
Las pruebas unitarias se centran en evaluar unidades de código de manera aislada, sin depender de las implementaciones reales de las dependencias externas. Esto significa que, en las pruebas unitarias, se utilizan mocks o simulaciones para representar las dependencias externas y controlar su comportamiento. El objetivo principal de las pruebas unitarias es verificar que cada unidad de código (como una función, método o clase) funcione correctamente por sí misma, independientemente de las dependencias externas.

Las pruebas de integración, por otro lado, tienen como objetivo evaluar la interacción y la integración de múltiples unidades de código o componentes, incluyendo sus dependencias externas. En las pruebas de integración, se prueban escenarios en los que varias partes del sistema trabajan juntas, y se verifica que se comuniquen y se integren de manera adecuada.

Es decir que las pruebas unitarias se realizan sin depender de las implementaciones reales de las dependencias externas, utilizando mocks o simulaciones, con el objetivo de probar unidades de código de forma aislada.

Para reemplazar estas dependencias reales por "dobles" o "fakes" se utilizan frameworks de Mock que simplifican significativamente el desarrollo de pruebas para clases con dependencias externas.

El framework de Mock (mocking framework) más comúnmente utilizado en el contexto de .NET Core es "Moq". Moq es una biblioteca de código abierto que permite crear objetos simulados (mocks) para representar dependencias externas y controlar su comportamiento durante las pruebas unitarias.

Un ejemplo común de lo que se "mockea" en las pruebas unitarias es una dependencia externa que involucre una llamada a una base de datos o un servicio web. Al mockear esta dependencia, se puede aislar la unidad de código que se está probando y evitar la necesidad de interactuar con una base de datos real o un servicio externo durante las pruebas.

Moq es un marco de pruebas y simulación (mocking framework) para el lenguaje de programación C# en el entorno de desarrollo de .NET. Permite a los desarrolladores crear objetos simulados, llamados "mocks" o "stubs", para simular el comportamiento de componentes del sistema durante las pruebas unitarias.

Algunas de las características y ventajas clave de Moq incluyen:

- Sintaxis Fluent: Moq utiliza una sintaxis fluent y expresiva que facilita la creación y configuración de objetos simulados. Esto hace que las pruebas sean más legibles y mantenibles.

- Generación Dinámica: Moq genera objetos simulados en tiempo de ejecución, lo que significa que no es necesario escribir clases separadas para implementar mocks. Esto ahorra tiempo y reduce la complejidad del código de prueba.

- Configuración de Comportamiento: Puedes configurar cómo debe comportarse un objeto simulado cuando se llama a sus métodos o propiedades. Esto incluye especificar los valores de retorno, establecer acciones personalizadas y verificar si se han llamado métodos específicos.

- Verificación de Llamadas: Moq permite verificar si se han llamado los métodos simulados y cuántas veces se han llamado. Esto es útil para asegurarse de que el código bajo prueba interactúa correctamente con sus dependencias simuladas.

- Soporte para Pruebas Parametrizadas: Moq es compatible con pruebas parametrizadas, lo que significa que puedes ejecutar la misma prueba con múltiples conjuntos de datos o escenarios, cambiando la configuración de los mocks según sea necesario.

- Integración con Marcos de Pruebas: Moq se integra bien con marcos de pruebas populares como NUnit y xUnit.NET, lo que facilita la incorporación de mocks en tus pruebas unitarias.

- Ligero y de Código Abierto: Moq es una biblioteca de código abierto y liviana que no agrega una sobrecarga significativa a tu proyecto.

En resumen, Moq es una herramienta valiosa para escribir pruebas unitarias efectivas en C#. Permite a los desarrolladores crear mocks de manera rápida y sencilla para simular el comportamiento de las dependencias y componentes externos, lo que facilita la prueba aislada de unidades de código y la identificación de problemas en el código durante el desarrollo.

### 4- Desarrollo:
#### Prerequisitos:
- Node.js
  - Para MAC OS:
    - Instalar Brew https://brew.sh/
    - Correr: 
	```bash
	# NOTE:
	# Homebrew is not a Node.js package manager.
	# Please ensure it is already installed on your system.
	# Follow official instructions at https://brew.sh/
	# Homebrew only supports installing major Node.js versions and might not support the latest Node.js version from the 20 release line.
	
	# download and install Node.js
	brew install node@20
	
	# verifies the right Node.js version is in the environment
	node -v # should print `v20.17.0`
	
	# verifies the right npm version is in the environment
	npm -v # should print `10.8.2`
	```
  - Para Windows:
    - Instalar Chocolatey https://chocolatey.org/
    - Correr: 
	```bash
	# NOTE:
	# Chocolatey is not a Node.js package manager.
	# Please ensure it is already installed on your system.
	# Follow official instructions at https://chocolatey.org/
	# Chocolatey is not officially maintained by the Node.js project and might not support the v20.17.0 version of Node.js
	
	# download and install Node.js
	choco install nodejs-lts --version="20.17.0"
	
	# verifies the right Node.js version is in the environment
	node -v # should print `20`
	
	# verifies the right npm version is in the environment
	npm -v # should print `10.8.2`
  	```
- Angular CLI
	```bash
 	npm install -g @angular/cli
 	```
- .NET Core 8 SDK https://dotnet.microsoft.com/en-us/download/dotnet/8.0
  
#### 4.1 Creación de una BD SQL Server para nuestra App
A\. Crear una BD Azure SQL Database (Ver Instructivo 5.1) o montar una imagen Docker de SQL Server como se solicitó en el punto 12 del [TP02]. (https://github.com/ingsoft3ucc/TPS_2024/blob/main/trabajos/02-introduccion-docker.md)

B\. En caso de optar por la opción de montar la imagen de docker, una vez levantada el contenedor, conectarse y ejecutar el siguiente script:
```sql

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Employees](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [nvarchar](max) NULL,
	[CreatedDate] [datetime2](7) NOT NULL,
 CONSTRAINT [PK_Employees] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
SET IDENTITY_INSERT [dbo].[Employees] ON 
GO
INSERT [dbo].[Employees] ([Id], [Name], [CreatedDate]) VALUES (1, N'Juan Perez', CAST(N'2024-09-05T00:00:00.0000000' AS DateTime2))
GO
INSERT [dbo].[Employees] ([Id], [Name], [CreatedDate]) VALUES (2, N'Carla Ruiz', CAST(N'2024-09-05T22:22:47.4405720' AS DateTime2))
GO
INSERT [dbo].[Employees] ([Id], [Name], [CreatedDate]) VALUES (3, N'Carlos Gomez', CAST(N'2024-09-06T09:16:50.0709430' AS DateTime2))
GO
INSERT [dbo].[Employees] ([Id], [Name], [CreatedDate]) VALUES (4, N'Joaquin Zarate', CAST(N'2024-09-06T09:19:37.8987160' AS DateTime2))
GO
INSERT [dbo].[Employees] ([Id], [Name], [CreatedDate]) VALUES (5, N'Luis Rodriguez', CAST(N'2024-09-06T09:23:31.3244340' AS DateTime2))
GO
SET IDENTITY_INSERT [dbo].[Employees] OFF
GO


```
#### 4.2 Obtener nuestra App
A\. Clonar el repo https://github.com/ingsoft3ucc/Angular_WebAPINetCore8_CRUD_Sample.git

B\. Seguir las instrucciones del README.md del repo clonado prestando atención a la modificación de la cadena de conexión en el appSettings.json para que apunte a la BD creada en 4.1 

C\. Navegar a http://localhost:7150/swagger/index.html y probar uno de los controladores para verificar el correcto funcionamiento de la API.
![image](https://github.com/user-attachments/assets/a537ad2e-7c4a-4099-a3e4-fb03fc3bd1f1)

D\. Navegar a http://localhost:4200 y verificar el correcto funcionamiento de nuestro front-end Angular
![image](https://github.com/user-attachments/assets/a2858f8a-4ce7-4d49-8852-167e8cc23660)

E\. Una vez verificado el correcto funcionamiento de la Aplicación procederemos a crear un proyecto de pruebas unitarias para nuestra API.

#### 4.3 Crear Pruebas Unitarias para nuestra API
A\. En el directorio raiz de nuestro repo crear un nuevo proyecto de pruebas unitarias para nuestra API 
```bash
dotnet new xunit -n EmployeeCrudApi.Tests
```
![image](https://github.com/user-attachments/assets/faba2065-cf36-44c8-be66-c616355b7659)


B\. Instalar dependencias necesarias

Primero, instala las siguientes bibliotecas mediante NuGet:

-**Moq**

Moq es una popular biblioteca de mocking en .NET que se utiliza en pruebas unitarias para simular el comportamiento de dependencias externas o de objetos complejos. El objetivo de Moq es ayudar a los desarrolladores a escribir pruebas unitarias aisladas sin tener que interactuar con implementaciones reales de dependencias, como bases de datos, servicios externos, APIs o archivos del sistema. De esta manera, se puede probar el código en condiciones controladas y reproducibles.
Sirve para:
  - Simular el comportamiento de dependencias: Moq permite crear versiones simuladas (mocks) de las dependencias externas (por ejemplo, interfaces o clases abstractas) para verificar cómo interactúa el código con ellas.

  - Aislamiento de pruebas: Permite aislar el código bajo prueba, garantizando que cualquier error en las dependencias externas no afecte las pruebas.

  - Verificación de interacciones: Moq puede verificar si los métodos de las dependencias se llamaron con los argumentos correctos o con qué frecuencia fueron invocados.

  - Simulación de resultados: Podemos configurar el comportamiento de los métodos simulados para que devuelvan valores específicos, excepciones o respuestas asíncronas para distintos escenarios.

  - Ejemplos de uso:
    - Configurar retornos de métodos: Se puede configurar un mock para que un método retorne un valor específico.
    - Verificar interacciones: Verificar si un método fue llamado, cuántas veces y con qué parámetros.
    - Simular excepciones: Probar cómo responde el código al manejar excepciones lanzadas por dependencias externas.
- **xUnit** 

xUnit es un marco de trabajo (framework) para pruebas unitarias en el ecosistema .NET. Es una de las opciones más populares para escribir pruebas automatizadas en proyectos de .NET, y es conocido por su simplicidad, flexibilidad y compatibilidad con varias versiones de .NET, incluyendo .NET Core y .NET 5/6/7/8.

- Características principales de xUnit:

  - Atributos de prueba:

    - **[Fact]**: Se usa para definir una prueba unitaria básica.
    - **[Theory]**: Permite ejecutar una prueba varias veces con diferentes parámetros, útil para probar múltiples casos de una misma lógica.

  - Inyección de dependencias: xUnit soporta inyección de dependencias en los constructores de las clases de prueba, lo que facilita la configuración y limpieza de las pruebas.

  - Configuración y limpieza de pruebas:
    
    - Los métodos `Dispose` permiten liberar recursos al final de cada prueba.
    - También se pueden usar los atributos **[ClassFixture]** y **[Collection]** para compartir el contexto entre pruebas y gestionar la configuración y limpieza antes o después de varias pruebas.

  - Integración con herramientas de CI/CD: xUnit se integra perfectamente con sistemas de integración continua y entrega continua (CI/CD) como **Azure DevOps**, **GitHub Actions**, y **Jenkins**, lo que lo convierte en una excelente opción para entornos de desarrollo ágiles.

  - Compatibilidad con múltiples plataformas: xUnit es compatible con **.NET Framework**, **.NET Core** y **.NET 5+**, lo que lo hace versátil y adaptable a diferentes proyectos.

  - Desventajas de NUnit y MSTest corregidas: xUnit surgió como una evolución de otros marcos como **NUnit** y **MSTest**, con el objetivo de corregir ciertas limitaciones. Por ejemplo, no utiliza métodos como `SetUp` o `TearDown` (propios de NUnit), sino que promueve el uso del constructor de clases para inicializar objetos.

- **Microsoft.EntityFrameworkCore.InMemory**

Este paquete es una implementación del proveedor InMemory para Entity Framework Core, y su propósito principal es permitir realizar pruebas unitarias y de integración en memoria, sin necesidad de conectarse a una base de datos física. Simula el comportamiento de una base de datos sin necesidad de utilizar un servidor de base de datos real. Esto es útil en las siguientes situaciones:

  * Pruebas unitarias: Con InMemory, es posible insertar datos en la base de datos simulada, realizar operaciones de consulta, actualización y eliminación, y verificar que el código funcione correctamente sin tener que preocuparnos por la conexión a una base de datos real. 
  * Prototipado rápido: Si estamos desarrollando una aplicación y necesitamos trabajar con datos sin configurar un entorno de base de datos completo, podemos usar InMemory para almacenar los datos de manera temporal mientras desarrollamos la lógica de la aplicación.
  * Aislamiento de pruebas: El proveedor InMemory garantiza que cada ejecución de prueba pueda tener su propia instancia de base de datos aislada, lo que ayuda a asegurar que las pruebas sean consistentes y no dependan de datos residuales de ejecuciones anteriores.

 

```bash
cd EmployeeCrudApi.Tests 
dotnet add package Moq
dotnet add package xunit
dotnet add package Microsoft.EntityFrameworkCore.InMemory

```

C\. Editar archivo UnitTest1.cs reemplazando su contenido por
```csharp
using EmployeeCrudApi.Controllers;
using EmployeeCrudApi.Data;
using EmployeeCrudApi.Models;
using Microsoft.EntityFrameworkCore;
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Xunit;

namespace EmployeeCrudApi.Tests
{
    public class EmployeeControllerTests
    {
        private ApplicationDbContext GetInMemoryDbContext()
        {
            var options = new DbContextOptionsBuilder<ApplicationDbContext>()
                .UseInMemoryDatabase(databaseName: Guid.NewGuid().ToString()) // Crear una nueva base de datos en memoria para cada prueba
                .Options;

            return new ApplicationDbContext(options);
        }

        [Fact]
        public async Task GetAll_ReturnsListOfEmployees()
        {
            // Arrange
            var context = GetInMemoryDbContext();
            context.Employees.AddRange(
                new Employee { Id = 1, Name = "John Doe" },
                new Employee { Id = 2, Name = "Jane Doe" }
            );
            context.SaveChanges();

            var controller = new EmployeeController(context);

            // Act
            var result = await controller.GetAll();

            // Assert
            Assert.Equal(2, result.Count);
            Assert.Equal("John Doe", result[0].Name);
            Assert.Equal("Jane Doe", result[1].Name);
        }

        [Fact]
        public async Task GetById_ReturnsEmployeeById()
        {
            // Arrange
            var context = GetInMemoryDbContext();
            context.Employees.Add(new Employee { Id = 1, Name = "John Doe" });
            context.SaveChanges();

            var controller = new EmployeeController(context);

            // Act
            var result = await controller.GetById(1);

            // Assert
            Assert.NotNull(result);
            Assert.Equal(1, result.Id);
            Assert.Equal("John Doe", result.Name);
        }

        [Fact]
        public async Task Create_AddsEmployee()
        {
            // Arrange
            var context = GetInMemoryDbContext();
            var controller = new EmployeeController(context);

            var newEmployee = new Employee { Id = 3, Name = "New Employee" };

            // Act
            await controller.Create(newEmployee);

            // Assert
            var employee = await context.Employees.FindAsync(3);
            Assert.NotNull(employee);
            Assert.Equal("New Employee", employee.Name);
        }

        [Fact]
        public async Task Update_UpdatesEmployee()
        {
            // Arrange
            var context = GetInMemoryDbContext();
            var existingEmployee = new Employee { Id = 1, Name = "Old Name" };
            context.Employees.Add(existingEmployee);
            context.SaveChanges();

            var controller = new EmployeeController(context);

            var updatedEmployee = new Employee { Id = 1, Name = "Updated Name" };

            // Act
            await controller.Update(updatedEmployee);

            // Assert
            var employee = await context.Employees.FindAsync(1);
            Assert.NotNull(employee);
            Assert.Equal("Updated Name", employee.Name);
        }

        [Fact]
        public async Task Delete_RemovesEmployee()
        {
            // Arrange
            var context = GetInMemoryDbContext();
            var employeeToDelete = new Employee { Id = 1, Name = "John Doe" };
            context.Employees.Add(employeeToDelete);
            context.SaveChanges();

            var controller = new EmployeeController(context);

            // Act
            await controller.Delete(1);

            // Assert
            var employee = await context.Employees.FindAsync(1);
            Assert.Null(employee); // Verifica que el empleado fue eliminado
        }
    }
}

```
Explicación:

Este código es una serie de pruebas unitarias para un controlador EmployeeController en C# usando el framework de pruebas XUnit. Las pruebas utilizan una base de datos en memoria (in-memory) proporcionada por Entity Framework Core para evitar dependencias con una base de datos real. A continuación, te explico cómo funciona el código y dónde se realiza el mockeo.

Análisis del código
1. Método GetInMemoryDbContext:
Este método crea un contexto de base de datos en memoria utilizando Entity Framework Core. Cada prueba obtiene su propia instancia de base de datos in-memory única (por el uso de Guid.NewGuid()).

```csharp
private ApplicationDbContext GetInMemoryDbContext()
{
    var options = new DbContextOptionsBuilder<ApplicationDbContext>()
        .UseInMemoryDatabase(databaseName: Guid.NewGuid().ToString()) // Crear una base de datos en memoria para cada prueba
        .Options;

    return new ApplicationDbContext(options);
}
```
- InMemoryDatabase: Crea una base de datos temporal en memoria que se usa solo durante la ejecución de las pruebas. Esto es útil para evitar la dependencia de una base de datos física.
- Guid.NewGuid(): Cada prueba tiene su propio contexto de base de datos único, lo que asegura que las pruebas no interfieran entre sí.

2. Prueba GetAll_ReturnsListOfEmployees:
Esta prueba verifica que el controlador puede recuperar correctamente una lista de empleados.
```csharp
[Fact]
public async Task GetAll_ReturnsListOfEmployees()
{
    // Arrange
    var context = GetInMemoryDbContext();
    context.Employees.AddRange(
        new Employee { Id = 1, Name = "John Doe" },
        new Employee { Id = 2, Name = "Jane Doe" }
    );
    context.SaveChanges();

    var controller = new EmployeeController(context);

    // Act
    var result = await controller.GetAll();

    // Assert
    Assert.Equal(2, result.Count);
    Assert.Equal("John Doe", result[0].Name);
    Assert.Equal("Jane Doe", result[1].Name);
}
```
- Arrange: Inicializa el contexto en memoria, agrega algunos empleados de prueba y luego crea una instancia del controlador.
- Act: Llama al método GetAll() del controlador para recuperar los empleados.
- Assert: Verifica que se recuperaron los empleados correctamente y que sus nombres coinciden con los esperados.

3. Prueba GetById_ReturnsEmployeeById:
Verifica que se pueda recuperar un empleado por su ID.

```csharp
[Fact]
public async Task GetById_ReturnsEmployeeById()
{
    // Arrange
    var context = GetInMemoryDbContext();
    context.Employees.Add(new Employee { Id = 1, Name = "John Doe" });
    context.SaveChanges();

    var controller = new EmployeeController(context);

    // Act
    var result = await controller.GetById(1);

    // Assert
    Assert.NotNull(result);
    Assert.Equal(1, result.Id);
    Assert.Equal("John Doe", result.Name);
}
```
- Similar a la prueba anterior, pero en este caso se verifica que el método GetById() funcione correctamente.

4. Prueba Create_AddsEmployee:
Verifica que se puede crear un nuevo empleado y que se almacene correctamente en la base de datos.
```csharp
[Fact]
public async Task Create_AddsEmployee()
{
    // Arrange
    var context = GetInMemoryDbContext();
    var controller = new EmployeeController(context);
    var newEmployee = new Employee { Id = 3, Name = "New Employee" };

    // Act
    await controller.Create(newEmployee);

    // Assert
    var employee = await context.Employees.FindAsync(3);
    Assert.NotNull(employee);
    Assert.Equal("New Employee", employee.Name);
}
```
- Act: Llama al método Create del controlador para agregar un nuevo empleado.
- Assert: Verifica que el empleado fue agregado a la base de datos in-memory correctamente.

5. Prueba Update_UpdatesEmployee:
Verifica que se pueda actualizar la información de un empleado existente
```csharp
[Fact]
public async Task Update_UpdatesEmployee()
{
    // Arrange
    var context = GetInMemoryDbContext();
    var existingEmployee = new Employee { Id = 1, Name = "Old Name" };
    context.Employees.Add(existingEmployee);
    context.SaveChanges();

    var controller = new EmployeeController(context);
    var updatedEmployee = new Employee { Id = 1, Name = "Updated Name" };

    // Act
    await controller.Update(updatedEmployee);

    // Assert
    var employee = await context.Employees.FindAsync(1);
    Assert.NotNull(employee);
    Assert.Equal("Updated Name", employee.Name);
}
```
- Act: Actualiza el empleado llamando a Update.
- Assert: Verifica que el nombre del empleado fue actualizado correctamente.

6. Prueba Delete_RemovesEmployee:
Verifica que se puede eliminar un empleado.
```csharp
[Fact]
public async Task Delete_RemovesEmployee()
{
    // Arrange
    var context = GetInMemoryDbContext();
    var employeeToDelete = new Employee { Id = 1, Name = "John Doe" };
    context.Employees.Add(employeeToDelete);
    context.SaveChanges();

    var controller = new EmployeeController(context);

    // Act
    await controller.Delete(1);

    // Assert
    var employee = await context.Employees.FindAsync(1);
    Assert.Null(employee); // Verifica que el empleado fue eliminado
}
```
- Act: Llama al método Delete del controlador para eliminar un empleado.
- Assert: Verifica que el empleado fue eliminado correctamente de la base de datos in-memory.

7. ¿Dónde ocurre el mockeo?
- In-memory database (mockeo del contexto de la base de datos): En este código, el mockeo se realiza principalmente mediante el uso de la base de datos en memoria. Se utiliza el método UseInMemoryDatabase() para crear una base de datos simulada para las pruebas, lo que permite probar el controlador sin interactuar con una base de datos real.
- EmployeeController: El controlador utiliza este contexto simulado para realizar operaciones CRUD durante las pruebas.

8. Resumen:
- El mockeo principal es la base de datos en memoria, que permite realizar operaciones de consulta, creación, actualización y eliminación sin necesidad de una base de datos real.
- Cada prueba crea un nuevo contexto de base de datos en memoria para asegurar que las pruebas no interfieran entre sí.
- Se cubren operaciones básicas del controlador: obtener todos los empleados, obtener un empleado por ID, crear, actualizar y eliminar empleados.

D\. Renombrar archivo UnitTest1.cs por EmployeeControllerUnitTests.cs
```bash
mv UnitTest1.cs EmployeeControllerUnitTests.cs 
```

E\. Editar el archivo EmployeeCrudApi.Tests/EmployeeCrudApi.Tests.csproj para agregar una referencia a nuestro proyecto de EmployeeCrudApi reemplazando su contenido por
```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>

    <IsPackable>false</IsPackable>
    <IsTestProject>true</IsTestProject>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="coverlet.collector" Version="6.0.0" />
    <PackageReference Include="Microsoft.EntityFrameworkCore.InMemory" Version="8.0.8" />
    <PackageReference Include="Microsoft.NET.Test.Sdk" Version="17.8.0" />
    <PackageReference Include="Moq" Version="4.20.71" />
    <PackageReference Include="xunit" Version="2.9.0" />
    <PackageReference Include="xunit.runner.visualstudio" Version="2.5.3" />
  </ItemGroup>

  <ItemGroup>
    <ProjectReference Include="../EmployeeCrudApi/EmployeeCrudApi/EmployeeCrudApi.csproj" />
  </ItemGroup>

  <ItemGroup>
    <Using Include="Xunit" />
  </ItemGroup>

</Project>

```
F\. Ejecutar los siguientes comandos para ejecutar nuestras pruebas
```bash
dotnet build
dotnet test
```
G\. Verificar que se hayan ejecutado correctamente las pruebas
![image](https://github.com/user-attachments/assets/5f69e693-ed99-418b-97c1-c69ebd5839fe)

H\. Verificar que no estamos usando una dependencia externa como la base de datos.

I\. Modificar la cadena de conexión en el archivo appsettings.json para que use un usuario o password incorrecto y recompilar el proyecto EmployeeCrudApi
```bash
dotnet build
dotnet run --urls "http://localhost:7150"
```
J\. Verificar que nuestro proyecto ya no tiene acceso a la BD navegando a http://localhost:7150/swagger/index.html y probando uno de los controladores:
![image](https://github.com/user-attachments/assets/33df73ea-bd02-48a6-a399-c4a312c1e360)

K\. En la carpeta de nuestro proyecto EmployeeCrudApi.Tests volver a correr las pruebas
```bash
dotnet build
dotnet test
```
L\. Verificar que se hayan ejecutado correctamente las pruebas inclusive sin tener acceso a la BD, lo que confirma que es efectivamente un conjunto de pruebas unitarias que no requieren de una dependencia externa para funcionar.
![image](https://github.com/user-attachments/assets/5f69e693-ed99-418b-97c1-c69ebd5839fe)

M\. Modificar la cadena de conexión en el archivo appsettings.json para que use el usuario y password correcto y recompilar el proyecto EmployeeCrudApi
```bash
dotnet build
dotnet run --urls "http://localhost:7150"
```
N\. Verificar que nuestro proyecto vuelve a tener acceso a la BD navegando a http://localhost:7150/swagger/index.html y probando uno de los controladores:
![image](https://github.com/user-attachments/assets/2fe6b621-db7b-48f2-96e8-d8e1b995474f)

#### 4.4 Creamos pruebas unitarias para nuestro front de Angular:
Intro\. 
Para las pruebas unitarias de nuestro front en Angular utilizaremos Jasmine y Karma, herramientas ampliamente utilizadas para pruebas unitarias en aplicaciones web, especialmente en proyectos de Angular.

- **Jasmine**: Es un framework de pruebas unitarias para JavaScript. Es popular porque no requiere dependencias externas y es fácil de usar. Jasmine se utiliza para escribir pruebas de manera estructurada y ofrece un conjunto de funciones para facilitar la verificación del comportamiento del código.
  - Características principales:
    - Sintaxis descriptiva: Jasmine permite escribir pruebas en un estilo de "BDD" (Desarrollo Orientado a Comportamiento). Usa palabras clave como describe, it, expect para definir pruebas de forma muy legible.
    - Sin dependencias externas: A diferencia de otros frameworks de prueba, Jasmine no necesita ninguna biblioteca externa para funcionar.
    - Espías (Spies): Jasmine permite observar llamadas a funciones, rastrearlas y verificar si fueron llamadas correctamente.

- **Karma**: Es un test runner (ejecutor de pruebas) que facilita la ejecución de pruebas en varios navegadores. Está diseñado para trabajar con frameworks de pruebas como Jasmine, Mocha, entre otros. Karma se integra perfectamente con proyectos de Angular y es parte del Angular CLI.
  - Características principales:
    - Soporte de múltiples navegadores: Karma permite ejecutar pruebas en diferentes navegadores (Chrome, Firefox, Safari, etc.) de forma automática.
    - Ejecución en modo de observación: Karma puede detectar cambios en los archivos y ejecutar las pruebas automáticamente en cuanto se modifican.
    - Generación de informes: Karma proporciona informes detallados sobre el resultado de las pruebas.
    - Integración con CI/CD: Se puede integrar con sistemas de integración continua como Azure Devops, Jenkins, Travis CI o CircleCI para ejecutar las pruebas automáticamente en un entorno controlado.
  - Flujo de trabajo con Karma:
    - Karma inicia un servidor.
    - Abre un navegador (o varios) y ejecuta las pruebas en cada uno de ellos.
    - Karma se queda a la espera de cambios en el código, ejecutando nuevamente las pruebas si detecta modificaciones.

A\. Nos posicionamos en nuestro proyecto de front, en el directorio EmployeeCrudAngular/src/app
```bash
pwd
```
![image](https://github.com/user-attachments/assets/1057289a-4d31-485b-8502-cfb817a53453)

B\. Editamos el archivo app.component.spec.ts reemplazando su contenido por:
```typescript
import { TestBed } from '@angular/core/testing';
import { AppComponent } from './app.component'; // Ajusta la ruta si es necesario

describe('AppComponent', () => {
  beforeEach(async () => {
    await TestBed.configureTestingModule({
      imports: [AppComponent], // Usa imports en lugar de declarations
    }).compileComponents();
  });

  it('should render title', () => {
    const fixture = TestBed.createComponent(AppComponent);
    fixture.detectChanges();
    const compiled = fixture.nativeElement as HTMLElement;
    expect(compiled.querySelector('h1')?.textContent).toContain('EmployeeCrudAngular');
  });

});
```
Explicación:

Este código realiza una prueba unitaria para el componente AppComponent en una aplicación de Angular utilizando Jasmine y TestBed para configurar el entorno de pruebas. A continuación se explica cómo funciona y dónde se realiza el mockeo:

Análisis del código:

1. Configuración del entorno de prueba:
El bloque beforeEach se ejecuta antes de cada prueba y configura el entorno de pruebas utilizando TestBed.
```typescript
beforeEach(async () => {
  await TestBed.configureTestingModule({
    imports: [AppComponent], // Usa imports en lugar de declarations
  }).compileComponents();
});
```
- TestBed: Es la clase principal en Angular que permite configurar y crear un entorno de pruebas para los componentes, servicios y módulos.
- compileComponents: Este método compila los componentes declarados, asegurando que todo el HTML y el CSS del componente se carguen correctamente antes de ejecutar las pruebas.

2. Prueba del título renderizado:
La prueba it verifica que el título del componente AppComponent se renderice correctamente en el DOM.
```typescript
it('should render title', () => {
  const fixture = TestBed.createComponent(AppComponent); // Crea una instancia del componente
  fixture.detectChanges(); // Dispara el ciclo de detección de cambios de Angular para renderizar el componente
  const compiled = fixture.nativeElement as HTMLElement; // Obtiene el DOM renderizado del componente
  expect(compiled.querySelector('h1')?.textContent).toContain('EmployeeCrudAngular'); // Verifica si el h1 contiene el texto 'EmployeeCrudAngular'
});
```
3. Mockeo en este código:
Este código en particular no realiza ningún mockeo explícito. Es decir, no está utilizando servicios externos ni llamadas HTTP que necesiten ser simuladas (mockeadas).

Sin embargo, en una prueba de componentes como esta, el mockeo podría ser necesario si:

- El componente depende de servicios: Si el AppComponent dependiera de un servicio para obtener datos, este servicio tendría que ser simulado (mockeado) para evitar llamadas reales a una API o a otros recursos externos.
- El componente tiene dependencias complejas: En esos casos, se podrían usar objetos o servicios falsos (mocks) para simular el comportamiento de las dependencias.

4. Resumen:
- TestBed se utiliza para configurar el entorno de prueba y crear una instancia del componente.
- No se realiza mockeo explícito, ya que esta prueba solo verifica la correcta renderización del título del componente y no interactúa con servicios o datos externos.

Si el componente fuera más complejo, necesitarías simular las dependencias, pero en este caso no es necesario debido a la simplicidad del componente.

C\. Creamos el archivo employee.service.spec.ts reemplazando su contenido por:
```typescript
import { TestBed } from '@angular/core/testing';
import { HttpClientTestingModule, HttpTestingController } from '@angular/common/http/testing';
import { EmployeeService } from './employee.service';
import { Employee } from './employee.model';
import { DatePipe } from '@angular/common';

describe('EmployeeService', () => {
  let service: EmployeeService;
  let httpMock: HttpTestingController;
  let datePipe: DatePipe;

  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [HttpClientTestingModule],
      providers: [
        EmployeeService,
        DatePipe
      ]
    });

    service = TestBed.inject(EmployeeService);
    httpMock = TestBed.inject(HttpTestingController);
    datePipe = TestBed.inject(DatePipe);
  });

  afterEach(() => {
    httpMock.verify();
  });



  it('should retrieve all employees', () => {
    const today = new Date();
    const expectedDateTime = datePipe.transform(today, 'dd/MM/yyyy HH:mm:ss', undefined) ?? '';  // Consistente con el servicio

    const dummyEmployees: Employee[] = [
      new Employee(1, 'John Doe', expectedDateTime),
      new Employee(2, 'Jane Smith', expectedDateTime)
    ];

    service.getAllEmployee().subscribe(employees => {
      expect(employees.length).toBe(2);
      employees.forEach((employee, index) => {
        // Agrega depuración aquí
        console.log('Employee createdDate:', datePipe.transform(employee.createdDate, 'dd/MM/yyyy HH:mm:ss', undefined)?? '');  // Imprimir el valor generado por el servicio
        console.log('Dummy employee createdDate:', datePipe.transform(dummyEmployees[index].createdDate, 'MM/dd/yyyy HH:mm:ss', undefined)?? '');   // Imprimir el valor esperado

        expect(datePipe.transform(employee.createdDate, 'dd/MM/yyyy HH:mm:ss', undefined)?? '').toEqual(datePipe.transform(dummyEmployees[index].createdDate, 'MM/dd/yyyy HH:mm:ss', undefined)?? '');  // Compara la fecha completa
      });
    });

    const req = httpMock.expectOne(`${service.apiUrlEmployee}/getall`);
    expect(req.request.method).toBe('GET');
    req.flush(dummyEmployees);
  });


});
```

Explicación:

Este código es una prueba unitaria para un servicio de Angular llamado EmployeeService, utilizando Jasmine como framework de pruebas y HttpClientTestingModule para simular las peticiones HTTP.

Análisis del código:
1. Configuración del entorno de prueba:
El bloque beforeEach se ejecuta antes de cada prueba y configura el entorno para la ejecución.
```typescript
beforeEach(() => {
  TestBed.configureTestingModule({
    imports: [HttpClientTestingModule], // Importa un módulo de prueba para simular HttpClient
    providers: [
      EmployeeService, // Proveedor del servicio a probar
      DatePipe         // Proveedor de DatePipe (para formatear fechas)
    ]
  });

  service = TestBed.inject(EmployeeService); // Inyecta el servicio `EmployeeService` que se va a probar
  httpMock = TestBed.inject(HttpTestingController); // Inyecta `HttpTestingController` para simular las peticiones HTTP
  datePipe = TestBed.inject(DatePipe); // Inyecta `DatePipe` para formatear fechas en la prueba
});
```
**HttpClientTestingModule:** Se utiliza para evitar realizar peticiones HTTP reales. Este módulo permite simular y controlar las peticiones que realiza el servicio durante la prueba.

**HttpTestingController:** Es el objeto que permite controlar y verificar las peticiones HTTP que realiza el servicio.

2. Mockeado y verificación de peticiones HTTP:
En la prueba (it), se verifica que el servicio getAllEmployee haga la petición HTTP correctamente y que los datos recibidos coincidan con los esperados.
```typescript
it('should retrieve all employees', () => {
  const today = new Date();
  const expectedDateTime = datePipe.transform(today, 'dd/MM/yyyy HH:mm:ss', undefined) ?? ''; // Formatea la fecha actual

  const dummyEmployees: Employee[] = [
    new Employee(1, 'John Doe', expectedDateTime),
    new Employee(2, 'Jane Smith', expectedDateTime)
  ];

  // Se simula la llamada al servicio
  service.getAllEmployee().subscribe(employees => {
    expect(employees.length).toBe(2); // Verifica que se reciban dos empleados
    employees.forEach((employee, index) => {
      // Compara la fecha formateada del servicio con la de los datos mockeados
      expect(datePipe.transform(employee.createdDate, 'dd/MM/yyyy HH:mm:ss', undefined) ?? '').toEqual(
        datePipe.transform(dummyEmployees[index].createdDate, 'MM/dd/yyyy HH:mm:ss', undefined) ?? ''
      );
    });
  });

  // Se espera que se haya hecho una petición GET
  const req = httpMock.expectOne(`${service.apiUrlEmployee}/getall`);
  expect(req.request.method).toBe('GET');

  // Simula la respuesta de la API con los datos de `dummyEmployees`
  req.flush(dummyEmployees);
});
```

**Dónde se realiza el mockeo?**
1. Mockeo de peticiones HTTP:

- HttpClientTestingModule y HttpTestingController permiten simular las peticiones HTTP realizadas por el servicio.
- El código httpMock.expectOne() se asegura de que se realice una solicitud a la URL correcta.
- El método req.flush() simula la respuesta de la API devolviendo los datos mockeados (dummyEmployees).

2. Datos mockeados:

- dummyEmployees es un arreglo de empleados ficticios que simula la respuesta de la API. Se compara con los datos reales que el servicio devuelve para asegurarse de que los empleados se han recibido y formateado correctamente.

3- Uso de DatePipe:
  El DatePipe se utiliza tanto en el servicio como en la prueba para garantizar que las fechas se formateen correctamente. La prueba compara las fechas formateadas de los datos recibidos con las fechas formateadas de los datos mockeados.

4- Resumen:
El código mockea:

- La respuesta de la API (con dummyEmployees).
- Las peticiones HTTP usando HttpClientTestingModule y HttpTestingController. Esto permite que la prueba se ejecute sin realizar llamadas reales a una API.

D\. Editamos el archivo employee.component.spec.ts ubicado en la carpeta **employee** reemplazando su contenido por:

```typescript
import { TestBed } from '@angular/core/testing';
import { EmployeeComponent } from './employee.component';
import { HttpClientTestingModule } from '@angular/common/http/testing';
import { DatePipe } from '@angular/common';

describe('EmployeeComponent', () => {
  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [EmployeeComponent, HttpClientTestingModule],
      providers: [DatePipe] // Añade DatePipe a los proveedores
    });
  });

  it('should create', () => {
    const fixture = TestBed.createComponent(EmployeeComponent);
    const component = fixture.componentInstance;
    expect(component).toBeTruthy();
  });
});
```
Explicación:
Este código realiza una prueba unitaria del componente EmployeeComponent utilizando Jasmine y TestBed. A continuación, se explica cómo funciona y dónde se lleva a cabo el mockeo (si lo hay).

Análisis del código:
1. Configuración del entorno de prueba:
El bloque beforeEach configura el entorno de pruebas para el EmployeeComponent.
```typescript
beforeEach(() => {
  TestBed.configureTestingModule({
    imports: [EmployeeComponent, HttpClientTestingModule], // Importa el componente y el módulo de pruebas HTTP
    providers: [DatePipe] // Proporciona el DatePipe para ser usado en las pruebas
  });
});
```
- TestBed: Es el entorno de pruebas para Angular que permite configurar módulos, componentes y servicios para pruebas.
- imports: En esta prueba, se importa el propio EmployeeComponent y el HttpClientTestingModule, que es un módulo proporcionado por Angular para realizar pruebas de HTTP sin hacer llamadas reales a una API.
- providers: Aquí se está proporcionando el DatePipe, que se puede usar para realizar transformaciones de fechas dentro del componente. Si EmployeeComponent lo necesita, estará disponible para inyección de dependencias.

2. Prueba de creación del componente:
Esta prueba simple verifica que el EmployeeComponent se pueda crear correctamente.
```typescript
it('should create', () => {
  const fixture = TestBed.createComponent(EmployeeComponent); // Crea una instancia de `EmployeeComponent`
  const component = fixture.componentInstance; // Obtiene la instancia del componente
  expect(component).toBeTruthy(); // Verifica que la instancia del componente sea válida
});
```
- fixture: Es el contenedor para una instancia del componente en el contexto de prueba. A través del fixture se puede interactuar con el componente y el DOM asociado.
- component: La instancia real del EmployeeComponent que se crea en la prueba.
- expect: La prueba verifica que el componente se haya creado correctamente, comprobando que el componente no sea null o undefined.

3. Mockeo en este código:
El mockeo explícito ocurre a través del uso de HttpClientTestingModule.

- HttpClientTestingModule: Este módulo de pruebas reemplaza el HttpClient real con un cliente HTTP simulado, evitando que se realicen solicitudes HTTP reales durante la prueba. Así se "mockea" cualquier solicitud HTTP que podría haber sido realizada por el EmployeeComponent al backend.
- DatePipe: Aunque se proporciona el DatePipe para ser utilizado en las pruebas, no se está realizando ningún mockeo sobre este en el código. Se está utilizando la implementación real del DatePipe.

4. ¿Dónde ocurre el mockeo?
- El mockeo principal ocurre en el uso de HttpClientTestingModule. Al incluir este módulo, cualquier llamada HTTP realizada por EmployeeComponent será interceptada por un servicio HTTP simulado, evitando solicitudes reales a un backend.

En esta prueba en particular, el enfoque está en verificar que el componente se crea correctamente, por lo que no se están simulando interacciones con el backend. Si se realizaran solicitudes HTTP dentro del componente, este mockeo sería gestionado por el HttpTestingController para interceptar las llamadas.

5. Resumen:
- TestBed configura el entorno de prueba para el EmployeeComponent.
- HttpClientTestingModule mockea cualquier solicitud HTTP, asegurando que no se realicen llamadas reales a la API.
- DatePipe se inyecta como proveedor, pero no se realiza ningún mockeo sobre él.
- La prueba verifica que el componente se cree correctamente.


E\. Editamos el archivo addemployee.component.spec.ts ubicado en la carpeta **addemployee** reemplazando su contenido por:
```typescript
import { TestBed } from '@angular/core/testing';
import { AddemployeeComponent } from './addemployee.component';
import { HttpClientTestingModule } from '@angular/common/http/testing';
import { ActivatedRoute } from '@angular/router';
import { of } from 'rxjs'; // para simular observables
import { DatePipe } from '@angular/common';

describe('AddemployeeComponent', () => {
  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [AddemployeeComponent, HttpClientTestingModule],
      providers: [
        DatePipe,
        {
          provide: ActivatedRoute, // Simula ActivatedRoute
          useValue: {
            params: of({ id: 1 }) // simula el parámetro id en la URL
          }
        }
      ]
    });
  });

  it('should create', () => {
    const fixture = TestBed.createComponent(AddemployeeComponent);
    const component = fixture.componentInstance;
    expect(component).toBeTruthy();
  });
});
```
Explicación:
Este código realiza una prueba unitaria del componente AddemployeeComponent en Angular utilizando Jasmine y TestBed. A continuación, se explica cómo funciona y dónde se realiza el mockeo.

Análisis del código:
1. Configuración del entorno de prueba:
En el bloque beforeEach, se configura el entorno de pruebas para el componente AddemployeeComponent.
```typescript
beforeEach(() => {
  TestBed.configureTestingModule({
    imports: [AddemployeeComponent, HttpClientTestingModule], // Importa el componente y módulo de pruebas HTTP
    providers: [
      DatePipe, // Inyecta DatePipe para el formateo de fechas en el componente
      {
        provide: ActivatedRoute, // Simula ActivatedRoute
        useValue: {
          params: of({ id: 1 }) // Simula el parámetro de la ruta (id) como observable
        }
      }
    ]
  });
});
```
- TestBed: Configura el entorno de pruebas para que puedas probar tu componente dentro del mismo.
- imports: Aquí se importa el propio componente AddemployeeComponent y el módulo HttpClientTestingModule, que es un mock del HttpClient para pruebas.
- providers: Define inyecciones de dependencias para el componente.
- DatePipe: Se inyecta el DatePipe, útil si el componente necesita realizar operaciones de formateo de fechas.
- ActivatedRoute: Se provee un mock de ActivatedRoute usando useValue. Esto permite simular un parámetro de la URL (en este caso, { id: 1 }) sin tener que usar el enrutador real.

2. Prueba de creación del componente:
Este test verifica que el componente AddemployeeComponent se crea correctamente.
```typescript
it('should create', () => {
  const fixture = TestBed.createComponent(AddemployeeComponent); // Crea una instancia de AddemployeeComponent
  const component = fixture.componentInstance; // Obtiene la instancia del componente
  expect(component).toBeTruthy(); // Verifica que el componente ha sido creado correctamente
});
```
- fixture: Es el contenedor que proporciona acceso a una instancia del componente en el contexto de prueba.
- component: Es la instancia real del componente AddemployeeComponent.
- expect: Verifica que el componente se haya creado correctamente.

3. Mockeo en este código:

En este código, se realizan varios mockeos importantes:

- HttpClientTestingModule: Este módulo reemplaza el HttpClient real con uno simulado para evitar realizar llamadas HTTP reales en el contexto de pruebas.
- ActivatedRoute: Se provee un mock de ActivatedRoute para simular parámetros de ruta. En este caso, params: of({ id: 1 }) simula que la ruta actual tiene un parámetro id con valor 1. Esto es útil si el componente depende de los parámetros de la ruta para cargar datos o realizar operaciones específicas.

4. ¿Dónde ocurre el mockeo?
- HttpClientTestingModule: Mockea las llamadas HTTP realizadas por el AddemployeeComponent. Si el componente hace solicitudes HTTP, estas serán interceptadas por el mock.
- ActivatedRoute: Se mockea usando useValue para simular los parámetros de la URL. En este caso, se está simulando que el parámetro id en la URL es 1, sin depender del enrutador real.

5. ¿Por qué es importante?
- El mockeo del ActivatedRoute permite probar el comportamiento del componente sin la necesidad de configurar un enrutador real ni rutas.
- HttpClientTestingModule evita que las pruebas hagan llamadas reales a una API, lo que hace que las pruebas sean más rápidas, confiables y controladas.

6. Resumen:
- TestBed configura el entorno de prueba para el componente AddemployeeComponent.
- HttpClientTestingModule mockea las llamadas HTTP para evitar solicitudes reales.
- ActivatedRoute está mockeado para simular los parámetros de la ruta, lo que permite probar el comportamiento dependiente de la URL.
- La prueba verifica que el componente se crea correctamente, pero no valida ningún comportamiento más allá de la creación del componente.

F\. En el directorio raiz de nuestro proyecto EmployeeCrudAngular ejecutamos el comando 
```bash
ng test
```
En proyectos de Angular, Jasmine se usa para escribir las pruebas, y Karma se encarga de ejecutarlas. Cuando ejecutamos el comando ng test, Karma se inicia, carga las pruebas escritas en Jasmine, y las ejecuta en un navegador.

G\. Vemos que se abre una ventana de Karma con Jasmine en la que nos indica que los tests se ejecutaron correctamente
![image](https://github.com/user-attachments/assets/d5bd574f-bab4-4f65-ac5e-6b95d6338bc3)

H\. Vemos que los tests se ejecutaron correctamente:
![image](https://github.com/user-attachments/assets/24172199-9b90-4e1c-8231-3c142f9d6160)


I\. Verificamos que no esté corriendo nuestra API navegando a http://localhost:7150/swagger/index.html y recibiendo esta salida:
![image](https://github.com/user-attachments/assets/550dd212-5254-4c7f-bea0-aa55c73021fe)

J\. Los puntos G y H nos indican que se han ejecutado correctamente las pruebas inclusive sin tener acceso a la API, lo que confirma que es efectivamente un conjunto de pruebas unitarias que no requieres de una dependencia externa para funcionar.

#### 4.5 Modificamos el código de nuestra API y creamos nuevas pruebas unitarias:

A\. Realizar las siguientes modificaciones al código de la API:
  - Al agregar y al editar un empleado, controlar que el nombre del empleado no esté repetido.
  - La longitud máxima del nombre y apellido del empleado debe ser de 100 caracteres.
  - Almacenar el nombre en la BD siempre con la primera letra de los nombres en Mayuscula y todo el apellido en Mayusculas. Ejemplo, si recibo juan carlos chamizo, se debe almacenar como Juan Carlos CHAMIZO.
  - Asegurar que el nombre del empleado no contenga caracteres especiales o números, a menos que sea necesario (por ejemplo, caracteres especiales en apellidos como "O'Connor" o "García").
  - Validar que el nombre tenga un número mínimo de caracteres, por ejemplo, al menos dos caracteres para evitar entradas inválidas como "A".
  - Verificar que el nombre no contenga números, ya que no es común en los nombres de empleados.
  - Asegurar que cada parte del nombre (separada por espacios) tenga al menos un carácter o más, por ejemplo, para evitar "A B".
  - Verificar que no haya palabras vacías o que el nombre no esté compuesto solo de espacios.
  - Prohibir el uso de nombres triviales o genéricos como "Empleado", "N/A", "Nombre", etc.
  - Evitar que se ingresen caracteres repetidos de forma excesiva, como "Juuuuaannnn".
  - Implementar un filtro para evitar el uso de palabras inapropiadas, ofensivas o que puedan violar políticas internas.
En todos los casos donde no se cumplan las condiciones, la API debe devolver un error de HTTP 400 Bad Request y un Json indicando el error, por ejemplo:
```json
{
  "status": 400,
  "error": "Bad Request",
  "message": "El nombre del empleado ya existe."
}
```

B\. Crear las pruebas unitarias necesarias para validar las modificaciones realizadas en el código

#### 4.6 Modificamos el código de nuestro Front y creamos nuevas pruebas unitarias:

A\. Realizar en el código del front las mismas modificaciones hechas a la API. 

B\. Las validaciones deben ser realizadas en el front sin llegar a la API, y deben ser mostradas en un toast como por ejemplo https://stackblitz.com/edit/angular12-toastr?file=src%2Fapp%2Fapp.component.ts o https://stackblitz.com/edit/angular-error-toast?file=src%2Fapp%2Fcore%2Frxjsops.ts

C\. Crear las pruebas unitarias necesarias en el front para validar las modificaciones realizadas en el código del front.


### 5- Instructivos:
#### 5.1 Crear una Base de Datos SQL en Azure

**Nota:** Se creará una BD con un costo de USD 4.90 por mes. El costo se prorratea por el tiempo que se utilice la BD (hasta que se elimine el recurso). Es decir que si por ejemplo se usa por 1 día se cobrarán de la Tarjeta de crédito de su suscripción  unos 0.17 USD-

1\. Navegar a [https://portal.azure.com/#home](https://portal.azure.com/#home)


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

```sql

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Employees](
	[Id] [int] IDENTITY(1,1) NOT NULL,
	[Name] [nvarchar](max) NULL,
	[CreatedDate] [datetime2](7) NOT NULL,
 CONSTRAINT [PK_Employees] PRIMARY KEY CLUSTERED 
(
	[Id] ASC
)WITH (STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
SET IDENTITY_INSERT [dbo].[Employees] ON 
GO
INSERT [dbo].[Employees] ([Id], [Name], [CreatedDate]) VALUES (1, N'Juan Perez', CAST(N'2024-09-05T00:00:00.0000000' AS DateTime2))
GO
INSERT [dbo].[Employees] ([Id], [Name], [CreatedDate]) VALUES (2, N'Carla Ruiz', CAST(N'2024-09-05T22:22:47.4405720' AS DateTime2))
GO
INSERT [dbo].[Employees] ([Id], [Name], [CreatedDate]) VALUES (3, N'Carlos Gomez', CAST(N'2024-09-06T09:16:50.0709430' AS DateTime2))
GO
INSERT [dbo].[Employees] ([Id], [Name], [CreatedDate]) VALUES (4, N'Joaquin Zarate', CAST(N'2024-09-06T09:19:37.8987160' AS DateTime2))
GO
INSERT [dbo].[Employees] ([Id], [Name], [CreatedDate]) VALUES (5, N'Luis Rodriguez', CAST(N'2024-09-06T09:23:31.3244340' AS DateTime2))
GO
SET IDENTITY_INSERT [dbo].[Employees] OFF
GO

```
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
- Subir un doc al repo con las capturas de pantalla de los pasos realizados
- Subir el proyecto a un repo para poder evaluar, revisar y ejecutar el código y las pruebas unitarias

### 7-  Criterio de Calificación
Los pasos 4.1 al 4.4 representan un 60% de la nota total, los pasos 4.5 y subsiguientes representan el 40% restante.




