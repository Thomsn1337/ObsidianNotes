# Comparisons

Comparisons are used to compare two or more values. They work the same way as in traditional math.

In [JavaScript](javascript.md) they are written like this:
- Greater/less than: `a > b`, `a < b`
- Greater/less than or equal: `a <= b`, `a <= b`
- Equals: `a == b` (double equals sign `==` means equality comparison, single equals `=` means value assignment)
- Not equals: `a != b`

Comparisons return a [boolean value](js_data_types.md):
- `true` if the comparison is correct
- `false` if the comparison is not correct

```js
console.log(2 > 1);   // true
console.log(3 == 4);  // false
console.log(3 != 1);  // true

// The result of a comparison can also be assigned to a variable:

let result = 6 > 2;
console.log(result);  // true
```

## String comparisons

When comparing two strings, JavaScript compares them letter-by-letter:

```js
console.log("Z" > "A");        // true
console.log("Glow" > "Glee");  // true
console.log("Bee" > "Be");     // true
```

To decide if a character is greater than another, JavaScript uses the [unicode order of characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters#Basic_Latin).

## Comparing different types

If two values of different type are compared using `==`, JavaScript will convert them to the same type before comparing:

```js
console.log("2" == 2);  //true
```

For boolean values `true` will become 1 and `false` will become 0:

```js
console.log(true == 1);   // true
console.log(false == 0);  // true
```

## Strict equality

Because of its default type conversion, the default equality operator `==` is also called the **loose equality operator**.

Because this loose equality check can often lead to problems, the **strict equality operator** `===` was introduced. It performs comparisons without converting the types of the values beforehand:

```js
console.log("0" === 0);   // false
console.log(1 === true);  // false
```

It is best practice to avoid using the loose equality operator `==` as much as possible.

## Boolean conversion

[Conditional statements](js_conditionals.md) convert their condition values to `boolean` in order to evaluate the condition:
- The number `0`, an empty string `""`, `null`, `undefined`, and `NaN` all become `false`. They are called `falsy` values.
- All other values become `true`, so they are called `truthy` values.

```js
if(0) {
	// 0 is falsy
	// this will never execute
}

if(1) {
	// 1 is truthy
	//this will always execute
}
```

## Logical operators

Logical operators are used to check if multiple conditions are met or to chain multiple comparisons together.

There are three logical operators in JavaScript:
- Logical AND `&&`
- Logical OR `||`
- Logical NOT `!`

### Logical AND

In classical programming, the logical AND operator `&&` returns `true` only if both operands are `truthy` values, and returns `false` otherwise:

```js
console.log(true && true);    // true
console.log(false && true);   // false
console.log(true && false);   // false
console.log(false && false);  // false
```

In JavaScript, `&&` looks for the first `falsy` value and returns it. If all values evaluate to `truthy`, the last value is returned.

```js
console.log(1 && "" && true);      // logs ""
console.log(1 && true && 2);       // logs 2
console.log(1 && 2 && null && 3);  // logs null
```

### Logical OR

In classical programming, the logical OR operator `||` returns `true` only if any of its operands is a `truthy` value, and returns `false` otherwise:

```js
console.log(true || true);    // true
console.log(false || true);   // true
console.log(true || false);   // true
console.log(false || false);  // false
```

In JavaScript, `||` looks for the first `truthy` value and returns it. If all values evaluate to `falsy`, the last value is returned.

```js
console.log(1 || 0);                  // logs 1
console.log(null || 1 || undefined);  // logs 1
console.log(undefined || null || 0);  // logs 0
```

### Logical NOT

The logical NOT `!` takes a single value as its argument and returns the inverse of its boolean value:
- Returns `false` for all `truthy` values
- Returns `true` for all `falsy` values

```js
console.log(!true);   // false
console.log(!1);      // false

console.log(!false);  // true
console.log(!null);   // true
```