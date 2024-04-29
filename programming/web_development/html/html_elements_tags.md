# Elements and Tags

All [HTML](html.md) pages consist of different types of **elements**. An element is basically a piece of content wrapped inside an opening and closing **HTML tag**.

An opening Tag consists of a keyword enclosed by angled brackets `<>`. A closing tag looks the same, but has a slash before the keyword `</>`. The content of the element is placed between the opening and the closing tag.

An example of a full paragraph element would look like this:

```html
<p>This is a paragraph</p>
```

There are many different predefined tags in HTML. A full list can be found [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

Some of the most important tags are:


| Tag               | Description                                                                                                                                          |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `<html>`          | Root element of the document                                                                                                                         |
| `<head>`          | Contains document metadata                                                                                                                           |
| `<link>`          | Links to external resources, mostly used to link to [CSS](../css/css.md) or icons                                                                    |
| `<body>`          | Contains all the visible content of the page                                                                                                         |
| `<div>`           | Generic container to group content                                                                                                                   |
| `<header>`        | Special container for the page header content                                                                                                        |
| `<main>`          | Special container for the main content of the page                                                                                                   |
| `<footer>`        | Special container for footer content                                                                                                                 |
| `<h1>` ... `<h6>` | Different levels of section headers. `<h1>` is the most important, `<h6>` the least                                                                  |
| `<p>`             | Generic text paragraph                                                                                                                               |
| `<ul>`            | Unordered list, rendered as bulleted list                                                                                                            |
| `<ol>`            | Ordered list, rendered as numbered list                                                                                                              |
| `<li>`            | List items inside of an unordered or ordered list                                                                                                    |
| `<a>`             | Hyperlink to another page, email, location in the current page...                                                                                    |
| `<img>`           | Displays an image on the page                                                                                                                        |
| `<button>`        | Creates a clickable button                                                                                                                           |
| `<script>`        | Used to embed [JavaScript](../javascript/basics/javascript.md) code either directly in the HTML document, or to link to an external JavaScript file. |