# HTML

`<!--...-->` a comment
`<!DOCTYPE>` a document type
`<html>` the root of an HTML document
`<h1>` to `<h6>` headers
`<hr>` horizont line
`<head>` information about a document
`<body>` document's body
`<div>` section in a document
`<button>` clickable button
`<br>` single line break
`<footer>` footer for a document or a section
`<b>` bold text
`<i>`
`<p>` paragraph

## Meta
`<meta>`meta about an HTML document
lays in `<head>` of the document
attributes:
* charset - specifies the character encoding for the HTML document
* content - gives the value associated with the http-equiv or name attribute
* http-equiv - provides an HTTP header for the information/value of the content attribute
  * content-type
  * default-style
  * refresh
* name  - specifies a name for the metadata
  * application-name
  * author
  * description
  * generator
  * keywords
  * viewport

```html
<meta charset="UTF-8">
<meta name="description" content="Page Description">
<meta name="keywords" content="HTML, CSS, Angular, Vocabulary, Stromy, ...">
<meta name="author" content="Nejakej Frajer">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

## Lists
### Ordered
`<ol>` ordered list
`<li>` list item
`<li value="5">` other items will be incremented from this number
### Unordered
`<ul>`  unordered list
`<li>` list item
### Definition
`<dd>` description/value of a term in a description list
`<dl>` a description list
`<dt>` term/name in a description list
```html
<dl>
  <dt>Coffee</dt>
  <dd>Black hot drink</dd>
  <dt>Milk</dt>
  <dd>White cold drink</dd>
</dl>
```


## Links
`<a>` hyperlink
attributes:
* href
* target
  * \_blank - opens in a new window or tab
  * \_self - opens in the same window/tab
  * \_parent - opens in the parent frame
  * \_top - opens in the full body of the window
  * framename - opens in a named frame
* title - text to be displayed on the mouse over

to same page, different section
```html
<a name="topmost">
<a href="#topmost">BACK TO TOP</a> <!-- will redirect uset to anchor above with name topmost -->
```
## Link tag
`<link>` relationship between a document and an external resource

`<link rel="stylesheet" type="text/css" href="theme.css">`

attributes:
* crossorigin
* href
* hreflang
* media
* rel dpecifies the relationship between the current document and the linked one
  * alternate, author, dns-prefetch, help, icon, license, next, pingback, preconnect, prefetch, preload, prerender, prev, search, **stylesheet**


## Select
`<optgroup>` group of related options in a drop-down list
`<option>` option of drop-down list
`<select>` a drop-down list

attributes:
* autofocus
* disabled
* form
* multiple - specifies that multiple options can be selected at once
* name
* required
* size


## Tables
`<table>`
`<caption>`table caption
`<tr>`  row in a table
`<th>` header cell in table
`<td>`  a cell in a table
`<thead>` groups the header content in a table
`<tbody>`  groups the body content in a table
`<tfoot>` groups the footer content in a table

```html
<table>
  <caption>Some Title</caption>
  <tr>
    <th>First column</th>
    <th>Second column</th>
  </tr>
  <tr>
    <td>10</td>
    <td>hello</td>
  </tr>
</table>
```

## Input
`<input>` an input controll
Attributes:
* autocomplete - on/off
* autofocus - autofocus
* checked - checked
* placeholder
* required - required
* maxlength - maximum number of characters
* minlength - minimum number of characters
* multiple
* name
* dirname
* disabled
* accept
* alt
* src
* form
* formaction
* formmethod
* formnovalidate
* formtarger
* height
* list
* readonly
* pattern
* type
* value

Types:
* button
* checkbox
* color
* date
* datetime-local
* datetime
* email
* file
* hidden
* image
* month
* number
* password
* radio
* range
* reset
* search
* submit
* tel
* text
* time
* url
* week

type number
* step - number/any
* max - number/date
* min - number/date

## Form
`<form>` form for user input
atributes:
* action
* target (\_self, \_blank, ...)
* method
* autocomplete
* enctype
* name
* novalidate
*

## Image Map
`<map>` defines an image-map (an image with clickable areas)
```html
<img src="" alt="" usemap="#someMap">

