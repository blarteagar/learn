# Angular Roadmap

Un recorrido por las principales características de Angular, la Plataforma de Google para el Desarrollo Web, a través de la construcción de una aplicación, generada con:

* Angular CLI v.13.3.7
* Node v.16.15.0
* npm v8.11.0

Antes de describir cada una de estas características, se debe definir qué es Angular, los archivos que componen un proyecto de desarrollo web y cuáles son las piezas de código que conforman esta Plataforma.

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

# Artefactos de Angular
Angular está conformado por diversas piezas de código, entre ellas se cuentan las siguientes:
* Modules
* Directives
* Components
* Pipes
* Guards
* Services
* Observers

Cada uno de estos artefactos es, en esencia, una Clase de TypeScript modificada por un decorador, el cual por su parte es un tipo de atributo o declaración, capaz de transformar el comportamiento de dicha clase mediante una configuración.

# Componentes
El bloque más pequeño de Angular es el Component (componente). En este caso el decorador se llama @Component y le otorga las siguientes propiedades:
* selector: es el nombre del componente.
* templateURL: es el enlace hacia el archivo HTML, también llamado template o plantilla.
* styleUrls: es el enlace hacia la hoja de estilos, que normalmente están en código SCSS.

Esto significa que el componente está coformado por varios archivos: uno de lenguaje de marcado (HTML), uno de lógica (TS) y una hoja de estilos (SCSS). Su combinación crea una UI (User Interface).

Si se desea insertar una pequeña cantidad de código HTML en un componente, se puede cambiar la propiedad templateURL por template e insertar etiquetas HTML, con la sintaxis de backsticks. Del mismo modo, podría modificarse styleUrls por styles y escribir todos los estilos necesarios, pero esto no se considera una buena práctica. Lo más profesional es tener la hoja de estilos en un archivo aparte.

Debajo del decorador hay una sentencia de exportación de la clase, que contiene el constructor y los métodos.
Un componente B puede ser invocado desde un componente A, mediante una notación similar a las de la etiquetas HTML. Por ejemplo, un componente llamado app-button puede invocarse con la etiqueta: `<app-button></app-button>`

En ese caso, se dice que el componente A es padre del componente B, y a su vez, el componente B será hijo del componente A.

# One way data binding
Texto texto texto

# Two way data binding
Texto texto texto

# Events binding
Texto texto texto

