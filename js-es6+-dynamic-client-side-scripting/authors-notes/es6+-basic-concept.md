# ES6+ Basic Concept

## `var` vs `let` vs `const`

ES6+ has a total of **6 ways** to declare variables.

ES5 has only **two ways** to declare variables:

* The `var` command&#x20;
* The `function` command.

ES6+ has added four more declare variables:

* the `let` and `const` commands
* the module command
  *   `import`

      ```javascript
      import moduleName from 'module'
      import { originalName as alias } from 'module'
      ```
  *   `export`

      ```javascript
      export default moduleName
      ```
* the `class` command

## Deconstructing

### Explanation

In essence, this writing belongs to "pattern matching". \
As long as the pattern on both sides of the equal sign is the same, the variable on the left will be assigned a corresponding value.

### Usage

```javascript
// 1. switch value;
let x = 1;
let y = 2;

[x, y] = [y, x];
```

```javascript
// 2. Return multiple values
	
	// return an array
	function example() {
		return [1, 2, 3];
	}
	let [a, b, c] = example();
	
	// return an object
	function example() {
		return {
			foo: 1,
			bar: 2
		};
	}
	
	let { foo, bar } = example();
```

```javascript
// 3. Extract JSON data
let jsonData = {
	id     : 42,
	status : "OK",
	data   : [867, 5309]
};

let { id, status, data: number } = jsonData;
console.log(id, status, number); // 42, "OK", [867, 5309]
```

```javascript
// 4. Iterate `Map` structure
const map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
	console.log(key + " is " + value);
}
```

## Rest + Spread

### Basic Syntax

```javascript
console.log(...[1, 2, 3])
// 1 2 3

console.log(1, ...[2, 3, 4], 5)
// 1 2 3 4 5

console.log(1, ...[2, 3, 4], 5, ...)
// error
```

### Usage&#x9;

```javascript
	// 1. Find out the maximum number
	// ES5:
	Math.max.apply(null, [14, 3, 77])
	// ES6:
	Math.max(...[14, 3, 77])
	// same to
	Math.max(14, 3, 77);
```

```javascript

	// 2. Combine two array
	// ES5:
	var arr1 = [0, 1, 2];
	var arr2 = [3, 4, 5];
	Array.prototype.push.apply(arr1, arr2);
	// ES6:
	let arr1 = [0, 1, 2];
	let arr2 = [3, 4, 5];
	arr1.push(...arr2);
```

## Function Syntactic Sugar

### Default parameter value

```javascript
function log({x, y = 'World'}) {
    console.log(x, y);
}

log({x: 'hello'})
```

### Rest parameters

```javascript
function _push(...values) {
	let arr = [...values];
	return arr;
}

_push(2, 5, 3) // [2, 5, 3]
```

### Arrow function

```javascript
// e.q.
var a = b => b
// same as
var a = function (b) {
	return b;
}
```

### Usage

```javascript
// Sort number in ascend
var array = [2, 4, 5, 22, 1, 8,10, 6, 44, 7, 3, 9, 11, 33];
const arr = [...array].map(temp => parseInt(temp, 10)).sort((a, b) => a - b);
console.log(arr);

// Think:
		// sort() vs sort((a, b) => a - b)
		// immutable
```

```javascript
// Sort array in element's length.
function mode(arr) {
		return arr.sort((a, b) => a.length - b.length));
}
		
mode(["pen" ,"apple" ,"pen" ,"pineapple" ,"apple pen" ,"pineapple pen" ,"pen pineapple apple pen"])
```

```javascript
// Get the element with the highest occurrence in an array
function mode(arr) {
	return arr.sort((a, b) => arr.filter(v => v === a).length - arr.filter(v => v === b).length).pop();
}

mode(["apple", "pen", "pineapple", "apple", "pen", "pineapple", "pen", "pen pineapple", "apple pen"]) //?	
```

## New `Math` + `Number` + `String` + `Object` + `Array` APIs

```javascript
// Some of the classic samples
Number.EPSILON // check object is finite or not.
Number.isInteger(Infinity) // false
Number.isNaN("NaN") // false

Math.acosh(3) // 1.762747174039086
Math.hypot(3, 4) // 5
Math.imul(Math.pow(2, 32) - 1, Math.pow(2, 32) - 2) // 2

"abcde".includes("cd") // true
"abc".repeat(3) // "abcabcabc"

Object.assign(Point, { origin: new Point(0,0) })

Array.from(document.querySelectorAll('*')) // Returns a real Array
Array.of(1, 2, 3) // Similar to new Array(...), but without special one-arg behavior
[0, 0, 0].fill(7, 1) // [0,7,7]
[1, 2, 3].find(x => x == 3) // 3
[1, 2, 3].findIndex(x => x == 2) // 1
[1, 2, 3, 4, 5].copyWithin(3, 0) // [1, 2, 3, 1, 2]
["a", "b", "c"].entries() // iterator [0, "a"], [1,"b"], [2,"c"]
["a", "b", "c"].keys() // iterator 0, 1, 2
["a", "b", "c"].values() // iterator "a", "b", "c"
```

## iterators: `for of`

### Basic theory of an iterators

```javascript
// Using a pure function
function makeIterator(array) {
	let nextIndex = 0;
	return {
		next: function() {
			return nextIndex < array.length ? {
				value: array[nextIndex++],
				done: false
			} : {
				value: undefined,
				done: true
			};
		}
	};
}

let it = makeIterator(['a', 'b']);

it.next() // { value: "a", done: false }
it.next() // { value: "b", done: false }
it.next() // { value: undefined, done: true }
```

&#x20;The data structure of the **Iterator interface** is as follows:

* Array
* String
* Symbol
* Map / Set
* TypedArray
* Function's arguments object
* NodeList object

