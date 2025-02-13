# Variables

## `null` vs `Undefined`

### Null

* `null` variable is assigned.
* `null` variable is always intentional.
* `null` variable indicates a lack of value.

### Undefined

* `undefined` variable can be assigned.
* `undefined` variable is often unintentional.
* `undefined` variable indicates a variable is declared but not defined.

### Both

* Both `null` and `undefined` are primitives values.
* Both `null` and `undefined` are falsy values.
* `null` and `undefined` are loosely equal.

## Equality and Comparisons

### The Equality Operator

```javascript
""           ==   "0"           // F
0            ==   ""            // T
0            ==   "0"           // T
false        ==   "false"       // F
false        ==   "0"           // T
false        ==   undefined     // F
false        ==   null          // F
null         ==   undefined     // T
" \t\r\n"    ==   0             // T
```

### The Strict Equality Operator

```javascript
""           ===   "0"           // F
0            ===   ""            // F
0            ===   "0"           // F
false        ===   "false"       // F
false        ===   "0"           // F
false        ===   undefined     // F
false        ===   null          // F
null         ===   undefined     // F
" \t\r\n"    ===   0             // F
```

### Comparing Objects

```javascript
new String('foo') === 'foo';     // F
new Number(10) === 10;           // F
let foo = {};
foo === foo;                     // T
{} === {}                        // Error
```

## Type Casting

JavaScript is a _weakly typed_ language, so it will apply _type coercion_ **wherever** possible.

```javascript
// These are true
new Number(10) == 10; // Number object is converted
                       // to a number primitive via implicit call of
                       // Number.prototype.valueOf method

10 == '10';           // Strings gets converted to Number
10 == '+10 ';         // More string madness
10 == '010';          // And more 
isNaN(null) == false; // null converts to 0
                       // which of course is not NaN

// These are false
10 == 010;
10 == '-10';
```

{% hint style="info" %}
To avoid the issues above, use of the [strict equal operator](https://bonsaiden.github.io/JavaScript-Garden/#types.equality) is **highly** recommended.
{% endhint %}

### \*Constructors of Built-In Types

The constructors of the built in types like `Number` and `String` behave differently when being used with the `new` keyword and without it.

```javascript
new Number(10) === 10;     // False, Object and Number
Number(10) === 10;         // True, Number and Number
new Number(10) + 0 === 10; // True, due to implicit conversion
```

Using a built-in type like `Number` as a constructor will create a new `Number` object, but leaving out the `new` keyword will make the `Number` function behave like a converter.

In addition, passing literals or non-object values will result in even more type coercion.

The best option is to cast to one of the three possible types **explicitly**.

### Casting to a String

```javascript
'' + 10 === '10'; // true
// By prepending an empty string, a value can easily be cast to a string.
```

### Casting to a Number

```javascript
+'10' === 10; // true
// Using the unary plus operator, it is possible to cast to a number.
```

### Casting to a Boolean

```javascript
// By using the not operator twice, a value can be converted to a boolean.

!!'foo';   // true
!!'';      // false
!!'0';     // true
!!'1';     // true
!!'-1'     // true
!!{};      // true
!!true;    // true

```
