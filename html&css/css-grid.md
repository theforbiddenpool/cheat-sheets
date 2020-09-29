Turn any HTML eleent into a grid container by setting `display: grid;`. The parent elements is called **container** and the children are called **items**.

`grid-template-columns` and `grid-template-rows` are used to define the grid's structure. The number of parameters indicates the number of columns/rows in the grid and the value the width of each column/row.
```css
.container {
  display: grid;
  grid-template-columns: 50px auto 1fr;
}
```
We can set the size of columns and rows with:
- normal CSS units (*e.g.* `px`, `em`);
- `fr` → sets the column/row to a fraction of the available space;
- `auto` → sets the column/row to the width or height to fit content automatically.

We can also limit the items size, using the function `minmax()`. The first value is the minimum size, and the second the maximum.
```css
.container {
  display: grid;
  grid-template-columns: 50px minmax(50px, 200px);
}
```

We can create a grid container within another using the display property on the item.

### Grip-Gap
To set the gap between the columns or rows we can use `grid-column-gap`, `grid-row-gap`, or the shorthand property `grid-gap`. If there are two values in `grid-gap` the first one sets the gap between the rows, and the second one the columns.
```css
.container {
  ...
  grip-gap: 1em 2em;
}
```

---
![CSS grid diagram](https://getflywheel.com/wp-content/uploads/2016/08/css-grid-layouts-grid-diagram.jpg)

### Control Spacing
To control the amount of columns/rows an item will consume, we can use `grid-column` and `grid-row`, respectively, in conjuction with the line numbers you want the item to start and stop at.
```css
.grid-item {
  grid-column: 1 / 3;
}
```

### Align Items
In CSS Grid, the content of each item is located in a box which is referred to as a cell. You can set the alignment of all cells in a grid container using the properties `justify-items` and `align-items`, or for each content's cell using the properties `justify-self` and `align-self`.
#### Values
Property | Values | Description
--- | --- | ---
`justify-self` | | align the content's position within its cell horizontally
| | `stretch`<sup>*</sup> | the content fills the whole width of the cell
| | `start` | aligns the content at the left of the cell
| | `center` | aligns the content in the center of the cell
| | `end` | aligns the content at the right of the cell
`align-self` | stretch, start, center, end | vertically align the contents of an item
`justify-items` | stretch, start, center, end | aligns all items horizontally
`align-items` | stretch, start, center, end | aligns all items vertically

## Area Templates
You can group cells of your grid together into an area and give the area a custom name using `grid-template-areas` on the container.
```css
.container {
  grid-template-areas:
    "header header header"
    "advert content content"
    "footer footer footer";
}
/** Merges the top three cells together into an area named header, etc. **/
```

Every word represents a cell and a every pair of `"` represents a row. You can use a period (`.`) to designate an empty cell in the grid.

After setting the areas, you can an item in the custom area using `grid-area` property on an item.
```css
.item1 { grid-area: header; }
```
If the grid doesn't have an areas template to reference, you can create an area on the fly.
```css
.item1 { grid-area: 1/1/2/4; }
/** h start / v start / h end / v end **/
```

## Creating Flexible Layouts
To avoid repetition, use the function `repeat()` function to create cells with the same size.
```css
grid-template-columns: repeat(100, 50px);
grid-template-rows: repeat(2, 1fr, 50px) 20px;
/** this translates into grid-template-columns: 1fr 50px 1fr 50px 20px; **/
```

We can also use `auto-fill` and `auto-fit` with `minmax()`:	
- `auto-fill` → automatically insert as many rows or columns of our desired size as possible. *e.g.* `repeat(auto-fill, minmax(60px, 1fr));`
- `auto-fit` → similar to `auto-fill`, but stops creating rows or columns when there are no more items, stretching the items to fit the size of the container. *e.g.* `repeat(auto-fit, minmax(60px, 1fr));`

We can use media-queries to rearrange the items on the grid as needed.

# Sources
[freeCodeCamp](https://www.freecodecamp.org/)\
[Flywheel - CSS Grid Diagram](https://getflywheel.com/layout/css-grid-layouts-how-to/)