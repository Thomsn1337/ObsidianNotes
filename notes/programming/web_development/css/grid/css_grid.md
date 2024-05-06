# CSS Grid

Grid is another layout model in [CSS](css.md), similar to [Flexbox](css_flexbox.md). It allows to create multiple dynamic rows and columns and is thus commonly used for *two-dimensional* layouts, but can be used for *one-dimensional* layouts aswell.

Grid and Flexbox share many similarities. Both use parent containers with child items. They use similar property names for positioning and alignment. Most things that can be done using Flexbox can also be achieved using Grid, sometimes easier, but not always.

## Creating a grid

Similar to Flexbox, a Grid container is created by setting the `display: grid;` property on any [element](../../html/html_elements_tags.md). Doing this will turn the element itself into a **Grid container** and all of its direct children into **Grid items**.

```html
<!-- index.html -->

<div class="container">
	<div>Item 1</div>
	<div>Item 2</div>
	<div>Item 3</div>
	<div>Item 4</div>
</div>
```

```css
/* style.css */

.container {
	display: grid;
}
```

Just like Flexbox, It is possible to create grids inside other grids by turning a Grid item into another container.

Once a grid is created, it can be inspected using the browser's [developer tools](../../tools/dev_tools.md). Grid containers will have a special `Grid` badge next to them in the inspector. Clicking this badge will show an overlay with all the grid lines and their numbers on the page. 

### Columns and rows

Columns and rows define the space where the grid items can be placed. Specifically, they define the empty space between grid lines.

They are defined using the properties `grid-template-columns` and `grid-template-rows` respectively. These properties create the columns and rows using the list of values provided to them. The values can be of any [unit](css_units.md).

```css
.container {
	display: grid;
	grid-template-columns: 50px 80ch;
	grid-template-rows: 50px 5rem;
}
```

The `grid-template` shorthand combines these two properties and allows to define rows and columns in a single go.

```css
.container {
	grid-template: grid-template-rows / grid-template-columns; 
}
```

The values for the rows are defined before the slash `/`, the values for the columns are defined after it.

```css
.container {
	display: grid;
	grid-template: 50px 5rem / 50px 80ch;
}
```

### Implicit and explicit grids

The above example will create a `2x2` grid which has space for four items. If a fifth item was to be added inside the grid, it would automatically be placed on a new row below the last defined one.

When using `grid-template-columns` and `grid-template-rows`, the grid tracks are being defined **explicitly**. However, if the grid needs additional space for extra content, it will **implicitly** define new tracks by itself. These implicitly defined tracks don't carry over the size values that were defined explicitly. They can be defined separately using the `grid-auto-columns` and `grid-auto-rows` properties. 

By default, CSS Grid will add implicit rows for additional content. This means, that extra content will be added on in a vertical fashion. This behavior can be changed by setting `grid-auto-flow: column;`. This will change the behavior to implicitly define new columns and to add new content horizontally.

### Gap

The `gap` property allows to define a gap between rows and columns. This could also be achieved by setting a `margin` on the children, but depending on the layout of the grid items this method could possibly require multiple selectors. Instead, the `gap` can be set a single time on the container.

The `gap` property is a shorthand for the `column-gap` and `row-gap` properties. If given two values, it will first define the gap between rows, followed by the gap between columns.

```css
.container {
	display: grid;
	grid-template-columns: 50px 80ch;
	grid-template-rows: 50px 5rem;
	gap: 25px 40px;
}
```