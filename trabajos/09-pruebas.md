## Trabajo Práctico 9 - Pruebas de unidad

## 1- Objetivos de Aprendizaje
 - Adquirir conocimientos sobre conceptos referidos a pruebas de unidad (unit tests).
 - Generar y ejecutar pruebas unitarias utilizado frameworks disponibles.

## 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 5 (Libro Ingeniería de Software: Cap 8)

## 3- Consignas a desarrollar en el trabajo práctico:
### Conceptos generales explicaciones de los mismos

#### ¿Qué son las pruebas de software?
Una prueba de software es una pieza de software que ejecuta otra pieza de software. Valida si ese código da como resultado el estado esperado (prueba de estado) o ejecuta la secuencia de eventos esperados (prueba de comportamiento).

#### ¿Por qué son útiles las pruebas de software?
Las pruebas de la unidad de software ayudan al desarrollador a verificar que la lógica de una parte del programa sea correcta.

Ejecutar pruebas automáticamente ayuda a identificar regresiones de software introducidas por cambios en el código fuente. Tener una cobertura de prueba alta de su código le permite continuar desarrollando características sin tener que realizar muchas pruebas manuales.

#### Código (o aplicación) bajo prueba
El código que se prueba generalmente se llama código bajo prueba . Si está probando una aplicación, esto se llama la aplicación bajo prueba .

#### Prueba unitarias (Unit Tests)
Una prueba de unidad es una pieza de código escrita por un desarrollador que ejecuta una funcionalidad específica en el código que se probará y afirma cierto comportamiento o estado.

El porcentaje de código que se prueba mediante pruebas unitarias generalmente se llama cobertura de prueba.

Una prueba unitaria se dirige a una pequeña unidad de código, por ejemplo, un método o una clase. Las dependencias externas deben eliminarse de las pruebas unitarias, por ejemplo, reemplazando la dependencia con una  implementación de prueba o un objeto (mock) creado por un framework de prueba.

Las pruebas unitarias no son adecuadas para probar la interfaz de usuario compleja o la interacción de componentes. Para esto, debes desarrollar pruebas de integración.

#### Frameworks de pruebas unitarias para Java
Hay varios frameworks de prueba disponibles para Java. Los más populares son JUnit y TestNG

#### ¿Qué parte del software debería probarse?
Lo que debe probarse es un tema muy controvertido. Algunos desarrolladores creen que cada declaración en su código debe ser probada.

En cualquier caso, debe escribir pruebas de software para las partes críticas y complejas de su aplicación. Si introduce nuevas funciones, un banco de pruebas sólido también lo protege contra la regresión en el código existente.

En general, es seguro ignorar el código trivial. Por ejemplo, es inútil escribir pruebas para los métodos getter y setter que simplemente asignan valores a los campos. Escribir pruebas para estas afirmaciones consume mucho tiempo y no tiene sentido, ya que estaría probando la máquina virtual Java. La propia JVM ya tiene casos de prueba para esto. Si está desarrollando aplicaciones de usuario final, puede suponer que una asignación de campo funciona en Java.

Si comienza a desarrollar pruebas para una base de código existente sin ninguna prueba, es una buena práctica comenzar a escribir pruebas para el código en el que la mayoría de los errores ocurrieron en el pasado. De esta manera puede enfocarse en las partes críticas de su aplicación.

## 4- Desarrollo:

4.1 Preparamos el entorno:
- Instalamos VS.Code: https://code.visualstudio.com/download

- Desde linea de comandos clonamos el proyecto MiSimpleApp, entramos a la carpeta y abrimos VS.Code

```bash
git clone https://github.com/ingsoft3ucc/MiSimpleApp.git
cd MiSimpleApp
code .
```
- Cerramos VS.Code
- Nos movemos una carpeta hacia arriba y creamos un nuevo proyecto de pruebas unitarias con NUnit:

```bash
dotnet new nunit -n MiSimpleAppTests
```
- Entramos a la carpeta del nuevo proyecto y agregamos los paquetes NUnit y NUnit.ConsoleRunner. Luego le agregamos al proyecto de pruebas una referencia al proyecto que vamos a probar. Nos movemos una carpeta hacia arriba y lo vemos en VS.Code

