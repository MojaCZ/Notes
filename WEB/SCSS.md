# Sass & SCSS
Syntactically Awesome Style Sheets & Sassy Cascading Style Sheets
difference is in sintax,
in Sass there are no `{}` and `;`.
SCSS is same syntax as CSS. It is newer.

features:
* [Nested Rules](#Nested-Rules)
  * [& Character](#&-Character)
* [Variables](#Variables)
* [Better Operators](#Operators)
* [Functions](#Functions)
* [Trigonometry](#Trigonometry)
* [Code Flow and Control Statements](#Code-Flow-and-Control-Statements)
* [Mixins](#Mixins)

`$i` `.someClass#{$i}` `#{$i}` vs

## Nested Rules
```css
#A {
  color: red;
}

#A #B {
  color: green;
}

#A #B #C p {
  color: blue;
}
```
the same in SCSS:
```scss
#A {
  color: red;
  #B {
    color: green;
    #C p {
      color: blue;
    }
  }
}
```
### & Character
`&` character is simply converted to the name of the parent element
```scss
a{
  font-weight: bold;
  &:hover {
    color: red;
  }
}
```
becomes:
```css
a { font-weight: bold; }
a:hover { color: red; }
```

## Variables
Starts with `$`

Cannot be reassigned!

```scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

## Operators
```scss
p {
  font-size: 10px + 2em;    // error: incompatible units
  font-size: 10px + 6px;    // 16px
  font-size: 10px + 6       // 16px
  height: 12% - 2%          // 10%
  width: 10px * 10px        // error
  width: 10px * 10          // 100px
  width: 5 * (5px + 5px)    // 50px

  top: 16px / 24px    // Outputs as classic CSS
  top: (16px / 24px)   // Does division
  top: #{$var1} / #{$var2} // Uses interpolation, outputs as CSS
  top: $var1 / $var2   // Does division
  top: random(4) / 5;   // Does division (when paired with function)
  top: 2px / 4px + 3px; // Does division (when part of arithmetic)
}
```

Example of zebra patterns (in tables) using reminder `%` with `@for` and `@if`
```scss
@mixin zebra(){
  @for $i from 1 through 7 {
    @if ($i % 2 == 1 ){
      .stripe-#{i} {
        background-collor: black;
        color: white;
      }
    }
  }
}

* { @include zebra(); }
```


## Functions
## Trigonometry
## Code Flow and Control Statements
SCSS has `functions()` and `@directives` (also known as rules)

functions:
* `if(boolean, return if true, return if false)`

directives:

* \@if
* \@else if
* \@for
```scss
for $i from 1 through 5 {
  .definition-#{$i} { width: 10px * $i; }
}
```

```scss
// function if() will return one of the two specified values, based on a condition
if(true, 1px, 2px) => 1px
if(false, 1px, 2px) => 2px

// directive @if will branch out based on a condition
p {
  @if 1 + 1 == 2  { border: 1px solid; }
  @if 7 < 5       { border: 2px dotted; }
  @if null        { border: 3px double; }
}
```

```scss
// check if parent exists
@if & {
  // some code
}
@else {
  // some other code
}
```

## Mixins
Is defined by the `@mixin` directive (mixin rule)
To use mixin use `@include mixinName()`

```scss
@mixin flexible(){
  display: flex;
  justify-content: center;
  align-item: center;
}
.centered-elements {
  @include flexible();
  border: 1px solid gray;
}
```

Good practice is to use it with webkits for different browsers
```scss
@mixin rotate($degree) {
  -webkit-transform: rotate($degree); // Webkit-based
  -moz-transform: rotate($degree);    // Firefox
  -ms-transform: rotate($degree);     // Internet Explorer
  -o-transform: rotate($degree);      // Opera
  transform: rotate($degree);         // standard CSS
}
```
