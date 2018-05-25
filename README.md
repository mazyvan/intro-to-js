# Into to Javascript

## What is ECMAScript (ES)?

> Para muchos la palabra ECMA no resulta tan conocida. Se trata de un acrónimo de “European Computer Manufacturers Association (ECMA)”, una organización internacional basada en membresías de estándares para la comunicación y la información.
En el año de 1997 se crea un comité (TC39) en la ECMA para estandarizar JavaScript. A partir de entonces, los estándares de JavaScript se rigen como ECMAScript. No solo JavaScript se basa en el lenguaje ECMAScript, existen otros como JScript y ActionScript 3 que también lo hacen. Haciendo una analogía, diremos que ECMAScript es el lenguaje y JavaScript, JScript y ActionScript 3 son dialectos de este lenguaje, siendo JavaScript su dialecto más conocido y utilizado.

Fuente: [DevCode](https://devcode.la/blog/que-es-y-por-que-aprender-ecmascript/)

En resumen ECMA es el organismo que define las especificaciones de Javascript (js) a través los estándares y versiones de ECMAScript (es)

## Values & Types

JavaScript tiene valores tipados, no variables tipadas. Los siguientes tipos están disponibles.

* `string`
* `number`
* `boolean`
* `null` y `undefined`
* `object`
* `symbol` (nuevo en ES6)

JavaScript proporciona el operador `typeof` que sirve para examinar una variable y determinar su tipo.

```js
var a;
typeof a;				// "undefined"

a = "hello world";
typeof a;				// "string"

a = 42;
typeof a;				// "number"

a = true;
typeof a;				// "boolean"

a = null;
typeof a;				// "object" -- weird, bug

a = undefined;
typeof a;				// "undefined"

a = { b: "c" };
typeof a;				// "object"
```

El valor que regresa el operador `typeof` siempre es uno de seis (siete en el caso de ES6! - el tipo "symbol") siempre de tipo string. De ese modo, `typeof "abc"` returns `"string"`, not `string`.

Solo los valores tienen tipo en JavaScript; las variables solo son contenedores para esos valores.

`typeof null` es un caso especial, porque erroneamente regresa  `"object"`, cuando uno esperaría que regresara `"null"`.

### Objects

El tipo de dato `object` es un tipo de valor compuesto al que puedes asignar propiedades (locaciones con nombre) en donde cada una de ellas puede contener sus propios valores de cualquier tipo. 

```js
var obj = {
	a: "hello world",
	b: 42,
	c: true
};

obj.a;		// "hello world"
obj.b;		// 42
obj.c;		// true

obj["a"];	// "hello world"
obj["b"];	// 42
obj["c"];	// true
```

La notación con corchetes resulta útil cuando se quiere consultar un valor de manera dinamica.

```js
var obj = {
	a: "hello world",
	b: 42
};

var b = "a";

obj[b];			// "hello world"
obj["b"];		// 42
```

Hay otros tipos de datos con los que comumente se interacuta en JavaScript: `array` y `function`. Pero en lugar de ser tipos de datos integrados, deberían ser considerados más bien como subtipos -- versiones especializadas del tipo `object`

#### Arrays

Un arreglo/vector es simplemente un objeto (`object`) que guarda valores (de cualquier tipo) pero en lugar de propiedades o "keys", usa posiciones indexadas. Por ejemplo:

```js
var arr = [
	"hello world",
	42,
	true
];

arr[0];			// "hello world"
arr[1];			// 42
arr[2];			// true
arr.length;		// 3

typeof arr;		// "object"
```

#### Functions

El otro subtipo de "`object`" que vas a usar en JS son las funciones.

```js
function foo() {
	return 42;
}

foo.bar = "hello world";

typeof foo;		// "function"
typeof foo();		// "number"
typeof foo.bar;		// "string"
```

### Built-In Type Methods

Los tipos de datos integrados y sus subtipos cuentan con comportamientos expuestos como propiedades y métodos sumamente útiles.

Por ejemplo:

```js
var a = "hello world";
var b = 3.14159;

a.length;             // 11
a.toUpperCase();      // "HELLO WORLD"
b.toFixed(4);	      // "3.1416"
```

El valor de tipo `string` se encapsula en el objeto `String`, un `number` se encapsula en un objeto `Number`, y un valor `boolean` se encapsula en un objeto `Boolean`. La mayor parte del tiempo uno no tiene que preocuparse de estas encapsulaciones, JS se encarga de esto de manera automatica.

### Comparing Values

El resultado de cualquier comparación es un valor estrictamente booleano (verdadero o falso), independientemente de qué tipo de valores se comparen.

#### Coercion

La coerción viene en dos formas en JavaScript: explícita e implícita. La coerción explícita es simplemente que usted puede ver obviamente en el código que una conversión de un tipo a otro ocurrirá, mientras que la coerción implícita es cuando la conversión del tipo puede suceder más como un efecto secundario no obvio de alguna otra operación.

Ejemplo de coerción *explícita*:

```js
var a = "42";

var b = Number( a );

a;				// "42"
b;				// 42 -- the number!
```

Y aquí hay un ejemplo de coerción *implícita*:

```js
var a = "42";

var b = a * 1;	// "42" implicitly coerced to 42 here

a;              // "42"
b;              // 42 -- the number!
```

#### Truthy & Falsy

Cuando un valor no booleano es coaccionado a un booleano. ¿Se convierte en verdadero o falso, respectivamente?

La lista específica de valores falsos en JavaScript es la siguiente:

* `""` (empty string)
* `0`, `-0`, `NaN` (invalid `number`)
* `null`, `undefined`
* `false`

Cualquier valor que no esté en esta lista falsa es "true". Estos son algunos ejemplos:

* `"hello"`
* `42`
* `true`
* `[ ]`, `[ 1, "2", 3 ]` (arrays)
* `{ }`, `{ a: 42 }` (objects)
* `function foo() { .. }` (functions)

#### Equality

Hay cuatro operadores de igualdad: `==`, `===`, `!=`, Y `!==`. Las formas `!` son, por supuesto, las versiones simétricas "no iguales" de sus contrapartes; La *no igualdad* no debe confundirse con la *desigualdad*.

La diferencia entre `==` y `===` normalmente se caracteriza por que `==` comprueba la igualdad de valor y `===` comprueba tanto el valor como la igualdad de tipo. Sin embargo, esto es inexacto. La manera correcta de caracterizarlos es que `==` chequea por igualdad de valor con coerción permitida, y `===` comprueba la igualdad de valor sin permitir coerción; `===` se llama a menudo "igualdad estricta" por esta razón.

Considere la coerción implícita que es permitida por la comparación `==` loose-equality y no se permite con la `===` estricta-igualdad:

```js
var a = "42";
var b = 42;

a == b;			// true
a === b;		// false
```

En la comparación `a == b`, JS advierte que los tipos no coinciden, por lo que pasa por una serie ordenada de pasos para coaccionar uno o ambos valores a un tipo diferente hasta que los tipos coincidan, donde entonces se puede comprobar una igualdad de valor simple.

Puedes leer la sección 11.9.3 de la especificación de ES5  (http://www.ecma-international.org/ecma-262/5.1/) para ver las reglas exactas, y le sorprenderá lo sencillo que es este mecanismo , En comparación con todo lo negativo que lo rodea.


Reglas simples para la mayoria de los casos:

* Si un valor (o lado) en una comparación podría ser `true` o `false` evita  `==` y usa `===`.
* Si cualquier valor en una comparación podría ser uno de estos valores específicos (`0`, `""`, or `[]` -- vector vacío), evita `==` y usa `===`.
* En todos los demás casos, es seguro utilizar `==`. No sólo es seguro, sino que en muchos casos simplifica tu código de una manera que mejora la legibilidad.

**Note:** For more information about the `==` equality comparison rules, see the ES5 specification (section 11.9.3) and also consult Chapter 4 of the *Types & Grammar* title of this series; see Chapter 2 for more information about values versus references.

#### Inequality

Los operadores `<`, `>`, `<=`, y `>=` se utilizan para la desigualdad, a la que se hace referencia en la especificación como "comparación relacional". Normalmente se utilizarán con valores comparables como números. Es fácil entender que `3 < 4`.

Pero los valores `string` de JavaScript también se pueden comparar por desigualdad, usando reglas alfabéticas típicas (`"bar" < "foo"`).

Considera:

```js
var a = 41;
var b = "42";
var c = "43";

a < b;		// true
b < c;		// true
```

What happens here? In section 11.8.5 of the ES5 specification, it says that if both values in the `<` comparison are `string`s, as it is with `b < c`, the comparison is made lexicographically (aka alphabetically like a dictionary). But if one or both is not a `string`, as it is with `a < b`, then both values are coerced to be `number`s, and a typical numeric comparison occurs.

El problema más grande que puedes encontrar aquí con comparaciones entre tipos de valor potencialmente diferentes - recuerda, no hay formas de "desigualdad estricta" para usar - es cuando uno de los valores no se puede convertir en un número válido, como:

```js
var a = 42;
var b = "foo";

a < b;		// false
a > b;		// false
a == b;		// false
```

¿Cómo pueden ser `false` las tres comparaciones? Debido a que el valor `b` está siendo coaccionado al "valor de número inválido" `NaN` en las comparaciones `<` y `>`, y la especificación dice que `NaN` no es ni mayor ni menor que cualquier otro valor.

## Variables

En terminos simles (considerando solo caracteres ASCII) un identificador debe comenzar con `a`-`z`, `A`-`Z`, `$`, o `_`. Entonces puede contener cualquiera de esos caracteres más los números `0`-`9`.

**Note:** For more information about reserved words, see Appendix A of the *Types & Grammar* title of this series.

### Function Scopes

Utilice la palabra clave `var` para declarar una variable que pertenecerá al ámbito de la función actual o al ámbito global si está en el nivel superior fuera de cualquier función.

#### Hoisting

Siempre que aparezca una `var` dentro de un ámbito, esa declaración se toma para pertenecer a todo el ámbito y es accesible en todas partes.

Metafóricamente, este comportamiento se denomina *hoisting*, cuando una declaración `var` es conceptualmente "movida" a la parte superior de su ámbito de inclusión.

Considera:

```js
var a = 2;

foo();    // works because `foo()`
          // declaration is "hoisted"

function foo() {
	a = 3;

	console.log( a );	// 3

	var a;                  // declaration is "hoisted"
                                // to the top of `foo()`
}

console.log( a );	        // 2
```

#### Nested Scopes

Cuando declara una variable, ella estará disponible en cualquier parte de ese ámbito, así como en cualquier ámbito inferior/interno. Por ejemplo:

```js
function foo() {
	var a = 1;

	function bar() {
		var b = 2;

		function baz() {
			var c = 3;

			console.log( a, b, c );	// 1 2 3
		}

		baz();
		console.log( a, b );		// 1 2
	}

	bar();
	console.log( a );                       // 1
}

foo();
```

Además de crear declaraciones para variables en el nivel de función, ES6 te permite declarar que las variables pertenecen a bloques individuales (pares de `{ .. }`), usando la palabra clave `let`. Además de algunos detalles matizados, las reglas de alcance se comportarán aproximadamente iguales a las que acabamos de ver con funciones:

```js
function foo() {
	var a = 1;

	if (a >= 1) {
		let b = 2;

		while (b < 5) {
			let c = b * 2;
			b++;

			console.log( a + c );
		}
	}
}

foo();
// 5 7 9
```

## Strict Mode

ES5 agregó un "modo estricto" al lenguaje, que fuerza las reglas para ciertos comportamientos. Generalmente, estas restricciones se consideran como mantener el código a un conjunto de directrices más seguro y más apropiado. Además, la adhesión al modo estricto hace que su código en general sea más optimizable por el motor. El modo estricto es un gran triunfo para el código, y deberías usarlo para todos tus programas.

Puedes optar por el modo estricto para una función individual, o un archivo entero, dependiendo de donde se puso el modo estricto:

```js
function foo() {
	"use strict";

	// this code is strict mode

	function bar() {
		// this code is strict mode
	}
}

// this code is NOT strict mode
```

Compara esto con:

```js
"use strict";

function foo() {
	// this code is strict mode

	function bar() {
		// this code is strict mode
	}
}

// this code is strict mode
```

Una diferencia clave (¡mejora!) con el modo estricto es rechazar la declaración implícita de variables globales automáticas al omitir la variable:

```js
function foo() {
	"use strict";	// turn on strict mode
	a = 1;          // `var` missing, ReferenceError
}

foo();
```

## Functions As Values

Hasta ahora, hemos discutido las funciones como el principal mecanismo de scope en JavaScript. Puedes recordar la sintaxis típica de la declaración de funciones de la siguiente manera:

```js
function foo() {
	// ..
}
```

Aunque no parezca obvio de esa sintaxis, `foo` es básicamente sólo una variable en el ámbito exterior que incluye una referencia a la función que se está declarando. Es decir, la función en sí es un valor, al igual que sería `42` o `[1,2,3]`.

Esto puede sonar como un concepto extraño al principio, pero piensalo un poco. No sólo puedes pasar un valor (argumento) a una función, sino que *una función en sí puede ser un valor que se asigna a variables*, o se pasa a, o se devuelve a otras funciones.


Como tal, un valor de función debe ser pensado como una expresión, al igual que cualquier otro valor o expresión.

Por ejemplo:

```js
var foo = function() {
	// ..
};
```

### Immediately Invoked Function Expressions (IIFEs)

En el ejemplo anterior, la expresion de función no se ejecutan - podríamos si hubiéramos incluido por ejemplo `foo()` al final.

Hay otra forma de ejecutar una expresión de función, que normalmente se denomina expresión de función inmediatamente invocada (IIFE):

```js
(function IIFE(){
	console.log( "Hello!" );
})();
// "Hello!"
```

Considera las similitudes entre `foo` y `IIFE` aquí:

```js
function foo() { .. }

// `foo` function reference expression,
// then `()` executes it
foo();

// `IIFE` function expression,
// then `()` executes it
(function IIFE(){ .. })();
```

### Closure

El *Closure* es uno de los conceptos más importantes, ya menudo menos comprendidos, en JavaScript

Puede pensar en el closure como una forma de "recordar" y seguir accediendo al ámbito de una función (y sus variables) incluso una vez que la función ha terminado de ejecutarse.


Considera:

```js
function makeAdder(x) {
	// parameter `x` is an inner variable

	// inner function `add()` uses `x`, so
	// it has a "closure" over it
	function add(y) {
		return y + x;
	};

	return add;
}
```

La referencia a la función interna `add(..)` que se retorna con cada llamada al `makeAdder(..)` externo es capaz de recordar cualquier valor x que se pasó en `makeAdder(..)`. Ahora, vamos a usar `makeAdder(..)`:

```js
// `plusOne` gets a reference to the inner `add(..)`
// function with closure over the `x` parameter of
// the outer `makeAdder(..)`
var plusOne = makeAdder( 1 );

// `plusTen` gets a reference to the inner `add(..)`
// function with closure over the `x` parameter of
// the outer `makeAdder(..)`
var plusTen = makeAdder( 10 );

plusOne( 3 );		// 4  <-- 1 + 3
plusOne( 41 );		// 42 <-- 1 + 41

plusTen( 13 );		// 23 <-- 10 + 13
```

## `this` Identifier

Otro concepto muy comúnmente mal entendido en JavaScript es el identificador `this`

Aunque a menudo parece que `this` está relacionado con "patrones orientados a objetos", en JS este es un mecanismo diferente.


Si una función tiene una referencia `this` dentro de ella, esa referencia `this` normalmente apunta a un `object`. Pero el `object` al que apunta depende de cómo se llamó la función.

Es importante darse cuenta de que `this` no se refiere a la función en sí, y ése es el error más común.

Here's a quick illustration:

```js
function foo() {
	console.log( this.bar );
}

var bar = "global";

var obj1 = {
	bar: "obj1",
	foo: foo
};

var obj2 = {
	bar: "obj2"
};

// --------

foo();				// "global"
obj1.foo();			// "obj1"
foo.call( obj2 );		// "obj2"
new foo();			// undefined
```

## Prototypes

El mecanismo prototype en JavaScript es bastante complicado.

Cuando hace referencia a una propiedad en un objeto, si esa propiedad no existe, JavaScript utilizará automáticamente la referencia de prototipo interno de ese objeto para buscar otro objeto en el que buscar la propiedad. Se podría pensar en esto casi como un `fallback` si la propiedad está desaparecida.


La forma más sencilla de ilustrarlo es con una utilidad incorporada llamada `Object.create(..)`.

Considera:

```js
var foo = {
	a: 42
};

// create `bar` and link it to `foo`
var bar = Object.create( foo );

bar.b = "hello world";

bar.b;		// "hello world"
bar.a;		// 42 <-- delegated to `foo`
```
