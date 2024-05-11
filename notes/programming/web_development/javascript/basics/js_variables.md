# JavaScript variables

Like any other programming language, [JavaScript](javascript.md) has variables to store data and to access it in your program.

There are three ways to create (declare) variables in JavaScript:

- `var` is used to create mutable variables, meaning their value **can** be reassigned
- `let` is also used to create mutable variables
- `const` is used to create a constant variable, meaning their value **can't** be reassigned. Creating an [array](../arrays/js_arrays.md) or [object](../objects/js_objects.md) with `const` doesn't actually create a constant array/object, it creates a constant reference to them. The properties of the created array/object can still be changed.

## Declaring variables

Variables are declared by using one of the above keywords, followed by the variable name and a value assignment using `=`:

```js
var x = "hello world";
let y = 1;
const z = true;
```

When using `var` and `let` it is also possible to assign a value at a later point in the program:

```js
var x;
let y;

// some logic

x = 1;
y = 2;
```

When using `const` the value assignment has to happen immediately:

```js
const x = 1; // Ok
const y; // SyntaxError: missing = in variable declaration
```

The values of `var` and `let` variables can be reassigned at a later point in the program, the values of `const` variables can't:

```js
var a = 1;
let b = "hello";
const c = true;

a = 2; // Ok
b = "bye"; // Ok
c = false; // TypeError: invalid assignment to const 'c'
```

`let` and `const` are relatively new methods to declare variables in JavaScript and it's recommended to use them over `var`. Using `var` should be avoided as much as possible. The main reason to use `let` and `const` over `var` is their different [scoping](js_scope.md) behavior.

## Variable name limitations

There are certain limitations when creating variable names:
- **Naming conventions**: Variables should have meaningful and descriptive names to make code more readable and maintainable. When using multiple words for a name, either `camelCase` or `snake_case` should be used. Only one of these styles should be used in a project and they shouldn't be mixed up.
- **Starting characters**: Variable names must start with a letter, an underscore or a dollar sign. They can't start with a number.
- **Allowed characters**: Variable names can include letters, numbers, underscores and dollar signs. Other special characters, for example Unicode characters are possible, but should not be used to avoid confusion.
- **Reserved words**: Reserved language keywords (such as `let`, `const`, `for`...) can not be used as variable names.
- **Case sensitivity**: Variable names in JavaScript are case-sensitive. `myVar`, `MyVar` and `myvar` would be treated as three different variables.