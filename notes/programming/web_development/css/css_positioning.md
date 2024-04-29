# Positioning in CSS

[CSS](css.md) provides a total of five "positioning modes" which define how an element will be placed on the page:
- `static`
- `relative`
- `absolute`
- `fixed`
- `sticky`

The positioning mode of an element can be set by setting the `position` property to one of the above values.

## Static positioning

Static positioning is the default positioning mode for all elements. This mode tells the element to follow the default document flow.

## Relative positioning

The relative positioning mode behaves almost the same as static positioning. The only difference is that it can be displaced relative to its normal position by using the properties `top`, `right`, `left` and `bottom`. 

However, relative positioning is generally not used for such displacement. Instead, it's used to create containers for elements that use absolute positioning.

## Absolute positioning

Absolute positioning allows to position an element anywhere on the page. Elements that are placed absolutely are removed from the default document flow. They can be positioned using `top`, `right`, `left` and `bottom` without disturbing the default document flow.

By default, an absolutely positioned element will be placed in relation to the viewport, so `top: 0;` and `left: 0;` will place it in the upper left corner.

When the parent of an absolutely positioned element is positioned either relative, fixed or sticky, the element will be placed in relation to its parent.

## Fixed positioning

Similar to absolute positioning, fixed elements are removed from the document flow and can be placed using `top`, `right`, `left` and bottom. The differences are, that they will always be positioned relative to the viewport and they will stay in their position, even if the user scrolls. This positioning mode is mainly used for things like navigation bars and floating chat bars.

## Sticky positioning

Sticky positioning combines both relative and fixed positioning. By default, a sticky element will follow the default page flow, but once the user scrolls past it, it will be removed from the default flow and stay in a defined position.