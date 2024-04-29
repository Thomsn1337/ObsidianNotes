# Array searching methods

[Arrays](js_arrays.md) provide different methods to search for elements within an array.

## Array.indexOf() and Array.lastIndexOf()

The `Array.indexOf()` method searches an array for a provided element value and returns the index of the first occurrence:

```js
const fruits = ["Apple", "Orange", "Lemon", "Cherry", "Orange"];

fruits.indexOf("Cherry");  // 3
fruits.indexOf("Orange");  // 1
```

The `Array.lastIndexOf()` method behaves like the `Array.indexOf()` method, but returns the index of the last occurrence:

```js
const fruits = ["Apple", "Orange", "Lemon", "Cherry", "Orange"];

fruits.lastIndexOf("Orange");  // 4
```

## Array.includes()

The `Array.includes()` method checks, if a provided element value is present in the array and returns a boolean value:

```js
const fruits = ["Apple", "Orange", "Lemon", "Cherry"];

fruits.includes("Lemon");   // true
fruits.includes("Banana");  // false
```

## Array.find()

The `Array.find()` method is used to find a specific element inside an array. It takes in a [callback function](../../async/js_callbacks.md) as its argument, which defines a test. The method returns the first value that passes the test:

```js
const myArray = [3, 7, 13, 25, 33];

let myNumber = myArray.find((number) => {
	return number > 20;
});

console.log(myNumber);  // 25
```

## Array.findLast()

The `Array.findLast()` method works similar to the `Array.find()` method, but it returns the last value that passes the test:

```js
const myArray = [3, 7, 13, 25, 33];

let myNumber = myArray.findLast((number) => {
	return number > 20;
});

console.log(myNumber);  // 33
```

## Array.findIndex()

The `Array.findIndex()` method works similar to the `Array.find()` method, but it returns the index of the first element that passes the test:

```js
const myArray = [3, 7, 13, 25, 33];

let myIndex = myArray.findIndex((number) => {
	return number > 20;
});

console.log(myIndex);  // 3
```


## Array.findLastIndex()

The `Array.findLastIndex()` method works similar to the `Array.findIndex()` method, but it returns the index of the last element that passes the test:

```js
const myArray = [3, 7, 13, 25, 33];

let myIndex = myArray.findIndex((number) => {
	return number > 20;
});

console.log(myIndex);  // 4
```