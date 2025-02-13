# Function Approaches

## Write a sample of callback function

```javascript
function writeBlog(topic, callback) {
    console.log(`Starting my ${topic} blog.`);
    // then execute the callback function that was passed
    callback();
}

writeBlog('JS', function() {
    console.log('Finished my blog!');
});
```

## Factorialize a Number

```javascript
// 1. Factorialize a Number With Recursion
function factorialize1(num) {
	if (num < 0)
		return -1;
	else if (num == 0)
		return 1;
	else {
		return (num * factorialize1(num - 1));
	}
}
factorialize1(5);

// 2. Factorialize a Number with a WHILE loop
function factorialize2(num) {
  var result = num;
  if (num === 0 || num === 1) 
    return 1; 
  while (num-- > 1) { 
    result *= num;
  }
  return result;
}
factorialize2(5);
```

## Function debounce

Debouncing is a very good to have feature, when user is expected to do a particular action very very quickly, such as typing a product name for searching in an e-commerce site.

Imagine on each key press the client code makes and API call for fetching the suggestions to be shown in the search result, these are so many api calls, to avoid this situation of making so many api call we can implement debouncing.

#### Debounce Algorithms:

1. Call a function on user action after a delay time
2. Clear the previous delay time on the next action if the action is performed before that delay time
3. Make use of `setTimeout`

```javascript
// debounce logic
let timer = null;
const debounce = (actionHandler, delay) => {
  if (timer) {
    // clearing timer
    clearInterval(timer);
  }
  timer = setTimeout(actionHandler, delay);
};

// some costly function
const fetchDataFromAPI = () => {

  //here you can put your fetch logic

  console.log("fetchData");
};

// event binding to input
const elem = document.getElementById("sample-id");
elem.addEventListener("input", e => {
  debounce(fetchDataFromAPI, 1000);
});
```



## Write a function that will reverse the arguments of a different function call.&#x20;

```javascript
/**
 * Write a function that will reverse the arguments of a different function call. 
 * eg:
 * console.log('1', '2', '3') // console 1 2 3
 * reversedFunc(console.log)('1', '2', '3') // console 3 2 1
 */

function reversedFunc(fn) {
    let rst = [];
  return function(...obj) {
    for (let i = obj.length - 1; i >=0 ; i--) {
      rst = [...rst, obj[i]];
    }
    return fn(...rst)
  }
}

reversedFunc(console.log)('1', '2', '3')
```

## Rebuilt - HOF - Prototype ver.

#### fake data class

```javascript
////////////////////////////////////////////////
// Create Developer Class with few properties //
////////////////////////////////////////////////

class Developer {
    constructor(favLang, type, salary, expInYears) {
        this.favLang = favLang;
        this.type = type;
        this.salary = salary;
        this.expInYears = expInYears;
    }
}

/////////////////////////////////////////
// Array of developers for ease of use //
/////////////////////////////////////////

const developers = [
    new Developer('javascript', 'fullstack', 100000, 5),
    new Developer('GoLang', 'backend', 120000, 3),
    new Developer('java', 'backend', 170000, 9),
    new Developer('shell', 'system', 90000, 5),
    new Developer('ruby', 'fullstack', 100000, 1),
    new Developer('react', 'frontend', 40000, 1)
];
```

### `Map()`

```javascript
////////////
// Map 🎯 //
////////////

// Method 1: Imperative Approach

/**
 * ES6 array function which returns array of salaries 
 */
const loopSalary = () => {
    const arr = [];
    const bonus = 3000;
    for (let i = 0, len = developers.length; i < len; i++) {
        arr.push(developers[i].salary + bonus)
    }
    return arr; // Most importantly it returns a new array.
}

console.log(loopSalary(3000)); // [ 103000, 123000, 173000, 93000, 103000, 43000 ]
```

```javascript
// Method 2: Declarative Approach

// Approach One
const mapSalary = bonus => developers.map(dev => {
    return dev.salary + bonus;
})

console.log(mapSalary(3000)); // [ 103000, 123000, 173000, 93000, 103000, 43000 ]

// Approach Two ( more functional )
const devs = addBonus => dev => dev.salary + addBonus;
const mapSalaryAgain = bonus => developers.map(devs(bonus));

console.log(mapSalaryAgain(3000)); // [ 103000, 123000, 173000, 93000, 103000, 43000 ]

```

