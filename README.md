# Angular Roadmap
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
* [13. Guards](#13-guards)
* [14. Lazy Loading](#14-lazy-loading)
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

## 2. Resumen del proyecto
En este proyecto se practicaron las principales características de Angular, mediante el desarrollo de una aplicación, utilizando:

* Angular CLI v.13.3.7
* Node v.16.15.0
* npm v8.11.0

La aplicación tiene varias vistas:

* Home
* Reactive form
* Template-driven form
* Users

La navegación entre ellas se realiza a través de una Barra de Navegación, que aloja los enlaces de las rutas que componen la aplicación.
En Home se muestra un listado de ciudades, recuperado de una API, provista de su propio código Backend, que realiza automáticamente operaciones CRUD (Create, Read, Update y Delete). La aplicación realiza peticiones HTTP a la API, y esta realiza las operaciones CRUD que la aplicación solicite. Tales solicitudes provienen de la interacción del usuario con el listado de ciudades, a saber:

* Selección de una ciudad, o bien, limpiar la selección.
* Actualización del nombre de una ciudad, siempre y cuando esté seleccionada.
* Adición de una nueva ciudad al listado.
* Los datos permanecerán almacenados en la API.

Durante la ejecución de las peticiones HTTP, podrá verse un spinner que aparecerá al inicio de la petición, y desaparecerá una vez que la misma haya sido completada. Este comportamiento es controlado por el servicio spinner.service.ts. El spinner actúa como HTTP interceptor, que centraliza todas las modificaciones que requieren las peticiones HTTP.
El Reactive Form es un formulario reactivo. Cuando se intenta salir de este formulario, una función de rutas (o un Observer) detecta que no se han guardado los cambios, y realiza la advertencia correspondiente. Si se hace click en “Cancelar”, el usuario permanece en el Reactive Form. Si se hace click en “Aceptar”, el usuario 
El Template-driven Form es un formulario construido con directivas ngModel, para enlazar el valor de cada input, al valor que se va a enviar a la consola para ser mostrado.
Users es un componente que se creó para probar la reacción de los Guards cuando se intenta acceder a un recurso para el cual no se cuenta con los permisos necesarios. Por esta razón, muestra un alert por defecto indicando que el usuario no cuenta con los permisos necesarios.
Si el usuario intenta acceder a un recurso que no existe, entonces se muestra una página 404.

### Componente principal (App.component)
Contiene un archivo src/app/app.component.ts, que contiene un decorador @Component.
Un decorador que es una declaración que modifica el comportamiento de una clase.
El decorador @Component se importa a este componente desde ‘@angular/core’.
El decorador @Component se declara en un archivo typescript, e indica las rutas donde se pueden encontrar los archivos de estilo y de lenguaje de marcado enlazados al componente.
Luego se declara la exportación de la clase.
El componente no implementa métodos de ningún tipo.
El archivo src/app/app.component.html contiene el llamado a otros componentes:

#### app-spinner
Spinner.interceptor.ts: Contiene la lógica del HTTP interceptor, que se encarga de detectar el momento en que dichas peticiones se activan o desactivan.
Spinner.service.ts: Se usa para alojar los métodos de mostrar y ocultar del spinner, que dependen del Observable isLoading$.
Spinner.component.ts: En la parte superior contiene las importaciones necesarias.
En el decorador @Component, en el apartado template, se ha incorporado directamente la plantilla HTML del spinner. El Pipe (isLoading$ | async) permite suscribirse al Observer isLoading$, y completar la suscripción cuando sea necesario.
El servicio spinnerSvc se inyecta en el constructor de la clase. El servicio es privado y de sólo lectura.
Spinner.component.scss: Contiene los estilos del spinner.

#### app-navbar: 
Es la barra de navegación, que permite ir a las diferentes vistas de la aplicación.
* Navbar.component.scss: Contiene algunos estilos de la barra de navegación. Otros estilos son aplicados con classes de Bootstrap.
* Navbar.component.html: Contiene la plantilla HTML de la barra de navegación.


#### router-outlet: 
Es el componente que renderiza cada vista en la aplicación principal, en un elemento tipo root ubicado en app.component.html. Renderiza el componente que coincide con el array de rutas declarado en app.routing.module.ts.

## 3. Estructura de un proyecto de Angular
En la carpeta root (directorio raíz) del proyecto, se puede encontrar la estructura de archivos y carpetas que conforman el proyecto de Angular. Entre ellos, destacan los siguientes:

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

## 5. Componentes
El bloque más pequeño de Angular es el Component (componente). En este caso el decorador se llama `@Component` y le otorga las siguientes propiedades:
* `selector`: es el nombre del componente.
* `templateURL`: es el enlace hacia el archivo HTML, también llamado template o plantilla.
* `styleUrls`: es el enlace hacia la hoja de estilos, que normalmente están en código SCSS.

Esto significa que el componente está coformado por varios archivos: uno de lenguaje de marcado (HTML), uno de lógica (TS) y una hoja de estilos (SCSS). Su combinación crea una UI (User Interface).

Si se desea insertar una pequeña cantidad de código HTML en un componente, se puede cambiar la propiedad `templateURL` por `template` e insertar etiquetas HTML, con la sintaxis de backsticks. Del mismo modo, podría modificarse `styleUrls` por `styles` y escribir todos los estilos necesarios, pero esto no se considera una buena práctica. Lo más profesional es tener la hoja de estilos en un archivo aparte.

Debajo del decorador hay una sentencia de exportación de la clase, que contiene el constructor y los métodos.
Un componente B puede ser invocado desde un componente A, mediante una notación similar a las de la etiquetas HTML. Por ejemplo, un componente llamado app-button puede invocarse con la etiqueta: `<app-button></app-button>`

En ese caso, se dice que el componente A es padre del componente B, y a su vez, el componente B será hijo del componente A.

## 6. One-way Data Binding
La interpolación (one-way data binding) permite colocar el valor de algunas propiedades o expresiones, entre elementos HTML. Dentro de un componente, en el archivo TS se declaran las propiedades (variables) y se pueden llamar desde el archivo HTML correspondiente. 
Sintaxis de ejemplo:

`<p> The value of the property is: {{property}} </p>`

Donde `property` es una propiedad declarada en el archivo TS del componente. En el One Way Data Binding, las propiedades creadas en el archivo TypeScript son de sólo lectura, no se pueden modificar.

## 7. Two-way Data Binding
El enlace bidireccional permite enlazar una propiedad en el TS, imprimirla o tenerla en el HTML y modificar su valor simultáneamente desde el input.
La sintaxis del two-way data binding es conocida también como “banana in the box” porque la caja serían los corchetes y la banana serían los paréntesis. Ejemplo:

`<input type=”text” [(ngModel)]=”name”>`

Para usarlo se debe importar el módulo de formularios `AngularFormsModule` en el archivo `app.module.ts`. 
El two-way data binding genera un doble enlace que permite actualizar el valor de una propiedad renderizado en una UI, cada vez que cambia el valor de dicha propiedad en un input de HTML, o bien, si cambia su valor declarado en el archivo TS.

## 8. Events Binding
En enlace de eventos o “event binding” permite llamar un método en el momento en que ocurre un evento: Click de un botón, o bien, eventos personalizados. Suponiendo que estamos adjudicando un evento al click de un botón, su sintaxis puede resumirse como sigue:

`<button (evento)=”metodo()”> Metodo </button>`

Cada método debe ser declarado en el archivo de lógica TypeScript correspondiente.

## 9. Pipes
El cometido principal de los Pipes es transformar datos. Por ejemplo, dar formato a un string que contenga un nombre propio, donde se deba poner la primera letra en mayúscula, y las demás en minúsculas. Es posible crear Pipes (custom Pipes). Los Pipes pueden ser Puros o Impuros:

* Puros: La transformación se realiza cuando el dato sufre un cambio.
* Impuros: Se transforman cada vez que se ejecuta el ciclo de detección de cambios, aun cuando la data no haya cambiado.
* Por defecto, los Pipes son puros.

Para crear un Pipe personalizado, se puede usar la terminal o puede ser creado desde cero como una Clase de TypeScript. Por ejemplo, se desea crear un filtro para encontrar los elementos de un array.

El Pipe recibirá un array de strings, así como un criterio de búsqueda (tipo string), y devolverá los valores del listado que coincidan con el criterio.
Se debe crear una carpeta llamada pipes y dentro de ella un archivo llamado `filter.pipe.ts`.

El Pipe es una Clase de TypeScript, que será llamada FilterPipe y debe implementar una interface que se llama `PipeTransform`:

Es importante asegurarse siempre de tener los métodos e interfaces necesarios, debidamente importados e implementados, cada vez que se trabaje con un artefacto de Angular (Module, Component, Directive, Service, Pipe, Observer, etc.).

En las líneas superiores, debajo del área de importación, se escribe el decorador `@Pipe({})`. Dentro de las llaves del Pipe se colocarán las propiedades y valores que definen al Pipe, como por ejemplo el nombre y su naturaleza (pure o impure).

El Pipe recibe un array de valores `values` y un argumento `arg`. Estos parámetros deben ser tipados, de esta manera:

`values: string[]`(un array de strings donde se realizará la búsqueda); 
`arg: string` (el string que ingresa el usuario en un input para compararlo con los strings del array principal).

El método devuelve un array de strings que contiene todos los valores que coincidan con el criterio de búsqueda.

* En el archivo filter.pipe.ts se crea el método transform( ), que en primer lugar verifica con un if ( ) si el argumento es null, es vacío o es cero; o bien, si su longitud es mayor a 3 caracteres. En esos casos, se debe devolver el array de valores. Luego, se implementa un bucle for, cuya variable iteradora value, recorrerá el array principal values, e irá comprobando si ese valor value coincide con el criterio arg; para ello se utiliza el bloque de decisión if( ) y el método indexOf( ); este último busca dentro de un substring para tratar de encontrar el argumento arg (introducido por el usuario en el input). Es necesario asegurar que tanto la entrada en el filtro de búsqueda, como los elementos del array, estén todos en minúsculas, de modo que se pueda hacer esa comparación, independientemente de si la entrada está escrita en minúsculas, mayúsculas, o todas las posibles combinaciones. Entonces todo será transformado a minúsculas aplicando el método toLowerCase( ) tanto al valor value que estamos buscando dentro del array, como al criterio de búsqueda arg que estamos introduciendo en el input de filtrado.

* Si el método indexOf() encuentra coincidencias, devuelve la posición (el índice); de lo contrario, devuelve el valor numérico -1. Entonces, si lo que encuentra es un número mayor a -1 (porque ha encontrado coincidencias), esto será incorporado a un array llamado result. Esa variable result debe ser declarada al inicio del método transform( ). Este array será inicializado en blanco y su tipo es: array de strings. Luego, con notación de parámetros REST, la variable result será igual a lo que haya inicialmente en ella, más el valor value que coincida con el criterio y se agregue al array. Una vez construido el resultado, se retorna.

* En el archivo app.component.html se inserta un input type=”text”, se le asigna la clase “form-control”, se le agrega un placeholder “Filter...”, y el atributo ngModel, con sintaxis de two-way binding, que estará asignado a una propiedad llamada “criteria”; esta última debe declararse en el archivo app.component.ts.

* En el archivo app.component.ts, al final del listado de propiedades escritas al inicio de la Clase AppComponent, se declara la propiedad: criteria = ‘’ (inicializada como string vacío)

* En el archivo app.component.html, donde se invoca el componente app-cities, en la directiva `*ngFor` donde se renderiza el array cities, se aplicará el Pipe: `ngFor=”let city of (cities | filter:criteria)”`.

## 10. Template-driven Forms
Los Formularios son una pieza muy importante en las aplicaciones, ya que permiten la interacción con el usuario a través del intercambio de datos.

* Los formularios Template-driven form se recomiendan para tareas sencillas, como la recolección del correo electrónico para la suscripción a un newsletter, por ejemplo.
* Para formularios más avanzados, con campos anidados, y que requieran una lógica más compleja, así como escalabilidad, la mejor elección son los Formularios Reactivos.
* Para trabajar con los formularios template-driven, es muy importante que en el app.module.ts esté importado el módulo de los Forms de Angular FormsModule.

Un ejemplo de formulario sencillo puede ser uno de contacto, donde se solicite a un usuario su nombre, la confirmación de su mayoría de edad, el departamento con el que se desea comunicar y el mensaje que desea enviar. Para ello:

1. Se crea un nuevo componente con los comandos de la CLI de Angular: `ng g c contact`. En el ejemplo se le dio el nombre “contact”.

2. En el archivo contact.component.html, se inserta una etiqueta h1 para el título del formulario. A continuación, se inserta la etiqueta form, donde se anidarán las restantes etiquetas para delimitar los campos que conforman el formulario:

3. Para cada campo, la estructura de etiquetas consta de: un `<div>` que envuelva todo el campo; un `<label>` para dar un título al campo; un `<input>` (cuyo tipo depende del propósito: “text”, “checkbox”, “select” y “textarea”) y finalmente un `<div>` para alojar un mensaje de error que ga "El campo es requerido", para el caso en que el campo sea inválido.

4. El primer campo corresponde al nombre del usuario. El input será type = “text”. La etiqueta label pondrá el texto “Nombre”. Los atributos label, id, name serán iguales a “name”. Se incluye también el atributo required.

5. El segundo campo corresponde a la verificación de la edad. El input será type = “checkbox”. La etiqueta label pondrá el texto “Are you over 18 years of age?”. Los atributos label, id, name serán iguales a “checkAdult”. Se agrega el atributo required.

6. El tercer campo corresponde a un select con opciones: “Open this menu”, “marketing”, “sales”, “other”. El input será type = “select”. Los atributos label, id, name serán iguales a “department”. Este campo no es obligatorio, por tanto no se agrega el atributo required.

7. El cuarto campo corresponde a un textarea, al que se le agrega un placeholder “Comment...” Los atributos label, id, name serán iguales a “comment”. Se agrega el atributo required.

8. Se crea un `<div>` para alojar un botón. El type será “button”.

9. Puede utilizarse Bootstrap para maquetar los campos del formulario.

10. En la etiqueta form se incorpora una variable de referencia de plantilla (sintaxis: incorporar una almohadilla `#` al inicio del nombre de la variable). En el caso presente, será `#contactForm`, y se iguala con la directiva ngForm: `#contactForm = ngForm`. A partir de allí se tendrá acceso a las propiedades de la directiva, pues automáticamente Angular hace un seguimiento del formulario y sus campos. La variable de referencia `#contactForm` puede ser interpolada en etiquetas HTML al principio del formulario; pero antes se le debe aplicar el Pipe json, nativo de Angular, el cual transforma un objeto en JSON. De este objeto se debe seleccionar la propiedad value, que aloja el contenido del formulario: `<pre> {{ contactForm.value | json }} </pre>`.

11. Para asociar los campos al formulario puede hacerse un enlace unidireccional (One-way Data Binding). Se debe incluir la directiva ngModel en las etiquetas de apertura de los input de los campos.

12. Se debe agregar funcionalidad al botón Send; para ello, en la etiqueta de apertura del formulario <form> se debe agregar el evento ngSubmit y asociarlo al método onSubmit(). Este método debe ser declarado en el archivo contact.component.ts.

13. El método onSubmit( ) será creado en contact.component.ts. El método no devuelve nada (: void) y mostrará un console.log de los valores del fomulario: ‘Form Values’, y se imprimirá la propiedad values del objeto contactForm.

Con el procedimiento anterior, los datos de los campos quedan enlazados al modelo del formulario, y van en dirección desde el input hacia el modelo. Es comunicación en una sola dirección (One-way data binding). Para casos donde se necesite cargar data en un formulario, se puede realizar un two-way data binding:

A. Se copia el modelo tipo objeto del formulario, que contiene las propiedades y valores generadas por el formulario:

```
{
	“name”: “Blanca”,
	“checkAdult”: true,
	“department”: “marketing”,
	“comment”: “Hello World!”
}
```

 B. En el archivo contact.component.ts, debajo del área de importaciones y por arriba del decorador @Component, se crea la interface contactForm, que tiene la forma del objeto mostrado en el apartado A. Una interface permite llegar a un contrato de un modelado de datos. Entonces tenemos un name, que será un string, un checkAdult, que será un booleano, department que será un string, y comment, que también será un string:

```
{
	“name”: string;
	“checkAdult”: boolean;
	“department”: string;
	“comment”: string;
}
```

C. Se crea un objeto model, debajo de la declaración de la clase del componente, y por arriba del constructor( ), para ser enlazado con el formulario:

```
{
	name: “”;
	checkAdult: false;
	department: “”;
	comment: “”;
}
```

D. En el archivo contact.component.html, se utiliza la directiva ngModel con sintaxis de two-way data binding, y para cada nombre de campo, se asocia a las propiedades del modelo. Por ejemplo, el valor `name` se recupera de `model.name`: `[(ngModel)]=”model.name”`.

E. En la aplicación, los datos estarán enlazados en doble vía. Lo que se ingresa en el formulario en el navegador, modifica el objeto, pero si el modelo `model` en el archivo contact.component.ts se inicializa con otras variables, estas también modificarán los valores correspondientes en el formulario, ya que sus campos están enlazados con el model de manera bidireccional.

Es importante realizar validaciones de los valores introducidos en los formularios. Para ello, Angular Forms cuenta con propiedades como `value`, `valid`, `pristine`, `dirty`, `touched`, que permiten validar el formulario en general, pero también cada uno de los campos de manera individual. Por ejemplo, `pristine` verifica que el campo no haya cambiado aún desde su valor inicial. También es necesario occultar mensajes de error que no correspondan. Para validar los valores en campos de formularios, se puede proceder como sigue:

1. Para cada campo, en el `<div>` del mensaje de error, se incluye el atributo hidden y se iguala a (property).valid, para asegurar que el mensaje permanezca oculto mientras el campo en cuestión sea válido. Otra condición que debe cumplirse para mantener oculto el mensaje de error, es que el usuario no haya modificado el valor del input; para ello se usa la propiedad `pristine`. La condición del atributo hidden, en el campo name, quedaría de este modo: `[hidden]="name.valid || name.pristine".

2. Este procedimiento se repite para cada campo.

3. El botón de Enviar puede permanecer deshabilitado mientras el formulario sea inválido. Sólo se podrá activar ese botón cuando el formulario sea válido. Para ello, en contact.component.html, en la etiqueta de apertura del botón se incorpora la directiva `[disabled]="contactForm.invalid"`

4. También es posible validar el formulario desde contact.component.ts. Si en el método onSubmit( ) se recibe el formulario completo, se podrían invocar las propiedades del objeto. Si (property).valid es true, se activa el botón; de lo contrario, se mantiene desactivado.

## 11. Reactive Forms

Los Reactive Forms se originan en una clase que se llama AbstractControl, la cual tiene varias subclases.

Las directivas de Reactive Forms son: FormGroup, FormControl, FormControlName, FormGroupName y FormArrayName.

Se considera que los formularios template-driven se deben emplear cuando las tareas son de lógica sencilla y se tienen muy pocos campos. Los reactivos, por su parte, se emplean cuando los campos están anidados y se requiere una lógica más compleja, así como escalabilidad del componente. Sin embargo, es posible usar los dos enfoques en una misma aplicación, siempre y cuando cada tipo de formulario se utilice en la tarea más adecuada.

* Para un formulario con un solo input, se usa el FormControl.
* Para un formulario con varios inputs, se usa el FormGroup.

Para ilustrar el funcionamiento de los formularios reactivos, se utilizará la misma estructura HTML del apartado anterior (Template-driven Forms), y a partir de la misma se realizarán los cambios necesarios. Específicamente se verá el uso de FormControlName y de FormControl.

1. Se genera un nuevo componente con el siguiente comando de la CLI de Angular:
`ng g c contact-reactive`.

2. En app.component.html, se invoca el componente `<app-contact-reactive></app-contact-reactive>`.

3. Para trabajar con formularios reactivos se debe importar el módulo de formularios reactivos `ReactiveFormsModule`: En `app.module.ts`, incorporarlo en el apartado de imports, y también escribir la sentencia de importación desde @angular/forms en el área de importaciones en la parte superior de ese mismo archivo.
4. En el archivo del template-driven form, `contact.component.html`, se copia el código HTML y se pega en `contact-reactive.component.html`.

5. Se elimina el código HTML que propicia la renderización del objeto asociado al form (`{{contactForm.value | json}}`) y el párrafo con el mensaje inicial del componente: `reactive.contact works!`.

6. En reactive forms no se requiere `ngModel` ni template variable; en su lugar se emplea `FormControlName` y debe asociarse al `name` del campo. Esto debe hacerse para cada uno de los campos. Por ejemplo, para el campo `name`, la etiqueta de apertura del `input` quedaría así:

`<input type=“text” class=“form-control” id=“name” name=“name” formControlName=”name” required>`

7. Para gestionar el formulario reactivo: En la etiqueta `<form>` que envuelve todo el formulario reactivo, se incorpora la directiva FormGroup y se iguala al nombre del formulario, (en este caso `contactForm`). Esa propiedad no existe, debe crearse en reactive-contact.component.ts.

8. En reactive-contact.component.ts, debajo del método `ngOnInit()`, se escribe el método `onSubmit()`, que no devuelve nada, y que solamente consta de un `console.log()` que muestre los valores del formulario:

```
onSubmit(): void {
	console.log(‘Form -> ‘, this.contactForm.value);
}
```

9. Debajo de la sentencia de exportación de la clase, se crea la propiedad contactForm, se le asigna el tipo FormGroup. Como no se está inicializando, se adjunta un signo de exclamación al nombre de la variable: `contactForm!: FormGroup;`

*Existen varias clases para trabajar con los formularios reactivos. Por ejemplo, FormControl (cuando se tiene un solo input). En este caso se puede crear una propiedad (“`myField`”, por ejemplo) e igualarla a FormControl; así, este campo hereda del FormControl y da acceso a todas las propiedades de FormControl. Si se desea ver cada vez que cambie el valor de ese input (`this.myField.valueChanges`, esto realmente es un Observable), se puede hacer. No se hará aquí, pero es importante conocer esta opción.*

10. Se utilizará `FormGroup`. Se recomienda escribir el método `initForm()`, que va a devolver un FormGroup. Aquí se declaran las propiedades del formulario, para ello se utiliza `FormBuilder`, que se debe importar en el constructor( ). 
`constructor(private readonly fb: FormBuilder) { }`
`FormBuilder` y `FormGroup` se importan desde ‘@angular/forms’, asegurarse de tener las importaciones declaradas.

11. El método initForm( ) trabajará con `this.fb.group`. Este método espera un objeto, que define los campos. En cada uno, se sigue la misa sintaxis: En el caso de `name`, se ponen dos puntos, se abren corchetes, y el primer argumento es el valor por defecto (se dejará vacío). Se pone una coma y se escriben las validaciones, que puede ser sólo una, o bien, un array. Para trabajar con las validaciones se debe importar `validators` desde ‘@angular/forms’. Al poner un punto, se pueden ver todos los métodos y propiedades a los que se tiene acceso en el formulario. Por ejemplo, es posible validar que ese campo es requerido, o también, por ejemplo, que el campo `name` tenga un mínimo de, por ejemplo, tres caracteres. En cuanto a los otros campos: `checkAdult` y `comment`, estos son requeridos. Por su parte `department` no es requerido ni necesita validación; por lo tanto, el método initForm( ) quedará de esta manera:

```
initForm(): FormGroup {
	return this.fb.group({
		name: [‘’, [Validators.required, Validators.minlength(3)]],
		checkAdult: [‘’, Validators.required],
		department: [‘’],
		comment: [‘’, Validators.required],
	})
}
```

12. Y en el método ngOnInit, la propiedad contactForm se igualará a lo que devuelva el método initForm( ). Ya esta propiedad tiene el modelo de datos descrito en initFom:
```
ngOnInit(): void {
	this.contactForm = this.initForm();
}
```

#### Validaciones en Reactive Forms

En template-driven forms se utilizó una directiva/atributo `hidden` y se evaluaron las condiciones en que el campo era `valid` o `pristine` (no modificado por el usuario). En reactive forms, esa directiva será eliminada, y en su lugar se utiliza la directiva ngIf en el `<div>` con el mensaje de error, bajo la condición: será impreso si el campo ha sido tocado, y también, si el campo es inválido. 

A. Para acceder al formulario se usa la propiedad contactForm.get(); entre paréntesis se debe pasar el nombre del campo en forma de string; en este caso, name. También se debe acceder a la propiedad `errors`, que sólo existe cuando se presentan errores, por eso, cuando esta se invoca se debe utilizar question mark (`?`): para asegurar que la propiedad existe (ya que pdría ser null). La directiva ngIf queda de la siguiente manera:

`*ngIf=”contactForm.get(‘name’)?.touched && contactForm.get(‘name’)?.errors?.[‘required’]”`

B. Para validar que el campo `name` sea de mínimo 3 caracteres, se usa una estructura de validación similar a la anterior. Debe verificarse, de nuevo, que el campo haya sido `touched` por el usuario, y en la segunda condición, en lugar del `required`, se incorpora la propiedad `minlength`. El mensaje de error en este caso es: `Name must be longer than 3 characters`:

`*ngIf=”contactForm.get(‘name’)?.touched && contactForm.get(‘name’)?.errors?.[‘minlength’]”`

Para especificar de manera dinámica la cantidad de caracteres de `name` en base a la cantidad establecida en minlength (método initForm( ) del archivo contact-reactive.component.ts), se interpola la lógica de validación de minlength utilizado en la línea anterior en el mensaje de error. al invocar la propiedad requiredlength. Posteriormente, en el método initForm( ) especificar un nuevo argumento para minlength (número entero). El `<div>` contentivo del mensaje de error queda como sigue:

`<div *ngIf=”contactForm.get(‘name’)?.touched && contactForm.get(‘name’)?.errors?.[‘required’]” class=”alert alert-danger”> Name must be longer than {{ contactForm.get(‘name’)?.errors?.[‘minlength’].requiredlength }} characters </div>`

Para manejar el error generado cuando el campo se deja en blanco y es obligatorio, el `<div>` contentivo del mensaje de error queda como sigue:

`<div *ngIf=”contactForm.get(‘name’)?.touched && contactForm.get(‘name’)?.errors?.[‘required’]” class=”alert alert-danger”> Name must be longer than {{ contactForm.get(‘name’)?.errors?.[‘minlength’].requiredlength }} characters </div>`

Las validaciones de errores se escribieron en el archivo HTML pero se pueden llevar a TS, mediante la escritura de varios métodos en los que se pueda comprobar el nombre del campo y manejar los errores generados. Esto da facilidad para agregar unit tests.

#### Diferencia entre los Métodos patchValue( ) y setValue( )

1. Dentro del archivo reactive-contact.component.ts se escribe el método onPatchValue( ), no va a devolver nada, y dentro del método se accede al formulario (this.contactForm). Se utiliza el método patchValue( ), al que se le puede pasar un objeto, donde se puede indicar uno o varios campos. El método onPatchValue() será llamado desde ngOnInit(), con la línea this.onPatchValue():
```
ngOnInit(): void {
	this.contactForm = this.initForm();
	this.onPatchValue();
}
ngOnInit(): void {
	this.contactForm.patchValue({name: ‘Natalia’});
}
```

2. Al abrir la aplicación en el navegador, se observa que en el campo de nombre del formulario, aparece el nombre asignado en el objeto (‘Natalia’), ya que patchValue( ) permite escoger algunas propiedades y asignarles valores sin ningún problema.

3. Se escribe el método onSetValue( ), donde se invoca al método setValue( ). Este método también espera un objeto. Se le envía el siguiente: `{comment: ‘Hola Mundo!’}`. Y se llama en el método ngOnInit( ), al igual que onPatchValue( ); este último método será comentado temporalmente, a fin de ver el resultado de onSetValue( ).

```
ngOnInit(): void {
	this.contactForm = this.initForm();
	this.onPatchValue();
	this.onSetValue();
}
//ngOnPatchValue(): void {
	//this.contactForm.patchValue({name: ‘Natalia’});
}
ngOnSetValue(): void {
	this.contactForm.setValue({comment: ‘Hola Mundo!’});
}
```

Al correr la aplicación en el navegador, en la consola se obtiene este error: `Must set a name for name property`. Esto ocurre porque el método setValue( ) obliga a asignar valores a todas las propiedades del formulario.


# 12. Routing

Las rutas permiten:
* La navegación de un componente a otro.
* Pasar parámetros.
* Redireccionar si una ruta no es correcta.
* Proteger rutas (guards) mediante clases que permiten proteger las rutas
* Asegurarse de que la data esté lista antes de imprimir un componente (resolvers).

Para comenzar a trabajar con rutas, se debe tener un módulo de rutas (el módulo app.routing.module.ts), el cual podría incluirse dentro de app.module.ts, pero lo recomendable es tenerlo en un módulo aparte. Se debe importar el módulo de rutas desde @angular/router. 

En el apartado de imports se inyecta el RouterModule y luego se crean las rutas necesarias (`const routes`).

Para utilizarlas se usa routerlink y la ruta (componente) que contiene la vista correspondiente.

Por último, desde app.component.ts, se invoca la directiva `<router-outlet></router-outlet>` para que imprima el componente que coincida con la ruta.

1. Se va a crear un nuevo componente utilizando la CLI de Angular:
`ng g c home`

2. Cuando se crea por primera vez el proyecto de Angular, la CLI pregunta si se desea que el proyecto tenga rutas. Si la respuesta es afirmativa, entonces se genera automáticamente el módulo de routing. Pero el presente proyecto fue creado omitiendo el paso de crear automáticamente las rutas, por lo tanto se deben generar los módulos y componentes de manera manual. En el directorio raíz (root) de la carpeta app se crea un archivo llamado app.routing.module.ts. 

3. El módulo de rutas es una Clase de TypeScript (llamada AppRoutingModule en la línea que declara `export class AppRoutingModule`) decorada `@NgModule()`, este decorador permite pasar una configuración a la clase a fin de modificar su comportamiento. En dicho decorador se insertarán dos propiedades:
`imports`: se importa el `RouterModule` de `Angular.forRoot()`.
`exports`: únicamente `RouterModule`, pero requiere un argumento: el array de rutas a utilizar en la aplicación. Para ello se crea una constante llamada `routes`, que será igual a un array de tipo Routes, importado desde @angular/router, y esa constante se pasa al `RouterModule.forRoot()` como argumento. Se debe importar NgModule desde `'@angular/core'`.

4. Se crean tres rutas: una para el template-driven form, otra para el reactive form, y la tercera para el home. En la constante `routes` se debe enviar un array de objetos, los cuales contienen varias propiedades: la primera es `path` (ruta), se escribe coma (`,`) y luego viene `component`. Por ejemplo, en el caso de ‘contact-reactive’, se requerirá que Angular imprima el ‘ContactReactiveComponent’. Se debe repetir este objeto tantas veces como rutas se requieran:

5. Se deben tomar previsiones para cuando el usuario no especifica ninguna ruta, o la que indica es incorrecta, pues en ese caso la pantalla se queda en blanco. Para evitar esto, se puede crear una ruta específica para cuando no haya coincidencia de ruta; en ese caso se debe hacer una redirección.

6. La ruta en blanco debe ser el primer elemento en el array de objetos, pues Angular lleva a cabo la evaluación en orden, desde el inicio. Si alguna ruta coincide, no evalúa las demás. La redirección se denota con un `redirectTo:`̣̣, donde se debe especificar la ruta a la cual será redirigida la navegación. Existe una propiedad (`pathMatch`) que determina el grado de coincidencia de la ruta; su valor debe establecerse en ‘full’:

```
const routes: Routes = [
  { path: '', redirectTo: ‘/home’, pathMatch: ‘full’ },
  { path: 'contact-reactive', component: ContactReactiveComponent },
  { path: 'contact-template', component: ContactComponent },
  { path: 'home', component: HomeComponent },
];
```

7. Se debe importar app.routing.module en app.modules.ts. En el apartado de `imports:` se agrega AppRoutingModule. Guardar y cerrar el archivo app,routing.module.ts. 

8. Una vez creadas todas las rutas, se debe insertar la directiva `<router-outlet></router-outlet>` en el componente principal app.component.html. 

9. Como se tiene un nuevo componente home, se traslada el código TypeScript y HTML. Se elimina el onInit y el constructor. Eliminando el implement y los imports que no se están realizando. Y con eso queda establecida la lógica de home.component.ts. Entonces app.component.html queda con esta estructura:

```
<div class="container">
  <div class="row">
    <div class="col-6">
      <router-outlet></router-outlet>
    </div>
  </div>
</div>
```

10. Se crea un nuevo componente: Navbar: `ng g c navbar -m app`
Como hay más de un módulo, se debe especificar en qué módulo se declara el componente, para ello debe adjuntarse el comando `-m app`, que indica que la declaración será en app.

11. En el app.component.html se incorpora el llamado a `<navbar></navbar>`.

12. En la documentación de Bootstrap se elige un código de navbar en Bootstrap y en el archivo navbar.component.html se copia el código. Se le da el formato deseado usando Bootstrap.

13. Personalizando el `navbar`. De momento se eliminará la `class= “active”`, pero luego se volverá a incorporar de otra manera.

14. Se colocan las rutas en enlaces, de momento, tipo href:

```
<nav class="navbar navbar-expand-lg navbar-light bg-info">
  <div class="container-fluid">
    <a class="navbar-brand" href="/">cities</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link" href="/">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href=”/contact-reactive">Reactive</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href=”/contact">Template-driven</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

15. Cuando se hace click en cualquiera de los enlaces del menú, la página vuelve a recargar completamente. Para solventar esto, y convertir la app en una verdadera Single-Page-Application (SPA), Angular ofrece el `routerLink`, donde se sustituye `href` por `routerLink`:

```
<nav class="navbar navbar-expand-lg navbar-light bg-info">
  <div class="container-fluid">
    <a class="navbar-brand" href="/">cities</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link" routerLink="/">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" routerLink=”/contact-reactive">Reactive</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" routerLink=”/contact">Template-driven</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

16. La clase `active` de Bootstrap para un link activo, no se percibe con claridad por la similitud en la paleta de colores del link habilitado con respecto al deshabilitado. Para resolver esa situación, se inspecciona el estilo del elemento en las herramientas del desarrollador en el navegador Chrome, y se pega (previa copia) en la hoja de estilos (`navbar.component.scss`):

```
.navbar-light .navbar-nav .nav-link.active, .navbar-light .navbar-nav .show>.nav-link {
color: rgb(188 16 16 / 90%);
background: red;
}
```

17. El enlace `home` está activo inicialmente, pero al seleccionar otra ruta, el enlace de home no pierde el estilo, y el seleccionado no toma el estilo correspondiente. Para solventar esto, Angular tiene una class llamada routerLinkActive, que se aplica como un atributo, y debe igualarse a “active”, que es la clase a aplicar cuando la ruta está activa:

```
<nav class="navbar navbar-expand-lg navbar-light bg-info">
  <div class="container-fluid">
    <a class="navbar-brand" href="/">cities</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link" routerLinkActive=”active” routerLink="/">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" routerLinkActive=”active” routerLink=”/contact-reactive">Reactive</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" routerLinkActive=”active” routerLink=”/contact">Template-driven</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

18. Es importante evaluar la forma en que Angular compara la coincidencia de las rutas. Como la ruta “/home” comienza con la barra diagonal `/`, todas las rutas coinciden. Para solventar esto, se sustituye la ruta `/` por `/home` en las referencias a las rutas en navbar.component.html. De igual forma, es posible modificar la manera en que Angular verifica la coincidencia de rutas. Para ello, en la primera alternativa de ruta, se puede aplicar el atributo [routerLinkActiveOptions], que se iguala al objeto: `{exact: true]`:

```
<nav class="navbar navbar-expand-lg navbar-light bg-info">
  <div class="container-fluid">
    <a class="navbar-brand" href="/">cities</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link" routerLinkActive=”active” routerLink="/">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" routerLinkActive=”active” [routerLinkActiveOptions]={exact: true] routerLink=”/contact-reactive">Reactive</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" routerLinkActive=”active” routerLink=”/contact">Template-driven</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

Para aquellos casos en que el usuario ingrese una ruta incorrecta, es importante tener una página que notifique la situación al usuario. Para ello, se debe:

1. Crear un nuevo componente. Como se tiene más de un módulo, el comando de la CLI debe ser el siguiente:

`ng g c pagenotfound -m app`.

2. Una vez creado el componente, se arranca la aplicación y en el array `routes` del archivo `app.routing.module.ts`, se inscribe, al final del listado, una nueva ruta: `’**’`. Este tipo de rutas son conocidas como “wildcards”, donde todo lo que no coincida con lo anterior, se maneja con esa ruta comodín, y redirige al `PagenotfoundComponent`:

```
const routes: Routes = [
   ...
   { path: ‘**’, component: PagenotfoundComponent }
];
```

3. Si el usuario pone una ruta que no existe, será redirigido a la Página 404 (componente `Pagenotfound`). También podría hacerse una redirección automática a otros componentes de la aplicación, pero esto no es muy recomendable. Es importante poner un mensaje al usuario indicando que el recurso al que está intentando acceder, no existe. 

#### QueryParams

Los `QueryParams` son conjuntos de propiedades y valores ubicados al final de una URL, después del símbolo de interrogación. 

Si, por ejemplo, se requiere encontrar todos los clientes cuya ciudad de residencia sea Lima, podríamos utilizar la URL: `http://myapi.com/customers?city=lima`.

Pueden usarse varios QueryParams, por ejemplo: http://myapi.com/customers?firstname=manuel&lastname=jerez&status=active. Esta URL podría utilizarse para buscar a todos los clientes donde el nombre es `manuel`, el apellido es `jerez` y el estatus es `activo`. Cuando se utiliza más de un QueryParam, es importante separar cada uno mediante el simbolo `&`.

A continuación se describe el funcionamiento de los `QueryParams`, utilizando `navbar` y los formularios creados en los apartados anteriores. 

Podría darse el caso en que se requiera enviar el nombre de un cliente como `QueryParam`, con la intención de que cuando este acceda al formulario de contacto, se pueda imprimir su nombre.

1. En el archivo `navbar.component.ts`, en el `constructor()`, se va a inyectar la clase `router`, de tipo `Router`, importada desde `’@angular/router’`.

2. Se crea, dentro de esa clase, el método `goToReactive()`, que devuleve `:void`. En este método podemos acceder a la instancia que tenemos del Router y vamos a buscar por aquí un método que es el navigate. A este método se le envía una URL que en este caso será `’contact-reactive’` , y como segundo parámetro se le pueden poner extras, se abren llaves, y se invoca la propiedad `queryParams`, dos puntos, a continuación las opciones, en este caso un objeto con una propiedad `name`, dos puntos, y un string que será ‘Gabriela’:

```
import { Component, onInit } from ‘@angular/core’;
import { Router } from ‘@angular/core’;

@Component({
   selector: ‘app-navbar’,
   templateUrl: ‘./navbar.component.html’,
   styleUrls: [‘./navbar.component.scss’]
})
export class NavbarComponent implements OnInit {

   constructor(private readonly router: Router) { }

   ngOnInit(): void {
   }
   goToReactive(): void {
   this.router.navigate([‘contact-reactive’], {queryParams: {[name: ‘Gabriela’}});
}
```

3. En el archivo `navbar.component.html`, en el enlace correspondiente al formulario reactivo, se sustituye`routerLink` por `(click)=”goToReactive()”`. El click sobre el enlace activará el método `goToReactive()`.

4. Al hacer click en la barra de navegación en el enlace `Reactive`, se navega normalmente, pero en la barra de direcciones, en el URL, hay un queryParam, donde está el signo de interrogación, el nombre de la propiedad, que en este caso es `name`, un signo `=` y el valor asignado, en este caso, fue `Gabriela`. Esto significa que este valor está siendo enviado como queryParam.

5. Para recuperar ese valor, se debe ir al archivo `contact-reactive.component.ts`, pues se espera recibir el valor en `contact-reactive.component.html`. Se crea una propiedad que se llame `name`, (que será un string, y como no está inicializado, se le adjunta el signo de exclamación); en esa variable se almacenará el valor enviado por la URL. A continuación, se utilizará una directiva que será llamada `route` y será de tipo `ActivatedRoute`. En el `constructor()` se crea la propiedad `route`, tipada con la interface `ActivatedRoute`:

```
   name!: string;

   constructor(
   ...
   private readonly router: ActivatedRoute) { }
   )
```

6. En el mismo archivo, en el método `ngOnInit()`, se accede a la propiedad `route`, y se invocan los `QueryParams`. Esta expresión es un Observable, según se indica al colocar el cursor sobre el nombre de la propiedad, por ello, es posible llamar al método `subscribe` para hacer seguimiento de esta variable. Esta suscripción devuelve todos los `params` (tipo `Params`), de los cuales se requiere la propiedad `name` recientemente creada. Se invoca `params` y se especifica que la propiedad a leer es `name`; (es la misma que proviene del `QueryParam` declarado en `navbar.component.ts`. Una vez escrito el método `ngOnInit()`, se debe importar la interface `Param`. Se guarda el archivo.

```
   ...
   ngOnInit(): void {
      this.route.queryparams.subscribe {
      (params: Params) => {
         this.name = params[‘name’]}
   }
```

7. En `contact-reactive.html`, en la etiqueta HTML del título del formulario, la propiedad `name` se puede interpolar:

```
   <h1>Contact form {{ name }}</h1>
   ...
```

8. Debería aparecer la propiedad `name` en conjunto con el título del formulario. Si se realizan modificaciones en el query Param de la URL en la barra de direcciones, al refrescar la página, los cambios deben aparecer reflejados:

#### Parámetros

Los Parámetros son propiedades que pueden transmitirse desde un componente hacia otro, mediante una dirección URL.

Por ejemplo, si se requiere imprimir el `id` de un usuario en el componente `template-driven`, se puede proceder de la siguiente manera:

1. En el archivo `navbar.component.ts`, al listado de métodos se agregará uno llamado `goToTemplate()`. Este método devuelve `void`, invoca `router.navigate`, y se le envía una ruta, que en el caso presente es `’contact-template’`. Se coloca una coma y se envía otro argumento (puede ser un string, o el nombre de una propiedad, pero se dejará un string). Se guardan los cambios: 

```
   ...
   goToTemplate(): void {
      this.route.navigate([‘contact-template’, ‘580’]);
   }
```

2. En el archivo `navbar.component.html` se  duplica la ruta que conduce a `’contact-template’`, se comenta la original para no confundirlas, y se procede de forma similar al caso de `’contact-reactive’`: se sustituye `routerLink` por `(click)=”goToTemplate()”`:

3. Para hacer dinámico el parámetro que aparece luego de la barra diagonal, al final de la URL, se debe realizar una modificación en el módulo de rutas `app.routing.module.ts`: En la ruta que conduce a `’contact-template’`, a continuación se especifica una propiedad (se llamará `id`), que se debe recuperar al momento de imprimirla en otros componentes:

```
const routes: Routes = [
   ...
   { path: ‘contact-template/:id’, component: ContactComponent }
];
```

4. En la aplicación, el routing debería reconocer la ruta con ese `id`, y si se modifica esa propiedad en la barra de direcciones, también debería reconocerla.

5. Para recuperar el `id`, en el archivo `contact.component.ts`, se va a declarar un `id` (tipo string), y en el `constructor()` se debe inyectar la interface `ActivatedRoute`. La interface se importa desde `’@angular/route’`. En el método `ngOnInit()`, se accede a `route.params`, que es un Observable. Se activa la suscripción, y se reciben los `params`. (tipo `Params`), luego se inserta una función flecha, y se establece que lo recibido en el parámetro `id` será enviado a la propiedad `id`. Debe recordarse que `id` es un parámetro que existe en la ruta, especificado en `app.routing.module.ts`. Se debe importar `Params` desde `’@angular/route’`. 

6. Posteriormente, en `contact.component.html` se interpola ese `id`:

```
   <h1>Contact form User id: {{ id }}</h1>
```

7. Al abrir la aplicación en el navegador, la ruta debe ser reconocida y el id es renderizado. Pero si volvemos a la homepage, recordemos que tenemos “hardcodeado” (asignado manualmente) el id = 580, y si volvemos a la ruta Template-driven, y lo que venga ya dinámicamente es lo que nosotros vamos a recuperar, y podríamos enviarlo a la API u otros lugares. 

#### Rutas hijas

Rutas hijas: Provienen de una ruta común; por ejemplo las rutas `http:/home/components/ ruta_hija1` y `http:/home/components/ ruta_hija2`. Es un tema muy interesante y que podría requerirse en aplicaciones grandes, medianas o pequeñas. 

1. Crear un componente con el siguiente comando de la CLI:
`ng g c users/user -m app`
2. Se desea crear un componente en una carpeta `users/` y que el componente a crear se llame `user`, y como ya en la aplicación se tiene más de un módulo, se establece que la declaración de este componente aparecerá en `app.module.ts`. Una vez creado el componente, dentro de esa misma carpeta se creará otro componente llamado `users/details`:
`ng g c users/details -m app`
3. Dentro de esa misma carpeta, se tendrá otro componente llamado `list`:
`ng g c users/list -m app`
4. Se cierra la terminal. Se tendrá la carpeta `users` y dentro de ella las carpetas de los componentes: `user`, `details` y `list`. 
5. En primer lugar se definen las rutas en el módulo de routing (`app.routing.module.ts`). Debajo del objeto que contiene la ruta ‘home’, se crea una ruta para ‘users’ y se invoca el componente `UserComponent`:

```
const routes: Routes = [
   ...
   { path: ‘home’, component: HomeComponent },
   { path: ‘users’, component: UserComponent }
];
```

6. Dentro de esta misma ruta, debe insertarse una propiedad llamada `children`; en ella se especifican las rutas hijas. La propiedad `children` espera un array de rutas. Por tanto, se ponen dos puntos, se abren corchetes, y dentro de la propiedad se colocan rutas, con el mismo formato de las rutas principales; es decir, un `path` y un componente a imprimir. Todo lo que esté dentro del array `children` proviene de la ruta `users`. Entonces, en `children` tendremos un `path`, que será `list`, y un `component` que será `ListComponent`. Se coloca una coma y escribimos el siguiente objeto: `path: details, component: DetailsComponent`:

```
const routes: Routes = [
   ...
   { path: ‘home’, component: HomeComponent },
   { path: ‘users’, component: UserComponent,
   children: [
      {path: ‘list’, component: ListComponent },
      path: ‘details’, component: DetailsComponent }
      ],
...
];
```

7. Debe prepararse al componente `users` para que sea realmente un padre. Para ello se debe ubicar el componente `user.component.html`. Se elimina el código existente en ese archivo, y se crea una estructura similar a la de `app.component.html`, con sus clases de Bootstrap: `container`, dentro del mismo se coloca un `row`, y dentro del mismo, dos columnas de 6: Una para un posible listado de usuarios, y la otra para ver posibles detalles del usuario. No se está escribiendo la lógica para estas funcionalidades en la aplicación; solamente se están creando componentes para ser impresos cuando sean llamados por el sistema de `routing`.

8. En el `navbar` no se ha creado el enlace para la ruta `Users`, por lo tanto, debe generarse el mismo, usando la directiva `”routerLink”`:

```
<nav class="navbar navbar-expand-lg navbar-light bg-info">
  <div class="container-fluid">
    <a class="navbar-brand" href="/">cities</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link" routerLinkActive=”active” routerLink="/">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" routerLinkActive=”active” (click)=”goToReactive()”>Reactive</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" routerLinkActive=”active” (click)=”goToTemplate()”>Template-driven</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" routerLinkActive=”active” routerLink=”/users”>Users</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

9. En la app desplegada en el navegador, en el `navbar` aparece la opción `Users`, junto con los textos (planos, sin enlaces) que corresponden a las rutas hijas `List` y `Details`. Esto significa que en realidad no se está accediendo a las rutas. Para ello, en el archivo `user.component.html` se crea un enlace para `Users List` con una etiqueta (`anchor`), y dentro de ella, la directiva `routerLink`. Se repite el procedimiento con `Details`. 

10. Se agrega la directiva <router-outlet></router-outlet> y se guardan los cambios.

```
<div class="container">
   <div class="row">
      <div class="col-6”>
         <a routerLink=”list”>Users List</a>
      </div>
      <div class="col-6">
         <a routerLink=”details”>Details</a>
      </div>
   </div>
</div>
<router-outlet></router-outlet>
```

11. En la aplicación, los enlaces `Users List` y `Details` ya deben ser funcionales, en el sentido de imprimir el componente correspondiente a cada uno.
En resumen, el uso de las rutas hijas consiste en: definir las mismas en el módulo de rutas, generar el enlace en la barra de navegación para el componente raíz de esas rutas hijas (`users`), invocar a los componentes de las rutas hijas en el HTML del componente raíz, en el cual debe insertarse también la directiva `<router-outlet></router-outlet>` para que estos puedan imprimirse.

# Guards

Los Guardianes (`Guards`) ayudan a proteger una determinada ruta, bien sea para evitar que los usuarios accedan a una ruta.

Por ejemplo, se podría proteger esta ruta para asegurar que el usuario haya iniciado sesión en la aplicación. 

Otra posibilidad podría ser cuando el usuario intente abandonar una ruta, podríamos verificar si en un formulario quedan datos por guardar, etc.

Para ilustrar la situación en que un usuario intenta acceder a una ruta para la que no tiene los permisos requeridos:

1. Se ejecuta en la terminal el siguiente comando:

```
ng g guard permissions
```

2. La CLI de Angular preguntará cuál es la `interface` que se desea implementar. Se selecciona `Can Activate` y se presiona `ENTER`. Esto crea el guard `permissions`.

3. Se crea otro `guard`, y esta vez se solicita a la CLI omitir la creación del archivo de testing. Este `guard` se llamará `withoutSave`:

```
ng g guard withoutSave --skip-tests=true
```

4. Se presiona `ENTEṚ`. La bandera `skip tests` impide que se generen los archivos de testing.

5. En un mismo `guard` se pueden tener simultáneamente varias implementaciones de interfaces. Se selecciona `Can Deactivate` y se presiona `ENTER`.

6. Se crea una carpeta `guards` para agrupar los recientemente generados. Los archivos de testing se pueden eliminar. El `guard` es una Clase de TypeScript que implementa una interface nativa de Angular. En este caso, `CanActivate` es la interface que controla el acceso de un usuario a una determinada ruta. En este momento no se tiene un sistema de `login` u otro mecanismo similar, por ello, en el archivo `permissions.guards.ts` se debe crear un método que simule si un usuario está autorizado o no. El método se llama `hasUser()`. Por ahora, el método devuelve `false`; en la interface `CanActivate` no se utilizarán rutas ni estados. Se debe comprobar, dentro de un `if()`, si el método `hasUser()` es `true` o `false`. Si es `true`, retorna `true`, y si es `false`, retorna `false`; en este último caso, a falta de otros componentes, se dispara una alerta para indicar al usuario que :
```
import { Injectable } from ‘@angular/core’;
import { ActivatedRouteSnapshot, CanActivate, RouterStateSnapshot, UrlTree } from ‘@angular/router’;
import { Observable } from ‘rxjs’;

@Injectable({
   providedIn: ‘root’
})
export class PermissionsGuards implements CanActivate {
   canActivate(): Observable<boolean | UrlTree> | Promise<boolean | UrlTree> | boolean | UrlTree {
      if (this.hasUser()) {
         return true;
      }
      //Redirect Login
      alert(‘You do not have permissions’);
      return false;
   }

   hasUser(): boolean {
      return false;
   }
}
```

7. En el módulo de rutas (`app.routing.module.ts`) se implementa la protección de la URL del acceso de usuarios no autorizados; para ello se establece que, dentro de la ruta a proteger, se desea utilizar `canActivate`, a la que se envía un array, ya que es posible utilizar más de un `guard` que aplique para una ruta. En el caso presente, el `guard` se llama `PermissionsGuard`:

```
const routes: Routes = [
   ...
   { path: ‘users’, component: UserComponent, canActivate: [PermissionsGuard],
   children: [
      {path: ‘list’, component: ListComponent },
      path: ‘details’, component: DetailsComponent },
      ],
   }
...
];
```

8. En la app, se espera poder navegar normalmente por las diferentes rutas, pero al querer acceder a `Users` aparece la alerta indicando que el usuario no tiene permisos, ya que el método `hasUser()` de `permissions.guard.ts`, por defecto devuelve `false`. Si se modifica el archivo y se cambia a `true`, entonces se podrá volver a acceder a esa ruta sin mayor inconveniente. Si se vuelve a cambiar a `false`, vuelve a negar el acceso, aun cuando se intente desde la barra de direcciones. E incluso, las rutas hijas, como `UsersList`, tampoco son accesibles, ya que están bajo la tutela del componente padre `users`. En `permissions.guards.ts`, la interface `CanActivate` también protege a las rutas hijas.

En resumen, en el método `canActivate()`, si se necesita que el usuario esté autorizado, no se muestra la ruta, sino que se deshabilita de alguna forma. Una opción es redirigir al Login, si se tiene ese componente preparado.

Segundo ejemplo: Uso de un `guard` para cuando el usuario intente abandonar un componente de formulario sin haber completado todos los datos.

1. En el archivo `withoutSave.guards.ts` se procederá de manera similar a la del ejemplo anterior: se crea un método llamado `hasUser()`, que devuelve un booleano, inicialmente `false` (usuario no ha iniciado sesión). En este método se podría recibir un componente (típicamente un formulario), como parámetro, puesto que normalmente estos `guards` son para los casos en que un usuario está interactuando con un formulario, pero de repente abandona (por ejemplo, hace click en la tecla `back` del navegador). La aplicación debe preguntar si el usuario se irá sin guardar sus cambios.

2. En el método `canDeactivate()`, se debe realizar una comprobación, con un `if()`. Si el usuario inició sesión, entonces el método `hasUser()` está devolviendo `true` porque el usuario está logado. En caso contrario, se utiliza el método `confirm()` de JavaScript; es un alert con la opción de cancelar o continuar; con el mensaje ‘You have unsaved changes’. El método `confirm()` es un booleano: si devuelve true, se le permite al usuario continuar, y de no ser así, se le impide seguir. 

```
@Injectable({
   providedIn: ‘root’
})
export class WithoutSaveGuard implements CanDeactivate<unknown> {
   canDeactivate(): 
      cmponent: unknown,
      currentRoute: ActivatedRouteSnapshot,
      currentState: RouterStateSnapshot,
      nextState: RouterStateSnapshot): Observable<boolean | UrlTree> | Promise<boolean | UrlTree> | boolean | UrlTree {
         return true;
      }
      //Redirect Login
      alert(‘You have unsaved changes’);
      return true;
   }
   hasUser(): boolean {
      return false;
   }
}
```

3. Para implementar este `guard`, se abre el archivo `app.routing.module.ts` y se ubica la ruta del formulario reactivo, se pone una coma y la propiedad a utilizar: para el caso presente, es `canDeactivate`, aquí también es posible pasar un array de `guards`, el de este ejemplo fue llamado `WithoutSaveGuard`. Se guardan los cambios.

4. En la app desplegada en el navegador, se espera poder navegar normalmente hasta el `Reactive Form`. No se ha implementado una lógica para comprobar si faltan datos por guardar; pero si el usuario intenta salir del reactive, se le da la advertencia de que no debería salir del form y que confirme que desea salir. Si se hace click en `cancel`, se mantiene al usuario en la misma ruta. Si se intenta volver a salir, vuelve a salir la pregunta, y si se hace click en `accept`, permite salir hacia otras rutas.
5. Queda por verificar si el usuario ha guardado o no, o si el formulario está `dirty`, punto a partir del cual se genera la confirmación. Si la respuesta es no, se perderían los cambios, y si la respuesta es sí, entonces que se asegure de guardar. Esta parte no se ha implementado aún.

Resumen del `Guard` de Angular: Asegurarse de si un usuario tiene permisos para acceder a una ruta (`canActivate`), o determinar si el usuario puede dejar esa ruta (`canDeactivate`).
Hay otras interfaces que se pueden implementar: `canLoad` y `canActivateChild`.

#### Resolvers en Angular

* Un resolver es una interface que las clases pueden implementar para ser un proveedor de datos.
* Se debe usar con el router para resolver para resolver datos durante la navegación.
* Se debe implementar un método `resolve()` que se invoca cuando comienza la navegación.
* El router espera a que se resuelvan los datos antes de que finalmente se active la ruta.

El resolver es una interface que las clases implementan para ser un proveedor de datos, pero más que eso, sirve como una especie de middleware que cuando inicia la navegación en Angular, él se encargará de retrasar la impresión de un componente hasta que no se tenga la data. Se debe usar con el `router` de Angular, entonces, cuando ese proceso de navegación inicia, el resolver se dispara y hace el `fetch` de la data.

En resumen, un resolver es un mecanismo de Angular que se encarga de tener unos datos listos para imprimir y el componente no inicia su ciclo de vida hasta que la data está lista, en el momento en que se va a llamar a un componente.

La manera de utilizarlo consiste en crear una clase en la que se implementa el método `resolve()`.

1. Dentro de la carpeta `app` se crea una carpeta `resolvers`, y dentro de ella un archivo llamado `data.resolver.service.ts`. El `resolver` se habría podido crear con la CLI de Angular, pero también se puede crear manualmente. Básicamente en Angular, todos los archivos, ya sean un servicio, un guard, un resolver, un componente, siguen el mismo proceso. Todos ellos son clases de typescript, que normalmente estarán decoradas por un decorador. En este caso, esta clase será llamada `DataResolverService`. Esta clase será decorada con el decorador `@Injectable`, y se indicará que está `providedIn: root`.

2. Esta clase tiene que implementar la interface `Resolve`. Esta interface se debe importar desde `’@angular/router’`. Si se hace `ctrl+click` sobre el nombre de esta interface, es posible ver su estructura. Implementa el método `resolve()`, recibe una ruta, un parámetro, un state, entre otros. De momento no se especificarán todas esas propiedades, pues hasta ahora no se tiene una API que esté sirviendo datos. Normalmente esto se suele hacer cuando se tiene una petición a una API y la respuesta puede ser un objeto sumamaente extenso, o no se tiene garantías de que la API responda en el tiempo estipulado; en esos casos se hace un `resolve()` para asegurar que el componente será cargado únicamente cuando se tenga esa data disponible.

```
import { Injectable } from “@angular/core”;
import { Resolve } from “@angular/route”;

