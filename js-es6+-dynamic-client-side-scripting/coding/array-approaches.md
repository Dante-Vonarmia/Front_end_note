# Array Approaches

## Merge the following two array

```javascript
/* INPUT:
[
	{ id: 3, name: "Matt" }, 
	{ id: 4, name: "Greg" }, 
	{ id: 1, name: "David" }, 
	{ id: 2, name: "John"}
];
[
	{ id: 2, position: "Leader" },
	{ id: 3, position: "Captain" },
	{ id: 6, position: "Rogue" },
	{ id: 4, position: "VP" },
	{ id: 5, position: "Pawn" }
];
*/
```

```javascript
/* OUTPUT:
[
    { id: 1, name: "David", position: null },
    { id: 2, name: "John", position: "Leader" },
    { id: 3, name: "Matt", position: "Captain" },
    { id: 4, name: "Greg", position: "VP" },
    { id: 5, name: null, position: "Pawn" },
    { id: 6, name: null, position: "Rogue" }
];
*/

// Using ES6 Map
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
const result = Array.from(_hash.values()); 
```

## Write a function to rotate the array from left to right, and explain its Big-O notation.

(P.S. Using **HOF** will be count as half scores)\
(P.S. And recursion is never a satisfying solution)\
(P.S. Surprise me by using any ADS, aka abstract data structure)

```javascript
// e.q.: [1,2,3] ==> [3,1,2] ==> [2,3,1]

/**
\* [arrayRotation description]
\* @param  {[Array]}     arr     [The target array that passed in]
\* @param  {[Number]}     steps     [The times need to do the rotation]
\* @return {[Array]}           [Return the result array]
\*/

function arrayRotation(arr, steps) {
    // Code here...
    // Get bonus score by explain your solution's performance
}

// Test Sample:
arrayRotation([1,2,3], 2)
```

#### Solution

```javascript
// Solution: for
function arrayRotation(arr, steps) {
    let tempArr = [] 
    for(let i=0; i<arr.length; i++){ // Save the rotated array with a new array
        tempArr[(i+steps) % arr.length] = arr[i] 
    }
    return tempArr;
}; // O(n)

// Solution: HOF, pop(), unshift()
function arrayRotation(arr, steps) {
    steps %= arr.length
    for(let i = 0; i < steps; i ++){
        arr.unshift(arr.pop()); // Remove the element from the end first, then put it to the front
    }
    return arr;
}; // It looks a cool solution but the big-O could be a disaster.

// Solution: HOF, hacking way
function arrayRotation(arr, steps) {
    steps %= arr.length
    arr.unshift(...arr.splice(arr.length - steps, steps));
    return arr;
}; // It looks a cool solution but the big-O could be a disaster.
```

## Use HOF methods to accomplish a quick sort for an array.

```javascript
var array = [2,4,5,22,1,6,44,7,3,9];
const arr = [...array].map(temp => parseInt(temp, 10)).sort((a, b) => a - b);
```

## Find out the duplicated number.

```javascript
const arr = [1, 2, 3, 4, 4, 5, 6, 7, 7, 8, 6, 10];
const findDupes = arr => {
	const observed = {};
	for (let i = 0, len = arr.length; i < len; i++) {
		if (!observed[arr[i]]) {
			observed[arr[i]] = arr[i];
		} else {
			console.log(arr[i]);
		}
	}
}

findDupes(arr); // Output: 4, 7, 6
```

## Find out the intersection part of following two arrays.

```javascript
let arr1 = ["mike", "sue", "tom", "kathy", "henry"],
		arr2 = ["howey", "jim", "sue", "jennifer", "kathy", "hank", "alex"];

function intersection(a, b) {
	return a.filter(e => b.indexOf(e) > -1)
}

intersection(arr1, arr2); // Output: ['sue', 'kathy']
```

## Return the maximum and minimum number in the array

```javascript
const arr = [1, 2, 3, 4, 100];
const findMaxMin = (arr) => {
  let max = arr[0];
  let min = arr[0];
  
  for(let i = 0; i < arr.length; i++) {
    if(arr[i] > max) {
      max = arr[i];
    } else if (arr[i] < min) {
      min = arr[i];
    }
  }  
  return {
    "max": max,
    "min": min
  };
}

console.log(findMaxMin(arr)); // Output: { "max": 100, "min": 1 }
```

## Return the maximum and minimum missing number in the array (unsorted version)

