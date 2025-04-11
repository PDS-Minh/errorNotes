Earlier, you can inquire, add, update, and delete data through simple manipulation using MongoDB Compass.

However, when entering data programmatically, you can manipulate the data by entering a query statement directly.

This is called Create Read Update Delete (CRUD).

Link => [MongoDB manual](https://www.mongodb.com/docs/manual/crud/)

# Create

There are two ways to create data in a collection

* db.collection.insertOne()

* db.collection.insertMany()

As you can see from the name, insertOne uses one piece of data and insertMany uses multiple pieces of data in batches.

The basic structure of insert is as follows.

```
db.collection.insertOne(
    <document>,
    {
      writeConcern: <document>
    }
)
```

## insertOne

When we put the virtual characters we added into MongoDB, they are expressed in a query statement as follows.

```
db.users.insertOne({
  "name": "Martine",
  "age": 33,
  "phone": "010-2222-3333",
  "hobby": [
	"read book",
	"soccer"
  ]
})
```

## insertMany

When you enter data in batches, you can enter it all at once in the form of a Json Array.

```
db.users.insertMany([
{
  "name": "Martine",
  "age": 33,
  "phone": "010-2222-3333",
  "hobby": [
	"read book",
	"soccer"
  ]
},
{
  "name": "Smith",
  "age": 30,
  "phone": "010-3333-4444",
  "hobby": [
	"basketball",
	"ski"
  ]
},
{
  "name": "Bob",
  "age": 32,
  "phone": "010-4444-5555",
  "hobby": [
	"bycicle",
	"baseball"
  ]
}
])
```

# Read

Here's how to query data in MongoDB.

```
db.users.find({ // collection
  name: "Bob",  // query
  age: { $gte: 30 } 
},{ // projection
  name: 1,
  age: 1
}).limit(3) // cursor modifier
```
* A query is an area for working with data.

* Projection is used to view or hide only the desired fields of the data.

As above, if you assign a value of 1 to name, age, you can only see name and age.

You can also expand Options in MongoDB Compass to set various query options.

![image](https://github.com/user-attachments/assets/c88a2c54-85c5-4f77-acb2-c16eef88c89b)

> 💡Tip
>
> age: {$gte: 30} to $gte means graterthen, which looks up all items with an age number of 30 or more.
> 
> Similar options include $gt (exceeded), $lt (less than), and $lte (less than).
> 
> query-comparison => [query-comparison](https://www.mongodb.com/docs/manual/reference/operator/query-comparison/)

# Update

There are three ways to update.

* db.collection.updateOne() : update one

* db.collection.updateMany() : update many

* db.collection.replaceOne() : This item is not used well, so if you want to use it, make sure to check the official document. 

[db.collection.replaceOne](https://www.mongodb.com/docs/manual/reference/method/db.collection.replaceOne/#mongodb-method-db.collection.replaceOne)

The basic structure of update is as follows.

```
db.collection.updateOne(
   <filter>,
   <update>,
   {
     upsert: <boolean>,
     writeConcern: <document>,
     collation: <document>,
     arrayFilters: [ <filterdocument1>, ... ],
     hint:  <document|string>,
     let: <document>,
     sort: <document>
   }
)
```

> 💡Tip
>
> The upsert option inserts if the filter does not have a matching condition.


**updateOne ** is only one viewed result updates the data.
```
db.users.updateOne(
  { name: "Bob" },
  { $set: { age: 40 } }
);
```

**updateMany ** updates all data that match the query conditions.

```
db.users.updateMany(
  { age: { $gt: 30 } },
  { $set: { age: 40 } }
);
```

# Delete

There are also two ways to delete.

* db.collection.deleteOne()

* db.collection.deleteMany()

The default structure of delete is as follows.

```
db.collection.deleteOne(
    <filter>,
    {
      writeConcern: <document>,
      collation: <document>,
      hint: <document|string>
    }
)
```

db.collection.deleteOne deletes one data that matches the query result.

```
db.users.deleteOne({
  name: "Bob"
})
```

db.collection.deleteMany deletes all data with matching query results, such as the name.

```
db.users.deleteMany({
  age: { $gt: 30 }
})
```