@Injectable({ providedIn: ‘root’ })
export class DataResolverService implements Resolve {
   }
```

3. Una vez importada la interface, se crea el método `resolve( )`. Este método por ahora devuelve un `Observable<>`, de cualquier tipo (tipo `any`), la interfaz `Resolve<>` también será tipada con `any` porque no se ha creado una interface para esto. 

4. Se importamos el `Observable` desde `‘rxjs’`. Como todavía no se tiene un service o un API en la aplicación, dentro del método se coloca un comentario con una tarea pendiente: `//TO DO: CALL SERVICE`. Normalmente el resolver se utiliza para hacer peticiones a la API. Antes del decorador `@Injectable`, y por debajo del área de importaciones, se crea una constante `departments`, que consta de un array de strings con los valores: `‘Marketing’, ‘Sales’, ‘Other’`. El método `resolve()` devuelve `return of()`; este último es un método proveniente de `rxjs`; esta expresión convierte el array en un Observable. En este método se pone la constante `departments` como argumento.

5. Una vez creado el método `resolve()`, este debe ser implementado. Lo primero para ello es ir a `app.routing.module.ts` (módulo de rutas). Supóngase que este resolve se desea aplicar a la ruta `‘contact-reactive’`. En dicha ruta ya está incorporado el guard `canDeactivate`. Se escribe coma, se agrega la propiedad `resolve`, que espera un objeto , y dentro del mismo se encuentra la propiedad `departments`, a la cual se asigna el resolver, en este caso llamado `DataResolverService`. Se importa desde su ubicación de origen.

