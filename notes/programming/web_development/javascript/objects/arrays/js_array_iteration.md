# Array iteration methods

[Arrays](js_arrays.md) provide iteration methods, which allow to iterate over each element of an array and do something with it. All these methods take in a [callback function](../../async/js_callbacks.md) as argument.

## Array.forEach()

The `Array.forEach()` method calls a callback function once for each element:

```js
const numbers = [10, 6, 24, 65, 32];
let sum = 0;

numbers.forEach(n => {
	sum += n;
});

console.log(sum);  // 137
```

## Array.map()

The `Array.map()` method creates a new array by performing a function on each array element. It returns a new array and does not alter the original one:

```js
const numbers = [2, 4, 6, 8, 10];

const newNumbers = numbers.map((n) => {
	return n * 2;
});

console.log(numbers);     // [ 2, 4, 6, 8, 10 ]
console.log(newNumbers);  // [ 4, 8, 12, 16, 20]
```

## Array.filter()

The `Array.filter()` method calls a test function on each element and creates a new array containing the elements that pass the test:

```js
const numbers = [45, 9, 17, 33, 12, 4];

const newNumbers = numbers.filter((n) => {
	return n > 16;
});

console.log(numbers);     // [ 45, 9, 17, 33, 12, 4 ]
console.log(newNumbers);  // [ 45, 17, 33 ]
```

## Array.reduce()

The `Array.reduce()` method reduces the elements of an array to a single value by calling a function on each element. It doesn't change the original value and returns the single value:

```js
const numbers = [1, 2, 3, 4, 5];

let value = numbers.reduce((total, num) => {
	return total * num;
});

console.log(value);  // 120
```

Other than the other methods, the callback function of the `Array.reduce()` method takes in an additional argument: `total`. The value of `total` will be the return value of the last iteration. In the first iteration, its value will either be the first value of the array or an additional value provided to the method:

```js
const numbers = [1, 2, 3, 4, 5];

// The start value will be 1
// The first value of the array
let value = numbers.reduce((total, num) => {
	return total * num;
});

// The start value will be 2
// The value provided to reduce() after the callback
let value2 = numbers.reduce((total, num) => {
	return total * num;
}, 2);
```

## Array.every() and Array.some()

The `Array.every()` method checks if all elements of an array pass a test and returns a boolean value:

```js
const numbers = [45, 4, 9, 16, 25];  

let allOver18 = numbers.every((num) => {
	return num > 18;
});

console.log(allOver18);  // false
```

The `Array.some()` method checks if any of the elements of an array passes a test and returns a boolean value:

```js
const numbers = [45, 4, 9, 16, 25];  

let allOver18 = numbers.some((num) => {
	return num > 18;
});

console.log(allOver18);  // true
```