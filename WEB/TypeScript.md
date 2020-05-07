# TYPESCRIPT
is a **superset** of JavaScript
Static typing (is optional)
Object oriented featured
Compile-time errors before deploying application.
Transpiling - whenever the application is builted


## install
`nmp install --global typescript`
windows: `npm install -g typescript`

## configure
`tsconfig.json` file into root directory, this file can be empty

## transpile TypeScript to JavaScript
`tsc filename.ts`

## types
* boolean
* string: can be with \'\', \"\" or \`\`
* number
* array
* tuple
* enum
* any
* void
* null and undefined - stays same as JS

```ts
// STRING
let word: string = "hello"
let sentence: string = `
this is some sentence with word ${hello} init
`

// ARRAY
let A1: string[] = ["first", "second", "third"]   
let A2: Array<string> = ["first", "second", "third"]

// void
const someFunc = (): void => {
  console.log("this function returns void");
};

// ANY
let whoKnows: any = 4;
whoKnows = 'hello';
whoKnows = true;

// TUPLE
let myTuple: [string, number, boolean];
myTuple = ['hello', 20, true];
myTuple = [5, 20, true]; // the first element should be a string, not a number

// ENUM
enum Sizes {
  Small,
  Medium,
  Large,
}
Sizes.Small;// => 0
Sizes.Medium;// => 1
Sizes.Large;// => 2
```

## ARROW FUNCTIONS
```ts
let log = function(message) {
  console.log(message);
}
let doLog = () => console.log("something to log");
let doLog = (message) => console.log(message);

```

## TYPE INTERFACE
Are purely for declaration, cannot include an implementation, only an signature of function.
Cannot have algorithm inside this interface.
I can have a function declaration init
```ts
interface Point {
  x: number,
  y: number,
  draw: () => void  // just declaration, cannot include a logic
}

let drawPoint = (point: Point) => {  // inline annotation
  ...
}
```

## TYPE CLASS
fields x: number
property: `get X(){}` `set X(value) {...}` represents setter and getter. Property looks like a field from outside, but behave like method inside a class
constructor:
  `constructor(x?: number)` means that x is optional, ALL arguments on right should be optional as well
  `constructor(private x?: number)`  typescript compiler will generate field x for me and assign a given value so I dont need `this.x = x`

```ts
class Point {
  // x: number;  // don't have to be here anymore because of 'private x?: number'
  // y: number;  // don't have to be here anymore because of 'private y?: number'
  constructor(private x?: number, private y?: number) {}

  draw(){
    console.log('X: ' + this.x + 'Y: ' + this.y);
  }

  get X() {
    return this.x;
  }
  set X(value) {
    if(valur < 0 )
      throw new Error("value should be less than 0!");

    this.x = value
  }
}

let point = new Point();
point.draw()
let x = point.X   // will set x to what is returned by property get X
point.X = 10;   // will do a validation and set new value
```

## MODULES
Thing of each file as a module
To make a file a module, the Class have to be exported with `export`
in file created for point class create a class definition
in each file I can export one or more types. These types can be **classes, functions, simple variables, objects, ...**

`main.ts` file
```ts
import { Point } from './point';
let point = new Point(1, 2);
point.draw();
```

`point.ts` file
```ts
export Point {
  constructor(private x?: number, private y?: number) {}

  draw(){
    console.log('X: ' + this.x + 'Y: ' + this.y);
  }
}
```



## TS with Node.js
### Configuration:
in empty folder init project with `npm init -y`   -> give a package of JSON   (create package.json)
`yarn add -D typescript`  -> initialize TS into project   (write to package.json)
`npx tsc --init`  -> init options for typesctipt compiler (create tsconfig.json)
it is good practice to have code in project folder in `./src/` file so `./src/index.ts`

in index file lets code `console.log("HELLO");`

to transpile from TS to JS in `package.json` adjust

```js
"scripts":{
  "start": "node ./src/index.js",
  "build":"tsc"
}
```

and lets run (transpile) it with `yarn build`
finally to run program use node src/index.js or if I add it into the scripts then `yarn start`

to use modules run in root folder of project `npm install @types/node --save`
