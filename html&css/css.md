# Selectors
| Selector | Example | Description |
| --- | --- | --- |
| Universal | `* {}` | applies to all elements in the document |
| Type | `h1, h2 {}` | matches element names |
| Class | `.note {}` or `p.note{}` | matches an element whose class attribute has a value that matches the one specified after the period symbol |
| ID | `#introduction {}` | matches an element whose id attribute has a value that matches the one specified after the pound or hash symbol |
| Child | `li > a {}` | matches an element that is a direct child of another |
| Descendant | `p a {}` | matches an element that is a descendent of another specified element, not just a direct child of that element |
| Adjacent Sibling | `h1+p {}` | matches an element that is the next sibling of another |
| General Sibling | `h1~p {}` | matches an element that is a sibling of another, although it does not have to be the directly preciding element


## Attribute selectors
| Selector | Example | Description |
| --- | --- | --- |
| Existance | `p[class]` | matches a specific attribute, whatever its value |
| Equality | `p[class="dog"]` | matches a specific attribute with a specific value |
| Space | `p[class~="dog"]` | matches a specific attribute whose value appears in a space-separated list of words |
| Prefix | `p[attr^"d"]` | matches a specific attribute whose value begins with a specific string |
| Substring | `p[attr*"do"]` | matches a specific attribute whose value contains a specific substring |
| Suffix | `p[attr$"g"]` | matches a specific attribute whose value ends with a specific string |

# Color
There are three possible color codes we can use with CSS:
- Color names, *e.g.* `green`
- RBG values, *e.g.* `rgb(46,170,56)`
- Hex codes, *e.g.* `#2eaa38`
- HSL, *e.g.* `hsl(125,73,67)`. HSL stands for Hue (angle of the color in a circle), Saturation (amount of grey), and Lightness (amount of white or black)

## Linear gradient
```css
body {
  background: linear-gradient(gradient_direction, color1, color2, color3, ...);
}
```
- `gradient_direction` → the direction from which the gradient starts. Can be a degree, *e.g.* `90deg`, or `45deg`.

### Create a Striped Element
Similar to `linear-gradient` with the major difference of repeating the specified gradient pattern.

```css
body {
  background: repeating-linear-gradient(90deg, yellow 0px, blue 40px, green 40px, red 80px)
}
/** Starts with the color yellow at 0 pixels, blends into the blue at 40px. 
  * It immediately changes to the green, because the color stop is at 40px too.
  * The green blends into red at 80px from the beginning of the gradient.
**/
```

# Size
Unit | Description
--- | ---
`px` | pixels
`%` | percentage, relative to the parent element
`em` | relative to the width of the letter m of the parent element
`rem` | relative to the width of the letter m of the browser
`vw` | relative to the viewport's width
`vh` | relavive to the viewport's height
`vmin` | relative to the viewport's smaller dimension (height vs. width)
`vmax` | relative to the viewport's bigger dimension (height vs. width)


# Text
## Fonts
### Typefaces
- `serif`
- `sans-serif`
- `monospace`
- `cursive`
- `fantasy` → designed for titles

### `@font-face`
Downloads the font if it's not on the users machine, allowing to use fonts that are not installed on the user's computer.
```css
@font-face {
  font-family: 'Open Sans';
  src: url("/fonts/OpenSans-Regular-webfont.woff2") format("woff2"),
       url("/fonts/OpenSans-Regular-webfont.woff") format("woff");
}
```

### Properties
Property Name | Description
--- | ---
`font-weight` | normal, bold, or numeric values
`font-style` | normal, italic, oblique
`text-transform` | uppercase, lowercase, capitalize, initial, none
`text-decoration` | none, underline, overline, line-through, blink
`line-height` | numeric value. Sets the height of an entire line of text. A good starter value is around `1.4` to `1.5em`
`letter-spacing` | numeric value. Control the space between each letter
`word-spacing` | numeric value. Control the space between each word
`text-align` | left, right, center, justify
`vertical-align` | baseline, sub, super, top, text-top, middle, bottom, text-bottom, length (px or em) or percentage
`text-indent` | px or ems. Indent the first line of text within an element
`text-shadow` | horizontal, vertical, blur, color