<map name="someMap">
  <area shape="rect" coords="34, 44, 270, 350" alt="name1" href="href1">
  <area shape="circle" coords="34, 44, 270, 350" alt="name2" href="href2">
  <area shape="rect" coords="34, 44, 270, 350" alt="name3" href="href3">
</map>
```

area:
* rect
* circle
* poly
* default - entire region

## Nested Webpage
`<iframe>` inline frame
`<iframe src="" height="" width=""></iframe>`

## New In HTML5



`<abbr>` abbreviation or an acronym
`<address>` contact information for the author/owned of a document
`<area>` area inside an image-map
`<article>`
`<aside>` content aside from the page content
`<audio>` sound content
`<base>` base URL/target for all relative URLs in a document
`<bdi>`
`<bdo>`overrides the current text direction
`<blockquote>` section that is quoted from another source
`<canvas>` to draw graphic via scripting
`<cite>`title of work
`<code>` piece of computer code
`<col>` column properties for each column with <colgroup> element
`<colgroup>` group of one or more columns in a table for formatting
`<data>` links the given content with a machine readable translation
`<datalist>` list of pre-defined options for input controls
`<del>` text that has been deleted from a document
`<details>` additional details that the user can view or hide
`<dfn>` defining instance of a term
`<dialog>` dialog box or window
`<em>` emphasized text
`<embed>` container for an external (non-HTML) application
`<fieldset>` groups related elements in a form
`<figcaption>` caption for a <figure> element
`<figure>` self-contained content
`<img>` image
`<ins>` text that has been inserted into a document
`<kbd>` keyboard input
`<label>` label for an <input> alement
`<legend>` caption for <fieldset> element
`<main>` main content of a document
`<mark>`marked/highlithed text
`<meter>` scalar measurement within a known range
`<nav>` navigation links
`<noscript>` alternative content for users that do not support client-side scripts
`<object>` embadded object
`<output>` result of calculation
`<param>` parameter for an object
`<picture>` container for multiple image resources
`<pre>` preformatted text
`<progress>` the progress of a task
`<q>` a short quotation
`<rt>` an explanation/pronunciation of a character
`<ruby>` a ruby annotation
`<s>` text that is no longer correct
`<samp>` sample output from a computer program
`<script>` a client-side script
`<section>` section in a document
`<small>` smaller text
`<source>` multiple media resources for media elements
`<span>` a section in a document
`<strong>` important text
`<style>` style information for a document
`<sub>` subscripted text
`<summary>` a visible heading for a <details> element
`<sup>` superscripted text
`<svg>` a container for SVG graphics
`<template>` template
`<textarea>` multiline input control
`<time>`  a date/time
`<title>` title for the document
`<track>`next track for media elements
`<u>` stylistically different text
`<var>` a variable
`<video>` a video or movie
`<wbr>` possible line-break

# QUESTIONS
## What is HTML?
HyperText Markup Language documents are made from content and tags that format it for proper display on page

difference between element and tag?: element is an individual component, tag is type of element (I can have many elements of <h1> tag)

single tags: `<img>` `<br>`

common lists: ordered, unordered, defimition, menu, directory

what is image map: lets you link to many different web pages using a single image by defining shapes in images

inserting a special symbols: &#..

does a hyperlink apply to text only?: NO, it can pointed to image, other document,...

why to group checkboxes?: just to organize them. Thay don't know about each other.

applets: small programs embedded within web page written in Java

can a single text link point to two different web pages? NO

what is a difference between the directory, menu list and unordered list?: directory and menu lists do not include attributes for changing the bullet style

limit of the text field size?: default is around 13chars but I can change it

do <th> tags always need to come at the start of a row or column? NO

create a text that will allow send an email when clicked:
`<a href="mailto:someemailaddress">some text</a>`
