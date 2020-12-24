`$` → dollar sign operator, invoques jQuery.

_Select all of the specified elements:_
```javascript
$('button')
```
You can use CSS selectors, like `$('.target:nth-child(n)')` or `$('.target:odd')`.

## Functions
Function | Description
--- | ---
`addClass('name-class')` | adds a new class
`removeClass('name-class')` | removes a class
`css('prop'[, 'value'])` | set or return the value of a style property
`prop('prop'[, 'value'])` | set or return the value of a property
`attr('prop'[, 'value'])` | set or return the value of an attribute
`removeProp('prop')` | remove a property
`html('...')` | add HTML code within an element
`text('...')` | alter text within an element. It doesn't add HTML tags
`remove()` | remove the element from the DOM
`appendTo('#element')` | append an element to another one
`clone()` | makes a copy of an element
`parent()` | get the parent of whichever element we've selected
`children()` | get the children of whichever element we've selected

# Sources
[freeCodeCamp](https://www.freecodecamp.org/)