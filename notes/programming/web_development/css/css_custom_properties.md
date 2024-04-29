# Custom properties

Custom properties in [CSS](css.md), also known as *CSS variables*, are similar to [variables in JavaScript](../javascript/basics/js_variables.md) or any other programming language. They allow to define a CSS value in a single spot and reference it as many times as needed throughout the file. A value that is used multiple times can be edited in a single place instead of having to update every single instance separately.

Custom properties can be especially useful for defining a colorscheme that will be used throughout the project.

## Using custom properties

Custom properties are defined similar to normal CSS rule declarations:

```css
.container {
	--color-text: #4c4f69;
	--color-accent: #5c5f77;
}
```

These values can be accessed using the `var()` [function](css_functions.md):

```css
.container {
	--color-text: #4c4f69;
	--color-accent: #5c5f77;

	color: var(--color-text);
	border: 2px solid var(--color-accent);
}
```

### Naming conventions and rules

Custom properties follow some default naming conventions and rules:

- They are prefixed with a double hyphen `--`
- Custom property names are case sensitive, for example: `--color-text` and `--Color-Text` are two different values.
- Spaces are not valid characters
- `Kebab-Case` is used to separate multiple words

### Fallback values

The `var()` function accepts two parameters, even tough it might commonly be used with only one. The first parameter is the custom property that should be assigned. The second one is an optional fallback value. 

The fallback value will be used by the `var()` function if the custom property is invalid or not declared yet. It is also possible to assign *another* custom property as fallback value.

```css
.fallback {
	--color-text: white;

	background-color: var(--undeclared-property, black);
	color: var(--undeclared-again, var(--color-text, yellow));
}
```


## Scope

Custom properties are accessible for the selector they were declared in and **all of its direct descendants**. This principle is called **scope** and works similar to [scope in JavaScript](../javascript/basics/js_scope.md).

```html
<body>
	<p>Some text</p>  <!-- This element won't be styled -->

	<div>
		<p>Some other text</p>  <!-- This element will be styled -->
	</div>
</body>
```

```css
div {
	--color-text: red;
}

div > p {
	color: var(--color-text);
}
```

### The :root selector

Sometimes it might be useful to limit the scope of a custom property, or redefine the value of an already defined custom property for a tighter scope. Other times it's more useful to have access to custom properties from many different, unrelated selectors.

This can be easily achieved by defining them inside the `:root` [pseudo-class](css_advanced_selectors.md). Custom properties defined here are accessible throughout the entire file (similar to globally scoped variables in JavaScript).

```css
:root {
	--main-color: red;
}

.header {
	border: var(--main-color);
}

.container .element {
	color: var(--main-color);
}
```

This can be useful when defining the project's color scheme or a default font size that will be used by multiple different elements like paragraphs, lists etc.

It is also possible to assign classes to the `:root` pseudo-class. This can be an easy method to switch between colorschemes:

```css
:root {
	--main-color: white;
	--main-text-color: black;
}

:root.dark {
	--main-color: black;
	--main-text-color: white;
}
```

```js
const themeSwitcher = document.querySelector("button#theme-switcher");

themeSwitcher.addEventListener("click", () => {
	const root = document.documentElement;
	root.classList.toggle("dark");
});
```