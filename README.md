# Angular Roadmap

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
La mayor parte del trabajo de desarrollo se realiza dentro de la carpeta `src`.

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
`<app-button></app-button>`
# One way data binding
Texto texto texto
# Two way data binding
Texto texto texto
# Events binding
Texto texto texto
# Pipes
El cometido principal de los Pipes es transformar datos.
Por ejemplo, transformar un string que contenga un nombre propio, donde se deba poner la primera letra en mayúscula, y las demás en minúsculas.
Es posible crear Pipes personalizados (custom Pipes).
Los Pipes pueden ser Puros o Impuros.

* Puros: La transformación se realiza cuando el dato sufre un cambio.
* Impuros: Se transforman cada vez que se ejecuta el ciclo de detección de cambios, aun cuando la data no haya cambiado.
* Por defecto, los Pipes son puros.


Ejemplo de uso de un Pipe dentro de una plantilla html:
<p>{{‘6/15/15, 9:03 AM’ | date:’full}}</p>
Lo anterior será impreso como una fecha larga:
Monday, June 15, 2015 at 9:03:00 AM GMT+02:00
Ejemplo de uso de más de un Pipe:
<p>My birthday is {{‘6/15/15, 9:03 AM’ | date:’full’ | uppercase}}</p>
Lo anterior será impreso como una fecha larga, completamente en mayúsculas:
MONDAY, JUNE 15, 2015 AT 9:03:00 AM GMT+02:00


Para crear un Pipe personalizado, se puede usar la terminal o puede ser creado desde cero como una Clase de TypeScript. Por ejemplo, se desea crear un filtro para encontrar los elementos de un array.
El Pipe recibirá un array de strings, así como un criterio de búsqueda (tipo string), y devolverá los valores del listado que coincidan con el criterio.
Se debe crear una carpeta llamada pipes y dentro de ella un archivo llamado filter.pipe.ts.
El Pipe es una Clase de TypeScript, que será llamada FilterPipe y debe implementar una interface que se llama PipeTransform:
Es importante asegurarse siempre de tener los métodos e interfaces necesarios, debidamente importados e implementados.
En las líneas superiores, debajo de la línea export, se aplicará el decorador @Pipe({}). Dentro de las llaves del Pipe se colocarán propiedades y valores. Una de ellas es name, la otra es pure, pero por defecto los Pipes son puros (“pure”), así que no es necesario indicarlo aquí.
Cómo funciona el Pipe: Recibe un array de valores values y un argumento arg. Estos parámetros deben ser tipados, de esta manera:
values: string[] (un array de strings donde se realizará la búsqueda).
arg: string (el string que ingresa el usuario en un elemento HTML input para compararlo con los strings del array principal).
El método devolverá un array de strings: string[] que contendrá todos los valores que coincidan con el criterio de búsqueda.
Se debe crear el método transform( ). Para ello se establece un bucle for con una variable iteradora value que recorrerá el array principal values, y va comprobando si ese valor value coincide con el criterio; para ello se utiliza el bloque de decisión if( ) y el método indexOf(); este último busca dentro de un substring para tratar de encontrar el argumento arg. Este argumento será introducido por el usuario en  El método indexOf(), si encuentra coincidencias, devuelve la posición (el índice); de lo contrario, devuelve el valor numérico -1. Entonces, si lo que encuentra es un número mayor a -1 (porque ha encontrado coincidencias), esto será incorporado a un array llamado result. Esa variable result debe ser declarada al inicio del método transform( ). Este array será inicializado en blanco y su tipo es: array de strings. Luego, con notación de parámetros REST, la variable result será igual a lo que haya inicialmente en ella, más el valor value que coincida con el criterio y se agregue al array. Una vez que se tenga un resultado, se debe retornarlo.
Esta es la primera parte del Pipe.
En el archivo app.component.html se inserta un input, se le asigna la clase “form-control”, se le agrega un placeholder “Filter...”, y también dentro de la etiqueta HTML del input se agregará un [(ngModel)] que estará amarrado a una propiedad llamada “criteria” (que crearemos enseguida).
En el archivo app.component.ts. Al final del listado de propiedades escritas al inicio de class AppComponent escribiremos el nombre de la propiedad:
criteria = ' ', que por ahora quedará como un string vacío.
Aparece otro error, que se debe a que no se ha incorporado FormsModule dentro del apartado imports de app.module.ts. Debemos siempre recordar las importaciones necesarias.
Probando la app. Usar la consola para comprobar que no haya errores.
Ir al archivo app.component.html para aplicar el Pipe. En el componente <app-cities>, en la directiva *ngFor donde se renderiza la lista de ciudades (array cities), se aplicará el Pipe, de este modo:
*ngFor=”let city of (cities | filter:’Barcelona’)” 
La palabra “Barcelona” está “hardcodeada” como criterio de búsqueda para probar el Pipe.
Es necesario declarar el Pipe en app.modules.ts. Si hubiéramos creado el Pipe usando la CLI de Angular, este proceso se habría realizado automáticamente. En el archivo app.module.ts, en el apartado @NgModule, bajo el apartado declarations, se agrega el nombre del Pipe: FilterPipe,. Guardar y cerrar.
16:50 probar el filtrado. De una vez inicia aplicando el filtrado cuyo criterio de búsqueda está “hardcodeado”. Si ahora “hardcodeamos” “barcelona” como criterio de búsqueda, no devuelve nada porque no encuentra coincidencia entre “barcelona” y “Barcelona”. Si ahora “hardcodeamos” algún string que no existe, evidentemente tampoco nos muestra nada.
17:00 Ahora lo vamos a hacer dinámico. Para ello, debemos darle como argumento al Pipe, la variable criteria:
*ngFor=”let city of (cities | filter:criteria)” 
17:22 probando la app y el filtro. Si en el input se coloca “bar”, no busca nada; pero si ponemos “Barce” ya devuelve “Barcelona”. Si añadimos la ciudad de “Badalona”, cuando en el input del filter ponemos “Ba”, ya devuelve “Barcelona” y “Badalona”. 
14:46 Tenemos que hacer varias cosas, porque si intentamos buscar en vacío, no nos retorna nada, entonces, es importante controlar un poco ese Pipe, para que valide un poco mejor los datos.
18:02 Abrir el archivo filter.pipe.ts, y al inicio del método transform asociado a FilterPipe crearemos un if () donde devolveremos directamente los valores que recibimos si el argumento es null, es vacío o es cero. O si nuestro argumento tiene una longitud mayor a 3 caracteres. 
  
  El Pipe queda de esta forma:
  
  
