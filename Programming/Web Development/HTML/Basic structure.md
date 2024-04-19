# Basic structure

All [HTML](HTML.md) documents have the same basic structure. The "homepage" of every website is called `index.html`, because web servers look for this file by default when the site gets accessed. Every HTML document contains some default (boilerplate) code with different [elements](Elements%20and%20Tags.md), which looks like this:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title></title>
    <link href="css/style.css" rel="stylesheet" />
  </head>

  <body></body>
</html>
```

## DOCTYPE

Every HTML document starts with a `<!DOCTYPE>` declaration, which basically tells the browser what version of HTML it has to use to render the content.

## HTML element

The `<html>` element is known as the root of the document, meaning that every other element is a descendant (or child) of this element.

## Head element

The `<head>` element contains different metadata about the page, as well as other information needed so the browser can render the page correctly

### Meta element

The `<meta>` element is used to specifically define metadata for the page, like the charset.

### Title element

The `<title>` element defines the title of the page, which will also be displayed in the browser tab

### Link element

The `<link>` element is used to link to different external resources, most commonly used to link to a [CSS](CSS.md) file which contains styling.

## Body element

The `<body>` element contains all the content that will be visible on the page.