# The module pattern - IIFE

Oftentimes, [factories](js_factory_functions.md) are not used to create many instances of an [object](js_objects.md). Instead, they are used to create a single instance of an object, that serves the purpose to wrap sections of code together, while having the convenience to hide private variables from the rest of the codebase.

This can be achieved by immediately invoking a function after its definition and assigning the returned object to a variable.

```js
const calculator = (function() {
	function add(a, b) {
		return a + b;
	}

	function subtract(a, b) {
		return a - b;
	}

	function multiply(a, b) {
		return a * b;
	}

	function divide(a, b) {
		return a / b;
	}

	return { add, subtract, multiply, divide }
})();

calculator.add(3, 5);  // 8
calculator.subtract(9, 2);  // 7
calculator.multiply(4, 5);  // 20
calculator.divide(15, 3);  // 5
```

This pattern is known as **IIFE** (immediately invoked function expression) or the **module pattern**. In this example, the anonymous factory function is invoked immediately after its definition and the return value is assigned to the `calculator` variable.

The main advantage of this pattern is the usage of [encapsulation](../../../basics/encapsulation.md). Code that purposes a specific function can be bundled into a single unit, allowing to only give selective access, so parts that don't need to be exposed to the rest of the program can be hidden away.

Wrapping parts of the program into their own **uniquely named** units leads to the usage of a principle called **namespacing**. Grouping multiple related properties and methods under a single *name* (in this case, object) helps preventing naming collisions as the program grows.