Con lo anterior, el resolver está creado e implementado. Podría utilizarse el mismo resolver en otra ruta, puede ser la del `template-driven form`, por ejemplo. Para asegurar que la data ya está lista antes de imprimir el componente:

A. Se debe ir al código del componente; en este caso, el de `reactive.component.ts`. En el `constructor()`, donde está inyectado ,`route`, en las primeras líneas del método `ngOnInit()`, se escribe `this.route.` y se accede a una propiedad llamada `snapshot` y de esta se invoca la propiedad data. Se abren corchetes y se solicita la data, que en este caso se llama ‘departments’.

B. Para ver si esto se cumple, debajo del área de imports, y antes del constructor, se crea una variable llamada `departments`, y se inicializa como un array vacío. Se vuelve al método `ngOnInit()` y se establece que `this.departments` será igual a lo que se recupere en la petición de la data:

```
export class ContactReactiveComponent implements OnInit {
   contactForm!: FormGroup;
   name!: string;
   departments: string[] = [];

constructor(
   private readonly fb: FormBuilder,
   private readonly route: ActivatedRoute) { }

ngOnInit( ): void {
   this.departments = this.route.snapshot.data[‘departments’];
   ...
}
```

C. No se conoce el tipo de data a recuperar, pero se puede ir al archivo `reactive.component.html`, incluir en las líneas iniciales `<pre>{{ departments }}</pre>` y desplegar la aplicación en el navegador para ver qué se visualiza.

