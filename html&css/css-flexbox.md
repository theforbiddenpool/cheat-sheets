Adding `display: flex;` to an element turns it into a flex container. This makes it possible to align any children of that element into rows or columns.

![flex container diagram](https://www.w3.org/TR/css-flexbox-1/images/flex-direction-terms.svg)

### Flex-Direction
Sets the direction (row or column) of the children elements.
- Row → aligns the children horizontally
- Column → aligns the children vertically
#### Values
`row`, `column`, `row-reverse`, `column-reverse`

### Justify-Content
Tells CSS how to align and space out the flex items. It aligns items along the main axis. For rows, the main axis is a horizontal line and for columns it is a vertical line.
- Row → push items left or right
- Column → push items up or down
#### Values
Value | Description
--- | ---
`center` | center of the flex container.
`flex-start` | start of the flex container.
`flex-end` | end of the flex container.
`space-between` | center of the main axis, with extra space placed between the items. The first and last items are pushed to the very edge of the flex container.
`space-around` | similar to `space-between`, but the space is distributed around all items.

### Align-Items
Similar to `justify-content` property, but aligns to the cross axis, which is the opposite of the main axis.
- Row → push items up or down
- Column → push items left or right
#### Values
Value | Description
--- | ---
`flex-start` | start of the flex container
`flex-end` | end of the flex container
`center` | center
`stretch` | stretch the items to fill the flex container
`baseline` | align items to their baselines

### Justify-Items
It kicks in when we have multiple lines of content. It refers to the space in-between the rows or columns of content, and not the flex items themselves.
#### Values
The property values are the same as `justify-content`: `center`, `flex-start`, `flex-end`, `space-between`, and `space-around`.

### Flex-Wrap
By default, a flex container will fit all flex items together. With this property, you can tell CSS to wrap items - extra items move into a new row or column. The break point of where the wrapping happens depends on the size of the items and the size of the container.
#### Values
Value | Description
--- | ---
`nowrap`<sup>*</sup> | does not wrap items. Default setting
`wrap` | wrap items left-to-right (row), or top-to-bottom (column)
`wrap-reverse` | wrap items right-to-left (row), or bottom-to-top (column)

## Properties used on child elements
### Flex-Shrink & Flex-Grow
When set, it allows an item to shrink/expand if the flex container is too small/large. Items shrink when the width of the parent container is smaller than the combined width of all the flex items within it. The opposite happens with `flex-grow`.
#### Values
This property takes numbers as values. The higher the number, the more it will shrink compared to the other items in the container. It describes how much - in relation to all the other flex items - the item will grow or shrink.

### Flex-Basis
Specifies the initial size of the item before CSS makes adjustments with flex-shrink or flex-grow. The units are the same as other size properties (px, em, etc.).

### Flex Shorthand Property
Use `flex` to set all the above in the order: *`flex-grow` `flex-shrink` `flex-basis`*.
```css
flex: 1 0 10px;
```

The default property settins are `flex: 0 1 auto;`.

### Order
Used to tell CSS the order how flex items appear in the flex container. By default, items will appear in the same order they come in the source HTML.
#### Values
The property takes numbers as values, and negative numbers can be used.

### Justify-Self & Align-Self
Allows to adjust each item's alignment individually, instead of setting them all at once.
#### Values
Accepts the same values as `align-items` and `justify-items`, respectively, and will override any value set by them.

# Keywords
__Baseline__ → is a text concept. It's the line that the letters sit on.

# Sources
[freeCodeCamp](https://www.freecodecamp.org)