## Pseudo-elements
__Text:__
- `:first-letter`
- `:first-line`

__Links:__
- `:link` → not visited.
- `:visited` → visited links.
- `:hover` → pointing device is hovering the element.
- `:active` → link is being clicked.
- `:focus` → element has focus, *e.g.* using the tab key to focus an element.


# Boxes
Property Name | Values | Description | Example
--- | --- | --- | ---
`overflow` | auto, hidden, scroll | tells the browser what to do if the content contained within a box is larger than the box itself
`box-shadow` | offset-x, offset-y, blur-radius, spread-radius, color | applies one or more shadows to an element | `box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23);`
`transform` | translateX(), scale(), etc. | allows scaling, moving, rotating, skewing, etc. our elements | `transform: scale(2);`

# Position
Values | Description
--- | ---
`static` | the element is positioned according to the normal flow of the document
`relative` | relative to its original position in the normal flow of the page. Doesn't remove the element from the normal flow
`absolute` | relative to the closest positioned ancestor. If no ancestor is positioned, it will default to the `<body>` tag. Removes the element from the flow of the page
`fixed` | locks an element relative to the browser window. Removes the element from the flow of the page

Excluding `position: static`, the CSS properties `top`, `left`, `right`, and `bottom` can be used to position elements.

## Float
Floating elements are removed from the normal flow of a document, and pushed to the left or right of their containing parent element.
```css
.some-class {
  float: left;
}
```

# Lists
Property Name | Values | Description
--- | --- | ---
`list-style-type` | [ul] none, disc, circle, square ; [ol] decimal, decimal-leading-zero, lower-alpha, upper-alpha, lower-roman, upper-roman | control the shape or style of a bullet point. Applies to `<ol>`, `<ul>`, and `<li>`
`list-style-position` | outside<sup>*</sup>, inside | where the marker should appear
`list-style` | | shorthand for list styles

# Table
Property Name | Values | Description
--- | --- | ---
`empty-cells` | show, hide, inherit | specify wheter or not empty cells' borders should be shown
`border-spacing` | | control the distance between adjacent cells
`border-collapse` | collapse, separate | collapse adjacent borders. Used to prevent the width of lines be twice that of the outside edges

## Good practices
- Give cells padding;
- Distinguish headings;
- Shade alternate rows;
- Align numerals to the right.