D. Como comportamiento ideal, se espera la impresión del array de strings. No es posible notar el proceso de búsqueda de la data, o del aseguramiento de recuperación de la data, previo a la impresión, porque la data no viene de un servicio externo y tampoco es una data extensa. Pero debe quedar bien establecida la idea de que Angular se asegura de que el componente no se renderiza hasta que la data no esté lista. Si se implementa esto con una API, se verá que el componente no se renderiza hasta que la data no esté lista. 

E. El array de strings corresponde a las categorías del `<select>` en el formulario reactivo. En el archivo `reactive.component.html`, en el `<select>` se incluirá la directiva `*ngFor`, con la variable iteradora local `department` para recorrer el array `departments`. Se crea el atributo `[value]` y se iguala a `department`, y en la etiqueta de la opción correspondiente, se interpolará `department`:

```
  <div class="mb-4">
    <label for="department" class="form-label">Department</label>
    <select name="department" id="department" class="form-select form-select-sm" formControlName="department">
      <option selected>Open this select menu</option>
      <option *ngFor="let department of departments" [value]="department">{{department}}</option>
    </select>
  </div>
```

F. Al abrir la aplicación en el navegador, se observa la impresión del array ubicado al inicio del formulario reactivo, y el `<select>` recorre el array elemento por elemento para desplegar las opciones.
De manera dinámica, si en el archivo `data.resolve.service.ts`, se añaden nuevos elementos al array `departments`, se renderizarán en el `<select>` del reactive form.
Resolver sirve para asegurar que, antes de la impresión de un componente, ya la data esté disponible y lista para ser renderizada.

