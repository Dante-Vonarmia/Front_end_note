# Scope

## What

The scope is the accessibility of variables, functions, or objects in some particular part of your code during runtime.

They came into existence when the principle of least privilege was applied in programming language designs.

## Why

1\. Security&#x20;

2\. Efficiency principle, Easy to Track&#x20;

3\. Reduce namespace collision

## Types

### Global and Local

```javascript
// Gobal 
var name = "Mouse";

function test1() { 
    // Local 
    var name = "Cat"; 
    console.log(name); 
}

function test2() { 
    // Local 
    var name = "Dog"; 
    console.log(name); 
} 

test1(); 
test2(); 
console.log(name);
```

### Lexical&#x20;

* When a function within another function, the inner function has access to the scope in the outer function, this is called Lexical Scope — also referred to as Static Scope as it may only be referenced from within the block of code in which it is defined.
* JavaScript starts at the innermost scope and searches outwards until it finds the variable/object/function it was looking for.
* Lexical scope does not work backward.

```javascript
function SocialMedia() {
  var channel = 'Facebook';
  function platForm() {
    // channel is accessible here
    function comments() {
      // Innermost level of the scope chain
      // channel is also accessible here
      var comments = 'Learning Scopes';
    }
  }
}
```

### Block&#x20;

```javascript
(function function_name(argument) {
  // body...
})() // IIFE
```

* The first is the anonymous function with lexical scope enclosed within the Grouping Operator `()`. This prevents accessing variables within the IIFE idiom as well as polluting the global scope.&#x20;
* The second part creates the immediately invoked function expression `()` through which the JavaScript engine will directly interpret the function.

### &#x20;Public and Private

Wrapping functions from the public (global) scope save them from vulnerable attacks.&#x20;

```javascript
// A Singleton example
const modulePattern = (function() {
  function privateMethod() {
    console.log('private');
  }

    return {
      publicMethod: function() {
        console.log('public');
      }
  }
})(); // IIFE

modulePattern.publicMethod() // public
modulePattern.privateMethod() // ​​modulePattern.privateMethod is not a function​​
```
