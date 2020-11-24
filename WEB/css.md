#CSS
##CSS-Integration
* **inline** - in element attributes`<p style="colour:skyblue;"> hello world!</p>`
* **external** - by link in head of the page `<link rel="text/css" href="your_CSS_file_location"/>`
* **internal** - with style element in DOM`<style>CSS here</style>`

## tables

## Selectors
```css
.class       /*class selector*/
.class1.class2    /*with both class1 and class2*/
.class1 .class2   /* all elements within class2 that is descendant of an element with class1 */
#id          /*id selector*/
*           /*all elements */
p           /* all p elements */
p.class     /* all p elements with class */
div, p      /*element*/
div p       /* all <p> elements inside <div> element */
div > p     /* all <p> where the parent is a <div> */
div + p       /* all <p> elements that are placed immediately after <div> elements */
p ~ ul        /* select every <ul> that are preceded by a <p> element */

[attribute]   /* all elements with a target attribute */
[attribute=value]   /* all elements with atribute value */
[attribute~=value]    /* all elements with attribute containing the word "value" */
[attribute|=value]    /* all elements with attribute value starting with "value" */
a[attribute^=value]    /* all <a> elements whose "attribute" atribute begins with "value" */
[attribute$=value]    /* -"- ends with */
[attribute*=value]    /* -"- contains */

a:active    /* an active link */
p::after    /* insert something after the content of each <p> element */
p::before   /* insert something before the content of each <p> element */
input:checked
input:default
input:disabled
p:empty
input:enabled
p:first-child
p::first-letter
p::first-line
p:first-of-type
input:focus
a:hover
input:in-range    /* input elements with a value within a specified rane */
input:indeterminate   /* all input elements in an indeterminate state */
input:invalid
p:lang(langguage)   /* all p elements with language "language" */
p:last-child
p:last-of-type
a:link   /* all unvisited links */
:not(p)   /* every element that is not a p*/
:root
::selection
#news:target
input:valid
a:visited{};
```

## Units
Absolute:
* cm - centimeters
* mm - milimeters
* in - inches
* px - pixels
* pt - points (1pt = 1/72 of 1in)
* pc - picas (1pc = 12pt)

Relative:
* em - relative to the font-size of element (2em = 2 times the size of the current font)
* ex - relative to x-height of the current font
* ch - relative to width of the "0"
* rem - relative to font-size of the root element
* vw - relative to 1% of the width of the viewport
* vh - relative to 1% of the height of the viewport
* vmin - relative to 1% of viewport's smaller dimension
* vmax - relative to 1% of viewport's larger dimension
* % - relative to parent element

## Box Models
It is a box that wraps around every single element in html.

elements:
* margin
* border
* padding
* content



box-sizing: (Not inherited by default.)
* content-box (default) - content (center part)
* border-box - the border is part of the box
* initial
* inherit

```css
p{
  height: 100px;
  width: 100px;
  box-sizing: content-box;  /* the content will be 100px X 100px */
  box-sizing: border-box;  /* the content will be 100px X 100px - padding */
}
```

## Specificity
In case of two conflicting styles, it is chosen by specificity.

To remember it, usually it is the one that target smaller (more specific group)

I can set the `!important` so it has preference

Hierarchy:
1. Inline styles - style attached directly to the element `<h1 style="color: #ffffff;">`
1. IDs -
1. Classes, attributes and pseudo-classes - `.classes` `[attributes]` and pseudo-classes `:hover`
1. Elements and pseudo-elements - includes element names `<hl><p>` and pseudo-elements `:before :after`

In case of two same specifiers, it will pick the **last one**
```css
div{
  background-color: blue;
}
div{
  background-color: red;
}
/* output will be RED */
```

```css
div.name{
  background-color: red;
}
div{
  background-color: blue;
}
/* output will be RED */
```

```css
#someClass{
  background-color: red !important;
}
#someID{
  background-color: blue;
}
/* output will be RED even though ID have preference in hierarchy */
```

## Positions
* Static (default)
* Relative - stays same until I will apply top left... **without effecting other elements**
* Absolute - will actual remove elements and other elements will behave like it **doesn't exists**
* Fixed - like an absolute, it **remove element** so others fits like it wasn't there, but is **referents to the page**

## Visibility vs Display
`visibility: hidden;` will hide element, but physically it is still there
`display: none;` will hide element as if it was newer there

### Align Into Center of Parent
```html
<div class="out">
  <div class="in"></div>
</div>
```

