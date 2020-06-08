Sass adds features that aren't available using basic CSS syntax. It is a preprocessor – takes code written using Sass syntax, and converts it into basic CSS.\
There are two syntaxes available for Sass: SCSS, which is an extension of the syntax CSS, and indented syntax (or Sass), an older syntax.

## Declaring a variable
```scss
$varname: value;
```

## Partials
__*__ → separate files that hold segments of CSS code. They are imported and used in other Sass files. It's a great way to group similar code into a module to keep it organized.

Naming: `_name.scss`\
Importing: `@import 'name`

## Nesting CSS
```scss
nav {
  ul {
    list-style: none
  }
}
```

## Mixins
__*__ → functions for CSS.

```scss
@mixing name($property, $var) {
  // css rules
  #{$property}: $var;
}

p {
  @include name(color, #ccc);
}
```

## Placeholder class
__*__ → special type of class that only prints when its extended.

```scss
%panel {
  // css rules
}

p {
  @extend %panel;
}
```

You can also copy all properties from an element to another one using the `@extend` keyword.

## Logic statements
### If
```scss
@if $var == true {}
@else if $var == success {}
@else {}
```

### For
```scss
@for $i from 1 through 12 {}

@for $j from 1 to 13 {}
```
- start `through` end → includes the end number;
- start `to` end → excludes the end number.

### Each
Loops over each item in a list of map.
```scss
@each $color in blue, red, green {}

$colors: (color1: blue, color2: red, color3: green);
@each $key, $color in $colors {
  .#{$color}-text { color: $color; }
}
```

### While
```scss
$x: 1;
@while $x < 13 {
  .col-#{$x} { width: 100%/12 * $x; }
  $x: $x + 1;
}
```

# Sources
[freeCodeCamp](https://freecodecamp.org)\
[Sass docs](https://sass-lang.com/documentation/)