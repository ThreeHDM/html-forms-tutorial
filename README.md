# html-forms-tutorial

Los formularios son una parte importante para las aplicaciones web.

Permiten a los usuarios interactuar con nuestra aplicación web enviando HTTP requests al servidor en dónde alojamos la aplicación.

## Pasos previos

Si bien podemos aprender sobre formularios sin la necesidad de utilizar estilos, para despreocuparnos de la parte gráfica en este tutorial usaremos la plantilla base de bootrap. La cual copio a continuación con algunas pequeñas modificaciones:

```html
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

    <title>Form</title>
  </head>
  <body>
        
  </body>
</html>
```

## Creación de un simple formulario

**FORM TAG**

Lo primero que tenemos que hacer es crear una etiqueta de formulario con su respectivo cierre. `<form></form>`

Si refrescamos la página veremos que nada ha pasado ya que la etiqueta `<form>` viene acompañada de etiquetas de ingreso de datos, es decir `<input>` (no tiene etiqueta de cierre)

**INPUT TAG**

Las etiquetas de tipo input se componen de muchos tipos (texto, mail, contraseña, etc.), para asignarle uno utilizamos el atributo `type`. Este es su valor default, pero de todas maneras es recomendable especificar el tipo de campo. Ya veremos más sobre esto.

En nuestro ejemplo usaremos inputs de tipo `text` y `password`. Este último permite ocultar los caracteres que tipea el usuario en la interface gráfica.

Como podemos tener muchas etiquetas de este tipo debemos nombrarlas con el atributo `name`.

Los inputs pueden tener un valor predeterminado. Para especificarlo usamos el atributo `value="valor_predeterminado"`

```html
    <input type="text" name="name" id="name" value="User">
```

Podemos ayudar al usuario informándolo lo que queremos que ingrese en nuestro input. Para ello utilizamos el atributo `placeholder`, el cual ingresa un texto sugerido en el campo.

```html
    <input type="text" name="name" id="name" placeholder="User Name">
```

En muchas ocasiones existe información que es requerida por nuestra aplicación para que el usuario pueda continuar. Como por ejemplo una contraseña y/o nombre de usuario. El usuario no puede avanzar si no brinda esos datos.

Para esos casos utilizamos el atributo `required` que en HTML5 no permite que se envíe el formulario hasta tanto esté completo ese campo.

```html
    <input type="text" name="name" id="name" placeholder="User Name" required>
```

**LABEL TAG**

Como queremos ayudar al usuario a comprender lo que tiene que hacer en nuestra aplicación, le daremos una pista sobre qué datos o acciones debe ingresar/realizar en nuestro formulario. Para ello utilizaremos la etiqueta `<label></label>`, que funciona como un título para cada input.

Los labels tienen un atributo llamado `for`, en el que especificamos a qué input pertenece. Esto sirve tanto para que el navegador comprenda a que input y form pertenece el label como también para Screen Readers.

Para ello debemos especificar en él, el id del elemento al que apunta.

Ahora al hacer click en el label se seleccionará el campo a completar.

**BUTTON TAG**

Por último para "Enviar" nuestro formulario debemos crear un botón utilizando la etiqueta `<button></button>`

Es útil agregar el atributo `type="submit"` a la etiqueta `<button>` ya que esto permite que el formuario se envíe si el usuario presiona la tecla INTRO y está posicionado en un campo del form.

Otro tipo muy interesante de los botones es `type="reset"` el cual devuelve a los campos a su valor default.

**Formulario Básico**

El formulario quedaría así

```html
    <form>
        <label for="name">Nombre</label>
        <input type="text" name="name" id="name">
        <label for="pass">Contraseña</label>
        <input type="password" name="pass" id="pass" required>
        <button type="submit">Enviar</button>
    </form>
```

Pero este formulario, si bien contiene los elementos básicos aún está lejos de estar terminado.

Si presionamos el botón en este momento veremos que ser refresca la página. Es decir, estamos enviando la información a la misma página en donde se encuentra el formulario. Nosotros queremos enviar la información a otra parte.

Para especificar a dónde enviamos la información utilizamos el atributo `action` dentro de la etiqueta form. En él escribimos la URL a la cual se dirigirá la información.

