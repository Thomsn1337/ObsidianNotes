# Advanced grid properties

[Grid](css_grid.md) defines quite some new properties, [functions](../css_functions.md) and even a new [unit](../css_units.md) to make working with them a bit easier.

## Repeat

It can be quite tedious to define multiple rows or columns, each with the same size.

```css
.container {
	display: grid;
	grid-template-columns: 150px 150px 150px 150px 150px;
	grid-template-rows: 200px 200px 200px;
}
```

To reduce such repetitive definitions, the `repeat()` function was introduced. This function is available for the grid template properties and does what the name implies: it repeats a given unit for a defined amount of times. This allows to define multiple rows or columns of the same size without having to type out each track's size individually.

```css
.container {
	display: grid;
	grid-template-columns: repeat(5, 150px);
	grid-template-rows: repeat(3, 200px);
}
```

## Fractional units

`fr` is a new unit introduced by CSS Grid which is known as fractional unit. It is used to create grid tracks with **dynamic sizes**, meaning that their size will change depending on the available viewport space.

`fr` will distribute the remaining space evenly. For example, if the maximum width of the container is `400px` and it has 4 columns, each assigned `1fr` as size, each track should be given `100px` of size. If one of the tracks is assigned `2fr`, it will be double the size than the other three.

```css
.container {
	display: grid;
	grid-template-columns: 1fr 3fr;
	grid-template-rows: 2rem 1fr;
}
```

Grid tracks with a fractional unit assigned as size will automatically resize, when the window size changes. There is no limit to how large they can get. However, they have a *smallest* size that they can't shrink past. This size is defined by the largest element inside the grid item. The track can shrink until the largest item's `min-content`, meaning the smallest size before it starts overflowing.

## Minimum and maximum track sizes

When using fractional units, by default content will grow as much as possible and shrink until `min-content` is reached. But most of the time, this is not the desired behavior and it is preferred to explicitly set minimum and maximum values.

The most simple way to achieve this is by using the `min()` and `max()` [functions](../css_functions.md) visited previously by providing them with a static and a dynamic value. This requires some inverted thinking:

### Maximum size

`min()` returns the smallest of its provided values. This can be used to define a maximum size for a track.

```css
.container {
	display: grid;
	grid-template-columns: repeat(5, min(250px, 1fr));
}
```

In this example, the columns will distribute the available space evenly (`1fr`), but they can't grow past `250px`.

### Minimum size

`max()` returns the biggest of its provided values. This can be used to define a minimum size for a track.

```css
.container {
	display: grid;
	grid-template-columns: repeat(5, max(100px, 1fr));
}
```

In this example, the columns will distribute the available space evenly (`1fr`), but they can't shrink past `100px`.

### Dynamic minimum and maximum

When using `min()` and `max()`, it is only possible to apply one size limit at the same time.

Because of this, CSS Grid introduces a new function called `minmax()`. It can only be used with four Grid properties:

- `grid-template-rows`
- `grid-template-columns`
- `grid-auto-rows`
- `grid-auto-columns`

This function is pretty straightforward and takes in two arguments:

1. The minimum size a track can have
2. The maximum size a track can have

While `min()` and `max()` require to use at least one dynamic value, it can make sense to use static values for both arguments of `minmax()` to define fixed boundaries.

```css
.container {
	display: grid;
	grid-template-columns: repeat(5, minmax(100px, 250px));
}
```

The tracks will take up even amounts of space, but won't grow or shrink past the boundaries of `100px` and `250px`.

Another approach is to use the previously visited `clamp()` function, which is not restricted to CSS Grid and can be used anywhere. Similar to `minmax()` it allows to set a minimum and maximum value, but it additionally allows to define a preferred value, which will most likely be dynamic.

```css
.container {
	display: grid;
	grid-template-columns: repeat(5, clamp(100px, 15%, 250px));
}
```

As long as none of the boundaries is reached, the tracks will distribute the space accordingly to the preferred value.

### auto-fit and auto-fill

The `auto-fit` and `auto-fill` values are a part of the `repeat()` function specification and are very useful for responsive layouts when used with the `minmax()` function. These values will dynamically change the number of grid tracks that will be defined by `repeat()`, depending on the available space.

```css
.container {
	display: grid;
	grid-template-columns: repeat(auto-fit, 200px);
}
```

This example will dynamically define the number of grid columns depending on the available space. Each column will have a width of `200px`. If there were only `200px` of space available in total, only one column would be created. If there were `600px` available, three columns would be created.

This behavior becomes especially useful when used in combination with the `minmax()` function. This allows to create dynamic amounts of grid tracks, with each track staying inside the boundaries defined by `minmax()`, without overflowing the grid container.

`auto-fit` will be set to the highest possible positive number that doesn't cause the grid to overflow. To define this, the browser will take the minimum value of the `minmax()` function and define, how many tracks of this size fit in the current grid space. Then it will grow them as much as possible without crossing the maximum value. If the available space changes, a new track will be added as soon as there is enough space for a minimum size track.

Generally, `auto-fit` will be the preferred value over `auto-fill`. In most cases, these values will behave the same. The difference is noticeable if there are less grid items than cells available per track:

- Using `auto-fit`, if there are not enough items to fill out the available space, the items will simply grow to their maximum size and no new tracks will be added.
- Using `auto-fill`, new tracks will be added as soon as enough space is available, even if there are no more items to fill out the space.