# Forms
It is hard to get select boxes, radio buttons, and checkboxes to look consistent across all browsers. The author of [formalize.me](https://formalize.me/) has done the hard work of making forms look consistent across browsers.

# Cursor styles
The `cursor` property controls the type of mouse cursor that should be displayed to users. The possible cursor property values:
- auto
- crosshair
- default
- pointer
- move
- text
- wait
- help
- url("cursor.gif")

# Images
Whenever you use consistently sized images across a site, you can use CSS to control the dimensions of the images, instead of putting the dimensions in the HTML.
You'll need to determine the sizes of the images that will be used commonly throughout the site, then give each size a name. For example: small, medium, large. Apply each class according to the size you want the image to be.

### Aligning images with text
Float is being increasingly used to align images. There are two ways that this is commonly achieved:
1. The float property is added to the class that was created to represent the size of the image.
2. New classes are created with names such as align-left or align-right to align the images to the left or right of the page.

It is also common to add a margin to the image to ensure the text does not touch their edges.

## Background Images
Property Name | Values | Description
--- | --- | ---
`background-image` | url(link-to-image.png) | sets one or more background images on an element
`background-repeat` | repeat, repeat-x, repeat-y, no-repeat | sets how background images are repeated
`background-attachment` | fixed, scroll, local | specifies whether a background image should stay in one position or move as the user scrools up and down the page
`background-position` | top, center, 25% 75%, etc. | when an image is not being repeated, you can specify where in the browser window the background image should be placed
`background` | _background-color background-image background-repeat background-attachment background-position_ | shorthand for all the other background propeties. It must be specified in the specified order

## Images Sprites
An image sprite is a collection of images put into a single image. A webpage with many images can take a long time to load and generates multiple server requests. Using image sprites will reduce the number of server requests and save bandwidth. With CSS, we can show just the part of the image we need.

## Image Rollover
Changes the image when the mouse hovers it, using the `:hover` property. Can be used in conjunction with image sprites.

## Retina Image
__Retina Display__ → is a brand name used by Apple for its series of IPS LCD and OLED displays that have a hight pixel density than traditional Apple Displays.

The simplest way to make images appear "retina" (and optimize them for retina displays) is to define their width and height values as only half of what the original file is.

# `::before` and `::after` pseudo-elements
This pseudo-elements are used to add something before or after a selected element. They must have a defined `content` property.
```css
q::before {
  content: "«";
  color: blue;
}

q::after {
  content: "»";
  color: red;
}
```
They are often used to add cosmetic content and small touches to the UI to an element, improving user experience. They are inline by default.

# `@keyframes` and animation properties
The `animation-` properties control how the animation should behave, while the `@keyframes` rule controls what happens during that animation.

Property Name | Values | Description
--- | --- | ---
`animation name` | | sets the name of the animation, which is later used by @keyframes to tell CSS which rules go with which animations |
`animation-duration` | | sets the length of time that an animation takes to complete one cycle
`animation-fill-mode` | none, forwards, backwards, both | specifies the style applied to an element when the animation is finished
| | `none` | the element will be displayed using any other CSS rules applied to it
| | `forwards` | the target will retain the computed values set by the last keyframe encountered during execution. The last keyframe depends on the value of `animation-direction` and `animation-iteration-count`
| | `backwards` | it will apply the rules defined in the first relevant keyframe. The first keyframe depends on the value of `animation-direction`
| | `both` | the animation will follow the rules for both forwards and backwards
`animation-iteration-count` | _num_, infinite| allows you to control how many times you would like to loop through the animation
`animation-timing-function` | ease<sup>*</sup>, ease-out, ease-in, linear, cubic-bezier | controls how quickly an animated element changes overthe duration of the animation

### Cubic Bezier
The shape of the curve represents how the animation plays out. The curve lives on a 1 by 1 coordinate system:
- X-axis → duration of the animation.
- Y-axis → change in animation.

[cubic-bezier.com](https://cubic-bezier.com/) is a good tool to create and compare Cubic Bezier curves.

```css
animation-timing-function: cubic-bezier(0, 1, 1, 0);
```

## `@keyframes`
__`@keyframes`__ → specifies exactly what happens with the animation over the duration. This is done by giving CSS properties for specific "frames" during the animation, with percentages raging from 0% to 100%.

```css
#anim {
  animation-name: colorful;
  animation-duration: 3s;
}

@keyframes colorful {
  0% {
    background-color: blue;
  }

  100% {
    background-color: yellow;
  }
}
```

# Media queries
__Media query__ → new technique introduced in CSS3. It applies CSS rules if the type of device and specified parameters are matched. We can have as many selectors and styles inside the media query as we want.

```css
@media screen and (max-width: 100px) {
  /* CSS Rules */
}
```

# Tips
## Inheritance
You can force a lot of properties to inherit values from their parent elements by using inherit.
```css
header > p {
  font-size: inherit;
}
```

## Multiple style sheets
```css
@import url("example.css");
```
It should appeart before the other rules.

## CSS Selectors Precedence
Certain selectors have precedence over other selectors, even if they come before in the CSS file.
```html
<style>
  div { width: 50px; height: 50px }

  #random {
    background-color: red;
  }

  .abc {
    background: yellow;
  }
</style>
<div id="#random" class="abc"></div>
```
In this example, the `div` will have a background color of red, because an id takes precedence over the class. This is called [__specificity__](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) in CSS.\
The more specific the selector is, the more importance it has:
```css
div.test span { color: green; }
div span { color: red; }
.test { color: blue; }
```
Here, the span will have a color text of green. The only exception to this rule is the keyword `!important`. It is prefered trying to make better use of CSS cascade instead of going for the `!important` rule.

# Sources
HTML & CSS Design and Build Websites, *Jon Duckett*\
[freeCodeCamp](https://freecodecamp.org)\
[MDN web docs](https://developer.mozilla.org/en-US/docs/Web/CSS)\
[Wikipedia - Retina Displays](https://en.wikipedia.org/wiki/Retina_display)