A los fines de hacer pruebas en este tutorial, usaremos el sitio [webhook.site](https://webhook.site/) el cual genera una URL random a donde podemos enviar información y realizar pruebas.

Copia la `Your randomly generated URL` dentro de action como se muestra en el ejemplo.

IMPORTANTE: COPIA TU URL y no uses la del ejemplo!!!

```html
<form action="https://webhook.site/9a687d56-325e-4230-be3f-81c8adb25f91">
    <label for="name">Nombre</label>
    <input type="text" name="name" id="name">
    <label for="pass">Contraseña</label>
    <input type="password" name="pass" id="pass" required>
    <button type="submit">Enviar</button>
</form>
```

Antes de continuar, probá tu formulario. Verás que en webhoo.site se capturará la información enviada y se detallarán los headers de tu petición HTTP.

## Métodos de petición HTTP

Ya dijimos que los formularios son interfaces que permiten realizar peticiones HTTP. Pero hay diferentes tipos de petición HTTP que dependen de la acción que queremos realizar.

Por default, los formularios realizan peticiones de tipo `GET`, que requieren información al servidor. Si no especificamos nada la información se enviará así.

IMPORTANTE: Las peticiones de tipo `GET` muestran la información enviada en la URL.

Otro método de petición HTTP es `POST` que, como su nombre lo indica, envía información al servidor.

Para especificar el tipo de petición HTTP que queremos que realice nuestro formuario debemos agregar el atributo `method` dentro de la etiqueta `<form>`.

En la [documentación de MDN](https://developer.mozilla.org/es/docs/Web/HTTP/Methods) podemos aprender sobre todos los tipos de petición HTTP.

```html
<form action="https://webhook.site/9a687d56-325e-4230-be3f-81c8adb25f91" method="POST">
    <label for="name">Nombre</label>
    <input type="text" name="name" id="name">
    <label for="pass">Contraseña</label>
    <input type="password" name="pass" id="pass" required>
    <button type="submit">Enviar</button>
</form>
```

## Tipos de INPUT

**EMAIL**

```html
    <input type="email" name="email" id="email">
```

Se difrencia del tipo texto ya que valida que se trate de una dirección de correo y además, en algunos dispositivos, modifica el teclado para facilitar al usuario el ingreso de un correo electrónico.

**NUMBER**

```html
    <input type="number" name="age" id="age" min="1" max="80">
```

No permite otros caractere más que números. Además permite agregar atributos de `min` y `max`, pero no son obligatorios.

**DATE**

```html
    <input type="date" name="fecha" id="fecha">
```

En  HTML5 nos brinda un campo de tipo fecha. Con un selector de almanaque.

**CHECKBOX**

```html
    <form>
        Comida Favorita
        <div>
            <label for="banana">Banana</label>
            <input type="checkbox" name="banana" id="banana" value="banana">
        </div>
        <div>
            <label for="manzana">Manzana</label>
            <input type="checkbox" name="manzana" id="manzana" value="banana">
        </div>
    </form>
```
Podemos elegir una o todas las checkboxes del formulario. Para elegir una o la otra usamos `radiobutton`

**RADIOBUTTON**

```html
<div>
            Género
            <div>
                <label for="genero">Masculino</label>
                <input type="radio" name="genero" id="masculino" value="masculino">
            </div>
            <div>
                <label for="genero">Femenino</label>
                <input type="radio" name="genero" id="femenino" value="femenino">
            </div>
            <div>
                <label for="genero">Otro</label>
                <input type="radio" name="genero" id="otro" value="otro">
            </div>
        </div>
```

Podemos elegir solo un valor de las 3 opciones. 

IMPORTANTE: el `name` de un radiobutton es siempre el mismo en todas las opciones.

Tanto en radiobuttons como en checkboxes es importante especificar el value del campo para enviar esa información al servidor.

**HIDDEN (OCULTO)**

```html
    <input type="hidden" name="oculto" value="escondido">
```

Son valores ocultos. No se muestran en la interface gráfica. Los usuarios no pueden interactuar con ellos. Los usamos para enviar datos que sirven a nuestra aplicación pero que el usuario desconoce.

Lo usaremos en caso de enviar información a un servidor o a otra página para manipularla con JavaScript.

**FILE**

```html
    <input type="file" name="archivo" id="archivo">
```

Nos permite enviar un archivo al servidor. Al utilizar esto debemos agregar un atributo a nuestro formulario. El atributo `enctype=multipart/form-data`, el cual le dice al navegador que si los archivos son muy grandes deberá enviarlos en múltiples partes.

```html
    <form action="ejemplo.php" method="POST" enctype="multipart/form-data">
        <input type="file" name="archivo" id="archivo">
        <button>Enviar Archivo</button>
    </form>
```

**PHONE**

```html
    <input type="tel" name="telefono" id="telefono">
```

En dispositivos móviles crea un teclado de tipo numérico para el usuario.

**URL**

```html
    <input type="url" name="url" id="url">
```
Ingreso de URLS

**COLOR**

```html
    <input type="color" name="color" id="color">
```

Desplega el selector de color del sistema para enviar el valor en Hexadecimal

## Otros elementos de los formularios

**SELECT**

```html
    <div>
        <h3>SELECT</h3>
        <div>
            <label for="colorojos">Color de ojos</label>
            <select name="colorojos" id="colorojos">
                <option value="marrones">Marrones</option>
                <option value="verdes">Verdes</option>
                <option value="azules">Azules</option>
            </select>
        </div>
    </div>
```

Despliega un menú selector. Por default podemos elegir solo una opción de las especificadas.

**TEXTAREA**

```html
        <div>
            <h3>TEXTAREA</h3>
            <div>
                <label for="bio">Biografía</label>
                <textarea name="biografia" id="biografia" cols="30" rows="10">En un agujero en el suelo, vivía un hobbit. No un agujero húmedo, sucio, repugnante, con restos de gusanos y olor a fango, ni tampoco un agujero seco, desnudo y arenoso...
                </textarea>
            </div>
        </div>
``` 

Es un elemento para ingresar textos más largos. Tiene etiqueta de apertura y de cierre. Si queremos darle un valor predeterminado debemos ponerlo entre éstas.

## Dando estilo al Formulario con Bootstrap 4

Bootstrap nos permite dar estilo a los formularios con diferentes clases. En este tutorial veremos un breve ejemplo de estilos con esta librería.

Para conocer más ver la [documentación de formularios](https://getbootstrap.com/docs/4.0/components/forms/)

Para ejemplos ver `bootstrap-forms.html`