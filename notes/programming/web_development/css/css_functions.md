# Functions in CSS

Similar to programming languages, [CSS](css.md) provides functions. Functions are reusable pieces of code that take in values as arguments and perform specific tasks. But unlike other programming languages, CSS does not allow to create custom functions. Instead, it comes bundled with premade functions which can be used for most common styling problems.

This note will only cover some basic functions provided by CSS. A complete list can be found [here](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions).

## calc()

The `calc()` function can be used to perform basic arithmetical calculations on numerical values. Its power lies in the ability to mix different [units](css_units.md) in calculations by automatically converting them.

This function can be useful when used to create [custom properties](css_custom_properties.md) which depend on each other. It is also possible to nest multiple `calc()` statements inside each other

```css
:root {
	--header: 3rem;
	--footer: 60px;

	--main : calc(100vh - calc(var(--header) + var(--footer)));
}
```

## min()

The `min()` function can be useful when designing responsive websites. It takes in one or more arguments and returns the smallest value of the provided ones. It is commonly used with at least one absolute and at least one relative unit:

```css
#image {
	width: min(200px, 100%);
	height: min(200px, 100%);
}
```

In this example, if there are more than `200px` available around the `#image` element (which will most likely be inside a container of some sort), the `min()` function will return `200px`, since the evaluated value of `100%` will be bigger than that.

If the container around the `#image` element shrinks to a point where there is less than `200px` available, the `min()` function will return the evaluated value of `100%`, since it's smaller than `200px`.

This function allows to perform basic math inside of it:

```css
#image {
	width: min(200px, 100% - 2rem);
}
```

## max()

The `max()` function is the inverse of the `min()` function. When provided with a list of different values, it will return the largest one. It can be useful to define a *minimum* allowed value for a property, for example a minimum width that an element can't shrink past.

## clamp()

The `clamp()` function takes in three arguments:

```css
clamp(min, ideal, max)
```

- `min` is the minimum value the property can have.
- `ideal` will be the value as long as neither `min` nor `max` are exceeded. This will most likely be a relative unit.
- `max` is the maximum value the property can have.

This function can be used to create a responsive design that can't grow or shrink past a certain point.