# Array sorting methods

[Arrays](js_arrays.md) provide different methods for sorting capabilities.

## Array.sort() and Array.toSorted()

The `Array.sort()` method sorts the elements of an array in alphabetical order:

```js
const fruits = ["Apple", "Orange", "Lemon", "Cherry"];

fruits.sort();  // [ "Apple", "Cherry", "Lemon", "Orange" ]
```

The `Array.toSorted()` method does the same, but returns a new array instead of altering the existing one.