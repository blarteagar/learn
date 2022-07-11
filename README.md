# Angular Roadmap

## Índice

* [1. Preámbulo](#1-preámbulo)
* [2. Resumen del proyecto](#2-resumen-del-proyecto)
* [3. Estructura de un proyecto de Angular](#3-estructura-de-un-proyecto-de-angular)
* [4. Artefactos de Angular](#4-artefactos-de-angular)
* [5. Componentes](#5-componentes)
* [6. One-way Data Binding](#6-one-way-data-binding)
* [7. Two-way Data Binding](#7-two-way-data-binding)
* [8. Events Binding](#8-events-binding)
* [9. Pipes](#9-pipes)
* [10. Template-driven Forms](#10-template-driven-forms)
* [11. Reactive Forms](#11-reactive-forms)
* [12. Routing](#12-routing)
* [13. Lazy Loading](#13-lazy-loading)
* [14. Guards](#14-guards)
* [15. Observables](#15-observables)
* [16. Services](#16-services)
* [17. HTTP Requests](#17-http-requests)

***

## 1. Preámbulo
### ¿Qué es Angular / Angular CLI?
* Angular es un framework para aplicaciones web.
* Desarrollado en TypeScript (TS), de código abierto, mantenido por Google.
* Su punto fuerte es la creación de SPA (single page applications).

Para trabajar con Angular se requiere la herramienta Angular CLI, que permite:

* Crear nuevos proyectos.
* Crear nuevos módulos, componentes, servicios, directivas, y otras piezas de código de la aplicación.
* Inicializar, desarrollar y mantener aplicaciones en Angular.
* Ejecutar tareas de testing.
* Realizar despliegue de la aplicación a producción.

Antes de describir cada una de estas características, se debe definir qué es Angular, los archivos que componen un proyecto de desarrollo web y cuáles son las piezas de código que conforman esta Plataforma.

## 2. Resumen del proyecto
En este proyecto se llevó a cabo la práctica de las principales características de Angular, la Plataforma de Google para el Desarrollo Web, a través de la construcción de una aplicación, generada con:

* Angular CLI v.13.3.7
* Node v.16.15.0
* npm v8.11.0

## 3. Estructura de un proyecto de Angular
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
* El archivo index.html contiene la etiqueta app-root, donde Angular inyecta todo el código.
* La carpeta app contiene todas las piezas de código de la aplicación: módulos, componentes, servicios, pipes, guards etc.
 
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

A continuación, se describen los artefactos de Angular que permiten construir una aplicación web.

## 4. Artefactos de Angular
Angular está conformado por diversas piezas de código, entre ellas se cuentan las siguientes:
* Modules
* Directives
* Components
* Pipes
* Guards
* Services
* Observers

Cada uno de estos artefactos es, en esencia, una Clase de TypeScript modificada por un decorador, el cual por su parte es un tipo de atributo o declaración, capaz de transformar el comportamiento de dicha clase mediante una configuración.

### Scripts / Archivos

#### General

##### `README.md`

Debe contener lo siguiente:

* Un título con el nombre de tu proyecto.
* Un resumen de 1 o 2 líneas de qué se trata tu proyecto.
* La imagen final de tu proyecto.
* Investigación UX:
Lista numerada:

  1. Explicar quiénes son los usuarios y los objetivos en relación con el
    producto.
  2. Explicar cómo el producto soluciona los problemas/necesidades de dichos
    usuarios.
  3. Luego colocarás la foto de tu primer prototipo en papel.
  4. Agregar un resumen del feedback recibido indicando las mejoras a realizar.
  5. Imagen del prototipo final.

A continuación describimos los archivos que utilizarás:

##### `src/index.html`

En este archivo va el contenido que se mostrará al usuario (esqueleto HTML).
Encontrarás 3 etiquetas iniciales, las cuales si deseas puedes borrar y empezar
de cero:

* `<header>`: encabezado de tu proyecto.
* `<main>`: contenido principal de tu proyecto.
* `<footer>`: pie de página de tu proyecto.


##### `src/validator.js`

Acá escribirás las funciones necesarias para que el usuario pueda verificar la
tarjeta de crédito y ocultar los dígitos de su número de tarjeta.
Esta función debe ser pura e independiente del DOM.
    Ejemplo de uso

    ```js
    maskify('4556364607935616') === '############5616'
    maskify(     '64607935616') ===      '#######5616'
    maskify(               '1') ===                '1'
    maskify(               '')  ===                ''
    ```

***

### Primeros pasos

1. Antes que nada, asegúrate de tener un :pencil: editor de texto en
  condiciones
2. Para ejecutar los comandos a continuación necesitarás una :shell:
  [UNIX Shell](https://github.com/Laboratoria/bootcamp/tree/master/topics/shell),
3. Una de las integrantes del equipo debe realizar un :fork_and_knife:
  [fork](https://help.github.com/articles/fork-a-repo/) 
  [configurar](https://gist.github.com/BCasal/026e4c7f5c71418485c1) un `remote`
  hacia el mismo.
4. :arrow_down: [Clona](https://help.github.com/articles/cloning-a-repository/)
  tu _fork_ a tu computadora (copia local).
5. 📦 Instala las dependencias del proyecto con el comando `npm install`. Esto
  asume que has instalado [Node.js](https://nodejs.org/) (que incluye [npm](https://docs.npmjs.com/)).
6. Si todo ha ido bien, deberías poder ejecutar las :traffic_light:
  pruebas unitarias (unit tests) con el comando `npm test`.
7. Para ver la interfaz de tu programa en el navegador, usa el comando
  `npm start` para arrancar el servidor web y dirígete a
  `http://localhost:5000` en tu navegador.
8. A codear se ha dicho! :rocket:


## 5. Componentes
El bloque más pequeño de Angular es el Component (componente). En este caso el decorador se llama @Component y le otorga las siguientes propiedades:
* selector: es el nombre del componente.
* templateURL: es el enlace hacia el archivo HTML, también llamado template o plantilla.
* styleUrls: es el enlace hacia la hoja de estilos, que normalmente están en código SCSS.

Esto significa que el componente está coformado por varios archivos: uno de lenguaje de marcado (HTML), uno de lógica (TS) y una hoja de estilos (SCSS). Su combinación crea una UI (User Interface).

Si se desea insertar una pequeña cantidad de código HTML en un componente, se puede cambiar la propiedad templateURL por template e insertar etiquetas HTML, con la sintaxis de backsticks. Del mismo modo, podría modificarse styleUrls por styles y escribir todos los estilos necesarios, pero esto no se considera una buena práctica. Lo más profesional es tener la hoja de estilos en un archivo aparte.

Debajo del decorador hay una sentencia de exportación de la clase, que contiene el constructor y los métodos.
Un componente B puede ser invocado desde un componente A, mediante una notación similar a las de la etiquetas HTML. Por ejemplo, un componente llamado app-button puede invocarse con la etiqueta: `<app-button></app-button>`

En ese caso, se dice que el componente A es padre del componente B, y a su vez, el componente B será hijo del componente A.


## 6. One-way Data Binding


## 7. Two-way Data Binding


## 8. Events Binding



## 9. Pipes
El cometido principal de los Pipes es transformar datos. Por ejemplo, dar formato a un string que contenga un nombre propio, donde se deba poner la primera letra en mayúscula, y las demás en minúsculas. Es posible crear Pipes (custom Pipes). Los Pipes pueden ser Puros o Impuros:

* Puros: La transformación se realiza cuando el dato sufre un cambio.
* Impuros: Se transforman cada vez que se ejecuta el ciclo de detección de cambios, aun cuando la data no haya cambiado.
* Por defecto, los Pipes son puros.
* 
Para crear un Pipe personalizado, se puede usar la terminal o puede ser creado desde cero como una Clase de TypeScript. Por ejemplo, se desea crear un filtro para encontrar los elementos de un array.

El Pipe recibirá un array de strings, así como un criterio de búsqueda (tipo string), y devolverá los valores del listado que coincidan con el criterio.
Se debe crear una carpeta llamada pipes y dentro de ella un archivo llamado filter.pipe.ts.

El Pipe es una Clase de TypeScript, que será llamada FilterPipe y debe implementar una interface que se llama PipeTransform:

Es importante asegurarse siempre de tener los métodos e interfaces necesarios, debidamente importados e implementados, cada vez que se trabaje con un artefacto de Angular (Module, Component, Directive, Service, Pipe, Observer, etc.).

En las líneas superiores, debajo de la línea de importación de la clase, se escribe el decorador @Pipe({}). Dentro de las llaves del Pipe se colocarán las propiedades y valores que definen al Pipe, como por ejemplo el nombre y su naturaleza (pure o impure).

El Pipe recibe un array de valores `values` y un argumento `arg`. Estos parámetros deben ser tipados, de esta manera: <code>values: string[]</code> (un array de strings donde se realizará la búsqueda); arg: string (el string que ingresa el usuario en un input para compararlo con los strings del array principal).
El método devolverá un array de strings que contendrá todos los valores que coincidan con el criterio de búsqueda.

* En el archivo filter.pipe.ts se crea el método transform( ), que en primer lugar verifica con un if ( ) si el argumento es null, es vacío o es cero; o bien, si su longitud es mayor a 3 caracteres. En esos casos, se debe devolver el array de valores. Luego, se implementa un bucle for, cuya variable iteradora value, recorrerá el array principal values, e irá comprobando si ese valor value coincide con el criterio arg; para ello se utiliza el bloque de decisión if( ) y el método indexOf( ); este último busca dentro de un substring para tratar de encontrar el argumento arg (introducido por el usuario en el input). Es necesario asegurar que tanto la entrada en el filtro de búsqueda, como los elementos del array, estén todos en minúsculas, de modo que se pueda hacer esa comparación, independientemente de si la entrada está escrita en minúsculas, mayúsculas, o todas las posibles combinaciones. Entonces todo será transformado a minúsculas aplicando el método toLowerCase( ) tanto al valor value que estamos buscando dentro del array, como al criterio de búsqueda arg que estamos introduciendo en el input de filtrado.

* Si el método indexOf() encuentra coincidencias, devuelve la posición (el índice); de lo contrario, devuelve el valor numérico -1. Entonces, si lo que encuentra es un número mayor a -1 (porque ha encontrado coincidencias), esto será incorporado a un array llamado result. Esa variable result debe ser declarada al inicio del método transform( ). Este array será inicializado en blanco y su tipo es: array de strings. Luego, con notación de parámetros REST, la variable result será igual a lo que haya inicialmente en ella, más el valor value que coincida con el criterio y se agregue al array. Una vez construido el resultado, se retorna.

* En el archivo app.component.html se inserta un input type=”text”, se le asigna la clase “form-control”, se le agrega un placeholder “Filter...”, y el atributo ngModel, con sintaxis de two-way binding, que estará asignado a una propiedad llamada “criteria”; esta última debe declararse en el archivo app.component.ts.

* En el archivo app.component.ts, al final del listado de propiedades escritas al inicio de la Clase AppComponent, se declara la propiedad: criteria = ‘’ (inicializada como string vacío)

* En el archivo app.component.html, donde se invoca el componente app-cities, en la directiva `*ngFor` donde se renderiza el array cities, se aplicará el Pipe: ngFor=”let city of (cities | filter:criteria)”

* Con este procedimiento, la palabra que se introduzca en el input


## 10. Template-driven Forms

* Se crea un nuevo componente. En el ejemplo se le dio el nombre “contact”.
* En el archivo contact.component.html, se inserta una etiqueta HTML para el título del formulario.
* La siguiente etiqueta es form, donde se anidarán las restantes etiquetas input necesarias para delimitar los campos que conforman el formulario (Opcionalmente, estos campos se maquetan con clases de Bootstrap).
* Para cada campo, la estructura de etiquetas consta de: un `<div>` que envuelva todo el campo; un `<label>` para dar un título al campo; un `<input>` (de tipo variable según el propósito; a saber: “text”, “checkbox”, “select” y “textarea”) y un `<div>` para alojar el mensaje de error en caso de que el campo sea inválido.
* El primer campo corresponde al nombre del usuario. El input será type = “text”. La etiqueta label pondrá el texto “Nombre”. Los atributos label, id, name serán iguales a “name”.
* El segundo campo corresponde a la verificación de la edad. El input será type = “checkbox” debemos agregar la clase llamada form-check. La etiqueta label pondrá el texto “Are you over 18 years of age?”. Los atributos label, id, name serán iguales a “checkAdult”.
* El tercer campo corresponde a un erá un <select>, se le adjudicará la clase form-select form-select-sm, Tendremos 3 opciones. En aplicaciones reales estas opciones aquí dentro son dinámicas, vienen del backend o una API, en este caso, serán hardcodeadas: “marketing”, “sales”, “other”.

  
  
## 11. Reactive Forms
  
  

## 12. Routing
  
## 13. Lazy Loading
  
## 14. Guards
  
## 15. Observables
  
## 16. Services
  
## 17. HTTP Requests




















