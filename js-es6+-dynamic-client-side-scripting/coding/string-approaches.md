# String Approaches

## Check the parenthesis is balanced or not.

```javascript
let isBalancedParenthesis = (str) => {
    return !str.split('').reduce((uptoPrevChar, thisChar) => {
        if (thisChar === '(' || thisChar === '{' || thisChar === '[') {
            return ++uptoPrevChar;
        } else if (thisChar === ')' || thisChar === '}' || thisChar === ']') {
            return --uptoPrevChar;
        }
        return uptoPrevChar
    }, 0);
}

// Test Cases
isBalancedParenthesis("[()]{}{[()()]()}"); // returns true
isBalancedParenthesis("[{()()}({[]})]({}[({})])((((((()[])){}))[]{{{({({({{{{{{}}}}}})})})}}}))[][][]"); // returns true
isBalancedParenthesis("({(()))}}"); // returns false
```

## Attributes name format transformation.

```javascript
// Camel case to dash, e.q.: camelToDash -> ab-cd-ef
function camelToDash(str) {
	return str.replace(/([A-Z])/g, $1 => "-" + $1.toLowerCase());
}
console.log('camelToDash ->', camelToDash('camelToDash')); // ab-cd-ef

// Dash to camel case, e.q.: ab-cd-ef -> camelToDash
let dashToCamel = str => {
	return str.replace(/(\-[a-z])/g, $1 => $1.toUpperCase().replace('-', ''));
}
console.log('ab-cd-ef ->', dashToCamel('ab-cd-ef')); // abCdEf
```

## Trim

```javascript
/**
 * Trim
 * @param  {str}
 * @param  {type} 
 * type:  1: Any space  2: Space before and after  3: Space before 4: Space after
 * @return {String}
 */
export const trim = (str, type) => {
    type = type || 1
    switch (type) {
        case 1:
            return str.replace(/\s+/g, "");
        case 2:
            return str.replace(/(^\s*)|(\s*$)/g, "");
        case 3:
            return str.replace(/(^\s*)/g, "");
        case 4:
            return str.replace(/(\s*$)/g, "");
        default:
            return str;
    }
}
```

## Customize string transform functions

```javascript
/**
 * @param  {str} 
 * @param  {type}
 * type:  1:Capitalize  2:Lowercase  3:Case conversion  4:All uppercase  5:All lowercase
 * @return {String}
 */
export const changeCase = (str, type) => {
    type = type || 4
    switch (type) {
        case 1:
            return str.replace(/\b\w+\b/g, function(word) {
                return word.substring(0, 1).toUpperCase() + word.substring(1).toLowerCase();

            });
        case 2:
            return str.replace(/\b\w+\b/g, function(word) {
                return word.substring(0, 1).toLowerCase() + word.substring(1).toUpperCase();
            });
        case 3:
            return str.split('').map(function(word) {
                if (/[a-z]/.test(word)) {
                    return word.toUpperCase();
                } else {
                    return word.toLowerCase()
                }
            }).join('')
        case 4:
            return str.toUpperCase();
        case 5:
            return str.toLowerCase();
        default:
            return str;
    }
}
```

## Check password strength

```javascript
export const checkPwd = (str) => {
    var Lv = 0;
    if (str.length < 6) {
        return Lv
    }
    if (/[0-9]/.test(str)) {
        Lv++
    }
    if (/[a-z]/.test(str)) {
        Lv++
    }
    if (/[A-Z]/.test(str)) {
        Lv++
    }
    if (/[\.|-|_]/.test(str)) {
        Lv++
    }
    return Lv;
}
```

## Insert a new string in the string

```javascript
/**
 * Insert a new string in the string
 * @param {string} soure: source character
 * @param {string} index: The position of the inserted character
 * @param {string} newStr: The character to be inserted
 * @returns {string} returns the newly generated characters
 */
export const insertStr = (soure, index, newStr) => {
    var str = soure.slice(0, index) + newStr + soure.slice(index);
    return str;
}
```

## Hexadecimal color to RGB  RGBA string

```javascript
/**
 * Hexadecimal color to RGB \ RGBA string
 * @param {String} val hexadecimal color value
 * @param {Number} opa Opacity, value 0 ~ 1
 * @return {String} RGB or RGBA color value after conversion
 */
export const colorToRGB = (val, opa) => {

    var pattern = /^(#?)[a-fA-F0-9]{6}$/; // Hexadecimal color value verification rules
    var isOpa = typeof opa == 'number'; // Check if opacity is set

    if (!pattern.test(val)) { // If the value does not fit the rules, return a null character
        return '';
    }

    var v = val.replace(/#/, ''); // If there is "#", remove "#" first
    var rgbArr = [];
    var rgbStr = '';

    for (var i = 0; i < 3; i++) {
        var item = v.substring(i * 2, i * 2 + 2);
        var num = parseInt(item, 16);
        rgbArr.push(num);
    }

    rgbStr = rgbArr.join();
    rgbStr = 'rgb' + (isOpa ? 'a' : '') + '(' + rgbStr + (isOpa ? ',' + opa : '') + ')';
    return rgbStr;
}
```

