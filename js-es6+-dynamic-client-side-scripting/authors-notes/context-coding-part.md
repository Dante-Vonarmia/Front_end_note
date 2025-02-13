# Context Coding Part

## Context - Definition

Context is always the value of the `this` keyword which is a reference to the object that “owns” the currently executing code or the function where it’s looked at.

### Global

```javascript
this
this === window // true

// Inside a function
function foo() {
	// foo is the function is defined at the global level 
	// and is called on global level object i.e `window`
	// so calling `foo` and `window.foo` is same. 
	// Hence the context is a window object.
	console.log(this);
}

foo() // undefined

// Whereas if we do new foo() at the global level then will get this as foo object.
new foo() // foo {}
```

### Under 2nd level function

```javascript
var x = {
	fn: function() {
		return this;
	},
	y: {
		fn: function () {
			return this;
		}
	}
}

x.fn()   === x // true --> fn: [λ: fn] | y: { fn: [λ: fn] }
x.y.fn() === x // false --> fn: [λ: fn] | y: { fn: [λ: fn] }
x.y.fn() === x.y // true --> fn: [λ: fn] | fn: [λ: fn]
```

### use strict

```javascript
function useStrict() {
	'use strict';
	return this;
}

useStrict() === window // false
useStrict() === undefined // true
```

### Arrow function

```javascript
const a = () => {
	return this;
}

a() === window // true
```

### Prototype Chain

```javascript
var obj = {
	func: function() {
		return this.x
	}
}

var newObj = Object.create(obj);

newObj // {}
newObj.func() // undefined
newObj.x = 10; // 10
newObj.y = 20; // 20
newObj // {x: 10, y: 20}
newObj.func() // 10
obj.func() // undefined
```

### Event Handlers

```javascript
document.getElementById('body').addEventListener('click', function(e) {
 	console.log(this) // body.document
 	console.log(this === window) // false
  console.log(e.currentTarget === this) // true
})

```
