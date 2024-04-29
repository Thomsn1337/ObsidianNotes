# Array sorting methods

[Arrays](js_arrays.md) provide different methods for sorting capabilities.

## Array.sort() and Array.toSorted()

The `Array.sort()` method sorts the elements of an array in alphabetical order:

```js
const fruits = ["Apple", "Orange", "Lemon", "Cherry"];

fruits.sort();  // [ "Apple", "Cherry", "Lemon", "Orange" ]
```

The `Array.toSorted()` method does the same, but returns a new array instead of altering the existing one.

## Array.reverse() and Array.toReversed()

The `Array.reverse()` method reverses the order of the elements in an array:

```js
const fruit = ["Apple", "Orange", "Lemon", "Cherry"];

fruits.reverse();  // [ "Cherry", "Lemon", "Orange", "Apple" ]
```

Combining `Array.sort()` and `Array.reverse()` allows to sort an array in descending order:

```js
const fruit = ["Apple", "Orange", "Lemon", "Cherry"];

fruits.sort();
fruits.reverse();  // [ "Orange", "Lemon", "Cherry", "Apple" ]
```

The `Array.toReversed()` method does the same, but returns a new array instead of altering the existing one.

## Sorting

Because arrays in JavaScript can contain any [data type](../../basics/js_data_types.md), and even different types at the same time, the `Array.sort()` method has to work no matter which types are stored in an array. To do this, it defaults to converting all elements to strings before sorting. This approach works, but has unexpected side effects, for example when sorting numbers:

```js
const myArray = [35, 10, 4, 94, 67];

myArray.sort();  // [ 10, 35, 4, 67, 94 ]
```

This happens, because the numbers get converted to strings before sorting. Then they get sorted by [unicode order of characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters#Basic_Latin).

### The compare function

This can be solved by providing a [callback function](../../async/js_callbacks.md) to the `Array.sort()` method, which handles, how the individual items should be compared. This specific function is also referred to as **compare function**:

```js
const myArray = [35, 10, 4, 94, 67];

myArray.sort(function {
	return a - b;
});

console.log(myArray);  // [ 4, 10, 35, 67, 94 ]
```

The purpose of the compare function is to define an alternative sort order. It has to take in two arguments and should return either a negative, zero, or a positive value:

```js
function(a, b) {
	return a - b;
}
```

When the `Array.sort()` method compares two values, it sends them to the provided compare function. Then it sorts the values based on the return value of the function:

- If the return value is negative, `a` is sorted before `b`.
- If the return value is positive, `b` is sorted before `a`.
- If the return value is `0`, the order of the values won't be changed.

The compare function can also be used to define a custom sorting logic when sorting an array which stores objects:

```js
const cars = [  
  {type:"Volvo", year:2016},  
  {type:"Saab", year:2001},  
  {type:"BMW", year:2010}  
];

cars.sort((a, b) => {
	return a.year - b.year;
});
```