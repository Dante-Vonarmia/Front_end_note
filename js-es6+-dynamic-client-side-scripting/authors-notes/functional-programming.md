---
description: Significant feature of JavaScript
---

# Functional Programming

> Being able to use call, apply, and bind skillfully is an important step for us to truly become a JavaScript programmer.&#x20;
>
> ——Dante Von Alcatraz

## High Order Function -- HOF

* Functions can be passed as parameters;
* Functions can be output as return values.

### `.map()`, `.forEach()`, etc.

* `.map()` vs `.forEach()` is basically immutable vs mutable.
* They are native JavaScript-array methods.
* The capability of taking a function that it can invoke is what makes it a higher-order function.

### Basic Example, `.map()`

```javascript
function prefixWordWithUnderscore(word) {
	return `_${word}`
}

const words = ['coffee', 'apple', 'orange', 'phone', 'starbucks']
words.map(prefixWordWithUnderscore) // ​​​​​[ '_coffee', '_apple', '_orange', '_phone', '_starbucks' ]​​​​​
```

### Multiple Variations

Using Higher-Order Functions to Support Multiple Variations of an Operation. Create a HOF so we can use it to create more variations of a desired operation.

```javascript
function utilizePrefixer(prefix) {
	return function(word) {
		return `${prefix}${word}`
	}
}

const withMoneySign   = utilizePrefixer('$'),
	  tenDollars      = withMoneySign('9.99');

const withCompanyName = utilizePrefixer('China'),
	  formHeader      = withCompanyName(' is my Country');

tenDollars // $9.99​​​​​
formHeader // ​​​​​China is my Country
```

### Internal State

#### 👎🏻 Example, traditional way:

```javascript
var myHOF = function (options) {
	const state = options // ​​​​​{ name: 'bobby', favoriteFood: 'steak' }​​​​​

	return function(args) { // { country: 'United States' }
		return function(fn) { // [λ]​​​​​ | prepareWithArgs(...) { ... }
			return fn(state, args) // { name: 'bobby', favoriteFood: 'steak' } | { country: 'United States' }
		}
	}
} // Callback hells

var baseData = {
	name         : 'bobby',
	favoriteFood : 'steak'
}

var anotherData = { country: 'United States' }

const prepare = myHOF(baseData);

const prepareWithArgs = prepare(anotherData)

const finalize = prepareWithArgs(function (state, options) {
	return Object.assign(state, options)
})

finalize // { name: 'bobby',​​​​​ favoriteFood: 'steak', country: 'United States' }​​​​​
```

#### 👍🏻 Example, ES6+ with Currying:

```javascript
var myHOF = options => (...args) => fn => fn(options, ...args)

var baseData = {
	name         : 'bobby',
	favoriteFood : 'steak'
}

var anotherData = { country: 'United States' }

const finalize = myHOF(baseData)(anotherData)(( state, options ) => ({ 
	...state,
	...options
}))

finalize // { name: 'bobby',​​​​​ favoriteFood: 'steak', country: 'United States' }​​​​​
```

### Composition

A practical sample of pub/sub pattern.

