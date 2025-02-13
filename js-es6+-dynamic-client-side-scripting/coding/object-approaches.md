# Object Approaches

## Add missed attribute(s) to the object that is need, and assign them by the default value

```javascript
let arr = [{
	name: 'poojan',
	age: '30'
}, {
	name: 'Justin'
}]

function addMissingKey(arr, key, defaultVal) {
	for (let index of arr) {
		if (!index.hasOwnProperty(key)) {
			index[key] = arr[key] || defaultVal;
		}
	}
	return arr;
}

addMissingKey(arr, 'age', 'NA') 
// Output: 
​​/*
	[{
		name: 'poojan',
		age: '30'
	}, {
		name: 'Justin',
		age: 'NA'
	}]​​​​​
*/
```

## Check whether two objects have the same key value

```javascript
/**
 * Check whether two objects have the same key value
 * @param {Object} a: first object
 * @param {Object} b: the first object
 * @return {Boolean} same as true, otherwise false
 */
export const isObjectEqual = (a, b) => {
    var aProps = Object.getOwnPropertyNames(a);
    var bProps = Object.getOwnPropertyNames(b);

    if (aProps.length !== bProps.length) {
        return false;
    }

    for (var i = 0; i < aProps.length; i++) {
        var propName = aProps[i];

        if (a[propName] !== b[propName]) {
            return false;
        }
    }
    return true;
}
```

## Flatten a JavaScript Object

Flattening deeply nested object can be easily achieved by using recursive technique.

```javascript
// Sample input
let user = {
  name: "Vishal",
  address: {
    primary: {
      house: "109",
      street: {             
        main: "21",
        cross: "32"
      }
    }
  }
};

//output
{
  user_name: "Vishal",
  user_address_primary_house: "109",
  user_address_primary_street_main: "21",
  user_address_primary_street_cross: "32",
}
```

#### Algorithms:

1. Iterate over keys of the object
2. Append child key name into the parent key name
3. If the child key's value is an object again call the same function
4. Else assign key to the new value

```javascript
let flattendObj = {};
const flattenObject = (obj, keyName) => {
  Object.keys(obj).forEach(key => {
    let newKey = `${keyName}_${key}` 
    if (typeof obj[key] === "object") {
      // calling the function again
      flattenObject(obj[key], newKey);
    } else {
      flattendObj[newKey] = obj[key];
    }
  });
};

flattenObject(user, 'user')
console.log(flattendObj);
```

## How to Check if Object is Empty in JavaScript <a href="#ce2b" id="ce2b"></a>

Here’s a Code Recipe to check if an object is empty or not.

```javascript
const empty = {};
/* -------------------------
  Plain JS for Newer Browser
----------------------------*/
Object.keys(empty).length === 0 && empty.constructor === Object // true

/* -------------------------
  Lodash for Older Browser
----------------------------*/
_.isEmpty(empty) // true
```

{% embed url="https://medium.com/@samanthaming/how-to-check-if-object-is-empty-in-javascript-aeab2674eeb1" %}
