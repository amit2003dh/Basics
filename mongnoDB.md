**MongoDB** is a **NoSQL, document-oriented database** used to store data in **JSON-like documents (BSON)** instead of rows and tables.

### In simple words

> MongoDB stores data as **documents**, not tables.

### What makes MongoDB different

* **Schema-flexible** → fields can change without migrations
* **Document-based** → data stored as key–value pairs
* **High performance** → fast reads and writes
* **Scalable** → easy horizontal scaling

### Basic structure

```
Database
 → Collections
   → Documents
```

### Example document

```json
{
  "name": "Amit",
  "role": "user",
  "orders": ["pizza", "burger"]
}
```

### Where MongoDB is used

* Web applications
* Real-time systems
* E-commerce & food delivery apps
* MERN stack projects

### Why developers choose MongoDB

* Natural fit for JavaScript/Node.js
* Handles nested and dynamic data easily
* Faster development for evolving apps

### Interview one-liner

> “MongoDB is a NoSQL document database that stores data in flexible JSON-like documents instead of tables.”

___

### MongoDB Shell Commands

`mongosh` → opens MongoDB shell

```bash
mongosh
```

`show dbs` → shows all databases

```js
show dbs
```

`use <db>` → switches or creates a database

```js
use foodApp
```

`db` → shows current database

```js
db
```

`show collections` → lists collections in current database

```js
show collections
```

`db.collection.insertOne()` → inserts one document

```js
db.users.insertOne({ name: "Amit", role: "admin" })
```

`db.collection.insertMany()` → inserts multiple documents

```js
db.users.insertMany([{ name: "A" }, { name: "B" }])
```

`db.collection.find()` → fetches documents

```js
db.users.find({ role: "admin" })
```

`db.collection.updateOne()` → updates first matched document

```js
db.users.updateOne({ name: "Amit" }, { $set: { role: "user" } })
```

`db.collection.updateMany()` → updates all matched documents

```js
db.users.updateMany({ role: "user" }, { $set: { active: true } })
```

`db.collection.deleteOne()` → deletes first matched document

```js
db.users.deleteOne({ name: "Amit" })
```

`db.collection.deleteMany()` → deletes all matched documents

```js
db.users.deleteMany({ active: false })
```

`db.collection.countDocuments()` → counts documents

```js
db.users.countDocuments()
```

`db.collection.find().sort()` → sorts results

```js
db.users.find().sort({ name: 1 })
```

`db.collection.find().limit()` → limits results

```js
db.users.find().limit(5)
```

`db.collection.find({}, projection)` → selects specific fields

```js
db.users.find({}, { name: 1, email: 1 })
```

`db.collection.createIndex()` → creates index for faster queries

```js
db.users.createIndex({ email: 1 })
```

`db.collection.drop()` → deletes a collection

```js
db.users.drop()
```

`db.dropDatabase()` → deletes current database

```js
db.dropDatabase()
```

---
Below is **ALL `find()` types**, **same clean format**, **nothing skipped**.
Each line = **command → short meaning → one example**.

---

### MongoDB `find()` Types

`find()` → fetches all documents

```js
db.users.find()
```

`find({ field: value })` → fetches documents matching condition

```js
db.users.find({ role: "admin" })
```

`find().pretty()` → displays formatted output

```js
db.users.find().pretty()
```

`find({}, projection)` → selects specific fields

```js
db.users.find({}, { name: 1, email: 1 })
```

`find().limit(n)` → limits number of documents

```js
db.users.find().limit(5)
```

`find().skip(n)` → skips given number of documents

```js
db.users.find().skip(5)
```

`find().sort({ field: 1 })` → sorts ascending

```js
db.users.find().sort({ name: 1 })
```

`find().sort({ field: -1 })` → sorts descending

```js
db.users.find().sort({ name: -1 })
```

`find({ field: { $gt } })` → greater than

```js
db.users.find({ age: { $gt: 18 } })
```

`find({ field: { $lt } })` → less than

```js
db.users.find({ age: { $lt: 60 } })
```

`find({ field: { $gte } })` → greater than or equal

```js
db.users.find({ age: { $gte: 18 } })
```

`find({ field: { $lte } })` → less than or equal

```js
db.users.find({ age: { $lte: 60 } })
```

`find({ field: { $ne } })` → not equal

```js
db.users.find({ role: { $ne: "admin" } })
```