# Pipes
El cometido principal de los Pipes es transformar datos. Por ejemplo, dar formato a un string que contenga un nombre propio, donde se deba poner la primera letra en mayúscula, y las demás en minúsculas. Es posible crear Pipes (custom Pipes). Los Pipes pueden ser Puros o Impuros.
* Puros: La transformación se realiza cuando el dato sufre un cambio.
* Impuros: Se transforman cada vez que se ejecuta el ciclo de detección de cambios, aun cuando la data no haya cambiado.
* Por defecto, los Pipes son puros.
Para crear un Pipe personalizado, se puede usar la terminal o puede ser creado desde cero como una Clase de TypeScript. Por ejemplo, se desea crear un filtro para encontrar los elementos de un array.
El Pipe recibirá un array de strings, así como un criterio de búsqueda (tipo string), y devolverá los valores del listado que coincidan con el criterio.
Se debe crear una carpeta llamada pipes y dentro de ella un archivo llamado filter.pipe.ts.
El Pipe es una Clase de TypeScript, que será llamada FilterPipe y debe implementar una interface que se llama PipeTransform:
Es importante asegurarse siempre de tener los métodos e interfaces necesarios, debidamente importados e implementados.
En las líneas superiores, debajo de la línea export, se escribe el decorador @Pipe({}). Dentro de las llaves del Pipe se colocarán las propiedades y valores que definen al Pipe, como por ejemplo el nombre y su naturaleza (pure o impure).
El Pipe recibe un array de valores values y un argumento arg. Estos parámetros deben ser tipados, de esta manera: values: string[] (un array de strings donde se realizará la búsqueda); arg: string (el string que ingresa el usuario en un input para compararlo con los strings del array principal).
El método devolverá un array de strings que contendrá todos los valores que coincidan con el criterio de búsqueda.
* En el archivo filter.pipe.ts se crea el método transform( ), que en primer lugar verifica con un if ( ) si el argumento es null, es vacío o es cero; o bien, si su longitud es mayor a 3 caracteres. En esos casos, se debe devolver el array de valores. Luego, se implementa un bucle for, cuya variable iteradora value, recorrerá el array principal values, e irá comprobando si ese valor value coincide con el criterio arg; para ello se utiliza el bloque de decisión if( ) y el método indexOf( ); este último busca dentro de un substring para tratar de encontrar el argumento arg (introducido por el usuario en el input). Es necesario asegurar que tanto la entrada en el filtro de búsqueda, como los elementos del array, estén todos en minúsculas, de modo que se pueda hacer esa comparación, independientemente de si la entrada está escrita en minúsculas, mayúsculas, o todas las posibles combinaciones. Entonces todo será transformado a minúsculas aplicando el método toLowerCase( ) tanto al valor value que estamos buscando dentro del array, como al criterio de búsqueda arg que estamos introduciendo en el input de filtrado.
* Si el método indexOf() encuentra coincidencias, devuelve la posición (el índice); de lo contrario, devuelve el valor numérico -1. Entonces, si lo que encuentra es un número mayor a -1 (porque ha encontrado coincidencias), esto será incorporado a un array llamado result. Esa variable result debe ser declarada al inicio del método transform( ). Este array será inicializado en blanco y su tipo es: array de strings. Luego, con notación de parámetros REST, la variable result será igual a lo que haya inicialmente en ella, más el valor value que coincida con el criterio y se agregue al array. Una vez construido el resultado, se retorna.
* En el archivo app.component.html se inserta un input type=”text”, se le asigna la clase “form-control”, se le agrega un placeholder “Filter...”, y el atributo ngModel, con sintaxis de two-way binding, que estará asignado a una propiedad llamada “criteria”; esta última debe declararse en el archivo app.component.ts. 
* En el archivo app.component.ts, al final del listado de propiedades escritas al inicio de la Clase AppComponent, se declara la propiedad: criteria = ‘’ (inicializada como string vacío)
* En el archivo app.component.html, donde se invoca el componente app-cities, en la directiva `*ngFor` donde se renderiza el array cities, se aplicará el Pipe: ngFor=”let city of (cities | filter:criteria)”


# Template-driven forms
* Los formularios Template-driven form se recomiendan para formularios sencillos, como un input sencillo para la inscripción en un newsletter, por ejemplo. Su comportamiento está sujeto a diferentes directivas, como ngModel, por ejemplo.
* Para formularios más avanzados, con campos anidados, y que requieran una lógica más compleja, así como escalabilidad, la mejor elección son los Formularios Reactivos.

Un ejemplo de formulario template-driven puede ser uno en que se solicite a un usuario su nombre, una marca de verificación (check) para indicar que se es mayor de edad, el departamento con el que se desea comunicar y el mensaje que desea enviar. Para ello:

