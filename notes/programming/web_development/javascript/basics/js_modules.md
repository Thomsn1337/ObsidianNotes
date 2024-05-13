# ES6 modules

Modules in [JavaScript](javascript.md) (known as ES6 modules or ESM) allow to split the source code of a project into multiple files for better navigation and maintainability. Code written inside of a file can be made accessible by other files by **exporting** it. This content can be **imported** into other files, so it can be used inside of them.

One of the main benefits of splitting up code like this is code reusability. An example for this could be defining different utility functions in their own module. This allows to import parts of the module into other files and use them as needed.

In order to use exports and imports in a file, it has to be interpreted as a **module** by the runtime it runs in. In [HTML](../../html/html.md), this can be done by adding the `type="module"` attribute to the `<script>` tag. Modules that export values will automatically inherit this attribute once they are imported into another file flagged as module

## Exporting

Values can be exported from a module using the `export` declaration. Most types of values, like [variables](js_variables.md), [functions](js_functions.md) or [classes](../objects/js_classes.md) can be exported.

A module can have two different types of exports: **named exports** and **default exports**. There can be multiple named exports, but only a single default export per module.

**Named exports** can be created by using the `export` declaration followed by a named variable declaration, function declaration or class declaration. It is also possible to export multiple values that were declared elsewhere in the file at once by using `export { name1, name2, ... }`.

```js
// Exporting a single expression on definition 
export function myFunction() {
	/* ... */
}

const myVar = 0;
class myClass {
	/* ... */
}

// Exporting multiple expressions after they were defined
export { myVar, myClass }
```

It is also possible to rename values when exporting them using the `as` keyword.

```js
function myFunction() {
	/* ... */
}

export { myFunction as renamedFunction }
```

**Default exports** allow any type of expression. They can also be used together with anonymous function or class declarations.

```js
export default function() {
	console.log("Hello World");
}
```

Named exports are commonly used to export multiple values from a single module. When importing a module this module, named exports must be referred with their exact name. Default exports are used when there is only a single value to be exported. This can then be imported using any name, it doesn't have to be the exact name of the export.

## Importing

The `import` statement is used to import values exported by another module. Imports have to happen on the [top level scope](js_scope.md) of a module.

Named imports are done using the `import { ... } from "..."` syntax. Inside the curly braces will be a list of value names that will be imported. These names have to match the exact names of the exports. The quotes will contain the path to the file from which the values will be imported.

```js
/* myModule.js */

function foo() {
	/* ... */
}

class bar {
	/* ... */
}

export { foo, bar }
```

```js
/* index.js */

import { foo, bar } from "./myModule.js";
```

It is also possible to rename imported values using the `as` keyword.

```js
import { reallyLongImportName as shortName } from "./myModule.js";
```

Importing a default export from another file allows to give it any desired name.

```js
/* myDefault.js */

export default function() {
	/* ... */
}
```

```js
/* index.js */

import myDefault from "./myDefault.js";
```

Since a single module file can have a default export and multiple named exports at the same time, they can also be imported using a single `import` statement. In this case, the default import has to be defined first, followed by the list of named imports.

```js
import myDefault, { foo, bar } from "./module.js";
```