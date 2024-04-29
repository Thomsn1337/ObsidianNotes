# Conditionals

When writing programs, it is possible to perform different actions based on different decisions. This is what **conditional statements** are used for. Most of the times, these conditional statements are used together with [logical operators or comparisons](js_comparisons.md).

There are four conditional statements in [JavaScript](javascript.md):
- `if` - Only executes its block of code if a specified condition is `true`
- `else if` - Can be used **only** after an `if` condition. Specifies a new condition to test if the first one is `false`.
- `else` - Can be used after an `if` or `else if` statement. Gets executed if all conditions before it are `false`.
- `switch` - Alternative syntax for an `if - else if - else` block

## The if - else if - else block

The code inside an `if` statement only gets executed, if the provided condition is `true`:

```js
if(condition) {
	// only if condition === true
}
```

The `else if` statement specifies a new condition to test if the each before it is `false`:

```js
if(condition1) {
	// only if condition1 === true
}
else if(condition2) {
	// only if condition1 === false
	// and condition2 === true
}
```

The `else` statement gets used at the end of an `if - else if - else` block to define the actions that should happen, if all previous conditions are `false`:

```js
if(condition1) {
	// only if condition1 === true
}
else if(condition2) {
	// only if condition1 === false
	// and condition2 === true
}
else {
	// only if condition1 === false
	// and condition2 === false
}
```

### The ternary operator

The ternary operator `?` tests a condition and returns one value if it's `true` and another value if it's `false`:

```js
const value = condition ? "Value 1" : "Value 2";
```

In the above example:
- `value` will be "Value 1", if the condition evaluates to `true`.
- `value` will be "Value 2", if the condition evaluates to `false`.

The ternary operator can be used as a replacement for simple `if..else` statements, which only have two choices based on a single `true/false` condition. 

It *can* also be used for longer conditional statements, but most of the times `if - else if - else` blocks are easier to read and make the code more maintainable.

## The switch statement

The `switch` statement provides alternative syntax for an `if - else if - else` block. It is used to select one of many code blocks which should be executed. It should be used, if the expression used for the decision can have **many** different values.

The syntax for a `switch` statement looks like this:

```js
switch(expression) {
	case x:
		// code block
		break;
	case y:
		// code block
		break;
	default:
		// default code block
		// if none of the above values match
}
```

How it works:
- The provided `expression` gets compared with the values of each `case`.
- If there is a match, the associated code block will be executed.
- If there are multiple matches, only the first one will be executed.
- If there is no match, the `default` block will be executed.
- The `break` keyword at the end of each `case` is needed to exit the switch after the code block has been executed. It it was missing, other (unexpected) matches and/or the `default` block would be executed aswell.