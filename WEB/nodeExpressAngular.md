## NodeJS $ Express & Angular
* [NodeJS](NodeJS)
* [Angular](Angular.md)
* []()
**npm:** (Node Package Manager)

## Project life cycle
1. create a project folder
2. init node: `npm init` which creates a `package.json`
3. init angular in /client folder: `ng new client`
4. in testing use `ng serve` in client folder (port 4200), any time a change is made, it is automatically updated to browser
5. build angular app: `ng build`
  * use `ng build --output-path="some/path"` or set `outputPath` in `angular.json` to different folder
6. with nodejs serve angular app build directory as static content
7. with nodejs create route for api

## my scripts in package.json
`npm run script-name`
* "build": "cd ./client && ng build --output-path='some/path'",
* "start": "node app.js;"

## packages to be installed
* typescript - `npm install -g typescript` or `nmp install --global typescript`
* express - `npm install -g express`
* express libraries - `npm install -g cookie-parser body-parser morgan`
  * cookie-parser
  * body-parser
  * morgan - middleware simplyfying process of logging requests to application
<!-- * Nodemon - `npm install -g nodemon` Will monitor for any changes in source and automatically restart service. -->
* Angular `npm install -g @angular/cli`
* Angular CLI - Command Line Interface `npm install -g @angular/cli`

## Structure
* [client](#Client Folder)        - for angular application
* static - here will be builded angular application
* node_modules  - node modules
* [routes](NodeJS.md#routes)
* [app.js](NodeJS.md#app.js)
* [package.json](#package.json)
* [tsconfig.json](#tsconfig.json)

## Client Folder
* node_modules
* src
  * app
    * /shared `SharedModule` lives here, it imports the `CommonModule`
    * /styles
    * /services
    * app.component.html serves as the skeleton of the app. Typically has a <router-outlet> to render the routes and heir content
    * app.component.ts the Angular component that provides functionality to the app.component.html file
    * app-routing.module.ts main routes. This routes are registered to the Angular RouterModule in the AppModule.
    * app.module.ts the main module of the project which will bootstrap the app

  * environments
  * assets
  * index.html
  * [tsconfig.json](#tsconfig.json)
* e2e           - end-to-end test of the application, written in Jasmine and run by protrator e2e test runner. Automated tests to simulate user.

## package.json
package.json with all the dependencies
for server side set start script to
```json
{
  ...
  "scripts":{
    "build":
    "start": "cd ./client; ng build --output-path='some/path'; node app.js;"
  }
}
```

## tsconfig.json
settings for typescript compiler

## components services ...
* components in `/client/src/app/components` create components with `ng generate component someComponentName`
* services `ng generate service someServiceName` and add this also in 'providers' of the` @NgModule-declaraion` in the `app.module.ts`

## additional assets
For **backend assets** create a folder in the root folder of app and require them additionally in the app.js.
For **frontend assets** (images, files, ...) use the /client/src/assets folder.

## Static