```javascript
// basic theory of an iterators, using iterator interface
const obj = {
	[Symbol.iterator]: function() {
		return {
			next: function() {
				return {
					value: null,
					done: true
				};
			}
		};
	}
};

// e.q.
let arr = ['a', 'b', 'c'];
let iter = arr[Symbol.iterator]();

iter.next() // { value: 'a', done: false }
iter.next() // { value: 'b', done: false }
iter.next() // { value: 'c', done: false }
iter.next() // { value: undefined, done: true}
```

## Symbol

### Explanation

* A new primitive type
* A mechanism to ensure that the name of each attribute is unique, so that the conflict of attribute names is fundamentally prevented.

### Basic Syntax

```javascript
		let s1 = Symbol();
		let s2 = Symbol();

		s1 === s2 // false

		let s1 = Symbol.for();
		let s2 = Symbol.for();

		s1 === s2 // true

		let t1 = Symbol.for("foo");
		Symbol.keyFor(t1) // "foo"

		let t2 = Symbol("foo");
		Symbol.keyFor(t2) // undefined
```

## Set and Map

### Set Explanation

* Object member's values are unique
* Set. It is a constructor itself, used to generate "Set" data structure`Set.prototype.constructor`

### Usage

```javascript
// e.q.
// The Set function can accept an array (or other data structure with an iterable interface) as a parameter for initialization.
var arr = [1, 2, 3, 1, 2]; 
var newArr= [...new Set(arr)]; // [1, 2, 3]
```

### Map Explanation

* JavaScript objects are essentially collections of key-value pairs (Hash structures). \
  `'key' ==> data[element] = 'metadata'`
*   But traditionally only strings can be used as keys. This puts a lot of restrictions on its use.

    `'key' : value`

### Basic Syntax

```javascript
	const m = new Map();
	const o = {
		p: 'Hello World'
	};

	m.set(o, 'content')
	m.get(o) // "content"
```

### Usage

```javascript
	// Merge the following two array and The output should be
	// [
	//   { id: 1, name: "David", position: null },
	//   { id: 2, name: "John", position: "Leader" },
	//   { id: 3, name: "Matt", position: "Captain" },
	//   { id: 4, name: "Greg", position: "VP" },
	//   { id: 5, name: null, position: "Pawn" },
	//   { id: 6, name: null, position: "Rogue" }
	// ];

	const a = [{id: 3,name: "Matt"}, {id: 4,name: "Greg"}, {id: 1,name: "David"}, {id: 2,name: "John"}];
	const b = [{id: 2,position: "Leader"}, {id: 3,position: "Captain"}, {id: 6,position: "Rogue"}, {id: 4,position: "VP"}, {id: 5,position: "Pawn"}];

	const _hash = new Map();
	const c = [...a, ...b];
	c.map(obj => {
		_hash.set(obj.id, {
			position: null,
			name: null,
			..._hash.get(obj.id),
			...obj
		});
	});
	const result = Array.from(_hash.values()); // Iteration operation value keys entries ...

```

## Class

### `static`

The class is equivalent to the prototype of the instance, and all methods defined in the class will be inherited by the instance. If you add the static keyword in front of a method, it means that the method will not be inherited by the instance, but called directly through the class, which is called "static method".

```javascript
class Foo {
  static classMethod() {
    return 'hello';
  }
}
Foo.classMethod() // 'hello'
let foo = new Foo();
foo.classMethod()
// TypeError: foo.classMethod is not a function
```

### `extends`&#x20;

Class can be inherited through the extends keyword, which is much clearer and more convenient than ES5's inheritance by modifying the prototype chain.

### `super`

The keyword super can be used both as a function and as an object. In both cases, its usage is completely different.

In the first case, when super is called as a function, it represents the constructor of the parent class. ES6 requires that the constructor of the subclass must execute the super function once. Equivalent to calling the parent method.

In the second case, when super is an object, in the ordinary method, it points to the prototype object of the parent class; in the static method, it points to the parent class.

It should be noted here that because super points to the prototype object of the parent class, the methods or properties defined on the instance of the parent class cannot be called by super.

```javascript
class Parent {
  constructor() {
    console.log(new.target.name);  
  }
  func() {
    return 2;
  }
}
class Child extends Parent {
  constructor() {
    super(); // First case
    console.log(super.func()); // Second case
  }
}
new Parent() // Parent
new Child() // Child
```

### Inheritance of native constructor&#x20;

Native constructor refers to the built-in constructor of the language, usually used to generate data structures. ECMAScript's native constructors are roughly the following.

* `Boolean()`&#x20;
* `Number()`&#x20;
* `String()`&#x20;
* `Array()`&#x20;
* `Date()`&#x20;
* `Function()`&#x20;
* `RegExp()`&#x20;
* `Error()`&#x20;
* `Object()`

## Promise

{% content-ref url="promise.md" %}
[promise.md](promise.md)
{% endcontent-ref %}

## Generator

### Explanation

* Syntactically
  * The Generator function is a state machine that encapsulates multiple internal states.
  * Executing the Generator function returns an Iteration object.
* Formally
  * The Generator function is a normal function, but has two characteristics.
  * First, there is an asterisk between the function keyword and the function name.
  * Second, the yield expression is used inside the function body to define different internal states (yield means "output" in English).

```javascript
// aka, Pausable Function
function* f() {
	yield console.log("I'm a generator function."); 
	yield console.log("The Generator function is a state machine.");
	yield console.log("Executing the Generator function returns a Iteration object.");
	yield console.log("The Generator function is a normal function, but has two characteristics.");
	// return undefined;
}

// Used as create an iterator
const run_f = f();
run_f.next();
```