```bash
cd MiSimpleAppTests
dotnet add package NUnit
dotnet add package NUnit.ConsoleRunner
dotnet add reference ../MiSimpleApp/MiSimpleApp.csproj
cd ..
code .
```

- Instalamos extensión ".NET Core Test Explorer"

  <img width="938" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/eb7e5845-24ad-462e-90a6-9fbc4817e4f4">
- Nos aparece un ícono de Pruebas, lo seleccionamos, hacemos click en ***Open Settings*** 

<img width="424" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/7257a4e7-4aea-433b-9ef2-28089c1952d5">

- Se abre el archivo settings.json y escribimos el nombre del proyecto de pruebas y el nombre de la dll resultante de la compilación del proyecto de pruebas:
  
```bash
{
    "dotnet-test-explorer.testProjectPath": "MiSimpleAppTests",
    "dotnet-test-explorer.testFileSuffix": ".Tests.dll"
}
```
- Guardamos el archivo, volvemos hacer click en el ícono de pruebas y ahora sí tenemos la posibilidad de correr pruebas haciendo click en el botón de ***Play***

  <img width="432" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/a03973af-a77f-45d0-ac94-d3e7872e12b7">

- Revisamos el código del proyecto MiSimpleApp:
	- Clases.cs:
   	```csharp
    	
	    public class Reservation
	    {
	        public User MadeBy { get; set; }
	
	        public bool CanBeCancelledBy(User user)
	        {
	            if (user.IsAdmin)
	                return true;
	            if (MadeBy==user)
	                return true;
	            return false;
	
	            //return (user.IsAdmin || MadeBy == user);
	        }
	        
	    }
	
	    public class User
	    {
	        public bool IsAdmin { get; set; }
	    }
	```
	- Program.cs:
	 ```csharp
	  using System;
	
	class Program
	{
	    static void Main()
	    {
	        Reservation reservation = new Reservation();
	        User user=new User();
	        user.IsAdmin=true;
	        bool result=reservation.CanBeCancelledBy(user);
	        Console.WriteLine(result);
	    }
	}
4.2: Creamos nuestros Tests:
- Dado que el método ***CanBeCancelledBy*** de la clase ***Reservation*** tiene una lógica con 3 caminos posibles, debemos probar esos 3 caminos:
- Modificamos nuestro archivo ***UnitTest1.cs*** del proyecto ***MiSimpleAppTests***

```csharp
namespace MiSimpleAppTests;

[TestFixture]
public class Tests
{
    [SetUp]
    public void Setup()
    {
    }

