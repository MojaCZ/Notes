# JAVASCRIPT

## Versions
ES5 (ECMAScript 5)
ES6 (2015)
ES2016
ES2017

# Table of Contents
1. [VARIABLES](#VARIABLES)
	1. [Types](#Types)
	1. [Typeof](#Typeof)
	1. [Variable Typing](#Variable-Typing)
	* [var let constant](#var-vs-let-vs-constant)
	* [two basic groups of datatypes](#two-basic-groups-of-datatypes)
1. [ERRORS](#ERRORS)
1. [FUNCTIONS](#FUNCTIONS)
	1. [Function Declaration vs Function Expression](#Function-Declaration-vs-Function-Expression)
	1. [Bind](#Bind)
	1. [IIFE](#IIFE)
	1. [Timers](#Timers)
	1. [Anonimous Function](#Anonimous-Function)
1. [SCOPE](#SCOPE)
	1. [Global Scope](#Global-Scope)
	1. [Hoisting](#Hoisting)
1. [UNDEFINED](#UNDEFINED)
	1. [Checking for Undefined](#Checking-for-Undefined)
1. [NULL](#NULL)
1. [OPERATORS](#OPERATORS)
	1. [Logical Operators](#Logical-Operators)
	1. [Conditional Operators](#Conditional-Operators)
1. [ARRAYS](#ARRAYS)
	1. [Spread Operator](#Spread-Operator)
1. [OBJECTS](#OBJECTS)
	1. [Generic Objects](#Generic-Objects)
	1. [Delete](#Delete)
	1. [Prototypal Inheritance](#Prototypal-Inheritance)
1. [CLOSURE](#CLOSURE)
1. [EXCEPTIONS](#EXCEPTIONS)
1. [SCREEN OBJECTS](#SCREEN-OBJECTS)
1. [PROMISES and DEFFERED](#PROMISES-and-DEFFERED)
1. [DOCUMENT MANIPULATION](#DOCUMENT-MANIPULATION)
	1. [Adding new Element Dynamically](#Adding-new-Element-Dynamically)
	1. [Style of Elements](#Style-of-Elements)
	1. [Submit a Form](#Submit-a-Form)
1. [SINGLE QUESTIONS](#SINGLE-QUESTIONS)

_________

## VARIABLES
### Types
All variables in the JS are **object data types**.
* string
* number
* boolean
* undefined (undefined)
* object	(also a null is an object)
* function

### Typeof
`typeof(variable)` will return a **string description** of the type of a variable.

`typeof(typeof(1))` will return `typeof("number")` and it is string.

### Variable Typing
same variable can be assigned to a number and a string
```js
a = 10;
a = 'string';
```
### var vs let vs constant
a = "hello" -> this is global variable, the keyword is omitted

### two basic groups of datatypes
* primitive: number and boolean
* reference types: complex types like strings, dates, ...
___

## PROTOTYPES
When I create a object directly, The object have created methods directly inside itself, they are not passed by `__proto__`. (I attached methods directly inside object constructor)

When I create a object a Generic way `class SomeClass{}`, any time I create new object `var C = new SomeClass();` the methods defined in the class block will be passed to created object by `__proto__`

Objects inherit properties and methods from a prototype. If I create a new array, this variable will inherit methods and properties of Array class `Array.properties`, and store them in prototype `__proto__` of a variable.

```js
let A = []	// this will create a new object inherited from Array
console.log(Array.prototype)
console.log(A.__proto__)		// __proto__ is object of type Array
```

I can also see all the properties and methods of a globe object window `console.log(this)`.

To use prototypes I don't have to type them, for example, the method of Array is `slice()` to use this method of prototype, I'll type `A.slice(2,3)`, not `A.__proto__.slice(2,3)`
___
## STRINGS
Properties:
* **constructor**
* **length**

Methods:
* **charAt** `.charAt(index)` Returns the character at the specified index
* **charCodeAt** `.prototype.charCodeAt(index)` Returns a number (UTF-16) code unit value at the given index
* **codePointAt** `.codePointAt(pos)` Returns a nonnegative integer Number that is the code point value of the UTF-16.
* **concat** `.concat(str [, ...strN ])` Combines the text of two (or more) strings and returns a new string.
* **includes** `.includes(searchString [, position])` Determines whether the calling string contains searchString.
* **endsWith** `.endsWith(searchString [, length])` Determines whether a string ends with the characters of the string searchString.
* **indexOf** `.indexOf(searchValue [, fromIndex])` Returns the index of the first occurrence of searchValue, or -1 if not found
* **lastIndexOf** `.lastIndexOf(searchValue [, fromIndex])` Returns the index of the last occurrence of searchValue, or -1 if not found.
* **localeCompare** `.localeCompare(compareString [, locales [, options]])` Returns a number indicating whether the reference string compareString comes before, after, or is equivalent to the given string in sort order.
* **match** `.match(regexp)` Used to match regular expression regexp against a string.
* **matchAll** `.matchAll(regexp)` Returns an iterator of all regexp's matches.
* **normalize** `.normalize([form])` Returns the Unicode Normalization Form of the calling string value.
* **padEnd** `.padEnd(targetLength [, padString])` Pads the current string from the end with a given string and returns a new string of the length targetLength.
* **padStart** `.padStart(targetLength [, padString])` Pads the current string from the start with a given string and returns a new string of the length targetLength.
* **repeat** `.repeat(count)`
* **replace** `.replace(searchFor, replaceWith)` Used to replace occurrences of searchFor using replaceWith. searchFor may be a string or Regular Expression, and replaceWith may be a string or function.
* **search** `.search(regexp)` Search for a match between a regular expression regexp and the calling string.
* **slice** `.slice(beginIndex[, endIndex])` Extracts a section of a string and returns a new string.
* **split** `.split([sep [, limit] ])` Returns an array of strings populated by splitting the calling string at occurences of the substring sep.
* **startsWith** `.startsWith(searchString [, length])` Determines whether the calling string begins with the characters of string searchString.
* **substr** `.substr()` Returns the characters in a string beginning at the specified location through the specified number of characters.
* **substring** `.substring(indexStart [, indexEnd])` Returns a new string containing characters of the calling string from (or between) the specified index (or indeces).
* **toLowerCase** Returns the calling string value converted to lowercase
* **toUpperCase** Returns the calling string value converted to uppercase
* **toSource** Returns an object literal representing the specified object; you can use this value to create a new object.
* **toString** Returns a string representing the specified object. Overrides the Object.prototype.toString() method
* **trim** Trims whitespace from the beginning and end of the string. Part of the ECMAScript 5 standard
* **trimStart** **trimLeft** Trims whitespace from the beginning of the string
* **trimEnd** **trimRight** Trims whitespace from the end of the string
* **valueOf** `.valueOf()` Returns the primitive value of the specified object.
___
## ERRORS
* **Load time errors**: Errors which come up when loading a web page like improper syntax errors. Are detected while in the page is getting loaded.
	* Uncaught SyntaxError: Invalid shorthand property initializer `var person = {name: "Lukas", age="30", city: "Kladno"}` age = 30 should be age:30
* **Run time errors**: Errors that come due to misused of the command inside the HTML language. Can be caused by illegal operation s, for example. division of a number by zero or trying to access a non-existent are of the memory.
* **Logical Errors**: errors that occur due to the bad logic performed on a function which is having different operation.

Error Objects:
* Error
* AggregateError
* EvalError
* IntervalError
* RangeError
* ReferenceError
* SyntaxError
* TypeError
* URIError
___
## FUNCTIONS
**ALL functions are object methods**. If not of a JavaScript object, then of the global object.

### Function Declaration vs Function Expression
If I want to pass function to another function, **I have to use function expression**

I can call function declaration before it is created, I cannot call function expression before it is assigned

```js
console.log(funcD())	// function declaration
console.log(funcE())	// ReferenceError: Cannot access 'funcE' before initialization
func funcD(){
	console.log("function declaration");
}
let funcE = function(){
	console.log("function expression");
}
```

### Arrow Function Expression
Is syntactically compact alternative to a regular function expression
```js
let func1 = () => return "HELLO";
let func2 = (val1, val2) => {
	str = "hello " + val1 + val2;
	return str;
}
```

`this` is not binded with arrow function.

Regular function - The The this keyword represents the object that **called** the function.

Arrow function - The this keyword represents the object that **defined** the function.

```js
Array.prototype.printThis = () => {
	console.log(this)		
}
Array.prototype.printThis = function() {
	console.log(this)		
}
Arr = [1, 2, 3]
Arr.printThis1() // global scope (window)
Arr.printThis2()	// the object that called it
```

### Arguments object
Is an Array-like object accessable inside functions that contains values of argument passed to the function.
```js
function func1(a, b) {
  console.log(arguments[0]); // expected output: 1
  console.log(arguments[1]); // expected output: 2
}
func1(1, 2);
```

Properties:
* **argument.callee** Reference to the currently executing function that the arguments belong to.
* **argument.caller** Reference to the function that invoked the currently executing function.
* **argument.length**
* **argument[@@iterator]** Returns a new Array iterator object that contains the values for each index in arguments.


### Function prototype object
Properties:
* **arguments** `Function.prototype.arguments` An array corresponding to the arguments passed to a function.
This is deprecated as a property of Function. Use the arguments object (available within the function) instead.
* **caller** `Function.prototype.caller` Specifies the function that invoked the currently executing function.
This property is deprecated, and is only functional for some non-strict functions.
* **length** `Function.prototype.length` Specifies the number of arguments expected by the function.
* **name** `Function.prototype.name` The name of the function.
* **displayName** `Function.displayName` The display name of the function.
* **constructor** `Function.prototype.constructor` Specifies the function that creates an object's prototype.

Methods:
* **apply** `Function.prototype.apply(thisArg [, argsArray])` Calls a function and sets its this to the provided thisArg. Arguments can be passed as an Array object.
* **bind** `Function.prototype.bind(thisArg[, arg1[, arg2[, ...argN]]])` Creates a new function which, when called, has its `this` set to the provided thisArg. Optionally, a given sequence of arguments will be prepended to arguments provided the newly-bound function is called.
* **call** `Function.prototype.call()` Calls a function and sets its `this` to the provided value. Arguments can be passed as they are.
* **toString** `Function.prototype.toString()` Returns a string representing the source code of the function.

### Bind
```js
setTimeout( (function(){
	console.log(this.type);
}).bind(this), 500)

var repeate = setInterval(( function(){
	console.log(this);
}).bind(this), interval);
```
### IIFE
(Immediately invoked function expression):
```js
var foo = function(){
	// this is function expression and I can immediately invoke
}();

( function foo(){} )();
```
if I put statement into brackets, JS will understand it as an expression and I can immediately invoke it

### Timers
* `setTimeout(function, delay)` start function after delay.
* `setInterval(function, delay)` repeatedly execute the given function in delay and is stopped when cancelled.
* `clearInterval(id)` stops interval

setTimeout makes asynchronous call and all asynchronous gets automatically at the end of the stack (execute last)

```js
setTimeout(function(){
	console.log("a")
}, 0);
console.log("b")
console.log("c")
// => 'b' 'c' 'a'
```

### Anonimous Function
Is a function that is declared without any named identifier.\
Anonymous function is inaccessible after its declaration.
```js
var anonym = function() {
	alert("I am anonymous");
};
anonym();
```
___
## SCOPE:
```js
( function foo(){} )();
console.log(foo);	//ReferenceError: foo is not defined
```

### Global Scope
`baz = 5`		-> without var, let or const it goes right to global scope!!! BED PRACTISE

### Hoisting
var - are declared at top of any function scope
functions written as statements as well
const and let - not hoisted and scoped within the block they are in
```js
hoist()
function hoist() {		// this works
	if (true) {
		console.log(action)		// undefined
	} else {
		console.log(action)		// undefined
	}
	var action;
	return action;
}

( function foo(){
	for(let i=0; i<10; i++) {
		console.log(SUM)	// ReferenceError: SUM is not defined
		const SUM = 10
	}
	console.log(i, SUM)	// ReferenceError: SUM is not defined
})()
```
___
## UNDEFINED:
* Variable used in the code doesn't exist
* Variable is not assigned to any value
* property doesn't exist

```js
let bar = {};
let baz = ['lukas', 'petr', 'bara'];
const quz = function() {
	// don't return anything
}
console.log(bar.name, baz[4], quz());	// undefined undefined undefined
```

### Checking for Undefined
**USE === to compare with *undefined***
```js
let foo;
console.log(typeof foo);	// "undefined" as a string
console.log(typeof bar);	// undeclared but also returns "undefined"

console.log(foo === undefined);	// true boolean
```
___
## NULL:
null has a value. Its value is null (nothing)
```js
const foo = null;
console.log(typeof(foo));	// object
console.log(foo === null);	// true boolean
```
___
## OPERATORS:
### Logical Operators
`===` -> strict equality
```js
let foo;
const bar = null;
console.log(foo == bar);	// true
console.log(foo === bar);	// false
```

### Conditional Operators:
`return a>b ? 1 : -1;`

___
## ARRAYS:
`var myArray=[[[]]];` declaration of an three dimensional array
```js
var myArray = ['a', 'b', 'c']
myArray.push("end")					// push to end
myArray.unshift("start")		// add to start
myArray.pop()		// takes the last element off of the array and returns it
myArray.shift() 	// takes the first element off of the array and returns it
myArray[myArray.length] = value;	// this will append a value to the end of array
```

### Spread Operator
`'...'`
applays for arrays and objects
allows an iterable such as an array expression or string to be expanded in places where yero or more arguments (for function calls) or elements (for array literals) are expanded

```js
var myArray = ["one", "two", "three"]
myArray = ["start", ...myArray]
myArray = [...myArray, "end"]
myArray = ["start", ...myArray, "end"]
var newArray = [...array1, ...array2]
```
Static Properties:
* **length**

### Methods
to list them: `console.log(Array.prototype)`

* **from** `.from(arrayLike[, mapFn[, thisArg]])` Creates a new Array instance from arrayLike, an array-like or iterable object.
* **isArray** `alue)` Returns true if value is an array, or false otherwise.
* **of** `.of(element0[, element1[, ...[, elementN]]])` Creates a new Array instance with a variable number of arguments
* **CopyWithin** `.copyWithin(target[, start[, end]])` Copies a sequence of array elements within the array.
* **fill** `.fill(value[, start[, end]])` Fills all the elements of an array from a start index to an end index with a static value.
* **pop** `.pop()` Removes the last element from an array and returns that element.
* **push** `.push(element1[, ...[, elementN]])` Adds one or more elements to the end of an array, and returns the new length of the array.
* **reverse** `.reverse()` Reverses the order of the elements of an array in place.
* **shift** `.shift()` Removes the first element from an array and returns that element.
* **unshift** `.unshift(element1[, ...[, elementN]])` Adds one or more elements to the front of an array, and returns the new length of the array.
* **sort** `.sort()` Sorts the elements of an array in place and returns the array **sorts ALPHABETICALLY** -> `[2, 3, 100].sort() // 100, 2, 3`
* **splice** `.splice(start[, deleteCount[, item1[, item2[, ...]]]])` Adds and/or removes elements from an array.
* **concat** `.concat([value1[, value2[, ...[, valueN]]]])` Returns a new array that is this array joined with other array(s) and/or value(s)
* **filter** `.prototype.filter(callbackFn(element[, index[, array]])[, thisArg])` Returns a new array containing all elements of the calling array for which the provided filtering callbackFn returns true.
* **includes** `.includes(valueToFind[, fromIndex])` Determines whether the array contains valueToFind.
* **indexOf** `.indexOf(searchElement[, fromIndex])` Returns the first (least) index of an element within the array equal to searchElement, or -1 if none is found.
* **join** `.join([separator])` Joins all elements of an array into a string.
* **lastIndexOf** `.lastIndexOf(searchElement[, fromIndex])` Returns the last (greatest) index of an element within the array equal to searchElement, or -1 if none is found.
* **slice** `.slice([begin[, end]])` Extracts a section of the calling array and returns a new array.
* **toString**  `.toString()` Returns a string representing the array and its elements.
* **toLocaleString** `.toLocaleString()` Returns a localized string representing the array and its elements.
* **entries** `.entries()` Returns a new Array Iterator object that contains the key/value pairs for each index in the array.
* **every** `.every(callbackFn(element[, index[, array]])[, thisArg])` Returns true if every element in this array satisfies the testing callbackFn.
* **find** `.find(callbackFn(element[, index[, array]])[, thisArg])` Returns the found element in the array if some element in the array satisfies the testing callbackFn, or undefined if not found.
* **findIndex** `.findIndex(callbackFn(element[, index[, array]])[, thisArg])`
Returns the found index in the array, if an element in the array satisfies the testing callbackFn, or -1 if not found.
* **forEach** `.forEach(callbackFn(currentValue[, index[, array]])[, thisArg])` Calls a callbackFn for each element in the array.
* **keys** `.keys()` Returns a new Array Iterator that contains the keys for each index in the array.
* **map** `.map(callbackFn(currentValue[, index[, array]])[, thisArg])` Returns a new array containing the results of calling callbackFn on every element in this array.
* **reduce** `.reduce(callbackFn(accumulator, currentValue[, index[, array]])[, initialValue])` Apply a callbackFn against an accumulator and each value of the array (from left-to-right) as to reduce it to a single value.
* **reduceRight** `.reduceRight(callbackFn(accumulator, currentValue[, index[, array]])[, initialValue])` Apply a callbackFn against an accumulator and each value of the array (from right-to-left) as to reduce it to a single value.
* **some** `.some(callbackFn(element[, index[, array]])[, thisArg])` Returns true if at least one element in this array satisfies the provided testing callbackFn.
* **values** `.values()` Returns a new Array Iterator object that contains the values for each index in the array.

___
## OBJECTS
assigning objects properties:
```js
obj["class"] = 12;
obj.class = 12;
```

Loop through object properties.
```js
var person = {
		name: "Lukas",
		age: "30",
		city: "Kladno",
		sayHello: function(){console.log("Hello, my name is ", this.name)}
	}

for(val in person) {
	console.log(val)
}
// => name  age  city sayHello
```

### Generic Objects
```js
class ValueObj {
	constructor(value) {
		this.value = value;
	}
	getValue() {
		return this.value
	}
}

var V = new ValueObj();
```

### Delete
delete property and value
```js
var student = {age: 20, name: "Lukas"};
delete student.age;
console.log(student.age)	// undefined
```

### Objects Prototypes
Properties:
* **length**
* **prototype**

Methods:
* **assign** `Object.assign()` Copies the values of all enumerable own properties from one or more source objects to a target object.
* **create** `Object.create()` Creates a new object with the specified prototype object and properties.
* **keys** `Object.keys()` Returns an array containing the names of all of the given object's own enumerable string properties.
* **values** `Object.values()` Returns an array containing the values that correspond to all of a given object's own enumerable string properties.
* **defineProperty** `Object.defineProperty()` Adds the named property described by a given descriptor to an object.
* **defineProperties** `Object.defineProperties()` Adds the named properties described by the given descriptors to an object.
* **entries** `Object.entries()` Returns an array containing all of the [key, value] pairs of a given object's own enumerable string properties.
* **fromEntries** `Object.fromEntries()` Returns a new object from an iterable of [key, value] pairs. (This is the reverse of Object.entries).
* **getPrototypeOf** `Object.getPrototypeOf()` Returns the prototype of the specified object.
* **setPrototypeOf** `Object.setPrototypeOf()` Sets the object's prototype (its internal [[Prototype]] property).
* **is** `Object.is()` Compares if two values are the same value. Equates all NaN values (which differs from both Abstract Equality Comparison and Strict Equality Comparison).
* **isExtensible** `Object.isExtensible()` Determines if extending of an object is allowed.
* **preventExtensions** `Object.preventExtensions()` Prevents any extensions of an object.
* **freeze** `Object.freeze()` Freezes an object. Other code cannot delete or change its properties.
* **isFrozen** `Object.isFrozen()` Determines if an object was frozen.
* **seal** `Object.seal()` Prevents other code from deleting properties of an object.
* **isSealed** `Object.isSealed()` Determines if an object is sealed.


### Prototypal Inheritance
every object has property "prototype".\
Object doesn't copy prototype (variables, methods, ...) of its parent but point to it. When method is called, It tries to find it in self methods and then look to its parent. *=> lighter inheritance*

```js
let car = function(model){
	this.model = model
}
car.prototype.getModel = function(){
	return this.model;
}
let toyota = new car('toyota')
console.log(toyota.getModel())	// toyota
```

## THIS
this reffers to object/function/scope I'm currently in
___
## CLOSURE:
Closure is a locally declared variable related to a function which stays in memory when the function has returned.

```js
function greet(message) {
	console.log(message);
}
function reeter(name, age) {
	return name + " says Hi! He is " + age + " years old";
}

var message = greeter("James", 23);	// generate message
greet(message)	// pass it explicitly to greet
```

the same with using closure

```js
function greeter(name, age){
	var message = name + " says Hi! He is " + age + " years old";
	return function greet() {
		console.log(message);
	}
}
```

```js
var num = 4;		// this gets overwritten by var num = 2
function outer(){
	var num = 2		// this gets overwritten by var num = 3
	function inner(){
		num++;
		var num = 3;		
		console.log(num)	// 3
	}
	inner();
}
outer();
// output will be 3
```

```js
var hero = {
	name: 'John Doe',
	getSecretItentity: function (){
		return this.name;
	}
}
console.log(hero)

var stoleSecretIdentity1 = hero.getSecretIdentity;
var stoleSecretIdentity2 = hero.getSecretIdentity.bind(hero)

console.log(stoleSecretItentity1());	//- undefined
console.log(stoleSecretItentity2());	//- John Doe
console.log(hero.getSecretItentity());	//- John Doe
```

### Deep Clone
```js
const obj = {
	a: {
		b: {
			c: 1
		}
	}
};
```
Use recursive copying

JSON.parse/stringify:
```js
const json.parse(json.stringify(obj))
```

Use libraries:
```js
_.cloneDeep(obj);		// lodash
angular.copy(obj, newObj)	// angular

```

Assign:
```js
var newObj = Object.assign({}, obj)
```

___
## EXCEPTIONS
```js
try {
	// Code
}
catch(exp) {
	// Code to throw an exception
}
finally {
	// Code runs either it finishes successfully or after catch
}
```
___
## JSON
JavaScript Object Notation
```json
{
	"person": {
		"name": "Lukas",
		"school": {
			"highSchool": "Sports Grammar school",
			"university": "CTU",
		},
		"years": 27
	}
}
```

Methods:
* **parse** `JSON.parse(text[, reviver])` Parse the string text as JSON, optionally transform the produced value and its properties, and return the value. Any violations of the JSON syntax, including those pertaining to the differences between JavaScript and JSON, cause a SyntaxError to be thrown. The reviver option allows for interpreting what the replacer has used to stand in for other datatypes.
* **stringify** `JSON.stringify(value[, replacer[, space]])` Return a JSON string corresponding to the specified value, optionally including only certain properties or replacing property values in a user-defined manner. By default, all instances of undefined are replaced with null, and other unsupported native data types are censored. The replacer option allows for specifying other behavior.

___
## SCREEN OBJECTS
Are used to read the information from the client's screen
* AvailHeight: height of client's screen
* AvailWidth: width of client's screen
* ColorDepth: bit depth of images on the client's screen
* Height: total height of the client's screen, including taskbar
* Width: total width of the client's screen, including the taskbar

___
## PROMICSES and DEFFERED
A **deferred object** is an object that can create a promise and change its state to `resolver` or `rejected`. Usually used if writting my own function and want to provide a promise to the calling code.

A **promise** is a promise about future value. I can attach callbacks to it to get the value.
___
## DOCUMENT MANIPULATION
`innerHTML = "text"` replace **whole** content of element with "text"\
innerHTML is not advised to use because the content is refreshed every time and thus is slower. There is also no scope for validation in innerHTML and therefore is easier to insert rouge code in the document and make web unstable\
`document.write("Hello World")` prints the text in the screen\

### Adding new Element Dynamically
```js
var newP = document.createElement("p");
document.getElementById("parentsID").appendChild(newP);

```
### Style of Elements
`element.style.fontSize = "20px"`
`element.className = "anyClass"`

### Submit a Form
`document.form[0].submit()`

## STANDARD BUILT-IN OBJECTS

Value Properties
* **Infinity**
* **NaN**
* **undefined**
* **globalThis**

Function Properties:
* **eval()** The eval() function evaluates JavaScript code represented as a string.
* **uneval()** The uneval() function creates a string representation of the source code of an Object.
* **isFinite()** The global isFinite() function determines whether the passed value is a finite number. If  needed, the parameter is first converted to a number.
* **isNaN()** The isNaN() function determines whether a value is NaN or not. Note, coercion inside the isNaN function has interesting rules; you may alternatively want to use Number.isNaN(), as defined in ECMAScript 2015.
* **parseFloat()** The parseFloat() function parses an argument (converting it to a string first if needed) and returns a floating point number
* **parseInt()** The parseInt() function parses a string argument and returns an integer of the specified radix (the base in mathematical numeral systems)
* **decodeURI()** The decodeURI() function decodes a Uniform Resource Identifier (URI) previously created by encodeURI() or by a similar routine
* **decodeURIComponent()** The decodeURIComponent() function decodes a Uniform Resource Identifier (URI) component previously created by encodeURIComponent or by a similar routine
* **encodeURI()** The encodeURI() function encodes a URI by replacing each instance of certain characters by one, two, three, or four escape sequences representing the UTF-8 encoding of the character (will only be four escape sequences for characters composed of two "surrogate" characters)
* **encodeURIComponent()** The encodeURIComponent() function encodes a URI by replacing each instance of certain characters by one, two, three, or four escape sequences representing the UTF-8 encoding of the character (will only be four escape sequences for characters composed of two "surrogate" characters)
* deprecated:
	* **escape()**
	* **unescape()**

Fundamental Objects:
* **Object**
* **Function**
* **Boolean**
* **Symbol**

Error Objects: [ERRORS](#ERRORS)

Other: Number, BigInt, Math, Date, String, RegExp, Array, Int8Array, Unit8Array, Unit8ClampedArray, Int16Array, ..., Map, Set, WeakMap, WeakSet, ArrayBuffer, SharedArrayBuffer, Atomic, DataView, JSON, Promise, Generator, GeneratorFunction, AsyncFunction, Iterator, AsyncIterator, Reflect, Proxy, Internationalization, WebAssembly

___
## TEMPLATE LITERALS
Are string literals allowing embedded expressions.
```js
var hi = "HELLO"
var a = 5, b = 10;
var S = `this string can be multi line
		and can have expressions: ${hi} inside`
var add = `this is an addition ${a + b} will add a + b and convert to string`
```

## COOKIES
Create: `document.cookie = "name=Lukas";` here a new Cookie is a string in form key=value
Create with expiration: `document.cookie = "username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC";`
Delete: set expiration to past time
Get cookie: `allCookies = document.cookie;`	to get all cookies from this location
___
## SINGLE QUESTIONS
**convert string of any base to int:** `parseInt("4F", 16); 	// => 79`

**result of `3 + 5 + "7"`:**  `= 57`

**Detect operating system of client**
	* `navigator.platform		// => "Win32"`
	* `navigator.appVersion`
**popup boxes:** `Alert`, `Confirm`, `Prompt`

**how to get status of a CheckBox?** `doument.getElementById('myCheckbox').checked`
`Void(0)`: used to call another method without refreshing the page

**load another page:** `location.href="..."`

**positive vs negative infinity:** `5/0 = Infinity` `-5/0 = -Infinity`

**what is `isNaN()`?** determines if value is an illegal number (Not-a-Number):
* isNan(123) -> flase
* isNan('123') -> false
* isNan('') -> true
* isNan(undefined) -> true

**what does `this` means?:** it refers to the object from where it was called

**does JS support automatic type conversions?** YES

**View State vs Session State:**
* View state is specific to a page in a session
* Session state: data can be accessed across all pages in the web application

**what is the use of `Void(0)`?:**
* it prevents page from refreshing and parameter 0 is passed while calling
* is used to call another method without refreshing the page

**how to force a page to load another page in JavaScript?**
```html
<script language="JavaScript" type="text/javascript">
	location.href="http://..."
</script>
```

**role of `break`:** used to come out of the current loop

**role of `continue`:** continues the current loop with a new recurrence

**what boolean operators can be used in JavaScript?** and `&&`, or `||`, not `!`

**is JS case sensitive?** YES

**hide JS code from old browserso that doesn't support JavaScript?:** <!-- --> old browsers will recognize multiple line comments, newer browsers with JS will be compiled.

**strict mode:** adds certain compulsions to JS, show different errors, can solve some mistakes with engines, ... `"use strict;"`

**what is event bubbling?:** DOM elements are nested inside each other. If the handler of the child is clicked, the handler of parent will also work as if it were clicked too.

**What is the use of blur function?:** Blur function is used to remove focus from the specific object

**window.onload:** function is not run until all the information on the page is loaded.

**onDocumentReady:** loads the code just after the DOM is loaded.

**what is DOM?:** Document Object Model, It represents the page and is an object-oriented representation. For HTML and XML.

**`escape()` function:** code a string to make the reansfer of the information from one computer to the other across a network. `escape("Hello? How are you!")	// -> Hello%3F%20How%20are%20you%21`

**`unescape()` function:** decodes the coded string. `unescape("Hello%3F%20How%20are%20you%21") // -> Hello? How are you!`

**namespacing:** is used for grouping the desired functions, variables etc. under a unique name and thus improve modularity in the coding and enables code reuse.

**what is target?:** is thing I clicked in

**what is currentTarget?:** is thing that was event listener attached to

**simple addition of two arrays?:** will convert them into string `[1, 2, 3] + [6, 8, 9] = "1,2,36,8,9"`

**sort an array:**
```js
var arr = [2, 3, 100, 11]
arr.sort() // 100, 11, 2, 3
arr.sort((a, b) => a - b);	// ascending sort
arr.sort((a, b) => b - a); 	// descending sort
```
