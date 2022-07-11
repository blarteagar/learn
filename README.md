# ¿Qué es Angular / Angular CLI?
* Angular es un framework para aplicaciones web.
* Desarrollado en TypeScript (TS), de código abierto, mantenido por Google.
* Su punto fuerte es la creación de SPA (single page applications).
Para trabajar con Angular se requiere la herramienta Angular CLI, que permite:
* Crear nuevos proyectos.
* Crear nuevos módulos, componentes, servicios, directivas, y otras piezas de código de la aplicación.
* Inicializar, desarrollar y mantener aplicaciones en Angular.
* Ejecutar tareas de testing.
* Realizar despliegue de la aplicación a producción.
# Estructura de un proyecto Angular
En la carpeta root (directorio raíz) del proyecto, se puede encontrar toda una estructura de archivos y carpetas que conforman el proyecto de Angular. Entre ellos, destacan los siguientes:
Un conjunto de archivos relacionados con la configuración de TypeScript:
* tsconfig.app.json, que extiende desde tsconfig.json.
* tsconfig.json, donde se expresa configuración de typescript para Angular.
* tsconfig.spec.json, relacionado con los testings.
El archivo package.json contiene la información de los paquetes que conforman el proyecto, la mayoría de ellos son similares a los de cualquier proyecto de node:
* El apartado scripts muestra los scripts ejecutables.
* El apartado dependencies muestra las dependencias de Angular instaladas por el CLI.
* El apartado devDependencies contiene las dependencias que sólo utilizaremos durante el desarrollo de la aplicación. Entre ellos, Typescript, Karma para testing y tipos.
El archivo angular.json está relacionado con la configuración del proyecto:
* Aquí se configuran algunas opciones, como por ejemplo el directorio donde se guardarán los archivos al hacer el build (bundle final a publicar en un hosting u otros lugares). Normalmente estos archivos se almacenan en la carpeta dist (distribución).
* Apartado styles: Si se desea trabajar con Bootstrap, por ejemplo, una vez terminada la instalación del paquete npm, se debe buscar este archivo, ir a esta propiedad y añadirlo. Se debe proceder de la misma manera con el apartado scripts.
En la propiedad de configuración para producción, se maneja la información para construir el bundle final de la aplicación cuando va a ser publicada en un hosting. Esta propiedad permite establecer un budget que limite el peso (tamaño) de la misma.
La mayor parte del trabajo de desarrollo se realiza dentro de la carpeta src. 
* El archivo styles.scss contiene los estilos, utilities y reglas que apliquen para toda la app.
* El archivo main.ts se encarga de levantar la aplicación según la plataforma. También se gestiona el bootstrap (componente de inicio) de la aplicación. 
* El archivo index.html contiene la etiqueta <app-root></app-root>, donde Angular inyecta todo el código.
* La carpeta app contiene todas las piezas de código de la aplicación: módulos, componentes, servicios, pipes, guards etc., 
Al crear un nuevo proyecto de Angular, se crean los archivos del componente app.component:
* Archivo app.component.html con el código de lenguaje de marcado HTML.
* Archivo app.component.ts que contiene la lógica del componente, en lenguaje TypeScript (TS). 
* Archivo app.component.scss que contiene los estilos que aplicarán para el componente (SCSS).
* Archivo app.component.spec.ts que se utiliza para el testing del componente.
* Archivo app.module.ts es el módulo principal de la aplicación. Los componentes se declaran aquí, en caso de que no tengan un módulo propio. 
En el apartado imports se deben inyectar otros módulos; por ejemplo, el de formularios, o el de HTTP de Angular. 
En el apartado providers se inyectan los servicios que deben estar disponibles en toda la aplicación.
El componente bootstrap es el que arranca en el boot de la aplicación.
En la carpeta assets se almacenan las imágenes, fuentes, iconos y otros elementos gráficos de la aplicación.
En el apartado environment hay dos archivos: el environment.prod.ts y el environment.ts. Ambos se utilizan para crear variables en la aplicación. Por ejemplo, la URL de una API.
Angular, durante el desarrollo, utiliza el archivo environment.ts, y cuando se efectúa el despliegue a producción, utiliza el archivo environment.prod.ts. 
# Componentes en Angular
Angular está conformado por diversas piezas de código, a saber: Modules, Directives, Components, Pipes, Guards, Services, Observers, entre otros. Cada uno de estos artefactos es, en esencia, una Clase de TypeScript modificada por un decorador, el cual por su parte es un tipo de atributo o declaración, capaz de transformar una Clase de TypeScript a través de una configuración.
La pieza de código más pequeña de Angular es el Component (componente). Consta de una Clase de TypeScript, modificada por el decorador @Component, que contiene las propiedades:
* selector: es el nombre del componente.
* templateURL: es el enlace hacia el archivo HTML, también llamado template o plantilla.
* styleUrls: es el enlace hacia la hoja de estilos, que normalmente están en código SCSS.
Esto significa que el componente está coformado por varios archivos: uno de lenguaje de marcado (HTML), uno de lógica (TS) y una hoja de estilos (SCSS). Su combinación crea una UI (User Interface).
Si se desea insertar una pequeña cantidad de código HTML en un componente, se puede cambiar la propiedad templateURL por template e insertar etiquetas HTML, con la sintaxis de backsticks. Del mismo modo, podría modificarse styleUrls por styles y escribir todos los estilos necesarios, pero esto no se considera una buena práctica. Lo más profesional es tener la hoja de estilos en un archivo aparte.
Debajo del decorador hay una sentencia de exportación de la clase, que contiene el constructor y los métodos.
Un componente A puede ser invocado desde un componente B, mediante una notación similar a las de la etiquetas HTML. Por ejemplo, un componente llamado app-button puede invocarse con la etiqueta:
<app-button></app-button>
# One way data binding
Texto texto texto
# Two way data binding
Texto texto texto
# Events binding
Texto texto texto
# Pipes
Texto texto texto
Texto texto texto
# Template-driven forms
Texto texto texto
# Reactive forms
Texto texto texto
# Routing
Texto texto texto
Texto texto texto
# Lazy Loading
Texto texto texto
Texto texto texto
# Guards
Texto texto texto
Texto texto texto
# Observers
Texto texto texto
Texto texto texto
# HTTP requests
Texto texto texto
Texto texto texto
# Services
Texto texto texto 
