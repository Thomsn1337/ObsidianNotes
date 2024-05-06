# Positioning grid items

Regarding positioning in [CSS Grid](css_grid.md), there is some additional terminology that has to be cleared to understand all the parts of a grid:

- **Tracks** are the rows and columns that are either explicitly defined using `grid-template-columns` and `grid-template-rows` or implicitly created by the grid for any extra content.
- **Lines** are automatically created by the grid after the tracks have been defined, they can't be defined manually. They can be thought of like outlines for the tracks, each track has a start line and an end line. The lines are numbered from left to right and from top to bottom starting at 1. These line numbers are used for positioning.
- A **cell** is the space that is shared between a single row track and a single column track. By default each grid item will occupy a single cell and the items will be placed automatically. But it is possible to place items manually and to make them stretch out over multiple cells.

## Positioning

Grid items can be placed manually inside any grid cell, they can also span across multiple cells. They can be placed using `grid-column-start` and `grid-column-end` to choose the column of the cell and using `grid-row-start` and `grid-row-end` to choose the row of the cell. All of these properties take in the line numbers of the desired tracks' starting and ending lines.

```css
.container {
	display: grid;
	grid-template-columns: 50px 80ch;
	grid-template-rows: 50px 5rem;
	gap: 25px 40px;
}

.item {
	grid-column-start: 1;
	grid-column-end: 3;
	grid-row-start: 2;
	grid-row-end: 3;
}
```

To make things a bit less verbose, there are the `grid-column` and `grid-row` shorthands.

- `grid-column` combines `grid-column-start` / `grid-column-end`
- `grid-row` combines `grid-row-start` / `grid-row-end`

So the example above can be simplified using these shorthands:

```css
.container {
	display: grid;
	grid-template-columns: 50px 80ch;
	grid-template-rows: 50px 5rem;
	gap: 25px 40px;
}

.item {
	grid-column: 1 / 3;
	grid-row: 2 / 3;
}
```

## Grid areas

The `grid-area` shorthand combines `grid-row-start` / `grid-column-start` / `grid-row-end` / `grid-column-end` into a single property.

```css
.container {
	display: grid;
	grid-template-columns: 50px 80ch;
	grid-template-rows: 50px 5rem;
	gap: 25px 40px;
}

.item {
	grid-area: 2 / 1 / 3 / 3;
}
```

But this is not the only use case for this property. It is mainly used to position items by giving the grid cells literal names.

Using `grid-template-areas` on the grid container allows to give names to cells. Items can be placed in the cells by setting `grid-area` to an area-name on them. This allows to easily position items in a rather complicated layout.

```css
.container {
	display: grid;
	grid-template-columns: 50px 80ch;
	grid-template-rows: 50px 5rem;
	gap: 25px 40px;
	grid-template-areas:
		"header header"
		"sidebar main";
}

.header {
	grid-area: header;
}

.sidebar {
	grid-area: sidebar;
}

.main {
	grid-area: main;
}
```

When defining `grid-template-areas`, each line will represent one row and each word per line will represent one cell per row. Setting multiple neighboring cells to the same value will combine them, meaning that content assigned to that area will span across all these cells.