* Se crea un nuevo componente.
* En la plantilla del mismo, se inserta una etiqueta HTML para el título del formulario.
* La siguiente etiqueta es form, donde se anidarán las restantes etiquetas input necesarias para delimitar los campos que conforman el formulario (Opcionalmente, estos campos se maquetan con clases de Bootstrap).
* Para cada campo, la estructura de etiquetas consta de: un `<div>` que envuelva todo el campo; un `<label>` para dar un título al campo; un `<input>` (de tipo variable según el propósito; a saber: “text”, “checkbox”, “select” y “textarea”) y un `<div>` para alojar el mensaje de error en caso de que el campo sea inválido.
Etiqueta form. Dentro de la etiqueta form tendremos los campos del formulario, que serán maquetados con Bootstrap. Crearemos un div con la clase mb-4 . Dentro tendremos label con la clase form-label. Este será el campo name. Dentro del mismo div, y debajo del label, tendremos el input con la clase típica de Bootstrap: form-control y también tendrá un id name. Quiero tener otro div para mostrar si el campo es inválido, y Bootstrap ya tiene una clase llamada invalid-feedback, y en medio de las etiquetas pondremos un texto que diga This field is required.
5:09 Esta estructura básica del formulario, la podremos replicar en estos casos: Un campo para name, un check para verificar que la persona es mayor de 18 años, un select y un textarea para que el usuario nos deje un comentario. Con ello se cubren algunos de los elementos más utilizados en los forms. 
5:53 En el segundo campo, debemos agregar la clase llamada form-check. La etiqueta label pondrá el texto Are you over 18 years of age?. El atributo label será checkAdult, el id será checkAdult igualmente. 
6:24 El tercer campo será un <select>, se le adjudicará la clase form-select form-select-sm, Tendremos 3 opciones. En aplicaciones reales estas opciones aquí dentro son dinámicas, vienen del backend o una API, en este caso, serán hardcodeadas: “marketing”, “sales”, “other”
7:30 en el select, el id será department, tanto para el name y para el label.
7:58 el check de edad debe ser de tipo checkbox y la clase form-check-input.
8:15 en el campo Department se le da el atributo selected a una opción adicional Open this select menu. Se pone una etiqueta al label Department. 
8:50 El último campo es el textarea. El id, label y name será comment. 
9:22 crear un div para alojar un botón. El botón siempre debe tener un type. Se le agregará la clase btn btn-info btn-lg.
9:53 Revisando el form cómo se ve en el navegador.
10:32 agregarle un placeholder al textarea y la clase form-control
10:58 Para que el botón estpe hacia la derecha, se le agregará una clase d-grid gap-2 col-4 float-end.
12:05 Por ahora no hemos hecho nada más que maquetar este formulario.
12:10 Estamos en la documentación de Angular. Directiva Ngform. en la API,  tenemos la directiva NgForm, cómo exportar el módulo de formularios. Y sus propiedades: La propiedad  submitted. que nos dice si el formulario fue enviado o no, la etiqueta form. la instancia de form.group. evento ngsubmit. Propiedades que se heredan de otra clase. Una vez creado el form y le hemos añadido la directiva ngForm, la propiedad value nos va a devolver todos los campos. También está la propiedad valid, invalid. Muchas más. Echar vistazo a la documentación. 
13:31 Crearemos una Template Variable Reference ngForm. Se crea una variable y se igualará a la directiva ngform. A partir de allí se tendrá acceso a las propiedades de la directiva.
13:52 En el código del contact.component.html se incorpora la variable (temporal) #contactForm, que se va a igualar a la directiva ngForm.
14:08 Es muy importante que en el app.module.ts esté importado el módulo de los Forms de Angular FormsModule. 
14:15 Entonces ahora automáticamente Angular hace un seguimiento de este el formulario y sus campos.  Si tomamos el valor contactForm y lo interpolamos en elementos HTML ubicados al final del formulario, pero antes debemos aplicarle el Pipe json que ya viene predefinido en Angular. En este momento no veremos nada porque el objeto está vacío, no hemos incorporado valores al form.
15:06 Como asociar los campos. Una es Dfiícilmente este formulario tendrá que cargar data de una API, por ejemplo. Normalmente cargará en blanco, en vacío, y el usuario introducirá sus datos, y esos datos nosotros los vamos a guardar en una API. No es igual que un formulario de productos, por ejemplo, que nosotros sí podamos necesitar cargar esa data de una API, eso tendremos que enlazarlo con un modelo. Eso lo veremos más adelante,
15:55  En este caso haremos enlace unidireccional. Comenzando con el campo name, agregamos la directiva ngModel. Pero antes de continuar veamos la consola, pues hay un error, donde se indica que se necesita un atributo name para asociarlo a ese campo. Será name=”name”. Y que se debe adjuntar la propiedad value a la variable asociada al ngForm, interpolada al final del formulario: contactForm.value | json.
Al guardar el archivo, se observa que aparece la propiedad name en el objeto asociado al form. Se trasladará la impresión del contactForm a la parte superior del form para poder visualizarlo mejor.  En la medida en que se ingresa información al input, el valor aparece en la propiedad.
17:30 Hay que añadir el atributo name y el ngModel a todos los campos. Agregaremos el atributo required a todos los campos, excepto a departments. 
18:40 Revisando el comportamiento de la app en el momento en que se rellenan los datos del formulario y cómo se va llenando el objeto asociado.
19:16 Cómo procesar la data una vez el usuario presiona send. Aún no se está controlando la acción del botón, pero en el archivo contact.component.html se agrega un “evento” ngSubmit, que cuando ese evento ocurra debemos activar el método onSubmit(). 
19:36 El método onSubmit será creado en contact.component.ts. El método no devuelve nada (: void)  y mostrará un console.log de los valores del fomulario: ‘Form Values’, podemos añadir dos tipos de cosas; la primera, crear una referencia de nuestro formulario y acceder a ese formulario., o también lo que podemos hacer es directamente pasar en el evento el contactForm como parámetro.
Desde contact.component.html:


