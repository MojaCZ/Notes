My current version: 3.6

important files:
`/etc/mongod.conf` - --bind_ip 0.0.0.0
`/var/log/mongodb`
`/var/lib/mongodb`

ubuntu commands:
`sudo systemctl start mongod`   // status, stop, restart
`mongo` to start shell
`systemctl daemon-reload` update systemd services
`netstat -plntu` to check if mongodb service is serving (port 27017)
`sudo systemctl enable mongodb` to enable MongoDB when system starts
`mongo -u admin -p admin123 --authenticationDatabase admin` to connect
`mongo mongodb://192.168.1.2:27017` to connect to server on address

# shell
`use admin` to use admin user
'db.createUser({user: "admin", pwd:"password", role: [{role:"root", db:"admin"}]})'




# collections
are similar to tables in relation databases
`db.createCollection('collectionName');`
`show collections;`

# documents
`db.collectionName.insert({});` to insert document into collection
`db.collectionName.insert([{...},{...}]);` to insert multiple document into collection
`db.collectionName.find()` to list all documents in collection
`db.collectionName.find().pretty()`
`"_id":ObjectId("156118616....")` is created automatically
`db.collectionName.remove({name:"John"})` will delete all
document match querry,
`db.collectionName.remove({name:"John"}, {justOne:true})` will delete first match

* if I don't add a field to document, and I would want to find it later (.find()) it is considered to be a null value even though it is not there

## find
`db.collectionName.find({age:{$gt:40}}).pretty()` will return all with age grater then

`db.collectionName.find().sort({name:1})`
`db.collectionName.find().count()`
`db.collectionName.find().limit(4)` will limit output to 4 documents
`db.collectionName.find().forEach(function(doc){print("Customer Name: "+doc.name)});`

## updating fields
`db.collectionName.update({name:"John"}, {name:"Peter", surname:"Benes", age:"20"})` will update all documents with name John !! and update/add fields specified in second argument, It will also **delete** fields which wasn't specified
* **$set** `db.collectionName.update({name:"John"}, {$set:{age:20}})` will leave previous records and just update/add given
* **$inc** `db.collectionName.update({name:"John"}, {$inc:{age:5}})` will increment his age by 5
* **$unset** `db.collectionName.update({name:"John"}, {$unset:{age:1}})` to get rid of field
* **$rename** `db.collectionName.update({name:"John"}, {$rename:{"name":"first_name"}})` will rename field


`db.collectionName.update({name:"John"}, {name:"Peter", surname:"Benes", age:"20"}, {upsert: true})` will create document if it doesn't exists


