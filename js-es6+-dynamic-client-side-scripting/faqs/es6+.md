# ES6+ new features

## What kinds of declaration does ES6 introduced? What are the scopes of each of them?

### Block scoping via `let` and `const`   <a href="#block-scoping-via-let-and-const" id="block-scoping-via-let-and-const"></a>

Both `let` and `const` create variables that are block-scoped – they only exist within the innermost block that surrounds them.&#x20;

### Other declaration and their scopes

#### Function declarations

* are block-scoped, like `let`.
* create properties on the global object (while in global scope), like `var`.
* are _hoisted_: independently of where a function declaration is mentioned in its scope, it is always created at the beginning of the scope.

The following code demonstrates the hoisting of function declarations:

```javascript
{ // Enter a new scope
    console.log(foo()); // OK, due to hoisting
    function foo() {
        return 'hello';
    }
}
```

#### Class declarations

* are block-scoped.
* don’t create properties on the global object.
* are _not_ hoisted.

Classes not being hoisted may be surprising, because, under the hood, they create functions. The rationale for this behavior is that the values of its `extends` clauses are defined via expressions and those expressions have to be executed at the appropriate times.

```javascript
{ // Enter a new scope
    const identity = x => x;

    // Here we are in the temporal dead zone of `MyClass`
    let inst = new MyClass(); // ReferenceError

    // Note the expression in the `extends` clause
    class MyClass extends identity(Object) {
    }
}
```

## What is an arrow function?&#x20;

First, it’s a new feature in ES6 standard. One thing worth to be mentioned is an arrow function actually doesn’t include the constructor. So, the context will be its outer.

## Difference between regular functions and arrow functions in JavaScript

#### **Arrow function has no keywords: `this`, argument**

So an arrow function as actionHandler no need to do `bind` in constructor

An arrow function expression is a syntactically compact alternative to a regular function expression, although without its own bindings to the `this`, arguments, `super`, or new.target keywords. Arrow function expressions are illustrated as methods, and they cannot be used as constructors.

* Arrow functions do not have a prototype property.
* Arrow functions cannot be used as constructors and will throw an error when used with `new`

Since arrow functions do not have their own this, the methods `call()` and `apply()` can only pass in parameters. Any this argument is ignored.

## What's the difference between spread operator and rest operator?

* Rest Parameter is collecting all remaining elements into an array .
* Spread Operator is unpacking collected elements such as arrays into single elements .

#### Reference:

{% embed url="https://medium.com/javascript-in-plain-english/es6-spread-parameter-vs-rest-operator-5e3c924c4e1f" %}