    [Test]
    public void CanBeCancelledBy_AdminCancelling_ReturnsTrue()
    {
        //Arrange
        
        User user=new User();
        user.IsAdmin=true;
        Reservation reservation=new Reservation();
        
        //Act
        
        bool result=reservation.CanBeCancelledBy(user);

        //Assert
        
        //Assert.IsTrue(result);
        Assert.That(result,Is.True);
        //Assert.That(result==true);
    }

    
    [Test]
    public void CanBeCancelledBy_SameUserCancelling_ReturnsTrue()
    {
        //Arrange
        User user=new User();
        Reservation reservation=new Reservation();
        reservation.MadeBy=user;

        //Act
        bool result=reservation.CanBeCancelledBy(user);

        //Assert
        Assert.That(result,Is.True);

    }

    
    [Test]
    public void CanBeCancelledBy_AnotherUserCancelling_ReturnsFalse()
    {
        //Arrange
        User user=new User();
        Reservation reservation=new Reservation();
        reservation.MadeBy=user;

        //Act
        User newUser=new User();
        bool result=reservation.CanBeCancelledBy(newUser);

        //Assert
        Assert.That(result,Is.False);

    }

}
```
- Ejecutamos los tests:

<img width="394" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/babadb4a-349a-42c7-b126-20b72618bc9a">

- Modificamos la lógica de nuestro código bajo prueba haciendo que devuelva false la linea 9 (recordar guardar el archivo):

<img width="581" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/2743ca29-bddc-46ca-aa26-521312bc1710">

<img width="547" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/1ee56c1c-513b-4f07-834a-e67d6482bfa2">

- Volvemos a ejecutar los tests:

<img width="411" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/bad95a68-a616-4202-a9b1-c5ce3bf6e493">

- Dejamos la línea 9 de nuestro código bajo prueba como estaba originalmente:

<img width="581" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/2743ca29-bddc-46ca-aa26-521312bc1710">

- Realizamos una refactorización de nuestro codigo y guardamos el archivo:

<img width="529" alt="image" src="https://github.com/ingsoft3ucc/TPs/assets/140459109/bb7a1afe-6572-4915-aede-7a83ca64ef8b">


- Por último ejecutamos nuestros tests desde la linea de comandos. Nos posicionamos en el directorio de nuestro proyecto de pruebas y ejecutamos el comando dotnet test

```bash
dotnet test
```

![image](https://github.com/ingsoft3ucc/TPs/assets/140459109/916f6a78-b85a-42f9-89c5-d7d12746fd29)

  


#### 5- Familiarizarse con algunos Decoradores y Assert más comunes:

En el contexto de pruebas unitarias y en lenguajes de programación como C# y Java, los "decoradores" son en realidad "atributos" o "anotaciones" en C# y Java, respectivamente. Los atributos son metadatos que se utilizan para proporcionar información adicional sobre clases, métodos, propiedades y otros elementos del código. Estos atributos no afectan directamente el comportamiento del código en sí, pero permiten que el entorno de desarrollo o las bibliotecas externas realicen acciones específicas en función de la información proporcionada por los atributos.

Estos atributos (decoradores) proporcionan información importante al marco de pruebas NUnit y permiten la configuración y ejecución de pruebas unitarias de manera controlada y estructurada.

| Decorador               | Objetivo                                                                                           |
| ----------------------- | -------------------------------------------------------------------------------------------------- |
| `[TestFixture]`         | Marca una clase como una clase de prueba que contiene métodos de prueba.                           |
| `[Test]`                | Marca un método como una prueba unitaria.                                                           |
| `[SetUp]`               | Marca un método que se ejecutará antes de cada prueba en la clase de prueba.                        |
| `[TearDown]`            | Marca un método que se ejecutará después de cada prueba en la clase de prueba.                     |
| `[TestCase]`            | Permite especificar múltiples conjuntos de datos de prueba para un método de prueba.               |
| `[TestCaseSource]`      | Permite especificar una fuente externa de datos para alimentar los casos de prueba de un método.   |
| `[Ignore]`              | Marca una prueba o una clase de prueba para que se ignore durante la ejecución de las pruebas.    |
| `[Category]`            | Etiqueta una prueba con una categoría específica.                                                  |
| `[MaxTime]`             | Establece un límite de tiempo máximo para la ejecución de una prueba.                                |
| `[Description]`         | Proporciona una descripción adicional para una prueba o una clase de prueba.                          |
| `[Parallelizable]`      | Indica que las pruebas pueden ejecutarse en paralelo.                                               |
| `[OneTimeSetUp]`        | Marca métodos que se ejecutan una vez antes de todas las pruebas en una clase de prueba.           |
| `[OneTimeTearDown]`     | Marca métodos que se ejecutan una vez después de todas las pruebas en una clase de prueba.        |


En NUnit, los comandos Assert se utilizan para verificar las condiciones y resultados de las pruebas unitarias. A continuación, se muestra una lista de algunos de los comandos Assert más comúnmente utilizados en NUnit:

| Comando                                  | Descripción                                                                                       |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `Assert.AreEqual(expected, actual)`      | Verifica si el valor `actual` es igual al valor `expected`.                                       |
| `Assert.AreNotEqual(notExpected, actual)` | Verifica si el valor `actual` no es igual al valor `notExpected`.                                  |
| `Assert.IsTrue(condition)`              | Verifica si la condición especificada es `true`.                                                  |
| `Assert.IsFalse(condition)`             | Verifica si la condición especificada es `false`.                                                 |
| `Assert.IsNull(object)`                 | Verifica si el objeto especificado es nulo.                                                         |
| `Assert.IsNotNull(object)`              | Verifica si el objeto especificado no es nulo.                                                     |
| `Assert.Throws<ExceptionType>(delegate)` | Verifica si se produce una excepción del tipo `ExceptionType` al ejecutar el delegado especificado. |
| `Assert.That(actual, expression)`        | Permite escribir aserciones más expresivas utilizando una sintaxis más flexible y legible.         |
| `Assert.IsEmpty(collection)`            | Verifica si una colección está vacía.                                                               |
| `Assert.IsNotEmpty(collection)`         | Verifica si una colección no está vacía.                                                            |
| `Assert.Contains(expectedItem, collection)` | Verifica si una colección contiene un elemento específico.                                        |
| `Assert.AreEqual(expectedCollection, actualCollection)` | Compara dos colecciones para verificar si son iguales en términos de contenido y orden. |
                                                                                                                                                            |
#### 1- Utilizando Unit test
  - ¿En el proyecto **spring-boot** para qué está esta dependencia en el pom.xml?
```xml
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
```
  - Analizar y ejectuar el metodo de unit test:

```java
public class HelloWorldServiceTest {

