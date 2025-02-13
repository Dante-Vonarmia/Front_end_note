# Variables and Types

## Implicit coercion

### Explanation

{% embed url="https://dev.to/promhize/what-you-need-to-know-about-javascripts-implicit-coercion-e23#:~:text=Javascript%27s%20implicit%20coercion%20simply%20refers,feature%20that%20is%20best%20avoided." %}

### Examples

```javascript
console.log(0.1 + 0.2 === 0.3) // false 
console.log(1 + '2') // 12
console.log(1 - '2') // -1
console.log(1 * '2') // 2
console.log(1 % '2') // 1
```

## Write a swap function to exchange two value. Use methods as much as you know. (Probably 4 ways)

```javascript
// Exclusive OR
const swap = (a, b) => {
	b = a ^ b;
	a = b ^ a;
	b = a ^ b;
	return [a, b];
}

// Using a Temp Variable
const swap = (a, b) => {
	let tmp = a;
	a = b;
	b = tmp;
	return [a, b];
}

// Without using a temp variable
const swap = (a, b) => {
	a = a + b;
	b = a - b;
	a = a - b;
	return [a, b];
}

// Deconstructing
const swap = (a, b) => {
	return [a, b] = [b, a];
}
```
