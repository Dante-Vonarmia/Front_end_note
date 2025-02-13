# Array

## The Array Constructor

### Explanation

Since the Array constructor is ambiguous in how it deals with its parameters, it is highly recommended to use the `array` literal - `[]` notation - when creating new arrays.

### Basic example - declaration

```javascript
[1, 2, 3]; // Result: [1, 2, 3]
new Array(1, 2, 3); // Result: [1, 2, 3]
```

In cases when there is only one argument passed to the Array constructor and when that argument is a Number, the constructor will return a new sparse array with the length property set to the value of the argument.

### Basic example - parameters

```javascript
[3]; // Result: [3]
new Array(3); // Result: []
new Array('3') // Result: ['3']
```

It should be noted that only the length property of the new array will be set this way; the actual indexes of the array will not be initialized.

```javascript
var arr = new Array(3);
arr[1]; // undefined
1 in arr; // false, the index was not set
```

Being able to set the length of the array in advance is only useful in a few cases, like repeating a string, in which it avoids the use of a loop.

```javascript
new Array(count + 1).join(stringToRepeat);
```

### In Conclusion&#x20;

Literals are preferred to the Array constructor. They are shorter, have a clearer syntax, and increase code readability.

## `for in` vs classic `for`

Although arrays in JavaScript are objects, there are no good reasons to use the `for in` loop. In fact, there are a number of good reasons against the use of `for in` on arrays.

Because the `for in` loop enumerates all the properties that are on the prototype chain and because the only way to exclude those properties is to use `hasOwnProperty`, it is already up to twenty times slower than a normal `for` loop.

## Performance in Iteration

### Basic Example

In order to achieve the best performance when iterating over arrays, it is best to use the classic `for` loop.

```javascript
let list = [1, 2, 3, 4, 5, ..., 100000000];
for(let i = 0, l = list.length; i < l; i++) {
    console.log(list[i]);
}
// There is one extra catch in the above example, 
// which is the caching of the length of the array via `l = list.length`
```

### Explanation

Although the length property is defined on the array itself, there is still an overhead for doing the lookup on each iteration of the loop.

And while recent JavaScript engines may apply optimization in this case, there is no way of telling whether the code will run on one of these newer engines or not.

In fact, leaving out the caching may result in the loop being only half as fast as with the cached length.

### In Conclusion&#x20;

For the best performance, it is recommended to always use the plain for loop and cache the length property. The use of for in on an array is a sign of badly written code that is prone to bugs and bad performance.
