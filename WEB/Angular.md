## Architecture
commands:
* `ng new projectName`
* `ng generate component componentName`
* `ng serve`

# ANGULAR
Is a Typescript framework.
Used for creating an SPA (Single Page Application)
Angular is maintained and developed by google.

## Angular
Versions
8: generated code is easier to read and debug, faster re-build time, improved re-build time, improved payload size, imporved template type checking
9: released on February 7 2020
* Angular works with TS 3.6 and 3.7, moves all to use ivy compiler and runtime.
* smaller bundle sizes
* faster testing
* better debugging
* improved CSS and style binding, type checking, errors, build times, enabling AOT on by default

building elements for Angular:
* components    - encaptulates data, HTML template and logic
* modules       - a group of related components
* templates
* metadata
* data binding
* directives
* services
* dependency injection

Angular doesn't have a "scope" concept or controllers.

Syntax is focused on "[]" for property binding, and "()" for event binding.

Features:
* Accessibility Applications
* Angular CLI
* Animation Support
* Cross Platform App Development
* Code Generation
* Code Splitting
* Synergy with Code Editors
* Template
* Testing

Advantages:
* Ability to add custom directives
* Community support
* Client and Server Communication
* Animation and Event Handlers
* MVC pattern
* Static and Angular Template
* Two Way Data Binding
* Dependency Injection
* RESTful services and validation

