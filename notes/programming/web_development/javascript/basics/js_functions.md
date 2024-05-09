# JavaScript functions

Like any other programming language, [JavaScript](javascript.md) allow to declare functions. A function can be thought of like a small bundle of code that can be reused multiple times inside the program. A function can take in parameters and can also return the result of an operation.

Functions can be used for code organization by logically grouping together parts of code which serve a specific task.

There are two ways of declaring functions in JavaScript:

```js
// The "traditional" way

function myFunc(param1, param2) {
	return param1 + param2;
}

console.log(myFunc(1, 2));
```

```js
// Arrow functions

const myFunc = (param1, param2) => {
	return param1 + param2;
}

console.log(myFunc(1, 2));
```

There are some differences between using normal function declarations and arrow functions:

- On normal functions, the context of [the `this` keyword](../objects/js_this_keyword.md) depends on how they are invoked. Arrow functions don't have their own `this` context, they inherit the `this` context from their surrounding scope.
- Normal functions have access to the `arguments` [object](../objects/js_objects.md), which contains all the arguments passed to the function. Arrow functions don't have their own `arguments` object, but they can access the `arguments` object of an enclosing non-arrow function.
- Normal functions can be used as [object constructors](../objects/js_object_constructors.md) to create new objects by using the `new` keyword. Arrow functions can't be used as constructors.
- When used as constructors, the `prototype` property of normal functions can be accessed to add properties and methods to the [prototype](../objects/js_object_prototype.md) of any object created by the constructor. This is not possible with arrow functions.