``export class FilterPipe implements PipeTransform {
transform{ values: string[], arg: string): string[] {
if(!arg || arg?.length < 3) return values;
let result: string[] = [];
for (const value of values) {
if (value.indexOf(arg) > -1) {
result = [...result, value];
}
}
return result;
}``

18:45 probando lo hecho. Al poner “ba” no devuelve nada; tampoco si ponemos “bar”, ya que hace búsqueda estricta en mayúscula/minúscula.
19:03 Para que no haya problema entre mayúsculas y minúsculas, debemos asegurarnos de que tanto nuestra entrada en el filtro de búsqueda, como los elementos que tenemos en nuestro array, estén todos en minúsculas, de modo que se pueda hacer esa comparación, independientemente de si la entrada es en minúsculas, mayúsculas, o todas las posibles combinaciones. Entonces todo será trasladado a minúsculas.
19:12 ¿cómo lo hacemos? Podemos aplicar el método toLowerCase() tanto al valor value que estamos buscando dentro del array como al criterio de búsqueda arg que estamos introduciendo en el input de filtrado.
export class FilterPipe implements PipeTransform {
transform{ values: string[], arg: string): string[] {
if(!arg || arg?.length < 3) return values;
let result: string[] = [];
for (const value of values) {
if (value.toLowerCase()indexOf(arg.toLowerCase()) > -1) {
result = [...result, value];
}
}
return result;
}

19:44 Comprobando que, si en el input de filtrado, ponemos “BAR”, obtendremos como resultado “Barcelona”. Ya tenemos un filtro. Pipe creado el día de hoy:
import { Pipe, PipeTransform } from "@angular/core";
@Pipe({
name: 'filter',
})
export class FilterPipe implements PipeTransform {
transform{ values: string[], arg: string): string[] {
if(!arg || arg?.length < 3) return values;
let result: string[] = [];
for (const value of values) {
if (value.toLowerCase()indexOf(arg.toLowerCase()) > -1) {
result = [...result, value];
}
}
return result;
}

19:50 Resumiendo: este es un Pipe muy sencillo pero es solamente una demostración para hacernos conscientes de que podemos crear nuestros propios Pipes.
20:00.
El inconveniente del filter con el Pipe es que, cuando no hay ningún resultado, no se muestra nada. Lo recomendable es la programación reactiva, que permite hacer filtros en las aplicaciones, de manera mucho más óptima.
Resumen. Un Pipe recibe una data y la transforma. Hay Pipes Puros e Impuros. Los Puros son aquellos que cambian cuando la data de entrada al Pipe cambia. Los Impuros son aquellos que cambian cada vez que Angular ejecuta su ciclo de detección de cambios. Hay Pipes creados por Angular que podemos utilizar, y hay otros que nosotros mismos podemos crear. En aplicaciones complejas y grandes, ciertamente podríamos requerir Pipes para la transformación de nuestra Data.
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