```javascript
// a not very good HOF approach
let arr = [4, 7, 9, 3, 6, 8, 13];
const findMissingNum = (arr) => {
	let [...obj] = new Set(arr.sort((a, b) => a - b)),
		result = [];
	for (let i = 1, length1 = obj[obj.length - 1]; i < length1; i++) {
		if (obj.includes(i)) {
			continue;
		} else {
			result.push(i)
		}
	}
	return {
		min: result.shift(),
		max: result.pop()
	};
}

console.log(findMissingNum(arr)); // Output: { min: 1, max: 12 }​​​​​
```

## Find out all the pairs that equal to the same summation

```javascript
let arr = [1, 5, 6, 1, 2, 3, 0, 1];
const findSumPairs = (arr, value) => {
  let sumsLookup = {};
  let output = [];

  for (let i = 0, len = arr.length; i < len; i++) {
    let targetVal = value - arr[i];

    if (sumsLookup[targetVal]) {
      output.push([arr[i], targetVal]);
    }

    sumsLookup[arr[i]] = true;
  }

  return output;
}

console.log(findSumPairs(arr, 6)); // Output: ​​​​​[ [ 5, 1 ], [ 1, 5 ], [ 0, 6 ], [ 1, 5 ] ]​​​​​
```

## The element with the most occurrences and the number of times.

```javascript
// Find out the target number's occurrences
function countOfElement(arr, N) {
  let encounteredNums = {};
  let num;
  for (let i = 0; i < arr.length; i++) {
    num = arr[i];
    if (encounteredNums[num]) {
      // value already encountered, count++
      encounteredNums[num]++;
    } else {
      // first encounter, initialize count
      encounteredNums[num] = 1;
    }
  }
  return {
    element: N,
    times: encounteredNums[N]
  } || 0; // 6 times
  // return encounteredNums[N] || 0; // 2
}

countOfElement([3, 4, 2, 3, 2, 2, 2, 2, 3, 2], 2); // Output:​​​​​ { element: 2, times: 6 }​​​​​
```

```javascript
// Find out the most Occurred number
let arr = [1,2,2,3,4,4,4,4,4,4,5,5,5,5,5,5,6,7,8,8,9];

function mostOccur(arr) {
  // if (arr) { ... } // common error check
  
  let obj = {},
      max = 0,
      output = new Array();
            
  for (let i = 0, length = arr.length; i < length; i++) {
    obj[arr[i]] ? obj[arr[i]]++ : obj[arr[i]] = 1;
    if (obj[arr[i]] > max) {
      max = obj[arr[i]]
    }
  }
  
  for (let prop in obj) {
    if (obj[prop] === max) {
      output.push(parseInt(prop));
    }
  }
  return output;
}

mostOccur(arr) // [4, 5]
```

## Find the number nth greatest number in an array.

```javascript
// Improved version
// Solved issue that the array might contain the same value
function Kth_greatest_in_array_object_solution(arr, k) {
	if (k > arr.length && k <= 0)
		return;

	let rst = {};
	for (idx of arr) {
		rst[idx] = null;
	}

	return Object.keys(rst)[Object.keys(rst).length-k]
}

Kth_greatest_in_array_object_solution([1, 2, 6, 6, 6, 6, 4, 5, 5, 2, 1], 2);
```

## Meandering Array

```javascript
let arr = [7, -5, 2, 7, 8, -2, 25, 25];
let result = [];

function meandering(arr) {
    if (!arr.length)
        return arr;
    arr.sort((prev, cur) => prev - cur);
    for (var i = 0, j = arr.length - 1; i <= j; i++, j--) {  
        result = [...result, arr[j], arr[i]];
        if (i === j) 
            result = [...result, arr[i]];
    }
    return result
}

console.log(meandering(arr)); // Output: ​​​​​[ 25, -5, 25, -2, 8, 2, 7, 7 ]​​​​​
```

## Find out the duplicated number that need to be remove. (Not all matched element need to be removed)

```javascript
const arr = [1, 5, 1, 3, 1, 3, 1, 5];
const removeDupes = (arr) => {
	let result = {},
		output = []

	for (var i = 0, len = arr.length; i < len; i++) {
		if (result[arr[i]] !== undefined) 
			output.push(i) // Elements need to be removed.
		else {
			result[arr[i]] = i; // Elements appeared the first time
		}
	}
	return output;
}

console.log(removeDupes(arr)); // Output: [ 2, 4, 5, 6, 7 ]
```

## Check whether the array1 contains the array2