## Setup
### install
* node `node -v`
* npm `npm -v`
* angular `npm install -g @angular/cli`
### Start building
* start angular app `ng new "my-new-angular-app"` or `ng init` (won't create folder, configer project in current one) will:    
  * create a folder "my-new-angular-app"
  * download and install Angular libraries and any other dependencies
  * installs and configures TypeScript
  * Install and configures Karma & Protractor (testing libraries)
* `ng serve` will runs the compiler in watch mode (looks for changes in the code and recompile if needed), start the server, launch app and keep app running while building it. ***port 4200***
* **new component** `ng g component my-new-component` will add a reference to components, directives and pipes automatically in the `app.module.ts`

##DECORATORS
Is function wrapping another function or a class and return it after decorating.


### Modules
Modules help organize an application into cohesive functionality blocks by wrapping components, pipes, directives and services. (***developers ergonomics***)

Application has to have at last one module (AppModule). For example one app with for major areas will have four modules plus one root module (AppModule).

Angular module is a class with the `@NgModule` decorator. **Decorator** is a function that modify JavaScript classes.
  * **declarations:** are relevant to views (components, directives and pipes).
  * **exports:** The classes that should be accessile to other modules components.
  * **imports:** Modules whose classes are needed by the components of this module.
  * **providers:** Services presented in one of the modules which are going to be used in the other modules or components.
  * **bootstrap:** The root component which is the main view of the application
  * **entryComponents:** is a component that Angular loads imperatively (not referencing in the template)

```ts
// import ...
// ...
import { nameComponent } from './name.component';

@NgModule({   // decorator
  declarations: [   // here will be all components of this model
    AppComponent,
    NameOfComponent  // must be also imported at top
  ]
})
```


### Components
Are the most basic building block of an UI and Angular application. A component controls one or more sections on the screen (called views).

Is self contained and represents a reusable piece of US that is constituted by three important things:
* A piece of html code that is known as the view.
* A class that encapsulates all available data and interactions to that view through an API of properties and methods architectured by Angular (***application logic***)
* The html element also known as selector

The ***component*** passes data to the ***view*** using a process called ***Data Binding***. This is done by Binding the DOM Element to component properties. Binding can be used to display property values to the user, change element styles, respond to a user event, etc.

A component must belong to an NgModule in order for it to be usable by another component or application.

#### Birth of component
1. Create
  * creste component `name.component.ts`
  * use decorator, export class, ....
2. Register it in a module
3. Add an element in an HTML

?? What is a decorator
  - it is a function which will take an object
  * selector: **whenever in html will be element with this selector, an Angular will put there a block**
    * `<elName>` the selector is `elName`
    * `<div class="someClass"></div>` the selector is `.someClass`
    * `<div id="someClass"></div>` the selector is `#someClass`

#### src/app/app.components.ts
```ts
import { Component } from '@angular/core';  // core library of angular

@Component({        // decorator
  selector: "app-root",
  templateUrl: "./app.component.html",
  // template: "<h1>some heather</h1>", // this or templateUrl
  styleUrls: ["./app.component.css"]
})

export class AppComponent {
  title = "Angular app";
  ARR = ["a1", "a2", "a3"];
  getTitle(){
    return this.title
  }
}

```

the new created component have to be added into module for example into
`app.module.ts`

example of App architecture:
* AppComponent
  * BreadcrumbComponent
  * CathegoryQuestions Component
    * NewQuestions ModalComponent
    * DeleteQuestion ModalComponent
  * QuestionAnswers Component
    * NewAnswer ModalComponent
    * UpdateAnswer ModalComponent
    * DeleteAnswer ModalComponent
  * Cathegories Component

### Templates
Are used to define component view.
Looks like regular HTML,

to display something dinamically - **data binding**
```html
<h2> {{ title }} </h2>
<h2> {{ "Title: " + title }} </h2>
<h2> {{ getTitle() }} </h2>
<ul>
  <li *ngFor="let element of array"> {{ element }}</li>
</ul>
```

### Services
**Are singleton objects that gets instantiated only once during the lifetime of application.**

Services contain methods that maintain the data throughout the life of an application.

They organize and share business logic models or data and functions with various components of an application.

Functions of service can be fired by any controller or directive.

Can be value, function, feature,... almost everything.

Is typically a class with a narrow, well-defined purpose.

Should something specific and do it well.

Main purpose is sharing resources across components.

CREATE SERVICE
  * create file in app folder named `name.service.ts`
  * to use service in component add a constructor
  * **!!** LATER WHEN I NEED TESTING, I CAN JUST DECLARE NEW SERVICE WHICH WILL NOT NEED A BACKEND SERVER, JUST FOR TESTING, I dont get it now, but I surely will later

**!!** it is called **Dependency injection** `constructor(service: NameService)` - I added dependency as a parameter to instructor, I decoupeled that class from dependency. NOT TIGHETLY COUPELED!!!
I instructed an angular to inject the dependency of this component into constructor. Injecting/providing an dependency in constructor.
To make this possible, I need to register this dependencies in `app.module.ts` to say that **components in this module is dependent on some service**. This **MUST** be done or there will be `ERROR: No provider ...`


```ts
// name.service.ts
export class NameService {
  getCourses() {
    // later here will be http request and as a response will be object
    return ["a1", "a2", "a3"]
  }
}

// name.component.ts
export class NameComponent {
  title = "Angular app";
  ARR;

  constructor(service: NameService) { // create new service object
    this.ARR = service.getCourses();
  }
}

// app.module.ts
@NgModule({
  declarations:[],
  imports: [],
  providers: [
    NameService
  ],  
  // ...
})
```

## DIRECTIVES
An Attribute directive changes the appearance or behavior of a DOM element.
* Components - directives with template
* Structural directives (NgFor, NgIf) - change the DOM layout by adding and removing DOM elements.
* Attribute directives (NgStyle) - change the appearance or behavior of an element, component, or another directive.

### Structural Directives
Are responsible for HTML layout. They shape or reshape the DOM's structure by adding, removing or manipulating elements.
Structural directives can be recognized by *
* NgIf  `<div *ngIf="hero" class="name">{{hero.name}}</div>`   make a chunk of the DOM appear or disappear by removing it from the DOM, not setting style
* NgFor `<ul><li *ngFor="let hero of heroes">{{hero.name}}</li></ul>`
* NgSwitch
```html
<div [ngSwitch]="hero?.emotion">
  <app-happy-hero     *ngSwitchCase="'happy'"     [hero]="hero"></app-happy-hero>
  <app-sad-hero       *ngSwitchCase="'sad'"       [hero]="hero"></app-sad-hero>
  <app-confused-hero  *ngSwitchCase="'confused'"  [hero]="hero"></app-confused-hero>
  <app-unknown-hero   *ngSwitchDefault            [hero]="hero"></app-unknown-hero>
</div>
```

## DATA BINDING
Connect components with template view. Components provides data, templates displays it.

Components stores most of its logic and data inside of its class decorated with `@Component`. This defines the class as a component with template HTML.

Binding is unidirectional ([element properties] and {{}} one way, (event) the other)

### Element Properties
`<any-element [property]="value">innerHTML</any-element>`
`[property]` mirrors the property in the DOM element's object node. **PROPERTY, not attribute**.

Once the DOM is parsed, it creates a properties of nodes. So properties are properties of node object and attributes are the elements of the `attribute` property.

`<input id="the-input" type="text" value="Name:">` after parsing DOM, the **id property is a reflected property of id attribute**.

### Event Handling
The `(event)` pertains to any valid event type. Event is bound to `"handler"` in the example. Event handlers are usually member functions of the component class.

```html
<button (click)="someFunction()">Click Me<button>
```

When the event is emitted, it passes the Event object in the form of `$event`.

The handler maps to the identically named handler function of the component class.

events:
* focus
* blur
* submit
* scroll
* cut
* copy
* paste
* keydown
* keypress
* keyup
* mouseenter
* mousedown
* mouseup
* click
* dbclick
* drag
* dragover
* drop

```ts
// my.component.ts
@Component({})
export class MyComponent {
  handler(event):void {
    // does stuff
  }
}
```
```html
<!-- my.component.html -->
<any-element (event)="handler($event)">innerHTML</any-element>
```

## PIPES
Built in pipes:
* **async**
* **currency**
* **date**
* **decimal**
* **json**
* **lowercase** **uppercase**
* **percent**
* **slice** `<li *ngFor="let item of someList | slice:2">{{ item }}</li>` arguments are start and end index


## Project Structure

### The App Folder

## App Navigation and Routing
to route to "http://localhost:4200/questions/about/cathegory-name"
`<a class="list-title" [routerLink]="['/some/route', someObject.slug]">{{someObject.title}}</a>`

to map URL paths to the components create a config file called `app.routes.ts` in same folder as the root module

for each route we provide a path and the component that should be rendered at that path.

Resolve in navigation routes allows to pre-fetch the component's data before the route is activated. **resolver must be ready** for application to continue.

```ts
import { Routes } from '@angular/router';

export const routes: Routes = [
  {
    path: '',
    component: Name1Component,
    resolve: {
      data: Nname1Resolver
    }
  },
  {
    path: 'some/route1/:categorySlug',
    component: Name2Component,
    resolve: {
      data: Name2Resolver
    }
  },...
]
```

Finally in the root module must be added reference to routes.
`AppModule`
```ts
import { routes } from './app.routes';

imports: [
  RouterModule.forRoot( routes, { useHash: false } )
],
```

## RESOLVER
I a service
1) generate service `ng generate service some-resolver`
2) in `app-routing.module.ts` add resolver to route, I will give it a object representing data (dataObject)
3) get data in component


