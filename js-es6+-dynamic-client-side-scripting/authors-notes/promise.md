# Promise

## Basic Concept Explanation

### Constructor

```javascript
// Create a Promise Object
let promise = new Promise((resolve, reject) => {
	// Async process
	// After that, call `resolve` or `reject`
})
```

### Instance Method

```javascript
promise.then(onFulfilled, onRejected)
// onFulfilled -> resolve
promise.then(onFulfilled).catch(onRejected)
// onRejected -> reject
```

### Static Method

```javascript
`Promise.all()`, `Promise.race()`, and `Promise.resolve()`
// Promise workflow
function asyncFunc() {
	// Return a promise object
	return new Promise((resolve, reject) => {
		setTimeout(() => resolve('Async'), 10);
	});
}

// Same as (without `catch`)
asyncFunc().then(value => console.log(value), error => console.log(error));

// use `then` to call callback function
// use `catch` to call error function
asyncFunc()
	.then(value => console.log(value))
	.catch(error => console.log(error));
```

### Promise's status

```javascript
'ES6 Promise Terms' | 'Promises/A+ Terms'
'has-resolution'    | 'Fulfilled'
'has-rejection'     | 'Rejected'
'unresolved'        | 'Pending'
```

## Usage - Create XHR's promise Object

```javascript
// First, create a function called getURL that wraps XHR processing with a promise.
function getURL(URL) {
	return new Promise((resolve, reject) => {
		let req = new XMLHttpRequest();
		req.open('GET', URL, true);
		req.onload = () => req.status === 200 ? resolve(req.responseText) : reject(new Error(req.statusText));
		req.onerror = () => reject(new Error(req.statusText));
		req.send();
	});
}

// Run the instance
let URL = "https://azu.github.io/promises-book/json/people.json";
getURL(URL).then(function onFulfilled(value) {
	console.log(value); // when result state is 200: call resolve
}).catch(function onRejected(error) {
	console.error(error);
});
```

## Resolve, Reject, Thenable

### `Promise.resolve`

```javascript
// `new` `Promise` shortcut method
// `Promise.resolve(value)` is static methods
Promise.resolve(value)
// same as
new Promise(resolve => resolve(value));
// turn the promise object's status into fulfilled immediately
```

### Thenable

`Promise.resolve` --> thenable object --> promise object&#x20;

thenable object: function with `.then` method

```javascript
// A react sample owns `.then` method
// ...
fetch('/sample.json')
	.then(response => response.json())
	.then(data => {
	this.setState({
		data: data.map((e) => e.url)
	})
	.catch(e => console.error(e))
});
// ...

// thenable to promise objct
let promise = Promise.resolve(fetch('/sample.json'))
promise.then(value => console.log(value));
```

### Promise.reject

```javascript
// `new` `Promise` shortcut method
// `Promise.reject(error)` is static methods
Promise.reject(new Error("Go Wrong!"));
// same as
new Promise((undefined, reject) => reject(new Error("Go Wrong!")));
// or
Promise.reject(new Error("Go Wrong!")).catch(error => console.error(error));
// Through the onRejected function, pass the `Error` object to it.
```

### Never use sync method to call callback methods

```javascript
// onready-as-promise
function onReadyPromise() {
	return new Promise((resolve, reject) => {
		let readyState = document.readyState;
		if (readyState === 'interactive' || readyState === 'complete')
			resolve();
		else
			window.addEventListener('DOMContentLoaded', resolve);
	});
}

onReadyPromise().then(() => console.log('DOM fully loaded and parsed'));
console.log('===Starting===')

// Output process in the wrong piority:
	// ===Starting===​​​​​​​​ ​​​ 
	// ​​​​​DOM fully loaded and parsed​​​​​
```

### A correct way to use onRejected

```javascript
function throwError(value) { // throw expectation
	throw new Error(value);
}
// <1> onRejected won't be call
function badMain(onRejected) {
	return Promise.resolve(42).then(throwError, onRejected);
}
// <2> onRejected will only be call when an exception occurs
function goodMain(onRejected) {
	return Promise.resolve(42).then(throwError).catch(onRejected);
}
// run the sample
badMain(function() {
	console.log("BAD");
});
goodMain(function() {
	console.log("GOOD");
});
// Then Catch flow
Promise.resolve(value).then(throwError).then(null, onRejected);
```

## Process multiple async request

### multiple-xhr-callback

