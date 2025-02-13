# Mathematic Approaches

## Given a positive integer, sum it up till only one digit.&#x20;

For instance, 55555 - 25 - 7, return 7

```javascript
let n = 55555; // Any positive integer
function onlyOneDigit(n) {
	if (n === 0)
		return 0
	else
		return n % 9 || 9
}

console.log(onlyOneDigit(n)) // Output: 7
```

## A Fibonacci number (Memoization)

```javascript
const fib = (num) => {
  let a = 1,
    b = 1;
  for (let i = 1; i <= num; i++) {
    [a, b] = [b, a + b];
    console.log([a , b])
  }
  return b;
}

fib(5) // 13
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
```

```javascript
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

## Find out the largest number that could be generated from a  sorted array

```javascript
let largestNumber = function(nums) {
    const res = nums.map(String).sort((a,b) => b.concat(a) - a.concat(b)).join('')
    res.length > 1 && res.charAt(0) == '0' ? return '0' : return res;
}

largestNumber([3,30,34,5,9]) // output: 9534330
```

## Prime Mover

Have the function `PrimeMover(num)` return the nth prime number. \
The range will be from 1 to 10^4.

For example: \
if `num` is 16 the output should be **53** as 53 is the 16th prime number.

```javascript
Input: 9
Output: 23
Input: 100
Output: 541
```

```javascript
/*By Haolin Yang*/
let primeMover = (nth) => {
    let curRange = nth * 2;
    let count = -1;
    let flags = [];
    while (count < nth) {
        flags = sieveOfEratosthenes(curRange);

        count = flags.reduce((prev, cur) => {
            if (cur) return prev + 1;
            else return prev;
        }, 0);

        curRange *= 2;
    }

    for (let i = 0, tmp = 0; i < flags.length; i++) {
        const e = flags[i];
        if (e) tmp++;
        if (tmp == nth) return i;
    }
};

let sieveOfEratosthenes = (range) => {
    // mark all prime num [0,range]
    let flags = new Array(range + 1).fill(true);
    flags[0] = false;
    flags[1] = false;

    for (let i = 2; i <= range; i++) {
        const e = flags[i];
        if (e === true) {
            for (let j = i * i; j <= range; j += i) {
                flags[j] = false;
            }
        }
    }

    return flags;
};
// first 1000 prime num: https://primes.utm.edu/lists/small/1000.txt
console.log(primeMover(1000));
```