## A popular fuzzbuzz question.

Write a loop and output 'fizz' everytime the `i` could be mod by **3**,\
output 'buzz' everytime the `i` could be mod by **5**,\
and output 'fuzzbuzz' everytime it could be mod by **the least common multiple**.

```javascript
// Complete following part
for (let i = 0; i < 100;) 
    console.log((++i % 3 ? '' : 'fizz') + (i % 5 ? '' : 'buzz') || i);
```

## Exclamify

```javascript
String.prototype.exclamify = n => `${this}${'!'.repeat(n)}`;

const testString = "hello";

console.log(testString.exclamify(3));
console.log(testString.exclamify(5));
```

## Find the Longest Word in a substring

```javascript
////////////////////////////////////////////////
// 1. Find the Longest Word With a `for` Loop //
////////////////////////////////////////////////

function findLongestWord1(str) {
	let strSplit = str.split(' '),
		longestWord = 0,
		result;

	for (let i = 0, len = strSplit.length; i < len; i++) {
		if (strSplit[i].length > longestWord) {
			longestWord = strSplit[i].length;
			result = strSplit[i]
		}
	}
	return result;
}
findLongestWord1("The quick brown fox jumped over the lazy dog");
```

```javascript
///////////////////////////////////////////////////////
// 2. Find the Longest Word With the `sort()` Method //
///////////////////////////////////////////////////////

function findLongestWord2(str) {
	let longestWord = str.split(' ').sort((a, b) => b.length - a.length);
	return longestWord.shift();
}
findLongestWord2("The quick brown fox jumped over the lazy dog");
```

```javascript
/////////////////////////////////////////////////////////
// 3. Find the Longest Word With the `reduce()` Method //
/////////////////////////////////////////////////////////

function findLongestWord3(str) {
	let longestWord = str.split(' ').reduce((longest, currentWord) => currentWord.length > longest.length ? currentWord : longest, "");
	return longestWord;
}
findLongestWord3("The quick brown fox jumped over the lazy dog"); 
```

## Check sentence is palindromes or not. (Regardless of Punctuation marks)

```javascript
//////////////////////////////////////////////////////
// 1. Check for Palindromes With Built-In Functions //
//////////////////////////////////////////////////////

function palindrome(str) {
  var re = /[\W_]/g;
  var lowRegStr = str.toLowerCase().replace(re, '');
  var reverseStr = lowRegStr.split('').reverse().join(''); 
  return reverseStr === lowRegStr;
}
palindrome("A man, a plan, a canal. Panama"); // Output: true
```

```javascript
//////////////////////////////////////////////
// 2. Check for Palindromes With a FOR loop //
//////////////////////////////////////////////

function palindrome2(str) {
 var re = /[^A-Za-z0-9]/g;
 str = str.toLowerCase().replace(re, '');
 var len = str.length;
 for (var i = 0; i < len/2; i++) {
   if (str[i] !== str[len - 1 - i]) {
       return false;
   }
 }
 return true;
}
palindrome2("A man, a plan, a canal. Panama"); // Output: true
```

```javascript
///////////////////////
// 3. JS HOF methods //
///////////////////////

// Check normal string.

function checkPalindrom(string) {
	return string == string.split('').reverse().join('');
}
checkPalindrom("A man, a plan, a canal. Panama"); // Output: false
checkPalindrom("amanap lanacanal panama"); // Output: true
```

## Longest Palindromic Substring

```javascript
const longestPalindrome = function (s) {
  const len = s.length;
  const dp = Array.from(new Array(len), () => new Array(len).fill(false));
  let res = '';
  for (let i = len - 1; i >= 0; i--) {
    for (let j = i; j < len; j++) {
      dp[i][j] = s.charAt(i) === s.charAt(j) && (j - i <= 2 || dp[i + 1][j - 1]);
      if (dp[i][j] && j - i >= res.length) {
        res = s.slice(i, j + 1);
      }
    }
  }
  return res;
};
```

## Reverse a String

```javascript
/////////////////////////////////////////////////
// 1. Reverse a String With Built-In Functions //
/////////////////////////////////////////////////
function reverseString1(str) {
	return str.split("").reverse().join("");
}
reverseString1("hello");
```

```javascript
//////////////////////////////////////////////////////
// 2. Reverse a String With a Decrementing For Loop //
//////////////////////////////////////////////////////
function reverseString2(str) {
	var newString = "";
	for (var i = str.length - 1; i >= 0; i--) {
		newString += str[i];
	}
	return newString;
}
reverseString2('hello');
```

```javascript
////////////////////////////////////////
// 3. Reverse a String With Recursion //
////////////////////////////////////////
function reverseString3(str) {
	return (str === '') ? '' : reverseString3(str.substr(1)) + str.charAt(0);
}
reverseString3("hello");
```
