
# Ejercicios

## JavaScript

### Scope & Hoisting

Determiná que será impreso en la consola, sin ejecutar el código.

> Investiguen cual es la diferencia entre declarar una variable con `var` y directamente asignarle un valor.

```javascript
x = 1;
var a = 5;
var b = 10;
var c = function(a, b, c) {
  var x = 10;
  console.log(x); // 10
  console.log(a); // 8
  var f = function(a, b, c) {
    b = a;
    console.log(b); // 8
    b = c;
    var x = 5;
  }
  f(a,b,c);
  console.log(b); // 9
}
c(8,9,10);
console.log(b); // 10
console.log(x); // 1
```
//


```javascript
console.log(bar); // undefined
console.log(baz); // undefined
foo();
function foo() { console.log('Hola!'); }
var bar = 1;
baz = 2;
```

//..



```javascript
var instructor = "Tony";
if(true) {
    var instructor = "Franco";
}
console.log(instructor); // Franco
```
//..


```javascript
var instructor = "Tony";
console.log(instructor); // Tony
(function() {
   if(true) {
      var instructor = "Franco";
      console.log(instructor); // Franco
   }
})();
console.log(instructor); // Tony
```

//..



```javascript
var instructor = "Tony";
let pm = "Franco";
if (true) {
    var instructor = "The Flash";
    let pm = "Reverse Flash";
    console.log(instructor); // The Flash
    console.log(pm); // Reverse Flash
}
console.log(instructor); // The Flash
console.log(pm); // Franco
```
//.. 


### Coerción de Datos

¿Qué crees que van dar estas operaciones?:

```javascript
6 / "3" // 2
"2" * "3" // 6 
4 + 5 + "px" // 9px
"$" + 4 + 5 // $45
"4" - 2 // 2
"4px" - 2 // NAN
7 / 0 // inf
{}[0] // [0]
parseInt("09") // 09
5 && 2 // 2
2 && 5 // 5
5 || 0 // 5
0 || 5 // 0
[3]+[3]-[10] // 23
3>2>1 // false
[] == ![] // true
```

> Si te quedó alguna duda repasá con [este artículo](http://javascript.info/tutorial/object-conversion).


### Hoisting

¿Cuál es el output que vemos en consola luego de ejecutar este código? Explicar porque es así:

```javascript
function test() {
   console.log(a); // undefined
   console.log(foo()); // 2

   var a = 1;
   function foo() {
      return 2;
   }
}

test(); // La variable 'a' se declara undefined ya que se llama antes de declararse, mientras que la funcion foo() al ser invocada segun las definiciones de Hoisting si corre.
```
//
Y el de este:

```javascript
var snack = 'Meow Mix';

function getFood(food) {
    if (food) {
        var snack = 'Friskies';
        return snack;
    }
    return snack;
}

getFood(false);  // Al utilizar el argumento 'false' siendo un booleano, se cancela la funcion getFood y ya que la variable tampoco se invoca la consola daria en blanco.
```


### This

¿Cuál es el output que vemos en consola luego de ejecutar esté código? Explicar porqué es así:

```javascript
var fullname = 'Juan Perez';
var obj = {
   fullname: 'Natalia Nerea',
   prop: {
      fullname: 'Aurelio De Rosa',
      getFullname: function() {
         return this.fullname;
      }
   }
};

console.log(obj.prop.getFullname()); // Aurelio De Rosa

var test = obj.prop.getFullname; 

console.log(test()); // undefined // El primer console da Aurelio pporque se llama especificamente ese valor del objeto, mientras que en el segundo se invoca una funcion que no existe.
```

### Event loop

Considerando el siguiente código, ¿Cuál sería el orden del ouput? ¿Por qué?

```javascript
function printing() {
   console.log(1); 
   setTimeout(function() { console.log(2); }, 1000);
   setTimeout(function() { console.log(3); }, 0);
   console.log(4); 
}
// 1 
// 4
// 3
// 2 Primero salen los dos console clasicos y luego por orden de tiempo los que contienen el set timeout.

printing();
```