`find({ field: { $in } })` → matches values in array

```js
db.users.find({ role: { $in: ["admin", "user"] } })
```

`find({ field: { $nin } })` → excludes values in array

```js
db.users.find({ role: { $nin: ["admin"] } })
```

`find({ $and })` → matches all conditions

```js
db.users.find({ $and: [{ role: "user" }, { active: true }] })
```

`find({ $or })` → matches any condition

```js
db.users.find({ $or: [{ role: "admin" }, { active: true }] })
```

`find({ field: { $exists } })` → checks field existence

```js
db.users.find({ email: { $exists: true } })
```

`find({ field: { $type } })` → checks data type

```js
db.users.find({ age: { $type: "number" } })
```

`find({ field: /regex/ })` → pattern matching

```js
db.users.find({ name: /^A/ })
```

`find({ field: { $size } })` → matches array size

```js
db.users.find({ skills: { $size: 3 } })
```

`find({ field: { $all } })` → array contains all values

```js
db.users.find({ skills: { $all: ["js", "react"] } })
```

`find({ field: { $elemMatch } })` → matches embedded array objects

```js
db.orders.find({ items: { $elemMatch: { price: { $gt: 100 } } } })
```

`findOne()` → fetches first matching document

```js
db.users.findOne({ role: "admin" })
```

---

### Interview One-Liner

> “MongoDB `find()` supports filtering, sorting, pagination, comparison, logical, and array-based queries.”

Below is **COMPLETE MongoDB Query Operators list**,
same **clean format** → **operator → short meaning → one example**.
Nothing extra. Nothing skipped.

---

### MongoDB Query Operators

#### Comparison Operators

`$eq` → equal to

```js
db.users.find({ age: { $eq: 25 } })
```

`$ne` → not equal to

```js
db.users.find({ role: { $ne: "admin" } })
```

`$gt` → greater than

```js
db.users.find({ age: { $gt: 18 } })
```

`$gte` → greater than or equal

```js
db.users.find({ age: { $gte: 18 } })
```

`$lt` → less than

```js
db.users.find({ age: { $lt: 60 } })
```

`$lte` → less than or equal

```js
db.users.find({ age: { $lte: 60 } })
```

`$in` → matches values in array

```js
db.users.find({ role: { $in: ["admin", "user"] } })
```

`$nin` → not in array

```js
db.users.find({ role: { $nin: ["admin"] } })
```

---

#### Logical Operators

`$and` → all conditions must match

```js
db.users.find({ $and: [{ role: "user" }, { active: true }] })
```

`$or` → any condition must match

```js
db.users.find({ $or: [{ role: "admin" }, { active: true }] })
```

`$not` → negates condition

```js
db.users.find({ age: { $not: { $gt: 30 } } })
```

`$nor` → none of conditions match

```js
db.users.find({ $nor: [{ role: "admin" }, { active: false }] })
```

---

#### Element Operators

`$exists` → checks field existence

```js
db.users.find({ email: { $exists: true } })
```

`$type` → checks data type

```js
db.users.find({ age: { $type: "number" } })
```

---

#### Evaluation Operators

`$regex` → pattern matching

```js
db.users.find({ name: { $regex: "^A" } })
```

`$expr` → compares fields

```js
db.orders.find({ $expr: { $gt: ["$paid", "$discount"] } })
```

---

#### Array Operators

`$all` → matches all array values

```js
db.users.find({ skills: { $all: ["js", "react"] } })
```

`$size` → matches array length

```js
db.users.find({ skills: { $size: 3 } })
```

`$elemMatch` → matches embedded document

```js
db.orders.find({ items: { $elemMatch: { price: { $gt: 100 } } } })
```

---

#### Bitwise Operators

`$bitsAllSet` → all bits set

```js
db.flags.find({ mask: { $bitsAllSet: 3 } })
```

`$bitsAnySet` → any bit set

```js
db.flags.find({ mask: { $bitsAnySet: 2 } })
```

---

#### Projection Operators

`$` → positional operator

```js
db.orders.find({ "items.id": 1 }, { "items.$": 1 })
```

`$slice` → limits array elements

```js
db.posts.find({}, { comments: { $slice: 3 } })
```

---

### Interview One-Line Summary

> “MongoDB query operators allow filtering using comparison, logical, array, and evaluation conditions.”




