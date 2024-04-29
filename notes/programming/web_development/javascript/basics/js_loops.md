# Loops

Loops allow to execute a block of code repeatedly until a specified condition is met. In [JavaScript](javascript.md) there are two types of loops: the `for` loop and the `while` loop.

## The for loop

The `for` loop is mainly used when the amount of iterations (loop cycles) is already known, for example when doing something to every item of a collection like an [array](../objects/arrays/js_arrays.md), or when doing an action for a predefined amount of times.

The default syntax for a `for` loop looks like this:

```js
for(initializer; condition; final-expression) {
	// code to run
}
```

The default `for` loop takes in three parameters:
- **Initializer** - The initializer is usually a [variable](js_variables.md) set to a number, which takes track of the loop cycles (how many times it ran already) Since it's a normal variable, it can be accessed inside the loop if needed. Sometimes it's also called the **counter**.
- **Condition** - A condition that defines when the loop should stop. The condition usually includes a comparison to check if the counter has exceeded a certain value.
- **Final expression** - The final expression gets evaluated (executed) every time the loop went through a full iteration. It is usually used to increment (or in some cases decrement) the counter to bring it closer to the point where the condition is no longer `true`.

A real-world application for a `for` loop could look similar to this:

```js
const animals = ["dog", "cat", "cow", "sheep", "bird"];

for(let i = 0; i < animals.length; i++) {
	console.log(animals[i]);
}
```

### The for...of loop

Since `for` loops are often used to loop through a collection of items, there is a special syntax specifically for this purpose. It's called the `for...of` loop:

```js
const animals = ["dog", "cat", "cow", "sheep", "bird"];

for(const animal of animals) {
	console.log(animal);
}
```

### The for...in loop

The `for...in` loop is another special type of `for` loop. It is used to iterate over each key of an [object](../objects/js_objects.md):

```js
const user = {
	name: "John",
	age: 30,
};

for(const key in user) {
	console.log(user[key]);
}
```

## The while loop

The `while` loop is usually used when the number of iterations is not known beforehand. It evaluates as long as the given condition evaluates to `true`:

```js
while(condition) {
	// code to execute
}
```

The `while` loop works very similar to the `for` loop, with a few exceptions:
- The **initializer** has to be defined before the loop.
- The **final expression** has to be defined inside the loop directly rather than inside the parentheses. It has to execute some kind of logic that will eventually change the initializer so that the **condition** no longer evaluates to `true`.

A simplified real-world example could look like this:

```js
let loggedIn = false;

while(!loggedIn) {
	displayLoginPage();
	loggedIn = checkForLogin();
}
```

> [!note]
> This above example uses the **logical NOT operator** to change the value of the [conditional](js_conditionals.md).

### The do...while loop

It is not ensured that a `while` loop will iterate even once. This happens, when the condition evaluates to `false` beforehand:

```js
let condition = false;

while(condition) {
	// this will never run.
}
```

For this purpose, there is an alternation of the `while` loop called the `do...while` loop. This loop will always iterate at least once, even if the condition evaluates to `false` beforehand:

```js
let condition = false;

do {
	// this will happen atleast once, even if the conditon is 'false'
} while(condition);
```

## Exiting loops

It is possible to exit a loop before all iterations have been completed or the exit condition is not met yet. This can be done by using the `break` statement.

An example for this could be to iterate over a collection of items and stop when finding a specific item:

```js
const items = ["item0", "item1", "item2", "item3"];

for(const item of items) {
	if(item === "item1") {
		break;
	}

	console.log(item);
}

// Output:
// "item0"
```

In this example, the `break` statement will immediately exit the loop as soon as it arrives at `item1`.

## Skipping iterations

It is also possible to skip an entire iteration of the loop by using the `continue` statement.

This statement behaves similarly to the `break` statement, but instead of exiting the loop completely, it skips the current iteration and continues with the next one:

```js
const items = ["item0", "item1", "item2", "item3"];

for(const item of items) {
	if(item === "item1") {
		continue;
	}

	console.log(item);
}

// Output:
// "item0"
// "item2"
// "item3"
```