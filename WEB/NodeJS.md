#NodeJS Express TypeScript

## Setting up Project
First install what is [needed](#Install)
1. create a project root folder
2. create [package.json](#package.json) with `npm init`
3. create [tsconfig.json](#tsconfig.json) with `tsc --init`
3. `npm install --save express`; `npm install --save @types/express`
3. create filesystem:
  * src - source files
    * [index.js](#insex.ts)
  * dist - distribution
5.
  *
## Project Structure
* dist/
* node_modules/
* src/
  * controllers/
  * interfaces/
  * middleware/
  * app.ts
  * server.ts
* package.json
* tsconfig.json

## Install
* node
* npm install -g express
* npm install -g typescript
* `npm install --save-dev @types/node @types/express` - update project so TypeScript can use the type declarations for Node.js and Express


## package.json
```json
"main": "src/index.js"
"scripts": {
  "dev": "ts-node dist/server.js",
  "start": "ts-node src/server.ts",
  "build": "tsc -p ."
}
```

## tsconfig.json
```json
{
    "compilerOptions": {
        "sourceMap": true,
        "target": "es6",
        "module": "commonjs",
        "outDir": "./dist",
        "baseUrl": "./src"
    },
    "include": [
        "src/**/*.ts"
    ],
    "exclude": [
        "node_modules"
    ]
}
```


## Static Files
`app.use(express.static('static'))` static will be folder the files are stored


## src/app.ts
main app
```ts
import * as express from 'express'
import { Application } from 'express'

class App {
  public app: Application
  public port: number

  constructor(appInit: { port: number; middleWares: any; controllers: any; }){
    this.app = express()
    this.port = appInit.port

    this.middlewares(appInit.middleWares)
    this.routes(appInit.controllers)
    this.assets()
    this.template()
  }

  private middlewares(middleWares: { forEach: (arg0: (middleWare: any) => void) => void;}) {
    middleWares.forEach(middleWare => {
      this.app.use(middleWare)
    })
  }

  private routes(controllers: { forEach: (arg0: (controller: any) => void) => void;}) {
    controllers.forEach(controller => {
      this.app.use('/', controller.router)
    })
  }

  private assets(){
    this.app.use(express.static('assets'))
  }

  public listen(){
    this.app.listen(this.port, () => {
      console.log(`App is listening on port ${this.port}`);

    })
  }
}
export default App
```

## src/server.ts
```ts
import App from './app'

import * as bodyParser from 'body-parser'
import loggerMiddleware from './middleware/logger'

import PostsController from './controllers/posts/posts.controller'
import HomeController from './controllers/home/home.controller'

const app = new App({
  port: 5000,
  controllers: [
    new HomeController(),
    new PostsController()
  ],
  middleWares: [
    bodyParser.json(),
    bodyParser.urlencoded({ extended: true}),
    loggerMiddleware
  ]
})

app.listen()
```

## middleware/logger.ts
shows HTTP verb and its path
```ts
import { Request, Response } from 'express'

const loggerMiddleware = (req: Request, resp: Response, next) => {
  console.log('Request logger: ', req.method, req.path);
  next()
}

export default loggerMiddleware
```

## interfaces/IControllerBase.interface.ts
every controller has to implement this interface
```ts
interface IControllerBase {
  initRoutes(): any
}

export default IControllerBase

```

## controllers/home.controller.ts
```ts
import * as express from 'express'
import { Request, Response } from 'express'
import IControllerBase from 'interfaces/IControllerBase.interface'

class HomeController implements IControllerBase {
  public path = "/"
  public router = express.Router()

  constructor(){
    this.initRoutes())
  }

  public initRoutes() {
    this.router.get('/', this.index)
  }
  index = {req: Request, res: Response} => {
    const users = {
      {
          id: 1,
          name: 'Ali'
      },
      {
          id: 2,
          name: 'Can'
      },
      {
          id: 3,
          name: 'Ahmet'
      }
    }

    res.render('home/index', { users })
  }
}

export default HomeController
```




## routes
```js
  var authRouter = require('./routes/auth')(router);
  var servicesRouter = require('./routes/services')(router);
  ....
  ..

  app.use('/auth', authRouter); // Route to authenticate login attempt
  app.use('/services', servicesRouter); // Route to perform other services
  ....
  ..
  // wildcard:
  app.get('*', (req, res) => {
    res.sendFile(path.join(__dirname + '/public/index.html'));
  });

  // INFO: Start the node server */
  app.listen(port, () => console.log(`Node's Express ice-dashboard-new is listening on
  Port ${port}..`));
```


## Environment variables
`console.log('The value of PORT is:', process.env.PORT);`

to load variables from .env file:
  * `npm install dotenv --save`
  * save enviromental variables onto the root of project into file called `.env`
  * `require('dotenv').load()`
  * `let port = process.env.PORT;` and so on
