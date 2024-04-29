# Units in CSS

There are many different units that can be used to define different sizes in [CSS](css.md). They can be categorized in **absolute units**, which are the same in any context, and **relative units**, which can change based on their context.

## Absolute units

Absolute units define the absolute (real, exact) value of an element. They are always the same, independent of the context.

The most used absolute unit is `px`. It defines the size of an element in pixels. It is also the **only** absolute unit that should be used in real world applications.

Other absolute units like `in` (inch) or `cm` (centimeter) should be avoided. These make more sense in a print setting, since they resemble physical units.

## Relative units

Relative units adjust their value based on their surrounding context. These should be preferred, because they allow for an easier creation of responsive layouts.

There are many different relative units, each with their own preferred and specific use cases.

### em and rem

Both `em` and `rem` refer to font sizes, but are also used to size other elements. They refer to the font size of a parent element and set their value according to it.

Sizing an element with `em` refers to the font size of the element itself (or its parent element, if explicitly set) and sets its value accordingly:

```html
<div class="parent">
	<p class="child">Hello world</p>
</div>
```

```css
.parent {
	font-size: 16px;
}

.child {
	font-size: 2em;
}
```

In the above example, the font size of `parent` was set to `16px`. Setting the font size of `child` using `em` refers to the parent and sets the value accordingly, in this case to `32px`. (`16px * 2em = 32px`)

`rem` does the same thing, but instead of referring to the parent element, it refers to the `root` element (either `:root` or `html`). The math works the same, but without the added complexity of having to keep track of each individual parent's font size. It is recommended to use `rem`, because many browsers allow to change the base font size. Using `rem` in this case allows to adjust the sizes of all elements accordingly.

### Line height units

The two relative units `lh` and `rlh` similar to `em` and `rem`. They are used to change the line height of an element, useful to space out text decorations like underlines.

They behave the same way like `em` and `rem`:

- `lh` is relative to the line height of the element itself (or its parent, if explicitly set)
- `rlh` is relative to the line height of the `root` element

### Percentages

Percentages always refer to the value of the parent element:

```html
<div class="parent">
	<p class="child">Hello world</p>
</div>
```

```css
.parent {
	width: 100px;
}

.child {
	width: 90%;
}
```

In the above example, the width of `child` will be set to 90% of the width of `parent`.

Percentages can be used for many different properties, like widths, heights, font sizes etc. Using a percentage to set a property will always refer to the according value of the parent element.

### Viewport units

The **viewport** is the area of the browser that displays the actual web page. This does **not** include things like the tab bar, the address bar or the bookmarks.

Viewport units are relative to the size of the viewport. Specifically, `1vh` is equal to `1%` of the viewport height and `1vw` is equal to `1%` of the viewport width.

Viewport units can be useful, but they **can cause issues on mobile browsers**, for example when the viewport height changes because of the keyboard coming up.

### ch

The `ch` unit refers to approximately the width of the character `0` in the applied font size. This unit can be especially useful to limit the maximum allowed characters per line in a paragraph.

## What unit to use

All of these units have their own specific use cases. There are some general rules of thumb which define the preferred use cases for each unit:

- **Font sizes** should always be set using `rem` for consistency.
- A good direction for setting **widths** are percentages in combination with setting a `max-width`. To limit the width of paragraphs, or the maximum characters per line, `ch` is a good option.
- When setting **heights**, it should first be questioned, if it is necessary to set a height. If it is, setting a `min-height` is preferred, so the container can still grow, if the content overflows. For this use case percentages, `em` or viewport units (keep in mind, viewport units can cause issues) can be an option.
- **Paddings and margins** should generally be set using `em` or `rem` for consistency. Generally `rem` should be used. Use cases for `em` can be padding for buttons, so the padding adjusts to the font size of the button itself, or margins around headings to give them extra whitespace in comparison to other text for better structure.
- **Media queries** should be defined using `em` for consistency across different browsers.
- `px` should only be used for smaller things like shadows or borders.