	@Test
	public void expectedMessage() {
		HelloWorldService helloWorldService = new HelloWorldService();
		assertEquals("Expected correct message","Spring boot says hello from a Docker container",helloWorldService.getHelloMessage());
	}
	
}
```
  - Ejecutar los tests utilizando la IDE

#### 3- Familiarizarse con algunos conceptos de Mockito
Mockito es un framework de simulación popular que se puede usar junto con JUnit. Mockito permite crear y configurar objetos falsos. El uso de Mockito simplifica significativamente el desarrollo de pruebas para clases con dependencias externas.

Si se usa Mockito en las pruebas, normalmente:
 1. Se burlan las dependencias externas e insertan los mocks en el código bajo prueba
 2. Se ejecuta el código bajo prueba
 3. Se valida que el código se ejecutó correctamente

Referencia: https://www.vogella.com/tutorials/Mockito/article.html

- Analizar el código del test
```java
public class ExampleInfoContributorTest {

	@Test
	public void infoMap() {
		Info.Builder builder = mock(Info.Builder.class);
		
		ExampleInfoContributor exampleInfoContributor = new ExampleInfoContributor();
		exampleInfoContributor.contribute(builder);
		
		verify(builder).withDetail(any(),any());
	}
}
```

#### 4- Utilizando Mocks

- Agregar un unit test a la clase **HelloWorldServiceTest** 
  - Cuando se llame por primera vez al método **getHelloMessage** retorne "Hola Hola"
  - Cuando se llame por segunda vez al método **getHelloMessage** retorne "Hello Hello"

- Crear la siguiente clase **AbstractTest**
```java
package sample.actuator;

import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
import org.springframework.test.context.web.WebAppConfiguration;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;
import org.springframework.web.context.WebApplicationContext;

@RunWith(SpringJUnit4ClassRunner.class)
@SpringBootTest(classes = SampleActuatorApplication.class)
@WebAppConfiguration
public abstract class AbstractTest {
    protected MockMvc mvc;

    @Autowired
    WebApplicationContext webApplicationContext;

    protected void setUp() {
        mvc = MockMvcBuilders.webAppContextSetup(webApplicationContext).build();
    }
}
```

- Agregar esta otra clase también en el mismo directorio

```java
package sample.actuator;

import static org.junit.Assert.assertEquals;

import org.junit.Before;
import org.junit.Test;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MvcResult;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;


public class SampleControllerTest extends AbstractTest {

    @Override
    @Before
    public void setUp() {
        super.setUp();
    }

    @Test
    public void testRootMessage() throws Exception {
        String uri = "/";
        MvcResult mvcResult = mvc.perform(MockMvcRequestBuilders.get(uri)
                .accept( MediaType.APPLICATION_JSON_VALUE)).andReturn();

        String content = mvcResult.getResponse().getContentAsString();
        int status = mvcResult.getResponse().getStatus();
        assertEquals(200, status);
        assertEquals(content,"Expected correct message","{\"message\":\"Spring boot says hello from a Docker container\"}");
    }
}
```

  - Analizar estos tests


#### 5- Opcional: Agregar otros unit tests
  - Agregar unit tests para mejorar la cobertura, pueden ser test simples que validen getter y setters.
  
#### 6- Capturar los unit tests como parte del proceso de CI/CD
  - Hacer los cambios en Jenkins (o en la herramienta de CICD utilizada) si es necesario, para capturar los resultados de los unit tests y mostrarlos en la ejecución del build.