!! observble and promices **must** be completed before sent


```ts
// app-routing.module.ts
...
{
  path: ''
  component: ...,
  resolve: { dataObject: someResolver }
}
```
```ts
// some-resolver.service.ts
import { Injectable } from ...
import { Resolver } from '@angular/router';
import { Observable } from 'rxjs'

@Injectable({
  providedIn: 'root'
})
export class SomeResolverService implements Resolve<any> {
  constructor(){};
  resolve():Observable<any> | Promise<any> | any {
    return this.appService.getData()    // !! without subscribe
  };
}
```

```ts
//some component
// ...
constructor(private route: ActivatedRoute){ }
ngOnInit() {
  this.activatedRoute.data.subscribe(data => console.log(data))
}
// ...
```

```ts
// THIS WORKS WITH RESOLVERS

// const observable: Observable<any> = Observable.create(observer => {
//   observer.next("HALLO HERE I AM");
//   observer.complete();
// })
// return observable.pipe(delay(2000));

// OR
return this.http.get("assets/classification-data.json").pipe(share());
```



## OBSERVABLES

Handles the stream of items. To start the stream I have to subscribe. The stream must be completed at the end, or it will never ends.

Provides support for passing messages between publishers and subscribers.

Usually used for event handling, asynchronous programming, and handling multiple values.

Are declarative.

A publisher create an *Observable* instance that defines a *subscriber* function. This function is executed when a consumer calls the *subscribe()* method.

If I subscribe twice to same subscrible, it will fire twice

## SERVICE WORKER
https://www.youtube.com/watch?v=5YtNQJQu31Y
`ng add @angular/pwa`
  * add to index.html
    * `<noscript>` to prevent executing page without javascript
    * `<link rel="manifest" href="manifest.json">`
  * generates *manifest.json* fpr PWA
  * in *app.module.ts*
    * import ServiceWorkerModule from @angular/service-worker
    * in \@NgModule in imports `ServiceWorkerModule.register('/ngsw-worker.js', { enabled: environment.production })`
  * *ngsw-worker.js* file will be auto generated during the build process and it will hold service worker
  * assets/icons
  * in package.json will modifies `"@angular/pwa": ...`
  * ngsw-config.json in this file will be configured the worker
    *
  * angular.json
    * serviceWorker: true for production build

`ng build --prod` will boundle and optimize entire app. The compiled app can be seen at */dist/angular-pwa* folder

`npm install -g http-server` and run `http-server -p 8081` to serve app. This is because service worker wont work on `ng serve`. The http server must be run at /dist/angular-pwa folder

