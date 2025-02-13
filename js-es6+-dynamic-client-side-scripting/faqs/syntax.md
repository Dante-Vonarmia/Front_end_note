---
description: Primitive data; Operator;
---

# Syntax

## What are the primitive data types in JS?

In [JavaScript](https://developer.mozilla.org/en-US/docs/Glossary/JavaScript), a **primitive** (primitive value, primitive data type) is data that is not an [object](https://developer.mozilla.org/en-US/docs/Glossary/object) and has no [methods](https://developer.mozilla.org/en-US/docs/Glossary/method). There are 6 primitive data types: [string](https://developer.mozilla.org/en-US/docs/Glossary/string), [number](https://developer.mozilla.org/en-US/docs/Glossary/number), [bigint](https://developer.mozilla.org/en-US/docs/Glossary/bigint), [boolean](https://developer.mozilla.org/en-US/docs/Glossary/boolean), [undefined](https://developer.mozilla.org/en-US/docs/Glossary/undefined), and [symbol](https://developer.mozilla.org/en-US/docs/Glossary/symbol). There also is [null](https://developer.mozilla.org/en-US/docs/Glossary/null), which is seemingly primitive, but indeed is a special case for every [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object): and any structured type is derived from `null` by the [Prototype Chain](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance).

## What is escape character and what is it used for? (hint: Backslash)

The backslash is used as a marker character to tell the compiler/interpreter that the next character has some special meaning. What that next character means is up to the implementation.

In JavaScript, the backslash is used to escape special characters, such as newlines (`\n`). If you want to use a literal backslash, a double backslash has to be used.

#### Usage:

* To search for special characters `[ \ ^ $ . | ? * + ( )` literally, we need to prepend them with a backslash `\` (“escape them”).
* We also need to escape `/` if we’re inside `/.../` (but not inside `new RegExp`).
* When passing a string `new RegExp`, we need to double backslashes `\\`, cause string quotes consume one of them.

## What happened when a `new` operator is used for an instance?

* Creates a blank, plain JavaScript object;
* Links (sets the constructor of) this object to another object;
* Passes the newly created object from Step 1 as the this context;
* Returns this if the function doesn't return its own object.

## `for` and `for in`. Which is faster? Why?

Although arrays in JavaScript are objects, there are no good reasons to use the `for in` loop. In fact, there are a number of good reasons against the use of `for in` on arrays.

Because the `for in` loop enumerates all the properties that are on the prototype chain and because the only way to exclude those properties is to use `hasOwnProperty`, it is already up to twenty times slower than a normal `for` loop.

## `undefined` and not defined? What's the difference? Show me samples.

### **Undefined**

Whenever we declare a variable without assigning any value to it, javascript implicitly assigns its value as undefined.

```javascript
let name;
console.log(name); //undefined
```

When value is not assigned in array or object

```javascript
let numArray = [1,2,,4];
console.log(numArray);  
//[1, 2, empty, 4]
typeof(numArray[2])
//"undefined"
```

When functions don’t have a return statement but are called for assigning a value to a variable.

```javascript
let add = (a,b) => {
    let c = a + b;
    //return c;
}
let sum = add(2, 3);
console.log(sum); 
```

### **Not defined**

A not defined is a variable which is not declared at a given point of time with declaration keyword like `var`, `let` or `const`.

```javascript
console.log(a); // undefined
var a = 5;
```

While if we don’t use `var` keyword above the output will be:

```javascript
console.log(b);
b = 5;
//Output:- "ReferenceError: b is not defined
```

The reason why the variable a was printed with undefined value above but b was declared as not defined was because of the way variable **hoisting** works in JavaScript. The variable declarations are processed before code execution takes place in javascript.\
