# CSS

CSS (Cascading Style Sheets) is a style sheet language primarily used in [web development](../basics/web_development.md) to control the visual appearance of [HTML](../html/html.md) documents. It is responsible for the positioning, the visual styling and the displaying on the screen or other media types (PC, phone...). Developers use CSS to create visually attractive and responsive websites, it can even be used for simple animations.

## Syntax

CSS is used to define different styling rules. A rule is made up of a **selector** and a list of **properties** and their assigned **values**.

![](../../../images/css_syntax.png)

### Selectors

Selectors are used to refer to the [HTML elements](../html/html_elements_tags.md) to which the rules will apply. A selector can be the name of an element, or its class or ID [attributes](../html/html_attributes.md):

```css
div {
	color: white;
}

.container {
	color: red;
}

#title {
	color: green;
}
```

It is also possible to apply rules to multiple elements at the same time by using multiple selectors:

```css
/* This rule targets all elements which have either the 'read' or the 'unread' class */

.read,
.unread {
	background-color: white;
	color: black;
}
```

For a more precise selection, selectors can also be chained together:

```css
/* Only elements which have both the 'section' and the 'title' class will be targeted */

.section.title {
	font-size: 1.3em;
	color: red;
}
```

Even more selections can be made by using [CSS combinators](css_combinators.md).


### Properties

Properties define the actual styles that will be applied to the selectors. They are used to apply different styles such as:
- Colors
- Fonts
- Width and height
- Positioning
- etc