# Lazy Loading

* El Lazy Loading en Angular, o la carga diferida, es una técnica que retrasa la carga de un determinado módulo hasta que realmente el usuario o la aplicación lo necesite.
* Lazy Loading puede contribuir a mejorar el desempeño de la aplicación.

Esto se puede entender mejor si se abre la terminal y, en la ruta de la aplicación, se ejecuta el comando `ng build`. Esto hace que Angular prepare la aplicación para llevarla a producción. El resultado del bundle final de Angular se muestra a continuación. Se tiene un archivo `main.js`, un archivo `polyfills`, para la compatibilidad entre navegadores, `runtime.js` y un archivo de estilos:

```
Initial Chunk Files                       | Names      | Raw Size    | Estimated Transfer Size
main.b71da01d8d5bba40.js         | main         | 271.72 kB  | 68.74 kB
polyfills.a31312576955ba21.js    | polyfills    | 36.22 kB    | 11.49 kB
runtime.44018e33d142a47b.js     | runtime     | 1.04 kB      | 598 bytes
styles.0512d26f419c5714.css      | styles         | 25 bytes     | 29 bytes
                                                     | Initial total | 309.00 kB | 80.84 kB
```

Por defecto, la aplicación carga todos los módulos, independientemente de si se necesiten o no. Por ejemplo, si el usuario está visitando la home page, ya está disponible toda la información necesaria para los formularios. Eso no tiene sentido, puesto que el usuario no está interactuando con esa parte de la aplicación en ese momento.

