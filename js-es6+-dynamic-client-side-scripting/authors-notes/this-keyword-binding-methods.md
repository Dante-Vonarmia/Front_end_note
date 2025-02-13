# "this" keyword Binding Methods

## Context — Implicit Binding

Called as a method of an object.

### Basic Example - passing a function

```javascript
function func() {
	return this;
}

func() // window object

var obj = {
	method: func
};

obj.method() === obj // true
obj.method() === window // false
```

### Basic Example - plain object

```javascript
var obj = {
	a: 1,
	getA: function() {
		console.log(this === obj); // Output: true 
		console.log(this.a); // Output: 1
	}
};
obj.getA();
```

## New Binding

Whereas if we do new `foo()` at the global level then will get this as `foo {}` object.

### Basic Example - `new` keyword

```javascript
// Constructor call
function foo() {
	console.log(this);
}

foo() // window object

new foo() // foo {}
```

### Explanation: `new` keyword

#### `new`:&#x20;

* Creates a blank, plain JavaScript object;&#x20;
* Links (sets the constructor of) this object to another object;&#x20;
* Passes the newly created object from Step 1 as the this context;&#x20;
* Returns this if the function doesn't return its own object.

#### constructor:

* A class or function that specifies the type of the object instance.&#x20;
* A constructor enables you to provide any custom initialization that must be done before any other methods can be called on an instantiated object.

#### arguments :

* A list of values that the constructor will be called with.

### Prototype Example

```javascript
var MyClass = function() {
	this.name = 'dva89';
	/* or */
	return { // Return an object explicitly
		name: 'dva89'
	}
};

var _obj = new MyClass(); // MyClass { name: 'dva89' }
```

### Proto method 1: `Object.prototype.constructor`

* The `constructor` property returns a reference to the `Object` constructor function that created the instance object.
* Note that the value of this property is a reference to the function itself, not a string containing the function's name.
* The value is only read-only for primitive values.

```javascript
var MyClass = function() { // MyClass {}
	this.name = 'dva89';
};

MyClass.prototype.age = function(a) { // MyClass { name: 'dva89' }
	return a;
};

var _obj = new MyClass(); // (factory pattern)

Object.prototype.toString.call(_obj) // [object object]

_obj.name; // dva89
_obj.age(30); // 30
typeof new MyClass(); // object
new MyClass().age(30); // 30
```

#### `proto` vs prototype

```javascript
// (continue previous example)
_obj // MyClass { name: 'dva89' }
_obj.__proto__ // // MyClass { age: [λ] }
```

### Proto Method 2:  `object`

```javascript
var MyClass2 = {
	name: function() {
		return this.name = 'dva89'
	}
};

MyClass2.age = function(a) {
	return a
};

MyClass2 // ​​​​​{ name: [λ: name], age: [λ] }​​​​​
MyClass2.__proto__ // {}
```

### Proto method 3: `Object.setPrototypeOf()`

```javascript
var country = {
	region: 'China'
}

Object.setPrototypeOf(MyClass2, country)
MyClass2.region // China


var _obj2 = Object.create(MyClass2)
 
_obj2.name() // dva89
_obj2.age(30) // 30
_obj2.region // China

_obj2 // { name: 'dva89' }
_obj2.__proto__ // ​​​​​{ name: [λ: name], age: [λ] }​​​​​
_obj2.__proto__.__proto__ // { region: 'China' }
```

### `Object.create()` vs `new`？

This is due to the important difference that `new` actually runs constructor code, whereas `Object.create` will not execute the constructor code.

## Explicit Binding

Called as a normal function.

### `call` vs `apply`

Different forms of the passed parameters

```javascript
// Function.prototype.call(thisArg: any, args...: any)
```

```javascript
// Function.prototype.apply(thisArg: any, argArray: Array)
```

#### Built-in, Basic Example:

```javascript
const max = Math.max.apply(null, [5, 6, 2, 3, 7]); // 7

const min = Math.min.call(null, 5, 6, 2, 3, 7); // 2

typeof Math.max // function
typeof Math.min // function
```

### Usage: Change `this` status

```javascript
var obj1 = {
	thyName: 'Adam'
}

var obj2 = {
	thyName: 'Eve'
}

var name = 'window';

var getName = function() {
	console.log(this) // window object
	console.log(this.name) // [empty string]
}

getName();

// Introduce new debug method `in` and `hasOwnProperty`
'thyName' in obj1 // true | { thyName: 'Adam' }
obj1.hasOwnProperty('thyName') // true
getName.hasOwnProperty('thyName') // false

// Change `this` status now.
getName.hasOwnProperty.call(obj1,'thyName') // true
```

### Using `bind` to fix "Leaked `this`" problem

Borrow object method (one of Composition concept)

```javascript
var myObject = {
	name: 'DVA89',
	getName: function() {
		return this.name;
	}
};

var _getName = myObject.getName;
_getName() // [empty string]
_getName.bind(myObject)() // DVA89
```

### Composition Over Inheritance

* More flexible, reusable in coding structure for the future
* Won't leak prototype method

## Lexical Binding

Closure is a classic Lexical Scope sample

```javascript
// Let's us "Encapsulation" a "private variable"

// variable img's scope and lifetime is inside of function block
var report = function(src) {
  var img = new Image();
  img.src = src;
};

report('https://www.google.co.jp/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png') //?

// Through return an anonymous function, aka HOF, 
// we could create a API and it will expend the scope and lifetime of the `img`,
// so we could access to it outside of the function block
var reportPrivate = (function() {
  var imgs = [];
  return function(src) {
    var img = new Image();
    img.src = src;
    imgs.push(img.src);
    return imgs;
  }
})();

reportPrivate('../pic1.jpg')
//​​​​​ [ 'http://localhost/pic1.jpg' ]​​​​​

reportPrivate('../pic2.jpg') 
// ​​​​​[ 'http://localhost/pic1.jpg', 'http://localhost/pic2.jpg' ]​​​​​

reportPrivate('../pic3.jpg')
/*
[ 'http://localhost/pic1.jpg',​​​​​ 
  'http://localhost/pic2.jpg',​​​​​ 
  'http://localhost/pic3.jpg' ]​​​​​
/*
```
