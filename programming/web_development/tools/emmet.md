# Emmet

Emmet is a powerful extension available for many text editors and IDEs, which allows to speed up [HTML](html.md) coding by the use of simple snippets. The snippets use [CSS](css.md)-like syntax and can be used to create big and complex nestings of tags really fast. It also allows fast assignment of classes and IDs while writing the snippets. If used properly, Emmet is a really powerful tool which can help code much faster.

## Examples

Generating an unordered list containing multiple list items with hyperlinks:

```
ul>li*4>a>
```

```html
<ul>
	<li><a href=""></a></li>
	<li><a href=""></a></li>
	<li><a href=""></a></li>
	<li><a href=""></a></li>
</ul>
```

Generating a div containing a header and a paragraph, each with a class, an ID or both:

```
div.container>h2#section-title+p.content#section-text>
```

```html
<div class="container">
	<h2 id="section-title"></h2>
	<p class="content" id="section-text"></p>
</div>
```