Si se abre la pestaña `Network`, de las herramientas del desarrollador de `Chrome Developer Tools`, y se refresca la carga de la aplicación en el navegador, pueden verse los archivos que cargan inicialmente. El `runtime`, el `polyfills`, el `main`, cargan todos a la vez. Sin embargo, es necesario indicarle a Angular que debe cargar ciertos módulos únicamente cuando se necesiten, y eso ayudará al desempeño de la aplicación.

En el código, es necesario generar un feature module y un módulo de rutas también, para que el Lazy Loading pueda funcionar.

1. Se ejecuta el siguiente comando en la terminal: 

`ng g m contact-reactive --routing:true`

`m` significa módulo

`contact-reactive` es el archivo donde se desea crear el módulo.

`routing:true` significa que creará dos módulos: Uno para las rutas, y otro módulo, conocido como feature module, que tiene la función de independizarse de la aplicación principal. Debajo de la línea de comandos, la respuesta que da la CLI al comando de creación del módulo en `contact-reactive`, muestra la creación de los dos módulos. Se cierra la terminal. 

2. Dentro de la carpeta del componente `contact-reactive` puede apreciarse la creación de los archivos `contact-reactive.routing.module.ts` (módulo de routing) y `contact-reactive.module.ts` (este es el feature module). En el feature module se hace la importación del módulo de routing:

```
import { NgModule } from ‘@angular/core’;
import { CommonModule } from ‘@angular/common’;
import { ContactReactiveRoutingModule } from ‘./contact-reactive-routing.module’;

@NgModule({
   declarations: [],
   imports: [
      CommonModule,
      ContactReactiveRoutingModule
      ]
})
export class ContactReactiveModule { }
```

3. En el módulo de routing `contact-reactive.routing.module.ts`, se definen las rutas relacionadas con este módulo en cuestión. En este archivo se tienen elementos similares a los de `app.routing.module.ts` (el routing de la aplicación principal): Se inicializan las rutas, se hace la importación del módulo de ruta de Angular, aunque aquí hay una diferencia: en `app.routing.module.ts` se utiliza el `forRoot` y en `contact-reactive.routing.module.ts`, el `forChild`. En `contact-reactive.routing.module.ts` es posible configurar todo lo que tenga que ver con el `contact-reactive`.
Desde el módulo principal donde están definidas las rutas (`app.routing.module.ts`), el objeto de rutas relacionado con `contact-reactive` se comentará de `app.routing.module.ts` y se copia y pega en `contact-reactive.module.ts`. La propiedad `path` se deja como un string vacío, ya que la ruta completa será importada dinámicamente en `app.routing.module.ts`:

```
import { NgModule } from "@angular/core";
import { RouterModule, Routes } from "@angular/router";

const routes: Routes = [
   {
      path: '',
      component: ContactReactiveComponent,
      canDeactivate: [WithoutSaveGuard],
      resolve: { departments: DataResolverService }
   },
];

@NgModule({
   imports: [RouterModule.forChild(routes)],
   exports: [RouterModule]
})
export class ContactReactiveRoutingModule { }
```

4. Debido a que la ruta absoluta del `reactive-contact` se establecer en `app.routing.module.ts`, entonces, en el `contact-reactive.routing.module.ts`, en la variable `routes` de inicialización de las rutas, se establece path: ‘’ Luego se escribe (coma), se utilizará una propiedad llamada loadChildren (dos puntos, función flecha y utilizando el dynamic import, se realizará la importación del módulo de manera dinámica. Se escribe `import` y se le envía un string, y en este string irá la ruta de ese componente hijo: `./contact-reactive/contact-reactive.module`. Esto devuelve una promesa, que a su vez devuelve un módulo `m` llamado `ContactReactiveModule`:

```
const routes: Routes = [
{ path: ‘ ‘, redirectTo: ‘./home’, pathMatch: ‘full’ },
{
   path: ‘contact-reactive’, loadChildren: () =>
      import(‘./contact-reactive/contact-reactive.module’).then(m => m.ContactReactiveModule)
},
{
   path: ‘contact-template/:id, component: ContactComponent,
   resolve: { departments: DataResolverService }
},
{
   path: ‘users’, component: UserComponent, canActivate: [PermissionGuard],
   children: [
      { path: ‘list’, component: ListComponent },
      { path: ‘details’, component: DetailsComponent },
   ]
},
{ path: ‘**‘, component: PageNotFoundComponent },
];
```

5. Ahora se debe trabajar con el routing del reactive form (`contact-reactive.routing.module.ts`). Se debe hacer la importación de todo lo que se requiere, como el Guard, el Resolver, y el componente como tal. Ya que se tiene un feature module, realmente, en el archivo `reactive-component.module.ts` se debe ir al apartado `declarations` e importar el formulario reactivo, que se llama `ContactReactiveComponent`. Del mismo modo, se tiene que sacar del módulo principal (`app.module.ts`), ya que esto estaba todo antes en el mismo bundle, se elimina la declaración y la importación de `ContactReactiveComponent`. Todo lo relacionado con el módulo de formularios, debe estar también en el feature module del formulario (reactive-component.module.ts); en este archivo se debe importar el `ReactiveFormsModule` desde `’@angular/forms’`:

```
import { NgModule } from ‘@angular/core’;
import { CommonModule } from ‘@angular/common’;
import { ContactReactiveRoutingModule } from ‘./contact-reactive-routing.module’;
import { ContactReactiveComponent } from ‘./contact-reactive.component’;
import { ReactiveFormsModule } from ‘@angular/forms’;

@NgModule({
   declarations: [ContactReactiveComponent],
   imports: [
      CommonModule,
      ContactReactiveRoutingModule,
      ReactiveFormsModule,
   ]
})
export class ContactReactiveModule { }
```

6. El nombre del módulo `ReactiveFormsModule` también se puede eliminar, tanto de la lista de declaraciones como de la de importaciones de `app.module.ts`.
7. Se abre la aplicación en el navegador, con su consola abierta en la pestaña `Network`, y se observa que el módulo `contact-reactive.module.ts` se carga únicamente cuando se navega hacia la ruta correspondiente. Se carga el módulo junto con todas sus dependencias.

Así se gana en performance, con el código modularizado.

Al comparar los resultados de los `ng build` de la app, antes y después de implementar un lazy loading de rutas, al finalizar el bundle aparece un nuevo apartado: `Lazy Chunk Files`, que corresponde a ese módulo independiente que se carga únicamente cuando es requerido.

## 15. Observables




## 16. Services





## 17. HTTP Requests