```javascript
// Declare Two array 
const array1 = ['a', 'd', 'm', 'x']; 
const array2 = ['y', 'x']; 
  
// Function call 
function findCommonElements2(arr1, arr2) { 

    if (!array2.length || array2 === 'undefined') {
        return false
    }
    
    // Create an empty object 
    let obj = {}; 
    // Loop through the first array 
    for (let i = 0, len = arr1.length; i < len; i++) { 
          
        // Check if element from first array 
        // already exist in object or not 
        if(!obj[arr1[i]]) { 
          
            // If it doesn't exist assign the 
            // properties equals to the  
            // elements in the array 
            obj[arr1[i]] = true; 
        } 
    }
      
    // Loop through the second array 
    for (let j = 0, len = arr2.length; j < len; j++) { 
          
        // Check elements from second array exist 
        // in the created object or not 
        if(!obj[arr2[j]]) { 
            return false; 
        } 
    } 
    return true; 
} 
  
console.log(findCommonElements2(array1, array2));
```

## Flattening multidimensional Arrays in JavaScript

#### Recursion Solution

```javascript
function flatten(arr) {
   return arr.reduce((acc, val) => Array.isArray(val) ? acc.concat(flatten(val)) : acc.concat(val), []);
}
flatten([1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]]) // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

#### ES6 HOF Solution (Infinitely Nested Arrays)

```javascript
const veryDeep = [[1, [2, 2, [3,[4,[5,[6]]]]], 1]];
veryDeep.flat(Infinity); // [1, 2, 2, 3, 4, 5, 6, 1]
```

## Chunk

Chunk into certain parts, e.q.: \[1,2,3,4,5,6,7,8] \[\[1,2,3],\[4,5,6],\[7,8]]

```javascript
let arrChunk = (data = [], space = 3) => {
    var result = [];
    for (var i = 0, len = data.length; i < len; i += space) {
        result.push(data.slice(i, i + space));
    }
    return {
        data: result,
        total: data.length,
        space
    };
}

arrChunk([1,2,3,4,5,6,7,8])
/*
{ data: [ [ 1, 2, 3 ], [ 4, 5, 6 ], [ 7, 8 ] ],​​​​​
​​​​​  total: 8,​​​​​
​​​​​  space: 3 }​​​​​
*/
```

## Queue Reconstruction by ascent or descent order

Suppose you have a random list of array in a queue. Each element is described by a pair of integers `(w, h)`, where `w` is the first value of the element and `h` is the second value of the element which both have the value greater than or equal to their previous one. Write an algorithm to reconstruct the queue.

#### Example

```javascript
`Input:`
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

`Output:`
​​​​​[[ 5, 0 ], [ 7, 0 ], [ 7, 1 ]]

let arr = [
	[1, 1],
	[4, 5],
	[5, 4],
	[2, 2],
	[4, 4],
	[3, 3],
	[3, 5]
];

let arr2 = [
	[5, 0],
	[6, 1],
	[7, 0],
	[7, 1]
];
```

#### By Ascent

```javascript
let byAscent = arr => {
	arr.sort();
	for (let i = 0, length1 = arr.length - 1; i < length1; i++) {
		if (arr[i + 1] !== undefined && arr[i + 1][0] > arr[i][0] && arr[i + 1][1] < arr[i][1]) {
			arr.splice(i, 1);
			i--;
		}
	}
	return arr;
}

byAscent(arr); // ​​​​​[ [ 1, 1 ], [ 2, 2 ], [ 3, 3 ], [ 4, 4 ], [ 5, 4 ] ]​​​​​
byAscent(arr2); // ​​​​​[ [ 5, 0 ], [ 7, 0 ], [ 7, 1 ] ]​​​​​
```

#### By descent

```javascript
let byDescent = arr => {
	arr = arr.sort((idx =>
		(a, b) =>
		(a[idx] === b[idx] ? (a[idx][1] > b[idx][1] ? 0 : -1) : (a[idx] > b[idx] ? -1 : 1))
	)(0));

	for (let i = 0, length1 = arr.length - 1; i < length1; ++i) {
		if (arr[i + 1] !== undefined && arr[i + 1][1] > arr[i][1]) {
			arr.splice(i + 1, 1);
			i--;
		}
	}
	return arr;
}

byDescent(arr); //? ​​​​​[ [ 5, 4 ], [ 4, 4 ], [ 3, 3 ], [ 2, 2 ], [ 1, 1 ] ]​​​​​
byDescent(arr2); //? ​​​​​[ [ 7, 1 ], [ 7, 0 ], [ 5, 0 ] ]​​​​​
```
