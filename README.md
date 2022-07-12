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

## 2. Resumen del proyecto
En este proyecto se practicaron las principales características de Angular mediante el desarrollo de una aplicación usando:

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
La interpolación (one-way data binding) permite colocar el valor de algunas propiedades o expresiones, entre elementos HTML. Dentro de un componente, en el archivo TS se declaran las propiedades (variables) y se pueden llamar desde el archivo HTML correspondiente. 
Sintaxis de ejemplo:

`<p> The value of the property is: {{property}} </p>`

Donde property es una propiedad declarada en el archivo TS del componente. En el One Way Data Binding, las propiedades creadas en el archivo TypeScript son de sólo lectura, no se pueden modificar.

## 7. Two-way Data Binding
El enlace bidireccional permite enlazar una propiedad en el TS, imprimirla o tenerla en el HTML y modificar su valor simultáneamente desde el input.
La sintaxis del two-way data binding es conocida también como “banana in the box” porque la caja serían los corchetes y la banana serían los paréntesis. Ejemplo:

`<input type=”text” [(ngModel)]=”name”>`

Para usarlo se debe importar el módulo de formularios AngularFormsModule en el archivo app.module.ts. 
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
Se debe crear una carpeta llamada pipes y dentro de ella un archivo llamado filter.pipe.ts.

El Pipe es una Clase de TypeScript, que será llamada FilterPipe y debe implementar una interface que se llama PipeTransform:

Es importante asegurarse siempre de tener los métodos e interfaces necesarios, debidamente importados e implementados, cada vez que se trabaje con un artefacto de Angular (Module, Component, Directive, Service, Pipe, Observer, etc.).

En las líneas superiores, debajo del área de importación, se escribe el decorador @Pipe({}). Dentro de las llaves del Pipe se colocarán las propiedades y valores que definen al Pipe, como por ejemplo el nombre y su naturaleza (pure o impure).

El Pipe recibe un array de valores `values` y un argumento `arg`. Estos parámetros deben ser tipados, de esta manera: <code>values: string[]</code> (un array de strings donde se realizará la búsqueda); arg: string (el string que ingresa el usuario en un input para compararlo con los strings del array principal).
El método devolverá un array de strings que contendrá todos los valores que coincidan con el criterio de búsqueda.

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

3. Para trabajar con formularios reactivos se debe importar el módulo de formularios reactivos `ReactiveFormsModule`: En app.module.ts, incorporarlo en el apartado de imports, y también escribir la sentencia de importación desde @angular/forms en el área de importaciones en la parte superior de ese mismo archivo.
4. En el archivo del template-driven form, `contact.component.html`, se copia el código HTML y se pega en `contact-reactive.component.html`.

5. Se elimina el código HTML que propicia la renderización del objeto asociado al form (`{{contactForm.value | json}}`) y el párrafo con el mensaje inicial del componente: `reactive.contact works!`.

6. En reactive forms no se requiere ngModel ni template variable; en su lugar se emplea FormControlName y debe asociarse al `name` del campo. Esto debe hacerse para cada uno de los campos. Por ejemplo, para el campo `name`, la etiqueta de apertura del input quedaría así:

`<input type=“text” class=“form-control” id=“name” name=“name” formControlName=”name” required>`

7. Para gestionar el formulario reactivo: En la etiqueta `<form>` que envuelve todo el formulario reactivo, se incorpora la directiva FormGroup y se iguala al nombre del formulario, (en este caso `contactForm`). Esa propiedad no existe, debe crearse en reactive-contact.component.ts.

8. En reactive-contact.component.ts, debajo del método ngOnInit( ), se escribe el método onSubmit( ), que no devuelve nada, y que solamente consta de un console.log( ) que muestre los valores del formulario:

```
onSubmit(): void {
	console.log(‘Form -> ‘, this.contactForm.value);
}
```

9. Debajo de la sentencia de exportación de la clase, se crea la propiedad contactForm, se le asigna el tipo FormGroup. Como no se está inicializando, se adjunta un signo de exclamación al nombre de la variable: `contactForm!: FormGroup;`

*Existen varias clases para trabajar con los formularios reactivos. Por ejemplo, FormControl (cuando se tiene un solo input). En este caso se puede crear una propiedad (“`myField`”, por ejemplo) e igualarla a FormControl; así, este campo hereda del FormControl y da acceso a todas las propiedades de FormControl. Si se desea ver cada vez que cambie el valor de ese input (`this.myField.valueChanges`, esto realmente es un Observable), se puede hacer. No se hará aquí, pero es importante conocer esta opción.*

10. Se utilizará FormGroup. Se recomienda escribir el método initForm( ), que va a devolver un FormGroup. Aquí se declaran las propiedades del formulario, para ello se utiliza `FormBuilder`, que se debe importar en el constructor( ). 
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

Los formularios reactivos son muy potentes, es importante conocer más sobre ellos. 💔 I love you 

## 12. Routing


## 13. Lazy Loading


## 14. Guards


## 15. Observables

## 16. Services

## 17. HTTP Requests
