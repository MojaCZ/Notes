# JASMINE

## Content
* [Main Idea](#Main-Idea)
* [describe()](#describe\(\))
* [it()](#it\(\))
* [xit()](xit())
* [fit()](#fit())
* [setup](#Setup)
* [setup](#Setup)

### Testing
Why?
* To get an error if you break code
* save time
* think about possible issues and bugs
* integrate into build workflow
* break up complex dependencies
* improve code (force me to write code correctly)

Kinds of Tests
* Unit Tests => Fully Isolated (testing one function)
* Integration Tests => With Dependencies
* End-to-End Tests => Full Flow


### Main Idea
I'll write a JavaScript part of project (the logic part), and then test against that

```js
function getOpposite(bool) {
  return !bool;
}
```

Here, `it()` is actual test
```js
describe('Write Your Test Group Descriptions Here', () => {
  it('Write Yout Test Expectation Here', () => {
    // arrange  - lets setup some data to test against
    let bool = false;

    // act      - I need to call some methods, to do some action
    const result = getOpposite(bool);

    // assert   - I expect something
    except(result).toBe(true);
  })
})
```
### setup

I have a html file in which I'll load all jasmine needed scripts
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/jasmine/3.5.0/jasmine.css"></link>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jasmine/3.5.0/jasmine.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jasmine/3.5.0/jasmine-html.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jasmine/3.5.0/boot.min.js"></script>
```

in mine own JS file I have test and I'll include it into html as well. In this are [describe](#describe()), [it](#it()) and so on
```html
<script src="specs/test.js"></script>
```
when I open html file on server, it will show me spec, failiures and all I need to know

### describe()

### it()

### xit()

### fit()

### beforeEach








## Setup