En contact.component.ts:

21:05 Inicio de la prueba de la aplicación en el navegador. Se llena el formulario y al hacer click en enviar, obtenemos los valores del formulario impresos en la consola. Dependiendo de las necesidades del proyecto, se puede enviar la data a una API, a una base de datos. Por ahora, se imprimirá en consola.
21:48 Lo anterior aplica para cuando hacemos comunicación de una sola vía: el usuario introduce una data, esta se almacena o se envía a servidores o lugares donde dicha data se necesite. 
22:07 Sin embargo, en algunos casos podemos necesitar cargar data en ese formulario, por ejemplo, en el caso de un formulario de productos, necesitamos cargar data en ese formulario. Y eso lo podemos hacer gracias al two-way data binding. 
22:18 Copiaremos el modelo tipo objeto del formulario:

22:23 En el archivo contact.component.ts, debajo del área de importaciones y por arriba del decorador @Component, se crea la interface contactForm:

22:35 Esta interface tendrá unos campos. Una interface permite llegar a un contrato de un modelo de datos, un modelado de datos. Qué es una interface. (Dominicode ofrece un video  pero me temo que no veo el enlace).
22:57 Entonces tenemos un name, que será un string, un checkAdult, que será un booleano, department que será un string, y comment, que también será un string:

23:20 Crearemos un objeto model, debajo de la declaración de la clase del componente, para ser enlazado con el formulario:

23:49 Iremos ahora al contact.component.html; y en lugar de utilizar la directiva ngModel, utilizaremos la sintaxis de banana in the box; es decir, el two-way data binding, y esto lo tenemos que asociar a una propiedad:

24:05 En primer lugar, se asociará a la propiedad name.
24:09 Hay que corregir la sintaxis del objeto model:

24:19 La propiedad está dentro de model.name
24:35 Y ahora, si nosotros volvemos a nuestra aplicación, ahora tenemos los datos enlazados en doble vía. Lo que se ingresa en el formulario en el navegador, modifica el objeto, pero si el modelo model en contact.component.ts se inicializa con otras variables, estas también modificarán los valores correspondientes en el formulario, ya que sus campos están enlazados con el model.
25:04 Entonces, por defecto, los campos del model en contact.component.ts los vamos a dejar en blanco:

