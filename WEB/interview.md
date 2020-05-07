# INTERVIEW QUESTIONS
## JS

### 1
Take object (make function), transform this object into array where the array elements will represents a values of properties.
```js
let x = {
  a: 1,
  b: 2
}
```

```js
// const xArr = Object.entries(x)  // this would give me an two dimensional array ([[property, value]])
const xArr = [];
for (let i in x) {
  console.log( "object: ", i, " value: ", x[i] )
  xArr.push( x[i] )
}
```

### 2
Let's have a string, and I want to convert it into a second string which will be reverse
```js
let x = "hi"
let y = "ih"  // this should be an output
```

```js
// split will split an string into array at each symbol ""
// reverse will reverse an array
// join will connect array into string
const reverseStr = (str) => str.split('').reverse().join('');
console.log(reverseStr(x))
```

### 3
I have an object with properties and one method, then there is another method. See a code.
```js
const obj = {
  a:1,
  b:2,
  getA(){
    console.log(this.a)
  },
  getB(){
    console.log(this.b)
  }
}
// I WANT:
// obj.getA().getB() to log a, b
```

```js
const obj = {
  a:1, b:2,
  getA(){
    console.log(this.a)
    return this;
  },
  getB(){
    console.log(this.b)
  }
}
obj.getA().getB() // will log out 1, 2
```

### 4
I have an array, I want to have a method called print which will prints the elements of this array
```js
// I want to have
[1, 2].print(); // 1,2
```

```js
Array.prototype.print = function(){
  console.log(this.join())
}
```


### 5
Change code to add getters and so it will get right values (with inheritance)
```js
const a = function(x) {
  this.x = x;
};

const b = function(x, y) {
  this.y = y;
};

const newB = new b('x', 'y');
newB.getX();
newB.getY();
```

```js
const a = function(x) {
  this.x = x;
};
a.prototype = {
  getX(){
    return this.x
  }
}

const b = function(x, y) {
  this.y = y;
  a.call(this, x);
  getY(){
    return this.y;
  }
};

const newB = new b('x', 'y');
newB.getX();
newB.getY();
```


### 6
If I will do `clone.a.b.c = 2;` `console.log(obj.a.b.c);` should give me still 1 (if i clone the object and change its value, the first one should stay same)
```js
const obj = {
  a: {
    b: {
      c:1
    }
  }
}
// const clone =
```
two simple ways (not using third party libraries)
```js
const json.parse(json.stringify(obj))
var newObj = Object.assign({}, obj)
```

### 7 Merging Arrays
Merge and let them sorted
```js
const a = [1, 2, 5, 7, 9]
const b = [2, 5, 7, 12, 100]
```

```js
const ab = [...a, ...b].sort((a, b) => a - b)
```

### 8 "this" in Object function
what will be output of `obj.getX()`?
```js
const obj = {
  x: 1,
  getX() {
    const inner = function() {
      console.log(this.x)
    }
    inner();
  }
}
obj.getX()
```

output will be `undefined` because `this` in function is reference to `getX()` and its scope where is no `x`. For it to work, I would have to use prototype.

With arrow function. This in arrow function refers to caller object.
```js
// ...
const inner = () => {
  console.log(this.x)
}
// ...
```

Create variable pointing to this and pass it in arguments.
```js
//...
const that = this;
const inner = function(that) {
  console.log(that.x)
}
inner(that);
// ...
```

use bind
```js
const inner = function() {
  console.log(this.x)
}
inner.bind(this)();
```