```javascript
// Method 3: Map Dissection

/**
 * Chaining new map function to Array.prototype,
 * which takes a callback function to execute.
 */
Array.prototype.myNewMap = callback => {
    const len = this.length;
    const result = new Array(length);
    let i = -1;

    while (++i < len) {
        result[i] = callback(this[i], i, this)
    }
    return result;
}

// executing newly built map on an array
const myNewMapResult = developers.myNewMap(dev => {
    return dev.salary + 3000;
});

// printing the result array
console.log(myNewMapResult);  // [ 103000, 123000, 173000, 93000, 103000, 43000 ]
```

### `Reduce()`

```javascript
///////////////
// Reduce 🍔 //
///////////////

// Method 1: Imperative Approach

/**
 * Defining function to calculate average
 * per year experince salary in the company.
 */
const averageSalaryPerYear = () => {
    let totalSalary = 0;
    let totalExp = 0;

    for (let i = 0; i < developers.length; i++) {
        totalSalary = totalSalary + developers[i].salary;
        totalExp = totalExp + developers[i].expInYears;
    }

    return Math.floor(totalSalary / totalExp);
}

console.log(averageSalaryPerYear()); // 25833
```

```javascript
// Method 2: Declarative Approach

/**
 * Using reduce to calculate the total salary,
 * total experince. Returning array has both of
 * these values.
 */
const averageSalExp = developers.reduce(([tSal, tExp], developer) => {
    tSal = tSal + developer.salary;
    tExp = tExp + developer.expInYears;
    return [tSal, tExp]
}, [0, 0])

// array destructuring to extract the values instead of ugly array[index]
const [totalSalary, totalExp] = averageSalExp;
const averageSalPerYear = Math.floor(totalSalary / totalExp);

console.log(averageSalPerYear); // 25833
```

```javascript
// Method 3: Reduce Dissection

/**
 * Reducer Implementation 
 * @param {*} array - array of data ( can be numbers or objects )
 * @param {*} callback - function to execute on the data
 * @param {*} accumulator - value to start adding 
 */
Array.prototype.myNewReducer = (callback, accumulator) => {
    const length = this.length;
    let i = -1;

    if (!accumulator && length > 0) {
        accumulator = this[++i];
    }

    while (++i < length) {
        accumulator = callback(accumulator, this[i], i, this);
    }

    return accumulator;
}

const addNumbers = [3, 5, 9, 1, 2].myNewReducer((acc, num) => acc + num, 0);
console.log(addNumbers); // 20 

const averageSalaryGainPerYear = developers.myNewReducer(([tSal, tExp], data) => {
    tSal = tSal + data.salary;
    tExp = tExp + data.expInYears;
    return [tSal, tExp];
}, [0, 0]);

const [tSalaryAmount, tExperinceYears] = averageSalaryGainPerYear;
const averageGainPerYear = Math.floor(tSalaryAmount / tExperinceYears);

console.log(averageGainPerYear); // 25833
```

### `Filter()`

```javascript
////////////////
// Filter 🔎 //
///////////////

// Method 1: Imperative Approach

/**
 * Function to find developers of required experience.
 * @param {*} requiredExp - developer required exp
 */
const expDevelopers = requiredExp => {
    let length = developers.length;
    let result = [];
    for (let i = 0; i < length; i++) {
        let developer = developers[i];
        if (developer.expInYears > requiredExp) {
            result.push(developer);
        }
    }

    return result;
}

let testDevs = expDevelopers(3);
console.log(testDevs.length); // 3 
```

```javascript
// Method 2: Declarative Approach

/**
 * Function using filters to find min experience developers.
 * @param {*} requiredExp - - developer required exp
 */
const expFilteredDevelopers = requiredExp => developers.filter(developer => {
    return developer.expInYears > requiredExp;
});

let filteredDevelopers = expFilteredDevelopers(3);
console.log(filteredDevelopers.length); // 3
```

```javascript
// Method 3: Filter Dissection

/**
 * Filter as array prototype method.
 */
Array.prototype.myNewFilter = callback => {
    let length = this.length;
    let result = new Array();

    let i = -1;
    while (++i < length) {
        let value = this[i];
        let filteredValue = callback(value, i, this);
        if (filteredValue) {
            result.push(value);
        }
    }
    return result;
}

const myNewFilteredDevs = developers.myNewFilter(developer => developer.expInYears > 3);
console.log(myNewFilteredDevs.length); // 3
```

## Rebuilt - HOF - Pure function ver.

#### Fake data

