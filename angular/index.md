# Angular

Añadir lo que queráis

## Como referenciar desde codigo un elemento HTML
No todos los datos de html se pueden usar con el "[(ngModel)]" (tambien conocido como banana in a box), 
en esos casos se tiene tiene que usar el "#" para poder crear un objeto basado en la etiqueta de html.
Ejemplo

```html

<input #range type="range" max="1" min="-1" step="0.01" />

```
En este caso, se habria creado el objeto "range", de este objeto se podrian obtener cualquier atributo, incluyendo el value
aunque no este incluido directamente en el elemento. 

Ejemplo util

```html

<input #range type="range" max="1" min="-1" step="0.01" (input)="texto = range.value" />

<p>{{texto}} </p>

```

En este caso cada vez que se haga un cambio, la variable texto cambiaria a valer lo mismo que el valor del rango. El nombre despues del "#" 
puede ser el que quiera.

Esto no se limitaria a inputs claro.

```html

<p #parrafo >Esto es un texto por defecto </p>

<p> {{parrafo.innerHTML}} </p>

 ```
En este caso, los dos parrafos tendrian el mismo contenido ya que esta cogiendo los datos de un p a otro p
