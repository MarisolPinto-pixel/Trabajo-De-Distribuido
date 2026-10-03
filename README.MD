# TRABAJO PRACTICO
# ALUMNA: Marisol Pinto

# 1. Configuración del Proyecto en Spring Initializr
Para dar inicio al desarrollo, ingrese al sitio web start.spring.io y configure los datos del formulario de la siguiente manera:

**Project:** Maven

**Language:** Java

**Spring Boot:** Seleccionar una versión estable 4.1.1 (o superior de acuerdo a la fecha de lectura de esta guía)

**Group:** com.distribuido

**Artifact:** producto

**Packaging:** Jar

**Java:** 17 (o la versión correspondiente al entorno de trabajo configurado)

![captura de inicializr](image.png)

### Dependencias requeridas: 
En el panel lateral derecho, proceda a seleccionar las siguientes 5 dependencias:   
+ Spring Boot DevTools: Proporciona reinicios automáticos de la aplicación y recarga en vivo para acelerar el proceso de desarrollo.   
+ Spring Web: Permite la construcción de aplicaciones web y la exposición de servicios RESTful utilizando Spring MVC.   
+ Spring Data JPA: Facilita la persistencia de datos en bases de datos relacionales mediante la API de Java Persistence y Hibernate.   
+ MySQL Driver: Controlador JDBC indispensable para conectar la aplicación con el motor de base de datos MySQL.   
+ Lombok: Librería de herramientas para desarrolladores que ayuda a reducir el código repetitivo (boilerplate code), generando automáticamente getters, setters, constructores y más mediante anotaciones.   

Posteriormente, haga clic en GENERATE, descargue el archivo comprimido .zip y proceda a descomprimirlo en su equipo.

# 2. Importación y Apertura en Sprimg Tools
La aplicacion se inicializo en Spring Tools

Seleccione la opción File > Open... y navegue hasta el directorio donde descomprimió el proyecto (auto).

Aguarde unos momentos mientras el gestor de dependencias Maven efectúa la descarga e indexación del proyecto.


![alt text](image-2.png)

Verifique que la estructura del
 directorio mantenga la siguiente forma:



# 3. Creación de la Estructura de Paquetes
Con la finalidad de respetar estrictamente la arquitectura en capas (Controller → Service → Repository → DB), es necesario crear 4 paquetes dentro de la ruta principal com.servicio.Auto:

Haga clic derecho sobre el paquete base ***com.servicio.Auto***.

Diríjase a ***New > Package***.

Incorpore cada uno de los siguientes paquetes:

+ com.servicio.auto.controller

+ com.servicio.auto.model

+ com.servicio.auto.repository

+ com.servicio.auto.service

La jerarquía dentro del proyecto deberá visualizarse de la siguiente manera:

![alt text](image-3.png)


# 4. Creación de la Entidad Producto.java
Vamos a empezar con el modelado de **Auto**, la clase Auto.java debe estar en el paquete Model.
Dentro del paquete model, se procederá a definir la clase de dominio que representará la tabla dentro de la base de datos. En este caso dado que se trata del primer microservicio que estamos haciendo utilizaremos únicamente tipos de datos elementales para facilitar la comprensión.

Seleccione ***New > Java Class*** e ingrese el nombre **Auto**.

![alt text](image-1.png)

***Creacion de Paquete y Clases, Interfaz e Implementacion***


+ La creación e implementación de la interfaz AutoRepository dentro del paquete repository.
. Paquete repository (o dao)
Para qué sirve: Es la capa de persistencia y acceso a datos. Se encarga de comunicarse directamente con la base de datos (realizar consultas, inserciones, actualizaciones y borrados).

Clases / Interfaces que lleva dentro:

Interfaces de Repositorio (ej. IAutoRepository): Extienden de JpaRepository<T, ID>. No necesitan implementación escrita a mano; Spring Data JPA genera automáticamente los métodos CRUD estándar (save, findAll, findById, deleteById) y permite crear consultas personalizadas con solo declarar nombres de métodos.
![alt text](image-4.png)

+ La creación e implementación de la clase AutoService dentro del paquete service.
 Paquete service
Para qué sirve: Contiene la lógica de negocio de la aplicación. Aquí se procesan las reglas del sistema, validaciones y la coordinación entre múltiples repositorios antes de que la información llegue al controlador o a la base de datos.

Clases implementacion / Interfaces que lleva dentro:
Interfaces de Servicio (ej. IAutoService): Definen el contrato o los métodos que la capa de negocio ofrece (ej. listar, guardar, buscar, eliminar,editar).



![alt text](image-6.png)

![alt text](image-7.png)

+ La creación e implementación de la clase AutoController dentro del paquete controller.
 Paquete controller (o rest)
Para qué sirve: Es la capa de presentación o interfaz de entrada (API REST). Expone los endpoints HTTP (GET, POST, PUT, DELETE) para que los clientes externos (como una aplicación de Angular/React, Postman o una app móvil) puedan consumir los servicios de la aplicación.

Clases que lleva dentro:

Controladores REST (ej. AutoController): Anotados con @RestController y @RequestMapping. Reciben las peticiones web, llaman a los servicios correspondientes para procesar la información y devuelven respuestas (habitualmente objetos convertidos automáticamente a JSON).
![alt text](image-8.png)


+ La configuración del archivo application.properties para entablar la conexión con la base de datos MySQL.
Paquete raíz / principal (ej. com.servicio.auto)
Para qué sirve: Es el punto de entrada y arranque de toda la aplicación Spring Boot. Se encarga de inicializar el servidor embebido (como Tomcat) y escanear todos los componentes de los demás paquetes.

Clases que lleva dentro:
Clase Principal (ej. AutoApplication): Contiene la anotación @SpringBootApplication y el método estandar public static void main(String[] args) con la llamada a SpringApplication.run.
![alt text](image-9.png)

+ Las instrucciones paso a paso para ejecutar la aplicación y verificar el funcionamiento de los endpoints utilizando Postman, Bruno o el navegador.

## Recursos de Apoyo para la Realización de la Guía
Para orientar el desarrollo correcto de la arquitectura y la configuración del entorno, considere los siguientes aspectos técnicos fundamentales:

Regla de Comunicación Estricta entre Capas
Al momento de diseñar e implementar el código de las capas faltantes, respete la jerarquía de llamadas del patrón arquitectónico:

```Plaintext
[ Controller ] -> [ Service ] -> [ Repository ] -> [ DataBase ]

El Controller llama al Service: Gestiona la petición HTTP y delega la ejecución de la lógica al servicio.

El Service llama al Repository: Procesa las reglas de negocio y solicita las operaciones de datos al repositorio.

El Repository llama a la DataBase: Ejecuta las consultas y la persistencia directa en el motor relacional.
```
### Configuración del Archivo application.properties
Para que el microservicio logre conectarse a la base de datos y ejecutarse en el puerto especificado, debe ingresar al archivo ubicado en la siguiente ruta. Recordar tener instalado y corriendo xampp:
```plaintext
src/main/resources/application.properties
```
Dentro de dicho archivo, incorpore las siguientes líneas de configuración:
![alt text](image-10.png)