```javascript
function getURLCallback(URL, callback) {
	let req = new XMLHttpRequest();
	req.open('GET', URL, true);
	req.onload = function() {
		if (req.status === 200)
			callback(null, req.responseText)
		else
			callback(new Error(req.statusText), req.response);
	}
	req.onerror = () => {
		callback(new Error(req.statusText));
	}
	req.send();
}

// Parse the JSON data securely
function jsonParse(callback, error, value) {
	if (error)
		callback(error, value);
	else {
		try {
			let result = JSON.parse(value);
			callback(null, result);
		} catch (e) {
			callback(e, value);
		}
	}
}

// Sending XHR request
let request = {
	comment: function getComment(callback) {
		return getURLCallback('https://azu.github.io/promises-book/json/comment.json', jsonParse.bind(null, callback));
	},
	people: function getPeople(callback) {
		return getURLCallback('https://azu.github.io/promises-book/json/people.json', jsonParse.bind(null, callback));
	}
}

// Sending multiple XHR requests, call `callback` when return request
function allRequest(requests, callback, results) {
	if (requests.length === 0)
		return callback(null, results);

	let req = requests.shift();
	req((error, value) => {
		if (error)
			callback(error, value)
		else {
			results.push(value);
			allRequest(requests, callback, results);
		}
	});
}

function main(callback) {
	allRequest([request.comment, request.people], callback, [])
}

// run the sample
main((error, results) => {
	if (error)
		return console.error(error);
	console.log(results);

});
```

#### pros

* Using the JSON.parse function directly may throw an exception, so a wrapper function is used here
* If multiple XHR processes are nested, it will be deeper, so the allRequest function is used and the request is called in it.
* The callback function uses the callback (error, value) method. The first parameter indicates the error message, and the second parameter is the return value.
* Using bind to reduce the times of using anonymous functions

**cons**

* Callback functions everywhere
* Need to display for exception handling
* In order not to let the nesting level be too deep, you need a function to process the request

### promise-then-xhr

```javascript
function getURL(URL) {
	return new Promise((resolve, reject) => {
		let req = new XMLHttpRequest();
		req.open('GET', URL, true);
		req.onload = () => {
			if (req.status === 200)
				resolve(req.responseText)
			else
				reject(new Error(req.statusText));
		}
		req.onerror = () => {
			reject(new Error(req.statusText));
		};
		req.send();
	});
}

let request = {
	comment: function getComment(callback) {
		return getURL('https://azu.github.io/promises-book/json/comment.json').then(JSON.parse);
	},
	people: function getPeople(callback) {
		return getURL('https://azu.github.io/promises-book/json/people.json').then(JSON.parse);
	}
}

function main() {
	function recordValue(results, value) {
		results.push(value);
		return results;
	}

	var pushValue = recordValue.bind(null, []);
	return request.comment().then(pushValue).then(request.people).then(pushValue);
}

// run the sample
main().then(value => { console.log(value) }).catch(error => { console.error(error) });
```

#### pros

* You can use the JSON.parse function directly
* function main () returns the promise object
* Handle the returned promise object directly in the place of error handling

#### cons

* 'then' part could be hard to understand
* should use Promise.all and Promise.race to deal with multiple requests

### promise-all-xhr

#### `Promise.all`&#x20;

* Receive array of promise objects as parameters&#x20;
* All promise objects are run in sync

```javascript
function getURL(URL) {
	return new Promise((resolve, reject) => {
		let req = new XMLHttpRequest();
		req.open('GET', URL, true);
		req.onload = () => {
			if (req.status === 200)
				resolve(req.responseText)
			else
				reject(new Error(req.statusText));
		}
		req.onerror = () => {
			reject(new Error(req.statusText));
		};
		req.send();
	});
}

let request = {
	comment: function getComment(callback) {
		return getURL('https://azu.github.io/promises-book/json/comment.json').then(JSON.parse);
	},
	people: function getPeople(callback) {
		return getURL('https://azu.github.io/promises-book/json/people.json').then(JSON.parse);
	}
}

function main() {
	return Promise.all([request.comment(), request.people()]);
}

// run the sample
main().then(value => { console.log(value) }).catch(error => { console.error(error) });
```

#### `Promise.race`

```javascript
let winnerPromise = new Promise((resolve) => {
	setTimeout(() => {
		console.log('this is winner');
		resolve('this is winner');
	}, 4);
});
let loserPromise = new Promise((resolve) => {
	setTimeout(() => {
		console.log('this is loser');
		resolve('this is loser');
	}, 1000);
});
// when first promise turn out to be fulfilled, then stop
Promise.race([winnerPromise, loserPromise]).then((value) => { console.log(value) });
```

## Recap

1.  Use `promise.then(onFulfilled, onRejected)`

    If an exception occurs in onFulfilled, the exception cannot be caught in onRejected.\

2.  In the case of `promise.then(onFulfilled).catch(onRejected)`

    Exceptions generated in then can be caught in `.catch()`


3.  `.then()` and `.catch()` are essentially the same

    It needs to be used in different occasions
