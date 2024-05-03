# Advanced selectors

[CSS](css.md) provides more advanced selectors for even more precise selection in addition to the default selectors and [combinators](css_combinators.md). These are also known as **pseudo-selectors**.

These pseudo-selectors can be categorized in two groups: **pseudo-elements** and **pseudo-classes**.

## Pseudo-classes

Pseudo-class selectors are prefixed with a single colon `:` and target existing [HTML elements](../html/html_elements_tags.md) that are in a specific state, e.g. the currently active input field or a button being hovered over by the mouse cursor.

There are many different pseudo-classes which can be grouped based on their use cases, so this note will only cover some basic ones. A full list can be found [here](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes).

### Tree-structural pseudo-classes

These pseudo-classes relate to the location of an element within the document tree.

- `:root`: Represents the root element of the document, similar to the `html` element, but with higher specificity. This is generally the place to define *global* CSS rules and [custom properties](css_custom_properties.md).
- `:first-child`: Matches an element that is the first of its siblings.
- `:last-child`: Matches an element that is the last of its siblings.
- `:only-child`: Matches an element that has no siblings.
- `:empty`: Matches an element with no children.

### User-action pseudo-classes

These pseudo-classes can be used to make elements more dynamic and interactive. They usually require some sort of user interaction to apply.

- `:hover`: Matches when the user hovers over the element with the mouse cursor.
- `:active`: Matches when the element is activated by the user, usually by clicking on it, e.g. when an input field is selected.
- `:focus`: Matches when the element has focus.

## Pseudo-elements

Pseudo-elements allow to style specific parts of a selected element. They are prefixed with double colons `::`.

There can only be one pseudo-element in a selector and it has to be the last part of the selector in which it appears. It's not allowed to use combinators or pseudo-classes after a pseudo-element.

Only some basic pseudo-elements will be covered in this note, a full list can be found [here](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements).

- `::before` and `::after`: Allow to add extra elements onto the page before and after the selected element respectively using CSS instead of HTML. A common use case for these is decorating text in various ways.
- `::marker`: Allows to style an `<li>` elements' list bullets or numbers.
- `::selection`: Changes the style of the highlighting when text is selected by the user.
- `::first-letter` and `::first-line`: target the first letter and the first line of some text respectively.

## Attribute selectors

Attribute selectors allow to select elements that have the specified [attributes](../html/html_attributes.md) set. There are three basic ways to use attribute selectors:

- `[attribute]`: Selects any element where the given attribute exists, independent of the value.
- `selector[attribute]`: Narrows the selection down so only specified elements with the provided attribute will be selected.
- `selector[attribute="value"]`: Only selects the element, if the attribute has a certain value.

```css
[src] {
	/* Any element with a "src" element will be selected */
}

img[src] {
	/* Only "img" elements with a "src" attribute will be selected */
}

img[src="logo.jpg"] {
	/* Only "img" elements, where the "src" attribute has a value of "logo.jpg", will
	be selected */
}
```

It is also possible to select elements where only a part of an attributes value has to match. This can be done by using syntax similar to [regular expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions):

- `[attribute^="value"]`: `^=` will match the string from the start.
- `[attribute$="value"]`: `$=` will match the string from the end.
- `[attribute*="value"]`: `*=` is a wildcard operator and will match anywhere in the string.