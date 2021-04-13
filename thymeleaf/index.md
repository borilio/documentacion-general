# Thymeleaf

Thymeleaf es un moderno motor de plantillas Java del lado del servidor para entornos web e independientes.
La documentación oficial la podemos encontrar en https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html.

## Empezando a usarlo

Para usar thymeleaf, debemos añadirle el atributo `xmlns` a las páginas html que tengamos, para que no den errores cuando usemos los "nuevos atributos" de thymeleaf. 

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <head>
    <title>Hola Mundo</title>
    <meta charset="UTF-8" />
  </head>

  <body>
    <p th:text="${saludo}"></p>
  </body>
</html>
```
Ten en cuenta que la página así, no pasaría ningún validador de HTML5. Si quieres tener un documento HTML5 validado, deberás hacer lo siguiente:

```html
<p data-th-text="${saludo}"></p>
```
La diferencia es que eso tendríamos que hacerlo en todos los atributos de thymeleaf `th:*`.

## Mostrando valores recibidos en el modelo

Cualquier variable enviada en el objeto `model`, la podemos mostrar en una vista cd thymeleaf, de la siguiente forma:

```java
//Desde el controlador java...
String usuario="salva@formador.es";
model.addAttribute("nombre", usuario);
```

```html
<!-- Desde HTML -->
<p th:text="${nombre}">El contenido será eliminado</p>
```

El texto de `El contenido del párrafo será eliminado`, será sustituido en tiempo de compilación por el contenido de la variable `nombre`, por lo que la plantilla una vez compilada, quedará de la siguiente forma:

```html
<p>salva@formador.es</p>
```

## Dev Tools

Para empezar a usar devTools, hay que instalar las dependencias necesarias con spring-boot.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-devtools</artifactId>
</dependency>
```

E instalar el plugin de [livereload para chrome](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei). En Chrome habrá que configurarlo para tenga acceso a localhost y ya funcionará directamente. Si guardas un documento html, se actualizará automáticamente en el navegador sin necesidad de recargarlo manualmente.


## Condicionales IF y UNLESS

En algunos casos necesitaremos hacer uso de condicionales para que se muestre una opción u otra dependiendo del resultado de dicha condicional.
Para esto hacemos uso de ``th:if``. 
He aquí un ejemplo con una variable ``edad`` que vale 25:

```html
<p th:if="${edad >= 18}">Eres mayor de edad</p>
```

El resultado sería de esta forma en la vista de cliente:

```html
<p>Eres mayor de edad</p>
```

Con ``th:unless`` es simplemente lo contrario. Si no se cumple dicha condición, se muestra el interior.

Esto sería como un ``else``.

```html
<a th:unless="${edad < 18}" href='www.hbo.com'>HBO</a>
```

Al no ser menor de 18 años, sino que todo lo contrario, no se cumpliría la condición expuesta en el ``unless`` y aparecería lo siguiente en la vista:

```html
<a href='www.hbo.com'>HBO</a>
```

Documentar como se hace un if [aquí](https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#conditional-evaluation)

## Bucles FOR

El bucle forEach [aquí](https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#iteration)
 A veces en nuestro programa necesitamos de una estructura que nos repita(itere) un bloque de código, para eso utilizamos bucles.
Para iterar a la manera en que lo hace un bucle foreach en la mayoría de los lenguajes sería de la siguiente manera.
Suponiendo que nos llega por ejemplo la lista articulos lo iteraremos y mostraremos así:

```html
<h1> articulos </h1>
<table>
<tr>
  <td>nombre</td>
  <td>descripción</td>
  <td>precio</td>
  </tr>
<tr th:each="articulo : ${articulos}">
  <td th:text="${articulo.nombre}"></td>
  <td th:text="${articulo.descripción}"></td>
  <td th:text="${articulo.precio}"></td>
</tr>
</table>
```
articulo es la variable donde se va introduciendo el resultado de cada iteración de articulos, que es la lista que nos llega.
el resultado que nos mostraría nuestro html en caso de que articulos contenga tres elementos. Es el siguiente:
```html
<h1> articulos </h1>
<table>
<tr>
  <td>nombre</td>
  <td>descripción</td>
  <td>precio</td>
  </tr>
<tr>
  <td>Bombilla</td>
  <td>Sirve para iluminar es muy potente</td>
  <td>12</td>
</tr>
  <tr>
  <td>Tornillo</td>
  <td>De acero inoxidable</td>
  <td>2</td>
</tr>
<tr>
  <td>Serrucho</td>
  <td>Para cortar madera</td>
  <td>36</td>
</tr>
</table>
```

## Aplicar clases con th:class

Con la `th:class` sirven para blablablaba

