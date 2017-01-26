# Lets Mongoose

**Within your squads explore these questions**

## What is an ODM?
```
- Object Document Mapper - maps between an Object Model and a Document Database.

```

## What is MongooseJS?
```
- Middleware for providing a schema and modeling your application data for use with MongoDb.
- 'Wrapper' for MongoDB
- Shell that organizes and structures data to make MongoDB easier to use
- Mongoose is not schema-less

```

## Why do we need MongooseJS?
```
It is an abstraction on top of working with Mongo to provide a schema and make it easier to 
perform CRUD operations because it makes working with Mongo more like working with Javascript 
objects.

```

## What does the word "abstraction" mean?
```
It is a way of removing complexity by providing an interface where we do not have to work with 
the low level details because they are already taken care of for us "under the hood" by the 
language/library/middleware etc.

```

## How do we use mongoose?
```
QuickStart Guide: http://mongoosejs.com/docs/

var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test');

```

## What are models in Mongoose?
```
Models are fancy constructors compiled from our Schema definitions. 
Instances of these models represent documents which can be saved and retrieved from our database. 
All document creation and retrieval from the database is handled by these models.

```

## Define what schema means in Mongoose?
```
Everything in Mongoose starts with a Schema. 
It is a plan or outline of how we will structure our mongoDB documents for a specific type of entry.
In the example below, we are creating a 'structural blueprint' for all blog posts.
Each schema maps to a MongoDB collection and defines the shape of the documents within that collection.

var blogSchema = new Schema({
  title:  String,
  author: String,
  body:   String,
  comments: [{ body: String, date: Date }],
  date: { type: Date, default: Date.now },
  hidden: Boolean,
  meta: {
    votes: Number,
    favs:  Number
  }
});

The permitted SchemaTypes are

String
Number
Date
Buffer
Boolean
Mixed
ObjectId
Array

If you are dealing with a collection of users, your schema would look something like this.

Name - String
Age - Number
Gender - String
Date of Birth - Date

And if you are dealing with a collection of products, your schema will look something like this

SKU - String
Name - String
Price - Number
InStock - Boolean
Quantity - Number

```

## How do we connect to our database?
```
mongoose.connect('localhost', 'gettingstarted');

```

## What is a "model"?
```
 A Fancy constructor compiled from schema definitions. Instances of these models 
represent the documents which can be saved and retireved from the database.  All of the
documents created or retrieved from the database are handled by these models.

```

## What is data denormalization and data deduplication?
```
data denormalization is the process of trying to improve the read performance
of a database at the expense of write performance.  done by adding redundant copies
of data or grouping data; often motivated by needing to carry out large amount of read ops.

data deduplication is a special data compression technique for eliminating
duplicate copies of repeating data, AKA Intelligent(data Compression & Single
Instance (data) Storage. 

```

## What is "built-in-typecasting" in Mongoose?
```
Mongoose will automatically force a data type to act as the given schematype for a single transaction. 

```

## What is the "population" feature in Mongoose
```
There are no joins in MongoDB, but might need to reference other collections.
Population is the process of automatically replacing specified paths in the document
with documents from other collections.  Population can be used on: a single document,
multiple documents, plain object, multiple plain pobjects, or all objects returned
from a query.  

```

## What does "virtual" do in Mongoose?
```
- (http://mongoosejs.com/docs/2.7.x/docs/virtuals.html)
- "Temporary" properties on model instance
- Virtual attributes are properties that are useful to have around but do not
    persist in the database
```
```js
// If you want the virtual field to be displayed on client side, then set 
// {virtuals: true} for toObject and toJSON in schema options as below ... :
var PersonSchema = new Schema({
    name: {
        first: String
      , last: String
    }
}, {
  toObject: {
  virtuals: true
  },
  toJSON: {
  virtuals: true 
  }
});

// ... then set: 
var Person = mongoose.model('Person', PersonSchema);

var theSituation = new Person({
    name: { first: 'Tiny', last: 'Meowingtons' }
});

// declare virtual attribute on Person
PersonSchema
.virtual('name.full')
.get(function () {
  return this.name.first + ' ' + this.name.last;
});

// ... then to retrieve name.full ... : 
theSituation.name.full;

```

## Explain built-in-promises in Mongoose?
```
- (http://mongoosejs.com/docs/promises.html) 
- Mongoose async operations (like .save() or queries) return Promises
- Then you can use operations like .then() / .exec() (if using .co() )
```
```js
var query = Band.findOne({name: "Guns N' Roses"});
assert.ok(!(query instanceof require('mpromise')));

// A query is not a fully-fledged promise, but it does have a `.then()`.
query.then(function (doc) {
  // use doc
});

// `.exec()` gives you a fully-fledged promise
var promise = query.exec();
assert.ok(promise instanceof require('mpromise'));

promise.then(function (doc) {
  // use doc
});

```

## How are documents mapped in Mongoose?
```
- (http://mongoosejs.com/docs/documents.html)
- Mongoose documents represent a one-to-one mapping to documents as stored in MongoDB. 
- Each document is an instance of its Model.

```

## What are custom instance methods and static methods?
```
- (http://mongoosejs.com/docs/2.7.x/docs/methods-statics.html)
- .method() adds an `instance method` to documents constructed from Models
```
```js
var schema = kittySchema = new Schema(..);

schema.method('meow', function () {
  console.log('meeeeeoooooooooooow');
})

```
```
- .static() adds static `class` methods to the Models itself
```
```js
var schema = new Schema(..);
schema.static('findByName', function (name, callback) {
  return this.find({ name: name }, callback);
});


```

## What are the 8 built-in types that we can specify for our properties in Mongoose?
```
The permitted SchemaTypes are

String
Number
Date
Buffer
Boolean
Mixed
ObjectId
Array

```


**Review this code snippet from Mongoose's homepage**

```
var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test');

var Cat = mongoose.model('Cat', { name: String });

var kitty = new Cat({ name: 'Zildjian' });
kitty.save(function (err) {
  if (err) {
    console.log(err);
  } else {
    console.log('meow');
  }
});

```

**Resources**
[Google Search Engine is your best friend](https://www.google.com/)
[Mongoose Official Doc](http://mongoosejs.com/)