```javascript
////////////////////////////////////////
// Write your own filter, map, reduce //
////////////////////////////////////////

// A higher-order function is a function that does at least one of the following:
	// - Takes one or more functions as arguments,
	// - Returns a function as its result.

let arr = [1, 2, 3, 4, 5];
```

### `map()`

```javascript
/////////////////////////////////////////////////
// map takes an array and function as argument //
/////////////////////////////////////////////////
// The `map()` method creates a new array with the results of calling a provided function on every element in the calling array.


// 1. Create an empty array `mapArr`.
// 2. Loop through array elements.
// 3. Call function `mapFunc` with the current element as the argument.
// 4. Push the result of the `mapFunc` function to the `mapArr` array.
// 5. Return the `mapArr` array after going through all the elements.

function myMap(arr, mapFunc) {
	const mapArr = []; // empty array        
	// loop though array
	for (let i = 0; i < arr.length; i++) {
		const result = mapFunc(arr[i]);
		mapArr.push(result);
	}
	return mapArr;
}

const squareArr2 = myMap(arr, num => num ** 2);
console.log(squareArr2); // prints [1, 4, 9, 16, 25]
```

### `reduce()`

```javascript
////////////////////////////////////////////////////////////////////
// reducer takes an array, reducer() and initialValue as argument //
////////////////////////////////////////////////////////////////////
// The `reduce()` method executes a reducer function (that you provide) on each member of the array resulting in a single output value.

// 1. Initialize `accumulator` variable with `0` or `initalValue` argument from the `reduce()`.
// 2. Loop through the array elements.
// 3. Call the reducer function with the `accumulator` and current element as the arguments.
// 4. Return `accumulator` after going through all the elements.

const sumReducer = (accumulator, currentValue) => accumulator + currentValue;

function myReduce(arr, reducer, initialValue) {
	let accumulator = initialValue === undefined ? 0 : initialValue
	// loop though array    
	for (let i = 0; i < arr.length; i++)
		accumulator = reducer(accumulator, arr[i], i, arr);
	return accumulator;
}

const sum = myReduce(arr, sumReducer);
console.log(sum); // prints 15
const sum2 = myReduce(arr, sumReducer, 5);
console.log(sum2); // prints 20
```

### `filter()`

```javascript
////////////////////////////////////////////////////
// filter takes an array and function as argument //
////////////////////////////////////////////////////
// The `filter()` method creates a new array with all elements that pass the test implemented by the provided function.

// 1. Create an empty array `filterArr`.
// 2. Loop through the array elements.
// 3. Called the `filterFunc` function with the current element as the argument.
// 4. If the result is true, push the element to the `filterArr` array.
// 5. Return `filterArr` array after going through all the elements.

function myFilter(arr, filterFunc) {
	const filterArr = []; // empty array        
	// loop though array    
	for (let i = 0; i < arr.length; i++) {
		const result = filterFunc(arr[i], i, arr);
		// push the current element if result is true 
		if (result)
			filterArr.push(arr[i]);
	}
	return filterArr;
}

const oddArr2 = myFilter(arr, num => num % 2 === 0);
console.log(oddArr2); //prints [2, 4]
```

## Throttling and Debouncing

### Throttle

```javascript
// Basic sample
const throttle = (func, limit) => {
  let inThrottle
  return function() {
    const args = arguments
    const context = this
    if (!inThrottle) {
      func.apply(context, args)
      inThrottle = true
      setTimeout(() => inThrottle = false, limit)
    }
  }
}
```

```javascript
const throttle = (func, limit) => {
  let lastFunc
  let lastRan
  return function() {
    const context = this
    const args = arguments
    if (!lastRan) {
      func.apply(context, args)
      lastRan = Date.now()
    } else {
      clearTimeout(lastFunc)
      lastFunc = setTimeout(function() {
        if ((Date.now() - lastRan) >= limit) {
          func.apply(context, args)
          lastRan = Date.now()
        }
      }, limit - (Date.now() - lastRan))
    }
  }
}

// Implementation
throttleBtn.addEventListener('click', throttle(function() {
  return console.log('Hey! It is', new Date().toUTCString());
}, 1000));
```

### Debounce

```javascript
const debounce = (func, delay) => {
  let inDebounce
  return function() {
    const context = this
    const args = arguments
    clearTimeout(inDebounce)
    inDebounce = setTimeout(() => func.apply(context, args), delay)
  }
}

// Implementation
debounceBtn.addEventListener('click', debounce(function() {
  console.info('Hey! It is', new Date().toUTCString());
}, 3000));

```
