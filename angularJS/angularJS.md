[NEXT CONTROLLERS](https://www.w3schools.com/angular/angular_http.asp)

# ANGULAR JS

  It is recomended to load the AngularJS library either in the `<head>` or start of `<body>`

  * AngularJS extends HTML with no-directives
  * the **ng-app** directive defines an AngularJS application
  * the **ng-model** directive binds the value of HTML controls (input, select, textarea) to application data
  * the **ng-bind** directive binds application data to the HTML view
  * the **ng-init** directive initializes AngularJS application variables

  ```html
  <div ng-app="" ng-init="first='John'">
    <p>Name:
      <input type="text" ng-model="first">
      <input type="text" ng-model="second">
    </p>
    <p ng-bind="first"></p>
    <p ng-bind="second"></p>
    <h1>Hello {{first}}</h1>
  </div>
  ```
  In example abowe **ng-app** tells AngularJS that the `<div>` element is the "owner" of an AngularJS application.\
  The **ng-model** directive binds the vlue of the input field to the application variable name.\
  The **ng-bind** directive binds the content of the `<p>` element to the application variable name.

## Good practices
* use ng-bind instead of {{}}
  * it is faster
  * will be applied only if variable is changed
* dont use $scope
  * it is better to hide a scope and expose the members from the controller to the view via an intermediary object

## Directives
  * allows to extend HTML
  * AngularJS has a set of built-in directives
  * I can define my own directives

  >* **ng-app**
  >  * defines the root element of an AngularJS application
  >   * will auto-bootstrap (auto initialize) the application when a web page is loaded
  >* **ng-init**
  >   * directive defines initial values for an AngularJS application
  >   * normally not used
  >* **ng-model**
  >   * binds the value of HTML controls (input, select, textarea) to the application data
  >   * provide type validation for application data (number, email, required)
  >   * provide status for application data (invalid, dirty, touched, error)
  >   * provide CSS classes for HTML elements
  >   * bind HTML elements to HTML forms
  >* **ng-repeat**
  >   * directive actually clones HTML elements once for each item in a collection.

  ```html
  <div np-app="" ng-init="names=['Jan', 'Petr', 'Vasek']">
    <ul>
      <li ng-repeat="x in names">
        {{ x }}
      </li>
    </ul>
  </div>
  ```
  New directives are created by using the .directive function.\
  To invoke the new directive, make element with the same tag name as the new directive\

  ```html
  <body ng-app="myApp">
    <myNewDirective></myNewDirective>

    <script>
        var app = angular.module("myApp", []);
        app.directive("myNewDirective", function() {
          return {
            restrict : "A",
            template : "<h1>Made by a directive!</h1>"
          }
        })
    </script>
  </body>
  ```

  * `E` for Element name
  * `A` for Attribute
  * `C` for Class
  * `M` for Comment

## Expressions

  Are written inside double braces `{{ expression }}`.\
  Angular will output data exactly where expression is written.\
  AngularJS expressions bind AngularJS data to HTML the same way as the ng-bind directives.\
  AngularJS expressions are like JavaScript expressions. Can contain literals, operators and variables.\
  `{{ 5 + 5 }}` `{{firstName + " " + lastName}}`.\
  \
  You can change properties:
  ```html
  <input style="background-color:{{myCol}}" ng-model="myCol">
  ```

### Objects
  Works like JS objects
  ```html
  <div ng-app="" ng-init="person={firstName:'Lukas', lastName:'Posekany'}">
    <p>Hi name is {{person.firstName}}</p>
  </div>
  ```

### Arrays
  ```html
  <div ng-app="" ng-init="points=[1, 2, 5, 6, 8, 12]">
    <p>{{ points[2] }}</p>
  </div>
  ```

## Modules
  * module defines an application.
  * the module is a container for the application controllers.
  * controllers always belong to a module.

  ```html
  <div ng-app="myApp"></div>
  <script>
    var app = angular.module("myApp", []);
  </script>
  ```

  myApp parameter refers to an HTML element in which the application will run.\
  I can add a controllers, directives, filters, ...

  ```js
  var app = angular.module("myApp", [])
  ```

## Controllers
  Application in AngularJS are controlled by controllers.\
  Because of the immediate synchronization of the model and the view, the controller can be completely separated from the view.\
  **AngularJS controllers are regular JavaScript objects**\
  The `$scope` is the application object (the owner of application variables and functions)
  ```js
  var app = angular.module("myApp", []) {

    app.controller("myCtrl", function($scope) {
      $scope.firstName = "John";
      $scope.lastName = "Doe"
    })
  }
  ```

  ```html
  <div>
    <h1 ng-click="changeName()">{{ firstName }}</h1>
  </div>
  <script>
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope) {
      $scope.firstName = "Josef";
      $scope.lastName = "Novak"
      $scope.changeName = function() {
        $scope.firstName = "Lenka";
      }
      $scope.fullName = function() {
        return $scope.firstName + " " + $scope.lastName;
      }
    })
  </script>
  ```

## Model

## Data Binding

Is synchronization between the model and the view

## Scopes
  * The scope is the binding part between the HTML (view) and the JavaScript (controller).
  * The scope is an object with the available properties and methods.
  * The scope is available for both the view and the controller.

  The `$scope` object is passed as an argument to controller when it is initialized.\
  When adding properties to the `$scope` object in controller, the view gets access to these properties.\
  **The `$scope`** represents "model" in the view-model-controller system.\
  `$rootScope` is available to the entire application. If there is same variable in `$rootScope` and `$scope`, the application uses the one in the current scope.

  ```html
  <body ng-app="myApp">
    <p>Color of $rootScope: {{ color }}</p>
    <div ng-controller="myCtrl">
      <p>Color of $scope {{ color }}</p>
    </div>
    <p>Color of $rootScope is still: {{ color }}</p>
    <script>
      var app = angular.module('myApp', []);
      app.run(function($rootScope){
        $rootScope.color = "blue"
      })
      app.controller('myCtrl', function($scope){
        $scope.color = "red";
      })
    </script>
  </body>
  ```

## Filters

  * **currency** Format a number to a currency format.
  * **date** Format a date to a specified format.
  * **filter** Select a subset of items from an array
  * **json** Format an object to a JSON string.
  * **limitTo** Limits an array/string, into a specified number of elements/characters.
  * **lowercase** Format a string to lower case.
  * **number** Format a number to a string.
  * **orderBy** Orders an array by an expression.
  * **uppercase** Format a string to upper case.

  Adding filters to Expressions
  ```html
    <div ng-app="myApp" ng-controller="personCtrl">
      <p> The name is {{ lastName | uppercase }} </p>
    </div>
  ```

  ```html
    <div ng-app="myApp", ng-controller="namesCtrl">
      <ul>
        <li ng-repeat="x in names | orderBy:'country'">
          {{ x.name + " is from " + x.town }}
        </li>
      </ul>
    </div>
  ```

  ```html
  <ul>
    <li ng-repeat="x in people | filter:{name:'i'}"> {{ x.name }} </li>
  </ul>
  ```
  filter people by people.name and display if name includes 'i'\

### Custom filters
  can be created by registering a new `.filter` factory function with module
  `.filter('filterName', function(){ return function(x){ return txt } });`
  ```html
  <ul ng-app="myApp" ng-controller="namesCtrl">
    <li ng-repeat="x in names"> {{ x | myFormat }}</li>
  </ul>
  <script>
    var app = angular.module("myApp", []);
    app.filter("myFormat", function() {
      return function(x){
        let txt
        for(let i=0; i<x.length; i++) {
          c = x[i]
          if(i%2 == 0){
            let c = c.toUpperCase()
          }
          txt += c;
        }
        return txt;
      }
    })
  </script>
  ```

## Services
  * A service is a function, or object, that is available for, and limited to, AngularJS application.
  * services **must** be passed in the controller as an argument.

  services:
  * **$location** has methods which return information about the location of the current web page
  * **$http** makes a request to the server, and lets your application handle the response
    * `$http.get( "URL".then( function(response){ console.log(response.data) } ) )`
  * **$timeout** is a AngularJS version of `window.setTimeout` function
  * **$interval** is a AngularJS version of `window.interval` function

  ```html
  <div ng-app="myApp" ng-controller="myController">
    {{ myUrl }}
  </div>
  <script>
    var app = angular.module('myApp', []);
    app.controller('myController', function($scope, $location){
      $scope.myUrl = $location.absUrl()
    })
  </script>
  ```

  ```js
    var app = angular.module('myApp'[]);
    app.controller('myCtrl', function($scope, $http) {
      $http.get("welcome.html").then(function(response) {
        $scope.myWelcome = response.data;
      })
    })
  ```

### Custom Services
  To create service, connect service to the module:

  ```js
  app.service('myServiceName', function(){
    this.myFunc = function(x){
      return x.toString(16);
    }
  })
  ```

  To use custom made service, add it as a dependency when defining the controller:
  ```js
  app.controller('myCtrl', function($scope, myServiceName) {
    $scope.hex = myServiceName.myFunc(255)
  })
  ```


## Http

## Tables

## Select

## SQL

## DOM

## Events

## Forms

## Validation

## API

## Includes

## Animations

## Routing

## Application

## EXAMPLES:
### filter names by user input
```html
<div ng-app="myApp" ng-controller="namesCtrl">
  <input type="text" ng-model="test">
  <ul>
    <li ng-repeat="x in names | filter : test">
      {{ x }}
    </li>
  </ul>
</div>
<script>
  angular.module("myApp", []).controller("namesCtrl", function($scope){
    $scope.names = [
      'Jani',
      'Carl',
      'Margareth',
      'Hege',
      'Joe',
      'Gustav',
      'Birgit',
      'Mary',
      'Kai'
    ]
  })
</script>
```

### sort a table by clicking on header:

### ASYNC and return promices
```js
$scope.asyncFunc = function(){
  return $http({   // I will return promice which I can then use with .then(...)
    ...
  }).then(function(response) {
    ...
  })
}
var foo = $scope.asyncFunc()
foo.then(function(){
  // this will execute after async ends
})
```


# ONE PAGE APPLICATION

## HTML
* import **angular route**
* content will be displayed in tag with **ng-view**
* the scripts with **type="text/ng-template" id="/ID"** will be displayed in view
* the views are route due to extention of URL **#!/goToLocation**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>onepage angularjs application</title>
  </head>

  <script src=".../angular.min.js"></script>
  <script src=".../angular-route.min.js"></script>

  <body ng-app="myApp">

    <a href="#!/"></a>
    <a href="#!/second"></a>

    <div ng-view></div>
  </body>

  <script type="text/ng-template" id="/someID1">
    <h1>Hello one page application 1</h1>
    <p>{{message}}</p>
  </script>
  <script type="text/ng-template" id="/someID2">
    <h1>Hello one page application 2</h1>
    <p>{{message}}</p>
  </script>
</html>
```

```js
var app = angular.module("myApp", ['ngRoute']);
app.config(function($routeProvider){
  $routeProvider
  .when('/',{
    templateUrl : '/someID1',
    controller : 'firstCtrl'
  })
  .when('/second',{
    templateUrl : '/someID2',
    controller : 'secondCtrl'
  })
})

app.controller('firstCtrl', function($scope){
  $scope.message = "here is first view"
})
app.controller('secondCtrl', function($scope){
  $scope.message = "here is second view"
})

```