# commands
* `use "DATABASE NAME"` create/select database
* `db` to check which database is selected
* `show dbs` to see all databases (doesn't show empty databases)
* `db."collection name".insert("data to insert, for example {"name": "xcv"}")` add data to database
* `show collections` to show mine collections
* `db."name of collection".drop()`
* `db.dropDatabase()`
* `db.createCollection("name", "options")`
  * example `db.createCollection("tags", {capped:true, size:1000,  max:2})`  maximum size is 2 items
  * add to collection `db.tags.insert([{"database":["mysql", "postgresql", "mongodb"]}, {"mongodb":"nosql"}])`
  `db.tags.find().pretty()
  `
  * !!! if I add another item, one item will be dropped from collection because max size is 2 `db.tags.insert({"database":"nodata"})` `db.tags.find().pretty()`
* `db.tags.find().pretty()` to show data in database

* `db.posts.insert({title:"Learning mongodb", description:"tutorial explaning ...", tags:["mongodb", "database", "NoSQL"], likes:100})`
* `db.posts.update({_id:ObjectId("5dbd5217...")}, {"title" : "lear...", description:...,...,...})` to update whole data of id
* `db.posts.update({_id:ObjectId("5dbd5217...")}, {$set: {"tags": ["mongodb", "NoSQL"]}}` to update just one item

* **find**
  * `find()`
  * `findOne()`
  * `db.posts.find({title:"Some Title"}).pretty()`
  * `db.posts.find({"likes":{$lt:500}}).pretty()`
    * **$lt** Less Than
    * **$lte** Less Than Equals
    * **$gt** Greater Then
    * **$gte** Grater Then Equals
    * **$ne** Not Equal
    * **$and** `db.posts.find( {$and:[ {"likes":{$gt:200}} , {"likes":{$lt:500}} ]} ).pretty()`
    * **$or**
  * `db.posts.remove({"title":"Some Title"})`
  * Projection `db.posts.find({},{_id:0, title:1, tags:1}).pretty()`
    * `.find({}` - I want all data
    * 1 or 0 stands for true or false `{_id:0, title:1, tags:1}` - display \_id false, title true, tags true
    * limits `db.posts.find().limit(10)`
    * sort `db.posts.find().sort({likes:1}).pretty()`

# users
after installing mongoDB, there are no users, so anyone can login into the system
## admin
1. create admin user:
  * use admin
  * create admin user:
2. allow authentication in `/etc/mongodb.conf` -> auth=true
3. after login into mongo shell activated user `db.auth("admin", "?@]34qF,!.<(/ZZ<" )`
```
db.createUser(
  {
    user: "admin",
    pwd: "?@]34qF,!.<(/ZZ<",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" }, "readWriteAnyDatabase" ]
  }
)
```

change password:
`db.changeUserPassword("myUserAdmin", "admin")`

## usual user
`use test`
```
use mealPlannerdb
db.createUser(
  {
    user: "mealAdmin",
    pwd: "g9p\KMSG`XxSZ+mY",
    roles: [ { role: "readWrite", db: "mealPlannerdb" },
             { role: "read", db: "reporting" } ]
  }
)
```
login will work only at test db - `use mealPlannerdb`, `db.auth("mealAdmin", "5hb9cWV8wJQgbUg4")`

## mongoose
`npm install --save mongoose`
`npm install @types/mongoose`

create Schema, create model
`?authSource=admin`

```ts
import mongoose from 'mongoose';
var mongoOpt = {
  "user":process.env.DB_USER,
  "pass":process.env.DB_PW,
   useNewUrlParser: true,
   useUnifiedTopology: true
}
await mongoose.connect("mongodb://176.222.224.212:27017/mealPlannerdb?authSource=admin", mongoOpt);
```

### create schema
```ts
// /src/models/resource.ts

import mongoose from 'mongoose';

const resourceSchema = new mongoose.Schema({
  _id: mongoose.Schema.Types.ObjectId,
  name: String,
  units: Object,
  // ...
  // ...
},{collection: 'resources'})

var Resource : mongoose.Model<any> = mongoose.model("Resource, resourceSchema")

export Resource
```

### find
```ts
// app.ts

import Resource = require('./models/resource');

Resource.find({name: "someName"})
  .exec()
  .then((doc:any) => {console.log(doc)})
  .catch((err:any) => console.log(err))
```


### findByIdAndRemove

```ts
Resource.findByIdAndRemove("5eadceb044c3bb01184ed9b8")
  .exec()
  .then((result:any) => {console.log("REMOVE", result)})
  .catch((err:any) => console.log("REMOVE", err))
```

### create new document

```ts
const newResource = new Resource({
  _id: new mongoose.Types.ObjectId(),
  name: "Ahoj",
  units: {"name": "g", "grammage":"1"},
  energy: 10,
  prot: 10,
  carb: 10,
  fat: 10,
  fib: 10,
  allergens: "al1",
  category: "cat1"
})

newResource.save()
.then((result:any) => {console.log(result)})
.catch((err:any) => {console.log(err)})
```

### findOneAndUpdate
```ts
let query = { /* query */ };
let update = {name: "newName"};
let options = {upsert: true, new: true, setDefaultsOnInsert: true};
let model = await Model.findOneAndUpdate(query, update, options);
```