25:13 Los datos sólo se modificarán mediante la inserción de data en el formulario, pero quería que supieras que esta es una forma de hacerlo para una comunicación de dos vías.
25:23 Tendremos el two-way data binding en todos nuestros campos, se sustituye la simple mención de la directiva ngModel por la sintaxis de banana en la caja, y enlazada con el campo correspondiente. 
26:30 Probando la app de nuevo, todo funciona bien. El campo de checkAdult viene marcado como true por defecto. Debería ser false. 
26:55 Vimos una manera con un formulario un poquito más tonto, y otra manera con un formulario que requiere tomar data de alguna fuente. Por ejemplo, este modelo model, probablemente tú lo recargarías aquí en el método ngOnInit, con una petición de la API, y lo cargarías en el formulario si lo necesitaras.
27:15 Ahora hablemos de validaciones de nuestros formularios. Cuando hacemos click en el botón submit del formulario, no estamos validando que los campos tengan el tipo que nosotros queremos, o que al menos cumplan nuestras reglas. 
Si vamos a la documentación de Angular Forms, hay un apartado que nos habla de la propiedad value, la propiedad valid que determina si un formulario es válido o no, pero también hay otras propiedades como pristine, dirty, touched, que nosotros podemos utilizar para validar nuestro formulario en general, pero también para validar cada uno de los inputs, es decir, yo puedo validar si el formulario ha sido tocado en general, uno de los campos, pero también puedo determinar si un campo específico fue tocado (touched). Por ejemplo, al revisar la documentación, en dirty, sale el listado de lo que significa cada una de esas propiedades, por ejemplo, pristine verifica que el campo no haya cambiado aún desde su valor inicial. Dirty es que el usuario no haya introducido ningún contenido y el touched se produce cuando el usuario introduce el cursor en el input pero hace lift, sale, allí es cuando se hace el tigger de onBlur.
29:03 En la app, estamos mostrando mensajes de que el campo es requerido, sin darle la oportunidad a nuestro usuario de que haya interactuado mínimamente con los campos, esto no da una buena experiencia de usuario. El otro tema a corregir es que no hay ninguna validación de la data enviada.
30:04 Para ocultar el error se debe ir al input  para saber qué input es para decidir si mostrar u ocultar. Para ello, vamos a utilizar una variable de referencia, en el input de name se coloca almohadilla name y se iguala con ngModel:

30:34 Una vez teniendo la variable de referencia, es posible ir al siguiente div y agregarle el atributo hidden, igualar a name.valid; es decir, cuando el campo sea válido, queremos ocultarlo. Pero además, se debe verificar que el usuario haya tocado ese campo ya. Entonces vimos que tenemos la opción del pristine:

30:57 En la app del navegador, el div con el mensaje de campo reqerido desaparece. Ya que el campo no ha sido tocado y no es válido. 
31:33 La clase Bootstrap de invalid-feedback no se ha aplicado. Entonces se sustituirá por la clase alert alert-danger.
31:54 Vamos a resumir lo que hemos hecho en este campo porque lo vamos a replicar en todos los demás campos.
32:07 Primero. Las validaciones: solamente muestro (el error) cuando el campo sea inválido o cuando el campo haya sido pristine, es decir, que el usuario haya cambiado algo en mi UI (interfaz de usuario). 
32:35 ¿De dónde viene el name? Viene de la variable de referencia del template igualada al ngModel.
32:53 Para todos los demás campos, debemos entonces crear la variable de plantilla de referencia (Template Variable Reference), la que se iguala al ngModel, que corresponda a cada campo del formulario. Y posteriormente hacer las validaciones hidden cuando el campo sea inválido o cuando sea pristine.
33:03 Haremos esto en cada uno de los campos.
34:12 Nuestro botón de Enviar, lo vamos a deshabilitar, y solamente lo vamos a enviar cuando el formulario sea válido.
34:21 Para ello, en contact.component.html, buscamos el botón y en su etiqueta incorporamos la directiva [disabled]=”contactForm.invalid”

34:55 Al abrir la app en el navegador, se observa que el botón está deshabilitado cuando el formulario aún no termina de ser llenado. 
35:21 También podríamos validar que nuestro formulario sea válido desde contact.component.ts. Si en el método onSubmit recibiéramos el formulario completo, podríamos aplicar las propiedades del objeto. Si valid es true, activamos el botón; de lo contrario, no hacemos nada. 
Ejercicio hecho: true

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