```javascript
const frogs = [
	{
		name: 'bobTheFrog',
		age: 2,
		gender: 'male',
		favoriteFood: 'fly',
		weight: 5,
	}, {
		name: 'lisaTheFrog',
		age: 3,
		gender: 'female',
		favoriteFood: 'fly',
		weight: 1,
	}, {
		name: 'sallyTheFrog',
		age: 10,
		gender: 'female',
		favoriteFood: 'caterpillar',
		weight: 20,
	}, {
		name: 'mikeTheFrog',
		age: 1,
		gender: 'male',
		favoriteFood: 'worm',
		weight: 7,
	}, {
		name: 'georgeTheFrog',
		age: 7,
		gender: 'male',
		favoriteFood: 'fly',
		weight: 28,
	}, {
		name: 'kellyTheFrog',
		age: 3,
		gender: 'female',
		favoriteFood: 'ladybug',
		weight: 3,
	}
]

var createFilterers = (function () {
	const _filters = {
		ids: [],
		fns: {},
	}

	return {
		addFilter(name, fn) {
		// addFilter: function(name, fn) {
			_filters.ids.push(name)
			_filters.fns[name] = fn
		},
		removeFilter(name) {
		// removeFilter: function(name) {
			const index = _filters.ids.indexOf(name)
			if (index !== -1) _filters.ids.splice(index, 1)
			delete _filters.fns[name]
		},
		filter(arr) {
		// filter: function(arr) {
			// Start filtering main processing
			return arr.reduce((acc, item) => {
				for (let index of _filters.ids) {
					const _filter = _filters.fns[index];
					if (!_filter(item)) {
						return acc;
					}
				}
				return acc.concat(item);
			}, [])
		},
	}
})()

createFilterers.addFilter('fat-frogs', frog => frog.weight >= 8)

createFilterers.addFilter('male-frogs', frog => frog.gender === 'male')

createFilterers.filter(frogs)
```

## Hook

### What

In computer programming, the term hooking covers a range of techniques used to alter or augment the behavior of an operating system, of applications, or of other software components by intercepting function calls or messages or events passed between software components.

### Why&#x20;

* Reusability, extendable, and flexibility.
* Hooks are not a native implementation, looks like callbacks.
* Hooks intercept the process and may interrupt the normal process.

### Basic Example

```javascript
// continue previous example
// In this sample, we use hook to supervise data change
// Actually, the pub/sub pattern itself is an entire hook

const frogs = [
	{
		name: 'bobTheFrog',
		age: 2,
		gender: 'male',
		favoriteFood: 'fly',
		weight: 5,
	}, {
		name: 'lisaTheFrog',
		age: 3,
		gender: 'female',
		favoriteFood: 'fly',
		weight: 1,
	}, {
		name: 'sallyTheFrog',
		age: 10,
		gender: 'female',
		favoriteFood: 'caterpillar',
		weight: 20,
	}, {
		name: 'mikeTheFrog',
		age: 1,
		gender: 'male',
		favoriteFood: 'worm',
		weight: 7,
	}, {
		name: 'georgeTheFrog',
		age: 7,
		gender: 'male',
		favoriteFood: 'fly',
		weight: 28,
	}, {
		name: 'kellyTheFrog',
		age: 3,
		gender: 'female',
		favoriteFood: 'ladybug',
		weight: 3,
	}
]

let hook = {
	prevState: {
		name: '',
		data: null
	},
	state: {
		name: '',
		data: null
	},
};

hook.before = (state, result) => {
	hook.prevState.name = name;
	hook.prevState.data = result;
}

hook.call = (state, result) => {
	hook.state.name = state;
	hook.state.data = result
}

var createFilterers = (function () {
	const _filters = {
		ids: [],
		fns: {},
	}

	return {
		addFilter(name, fn) {
			_filters.ids.push(name);
			_filters.fns[name] = fn;

			// set hook
			hook.before(name, hook.state.data)
		},
		removeFilter(name) {
			const index = _filters.ids.indexOf(name)
			if (index !== -1) _filters.ids.splice(index, 1)
			delete _filters.fns[name]
		},
		filter(arr) {
			return arr.reduce((acc, item) => {
				for (let index of _filters.ids) {
					const _filter = _filters.fns[index];
					if (!_filter(item)) {
						return acc;
					}
					// hook.call()
				}

				hook.call('state', acc.concat(item))
				return acc.concat(item);
			}, [])
		},
	}
})()

createFilterers.filter(frogs) 
hook //? check hook's status

createFilterers.addFilter('fat-frogs', frog => frog.weight >= 8)
hook //? check hook's status
createFilterers.filter(frogs)

createFilterers.addFilter('male-frogs', frog => frog.gender === 'male')
hook //? check hook's status
createFilterers.filter(frogs)
```

{% hint style="info" %}
Reference: [https://code-boxx.com/vanilla-javascript-hooks/](https://code-boxx.com/vanilla-javascript-hooks/)
{% endhint %}
