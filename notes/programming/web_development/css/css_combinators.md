# Combinators

Combinators allow to combine multiple selectors by using their relationships, allowing for more precise selections.

There are four different combinators in [CSS](css.md):

- Descendant selector (`' '`)
- Child selector (`>`)
- Adjacent sibling selector (`+`)
- General sibling selector (`~`)

## Descendant selector

The descendant selector `' '` matches all elements that are descendants of a specified element. They don't have to be direct children, they just have to be inside the element.

```css
div p {
	color: white;
	background-color: black;
}
```

```html
<body>
	<!-- This won't be selected -->
	<p>Outside the div</p>

	<div>
		<!-- This will be selected -->
		<p>Inside the div</p>
		<section>
			<!-- This will also be selected -->
			<p>Deeper inside</p>
		</section>
	</div>
</body>
```

## Child selector

The child selector `>` selects all elements that are **direct children** of a parent element. Elements nested deeper inside the parent **won't be selected**.

```css
div > p {
	color: white;
	background-color: black;
}
```

```html
<div>
	<!-- This will be selected -->
	<p>Inside the div</p>
	<section>
		<!-- This won't be selected -->
		<p>Deeper inside</p>
	</section>
</div>
```

## Adjacent sibling selector

The adjacent sibling selector `+` selects an element that is directly after a specified element. *Adjacent* means *immediately following* in this case. The two elements must have the same parent.

```css
div > p {
	color: white;
	background-color: black;
}
```

```html
<section>
	<p>text 1</p>  <!-- not selected -->
	
	<div></div>
	<p>text 2</p>  <!-- selected -->
	<p>text 3</p>  <!-- not selected -->
</section>
```

## General sibling selector

The general sibling selector `~` selects all next siblings of a specified element. They don't have to be direct directly following siblings, but they have to be somewhere after the specified element.

```css
div ~ p {
	color: white;
	background-color: black;
}
```

```html
<section>
	<p>text 1</p>  <!-- not selected -->
	
	<div></div>
	<p>text 2</p>  <!-- selected -->
	<p>text 3</p>  <!-- selected -->
	
	<section></section>
	<p>text 4</p>  <!-- selected -->
</section>
```