```css
.out {
  width: 300px;
  height: 300px;
  background-color: yellow;
  position: relative;
}
.in {
  width: 100px;
  height: 100px;
  background-color: green;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
}
```

## FLEXBOX
Especially for smaller areas within the site. Good to use them to align along single axe.

Main purpose is to **align items in horizontal or vertical axes, space them out automatically**.

* container:
  * `flex-direction: row | row-reverse | column | column-reverse;`
  * `flex-wrap: nowrap | wrap | wrap-reverse;`
  * `justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly | start | end | left | right | ... + safe | unsafe;`
  * `align-items: stretch | flex-start | flex-end | center | bseline | first baseline | last baseline | start | end | self-start | self-end + ... safe | unsafe;`
  * `align-content: flex-start | flex-end | center | space-between | space-around | space-evenly | stretch | start | end | baseline | first baseline | last baseline + ... safe | unsafe;`
* items
  * `order: <integer>;`
  * `flex-grow: <number>;`
  * `flex-shrink: <number>;`
  * `flex-basis: <length> | auto;`
  * `flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ];`
  * `align-self: auto | flex-start | flex-end | center | baseline | stretch;`

## CSS GRID
Layout tool for the entire page. Good to use it to align along both axes.

## MEDIA QUERIES
`<meta name="viewport" content="width=device-width, initial-scale=1">`

`@media only screen and (max-width: 768px){}`

for mobile-first approach
```css
/* mobile styles */
body {
    font-size: 1em;
}

/* desktop styles */
@media only screen and (min-width: 768px) {
    body {
        font-size: 1.5em;
    }
}
```

## BROWSER SUPPORT
```css
@supports (display: grid) {
  div {
    display: grid;
  }
}
@supports not (display: grid) {
  div {
    float: right;
  }
}
```

## SHEDOW DOM
The CSS is global. If I write a style for one element, it can impact style of another. Web components needs own components so it is not impacting another document.
Is scoped subtree inside element. Usually in <template> element which are newer rendered, it is inserting content programmatically.
The elements in <template> will have own scoped CSS.

## PSEUDO ELEMENTS
Are used to give elements selectors special markup without destroying environment.
* p::after
* p::before
* ...
`p:hover::after{content: "I AM HERE";}` will insert text after each `<p>` element on hover.

## DATA ATTRIBUTES
For storing data.
`<div class="profile" data-name="someName" data-youtube-name="someYouTube" data-id="1">Profile</div>`

```css
.profile:hover::before {
  display: inline-block;
  content: attr(data-name)
}
```

## SHAPES
`<div class="triangle"></div>`
by setting width and height to 0 and changing borders properties, I can get different shapes.
```css
.triangle {
  height: 0px;
  width: 0px;
  border-top: 100px solid transparent;
  border-bottom: 100px solid transparent;
  /* border-left: 10px solid white; */
  border-right: 100px solid yellow;
}

```

## FONTS
* font-style
* font-weight
* font-variant
* font-size/line-height
* caption
* icon


## COLORS
RGB: `rgb(r,g,b)`

hexadecimal: `#00cjfi`


## TRICKS

### To show on hover with transitions
show item with transition from bottom to top `.container`, `.item`

```css
.item {
  transform: scaleY(0);    
  transform-origin: bottom;
  transition: transform 0.26s ease;

  height: 28px;
  position: absolute;....
}
.container:hover .item {
  transform: scaleY(1);
}

```

## QUESTIONS
what is a box model or what are box model properties? [answer](Box Models)
what is specificity? [answer](#Specifity)
how to allign element inside of an element: tables, flexbox, css grids, css positions, margin [answer](#Align-Into-Center-of-Parent)

In how many ways can be CSS integrated as a web page? [answer](#CSS-Integration)

Purpose of the z-index?: order the elements stack at each other

Rule set:
  * Selector  `.class, p, #id`
  * declaration block `{}`

Limitations of CSS:
  * no logic or arithmetical tasks
  * not able to read files
  * not total control (depends on browsers)
  * limitations of vertical controll
  * no expressions, just text-based coding
  * no column declaration
  * pseudo-class not controlled by dznamic behaviour

Pseudo Elements and pseudo classes?: `p::first-line{}` and `.link:hover{}`

Sizing fonts: `px` `em` `rem` `%` `vs` `vh`, pixels doing pretty well now

Save fonts and fallback fonts?:

Tools for browser support? For example https://caniuse.com/

CSS preprocessors?: Sass, SCSS, LESS, Stylus,
