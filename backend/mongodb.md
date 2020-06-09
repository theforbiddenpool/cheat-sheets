__MongoDB__ → database that stores data records (documents) for use by an application. It's a non-relational, NoSQL database. Mongo uses JSON as its document structure.
__Mongoose.js__ → npm module. Allows you to write object for Mongo as you would in JavaScript.

# MongoDB

# Mongoose
## Connecting to database
You should store the database URI in the `.env` file. Require the `mongoose` and connect to the database:
```javascript
mongoose.connect(process.env.<uri>, { useNewUrlParser: true, useUnifiedTopology: true });
```

## Interaction with the DB
The interactions with the db happen in handler functions, using the event system in Node.
```javascript
const func = function(done) {
  // ... do something
  if(error) return done(error)
  done(null, result)
}
```

__`done()` function__ → callback that tells us we can proceed after completing an asynchronous operation (inserting, searching, etc.). It's following the Node convention. Should be called as `done(null, data)` on success, or `done(err)` on error.

# Schema, Model & Document
__Schema__ → defines the shape of the documents within a collection. Each schema maps to a MongoDB collection. They are the building blocks for Models. They can be nested to create complex models.\
__Model__ → allows to create instances of our objects, called documents.

_Create new schema:_
```javascript
const Schema = mongoose.Schema
const personSchema = new Schema({
  name: { type: String, required: true },
  age: Number,
  favoriteFoods: Array
})
```

To use our schema definiton, we need to convert it into a Model we can work with.

_Converting schema into Model:_
```javascript
const Person = mongoose.model('Person', personSchema)
```

_Create & save a new record of a model:_
```javascript
const createAndMakePerson = function(done) {
  const person = new Person({<args>})
  person.save((err, data) => {
    if(err) return done(err)
    done(null, data)
  })
}
```

_Create multiple records:_\
You can use `Model.create()` to create multiple records. It accepts the array with the data and a callback function as arguments.
```javascript
const func = function(array, done) {
  Person.create(array, (err, data) => {
    if(err) return done(err)
    done(null, data)
  })
}
```

## Seaching the database
_Return all matching documents:_
```javascript
const func = function(personName, done) {
  Person.find({ name: personName }, (err, data) => {
    if(err) return done(err)
    done(null, data);
  })
}
```

_Return only one document:_
```javascript
const func = function(food, done) {
  Person.findOne({ favoriteFood: food}, (err, data) => {
    ...
  })
}
```
It is special useful when searching by properties that you have declared as unique.

_Find by ID:_
```javascript
const func = function(personId, done) {
  Person.findById(personId, (err, data) => {
    ...
  })
}
```
When saving a document, mongodb automatically adds the field _id, and set it to a unique alphanueric key. Searching by _id is an extremely frequent operation.

## Update and Removing Documents
_Update documents in bulk:_
```javascript
const func = function(personId, done) {
  Person.findById(person, (err, data) => {
    if(err) return done(err)

    data.favoriteFood.push(foodToAdd)
    data.save((err, data) => err ? done(err) : done(null, data))

    done(null, data)
  })
}
```
It is bound to the low-level mongo driver. It can bulk edit many documents matching certain criteria, but it only sends a 'status' message. You need to call `document.save()` to save it to the database.

_Update a document:_
```javascript
const func = function(filter, done) {
  let doc = await Person.findOneAndUpdate(filter, update, { new: true })
  done(null, doc)
}
```
The `new: true` option returns the document after `update` was applied, as by default it returns the document as it was before it. `findOneAndUpdate()` returns the document itself, not a result object.\
There is also a method to find by id: `findByIdAndUpdate()`.

_Remove a document:_
```javascript
let doc = await Person.findByIdAndRemove(personId)
```
There is another method to find using another type of filter: `findOneAndRemove()`.

_Delete all documents matching given criteria:_
```javascript
Person.delete(filter, (err, data) => err ? done(err) : done(null, data))
```
It returns a JSON object containing the outcome of the operation, and the number of items affected.

## Query Chain
If you don't pass the callback as the last arguments to `Model.find()`, the query is not executed. You can build up a query using chaining syntax. The query is executed when you call `.exec()` in the chain.
```javascript
Person.find({favoriteFoods: foodToSearch})
  .sort({ name: 'asc' })
  .limit(2)
  .select('name favoriteFoods')
  .exec((err, data) => (err) ? done(err) : done(null, data))
```


# Keywords
NoSQL database → this type of database stores all associated data within one record, instead of across many preset tables. Some of its benefits are:
- __Scalability__ → by default, they are split across many systems, making it easir to improve performance at a lower cost.
- __Flexibility__ → new datasets and properties can be added to a document without the need to make a new table.
- __Replication__ → copies of the database run in parallel. So if one goes down, one of the copies becomes the new primary data source.

# Sources
[freeCodeCamp](https://freecodecamp.org)\
[mongoose Docs](https://mongoosejs.com/docs)