ngsw-config.json:
  * installMode, updateMode:
    * **prefetch** the content will be cached at the page loading
    * **lazy** the content will be cached after required once (at some point at time)
  * if I want to include font or other third party file, I can add it by adding after "files" array `"urls":["https://..."]`
  * for dynamic files I can add a `"dataGroups":[...]`

Service worker will do:
* Caching an application. The application is cached as one unit, and all files update together.
* Application continues to run with the same version of all files.
* When user refresh the application, they see the latest fully cached version. New tabs load the latest cached code.
* Update happen in the background after changes are published. The previous version of the application is served until an update is installed and ready.
* The service worker conserves bandwidth when possible. Resources are only downloaded if they've been changed.

SwUpdate:
* Getting notified of *available* updates. (new versions of the app to be loaded if the page is refreshed)
* Getting notified of update *activation*. (when the service worker starts serving a new version of the app immediately)
* Asking the service worker to check the server for new updates.
* Asking the service worker to activate the latest version of the app for the current tab.


## RxJs Operators
https://www.youtube.com/watch?v=5TnWFaI49aw&t=15s
Not specific to angular but can be used with js or ts code as well

of:
Creates a Observable

from:
Creates a Observable from Promise

pipe map:
I want to change data
will apply before subscription
```ts
const source = of('david')
source.pipe(map(name => doSomeStuf))
source.subscribe()
```

pipe tap:
Same as map except **I don't want to change data**

share:
will make sure that if I will subscrive twice to same Observable, it will come from same source. So If I will subscribe twice to same http request, it will call server only once.

swichMap:
Gets variable from first observable, and switch to second Observable.


## MATERIALS

### SETUP

`ng -i -g @angular/cli`
`npm i --save @angular/material @angular/cdk`
`npm i --save @angular/animations`
`npm i --save hammerjs` - for gestures
`ng add @angular/material`
  - will update Angular project with the correct dependencies
  - will perform configuration changes and execute initialization code
import Angular Material component modules:

main.ts `import 'hammerjs';`

app.module.ts
```ts
import { BrowserAnimationModule } from '@angular/platform-browser/animations';
import { MaterialModule } from './material'
// ...;
imports:[
  // ...
  BrowserAnimationModule,
  MaterialModule
]
```

create new file in /app/material.ts
```ts
import { MatButtonModule, MatCheckboxModule } from '@angular/material';
import { NgModule } from '@angular/core';

@NgModule({
  imports: [MatButtonModule, MatCheckboxModule],
  exports: [MatButtonModule, MatCheckboxModule]
})
export class MaterialModule { }
```

include theme in /src/styles.scss
```css
@import '@angular/material/prebuilt-themes/indigo-pink.css';
```

### Dialogs
add button that will open dialog
```html
<button mat-raised-button (click)="openDialog()">Open Dialog</button>
```

in component implement dialog service
```ts
import { MatDialog } from '@angular/material';
import { DialogExampleComponent } from './dialo...'
// ...
// ...
export class AppComponent {
  constructor(public dialog: MatDialog) {}
  openDialog(){
    this.dialog.open(DialogExampleComponent)
  }
}
```

`dialog.open(component, optional configuration)` excepts two parameters

`ng g c dialog-example` generate dialog component

```ts
//app.module.ts
entryComponents: [
  DialogExampleComponent
],
```

### Icons

### Tables
https://www.youtube.com/watch?v=ao-nY-9biWs
`ng generate @angular/material:material-table --name="my-table-name"` will create new component with all properties of angular table.

* datasource.ts
  - connect() method: is called when dataTable is first created
  - getPagedData() method: handles the paging of the table (1-10, 11-20...)
  - getSortedData() method: handles sorting of table rows
* component.html
* component.ts


## EXPORT TO PDF
`npm install jspdf --save`
`npm install @types/jspdf --save-dev`

in component create method which will be fired after button click
```ts
import { Component, ViewChild, ElementRef } from '@angular/core';
import * as jsPDF from 'jspdf';

@ViewChild('content') content: ElementRef;

public downloadPDF() {

  let doc = new jsPDF();

  let specialElementHandlers = {
    '#editor' : function(element, renderer) {
      return true;
    }
  };

  let content = this.content.nativeElement;

  doc.fromHTML(content.innerHTML, 15, 15, {
    'width': 190,
    'elementHandlers': specialElementHandlers
  })
  doc.save('test.pdf')

}
```


## FORMS
https://stackblitz.com/edit/example-angular-material-reactive-form?file=app%2Fapp.component.ts

this.myFormGroup.valueChanges.subscribe() // will subscribe and return values on change
