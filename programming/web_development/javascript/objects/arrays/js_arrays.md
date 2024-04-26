# Arrays

An array is a fundamental data structure in [JavaScript](javascript.md) used to store multiple different values inside of a single variable. Often times they are considered a separate [data type](js_data_types.md), but in reality they are a specialized form of [object](js_objects.md). They behave like traditional arrays in other programming languages, but possess the characteristics of a JavaScript object. This means that they can have properties and methods attached to them, just like regular objects.

## Using arrays

Arrays are used to store larger amounts of related data inside of a single [variable](js_variables.md) instead of using a separate variable for each value:

```js
// Instead of this...
let car1 = "BMW";
let car2 = "Audi";
let car3 = "Toyota";

// ...this can be done
const cars = ["BMW", "Audi", "Toyota"];
```

Not only do arrays store multiple values inside of a single variable, they also allow to iterate over them and do something with each value, or to search for a specific value.

The elements inside an array are indexed starting from `0`. An element can be accessed by its index using **bracket notation**:

```js
cars[0];  // "BMW"
cars[1];  // "Audi"
cars[2];  // "Toyota"
```

Bracket notation is also used to change the value of a specific element:

```js
cars[1] = "Fiat";
console.log(cars);  // [ "BMW", "Fiat", "Toyota" ]
```

Arrays can store values of any type, even other arrays or objects. The values inside of an array also don't have to be of the same type:

```js
const myArray = [1, 2, "hello", true];
myArray[0] = {
	name: "John",
	age: 25,
};

myArray[1] = ["test", 1, 2];
```

Accessing the values inside of a nested array can be done by using **bracket notation**, accessing the values of an object inside of an array can be done by using **either bracket or dot notation**:

```js
myArray[1][0];     // Output: test
myArray[0].name;   // Output: John
myArray[0]["age"]; // Output: 25
```

## Array methods

Arrays have many different methods to interact with them. They can be categorized into [common methods](js_array_methods.md), [searching methods](js_array_search.md), [sorting methods](js_array_sorting.md) and [iteration methods](js_array_iteration.md).

> [!note] Callback functions
> Some array methods take in [callback functions](js_callbacks.md) as arguments. By default these functions expect three arguments:
> 
> - The item value
> - The item index
> - The array itself
>
> If only the item value is needed, the other two arguments can be omitted. 