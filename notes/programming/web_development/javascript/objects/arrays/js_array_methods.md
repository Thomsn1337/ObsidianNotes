# Array properties and methods

[Arrays](js_arrays.md) have many different properties and methods attached to them. These can be used to directly interact with an array.

## Array.length

The `Array.length` property contains the amount of items stored inside of the array (the length of the array):

```js
const myArray = [1, 2, 3, 4];
console.log(myArray.length);  // 4
```

## Array.toString()

The `Array.toString()` method converts the contents of the array into a string with the values being separated by commas:

```js
const fruits = ["Apple", "Banana", "Orange"];
console.log(fruits.toString());  // "Apple,Banana,Orange"
```

## Array.at()

The `Array.at()` method is an alternative to bracket notation for accessing values:

```js
const fruits = ["Apple", "Banana", "Orange"];

// These do the same
let fruit = fruits.at(1);    // "Banana"
let otherFruit = fruits[2];  // "Orange"
```

It is preferred to use bracket notation over this method to access array values, so it's not used very often.

## Array.join()

The `Array.join()` method behaves exactly like the `Array.toString()` method, but it allows to specify the separator:

```js
const fruits = ["Apple", "Banana", "Orange"];
console.log(fruits.join(" : "));  // "Apple : Banana : Orange"
```

## Array.pop() and Array.push()

The `Array.pop()` method removes the last element from an array and (optionally) returns its value:

```js
const fruits = ["Apple", "Banana", "Orange"];
const fruit = fruits.pop();

console.log(fruits);  // [ "Apple", "Banana" ]
console.log(fruit);   // "Orange"
```

The `Array.push()` method appends the provided element to the end of the array and (optionally) returns its new length:

```js
const fruits = ["Apple", "Banana", "Orange"];
const newLength = fruits.push("Kiwi");

console.log(fruits);     // [ "Apple", "Banana", "Orange", "Kiwi" ]
console.log(newLenght);  // 4
```

## Array.shift() and Array.unshift()

These methods behave like `Array.push()` and `Array.pop()`, but they operate at the start of the array.

The `Array.shift()` method inserts a new element at the start of the array and (optionally) returns the new length:

```js
const fruits = ["Apple", "Banana", "Orange"];
fruits.shift("Kiwi");

console.log(fruits); // [ "Kiwi", "Apple", "Banana", "Orange" ]
```

The `Array.unshift()` method removes the first element of the array and (optionally) returns its value:

```js
const fruits = ["Apple", "Banana", "Orange"];
fruits.unshift();

console.log(fruits): // [ "Banana", "Orange" ]
```

## Array.splice() and Array.slice()

The `Array.splice()` method takes in these arguments:

```js
Array.splice(start, amount, ...items);
```

- `start` - the starting index where items should be added or removed
- `amount` - the amount of items to be removed
- `...items` - all arguments after the `amount` define the new elements to be added

This method can be used to either add or remove items at a specified position of an array:

```js
// Remove items
const fruits = ["Apple", "Banana", "Orange"];
fruits.splice(1, 0);  // [ "Apple", "Orange" ]

// Add in new items
const fruits2 = ["Apple", "Banana", "Orange"];
fruits2.splice(2, 0, "Kiwi"); // [ "Apple", "Banana", "Kiwi", "Orange" ]
```

The `Array.slice()` method slices out a piece of an array and returns a new array. It takes in two indexes as its parameters, starting to slice at the first and going up to, **but not including**, the second:

```js
const fruits = ["Banana", "Lemon", "Orange", "Cherry"];
const citrus = fruits.slice(1, 3);

console.log(citrus); // [ "Lemon", "Orange" ]
```

> [!note]
> `Array.slice()` returns a new array and doesn't make any changes to the source array!