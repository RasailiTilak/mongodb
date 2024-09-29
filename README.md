# here is How mysql user can learn fast the mongodb


## 3.1 Create a Database
### MySQL Equivalent:
```
CREATE DATABASE mydatabase;
USE mydatabase;
```

### MongoDB:

In MongoDB, you switch to a database using the use command. The database is created when you first store data in it.

MongoDB Shell
- javascript
```
use mydatabase
```
- Python
```
from pymongo import MongoClient
client = MongoClient('mongodb://localhost:27017/')
db = client['mydatabase']
```
- JavaScript (Node.js)
javascript
```
const { MongoClient } = require('mongodb');
const uri = 'mongodb://localhost:27017/';
const client = new MongoClient(uri);
async function run() {
  await client.connect();
  const db = client.db('mydatabase');
  // Proceed with operations
}
run();

```
## 3.2 Delete a Database
### MySQL Equivalent:

sql
```
DROP DATABASE mydatabase;
```
### MongoDB:

- MongoDB Shell
 javascript

```
use mydatabase
db.dropDatabase()
```
- Python
python
```
client.drop_database('mydatabase')
```

- JavaScript (Node.js)
```
javascript
await client.db('mydatabase').dropDatabase();
```


# 4. Creating and Managing Collections (Tables)
## 4.1 Create a Collection (Table)
### MySQL Equivalent:

sql
```
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100),
  age INT
);
```
### MongoDB:


Collections are created when you insert the first document. Alternatively, you can create an empty collection.

###
- MongoDB Shell
 javascript
```
db.createCollection('users')
```
- python
```
collection = db['users']

```
- JavaScript (Node.js)
javascript
```
const collection = db.collection('users');
```

## 4.2 Delete a Collection (Table)
### MySQL Equivalent:

sql
```
DROP TABLE users;
```
### MongoDB:

- MongoDB Shell

javascript
```
db.users.drop()
```
- Python

```
db.drop_collection('users')
```

- JavaScript (Node.js)

javascript
```
await db.collection('users').drop();

```
## 4.3 Edit a Collection (Table)

Since MongoDB is schema-less, you don't need to define or alter the schema. You can add or remove fields (columns) in documents as needed.

### 4.4 Update a Collection (Table)
Updating a collection typically involves modifying the documents within it, such as adding indexes or changing data.

## 5. Working with Documents (Rows)
###
 5.1 Insert Documents (Rows)
##### MySQL Equivalent:

sql
```
INSERT INTO users (name, age) VALUES ('Alice', 30);
```
##### MongoDB:

- MongoDB Shell
javascript
```
db.users.insertOne({ name: 'Alice', age: 30 })
```
- Python
python
```
collection.insert_one({ 'name': 'Alice', 'age': 30 })
```
- JavaScript (Node.js)
javascript
```
await collection.insertOne({ name: 'Alice', age: 30 });
```
### 5.2 Query Documents (Rows)
#### MySQL Equivalent:

sql
```
SELECT * FROM users WHERE age > 25;
```
#### MongoDB:

- MongoDB Shell
javascript
```
db.users.find({ age: { $gt: 25 } })
```
- Python
python
```
for user in collection.find({ 'age': { '$gt': 25 } }):
    print(user)
```
- JavaScript (Node.js)
javascript
```
const cursor = collection.find({ age: { $gt: 25 } });
await cursor.forEach(console.log);
```
### 5.3 Update Documents (Rows)

#### MySQL Equivalent:

sql
```
UPDATE users SET age = 31 WHERE name = 'Alice';
```

#### MongoDB:

- MongoDB Shell
javascript
```
db.users.updateOne({ name: 'Alice' }, { $set: { age: 31 } })

```
- Python
python
```
collection.update_one({ 'name': 'Alice' }, { '$set': { 'age': 31 } })
```
- JavaScript (Node.js)
javascript
```
await collection.updateOne({ name: 'Alice' }, { $set: { age: 31 } });
```

### 5.4 Delete Documents (Rows)
#### MySQL Equivalent:

sql
```
DELETE FROM users WHERE name = 'Alice';
```
#### MongoDB:

- MongoDB Shell
javascript
```
db.users.deleteOne({ name: 'Alice' })
```
- Python
python
```
collection.delete_one({ 'name': 'Alice' })
```
- JavaScript (Node.js)
javascript
```
  await collection.deleteOne({ name: 'Alice' });
```


## 6. Working with Fields (Columns)
In MongoDB, since the schema is flexible, you can add or remove fields in documents at any time.

### 6.1 Add a Field (Column) to Documents
#### MySQL Equivalent:

sql
```
ALTER TABLE users ADD COLUMN email VARCHAR(100);
```
#### MongoDB:

- MongoDB Shell
javascript
```
db.users.updateMany({}, { $set: { email: null } })
```
- Python
python
```
collection.update_many({}, { '$set': { 'email': None } })
```
- JavaScript (Node.js)
javascript
```
await collection.updateMany({}, { $set: { email: null } });
```
### 6.2 Remove a Field (Column) from Documents
#### MySQL Equivalent:

sql
```
ALTER TABLE users DROP COLUMN age;
```
#### MongoDB:

- MongoDB Shell
javascript
```
db.users.updateMany({}, { $unset: { age: "" } })
```
- Python
python
```
collection.update_many({}, { '$unset': { 'age': "" } })
```
- JavaScript (Node.js)
javascript
```
await collection.updateMany({}, { $unset: { age: "" } });
```
### 6.3 Rename a Field (Column)
#### MySQL Equivalent:

sql
```
ALTER TABLE users CHANGE COLUMN email email_address VARCHAR(100);
```
#### MongoDB:

- MongoDB Shell
javascript
```
db.users.updateMany({}, { $rename: { email: 'email_address' } })
```
- Python
python
```
collection.update_many({}, { '$rename': { 'email': 'email_address' } })
```
- JavaScript (Node.js)
javascript
```
await collection.updateMany({}, { $rename: { email: 'email_address' } });

```



## 7. Data Types in MongoDB
MongoDB supports various data types similar to MySQL, but with some differences.

### 7.1 Common Data Types
```
Integer: NumberInt, NumberLong
Float: NumberDouble
String: String
Boolean: Boolean
Date: Date
Array: Array
Object: Object

```

#### 7.2 Storing Different Data Types
##### Integer


- MongoDB Shell

javascript
```
db.numbers.insertOne({ value: NumberInt(42) })
```
- Python
python
```
collection.insert_one({ 'value': 42 })
```
- JavaScript (Node.js)
javascript
```
await collection.insertOne({ value: 42 });
```

Note: In MongoDB, numbers without decimal points are stored as 32-bit or 64-bit integers based on their size.
##### Float
- MongoDB Shell

javascript
```
db.numbers.insertOne({ value: 3.14 })
```
- Python
python
```
collection.insert_one({ 'value': 3.14 })
```
- JavaScript (Node.js)
javascript
```
await collection.insertOne({ value: 3.14 });
```
##### String

Strings are stored as String data type.

Varchar Equivalent
In MongoDB, strings are not limited in length by default. If you need to enforce length, you can validate documents upon insertion.

## 8. CRUD Operations in Python
Below is a summary of how to perform CRUD operations in Python using pymongo.

#### 8.1 Connect to MongoDB
- python
```
from pymongo import MongoClient

client = MongoClient('mongodb://localhost:27017/')
db = client['mydatabase']
collection = db['users']
```
#### 8.2 Create (Insert)

- python
```
# Insert one document
collection.insert_one({ 'name': 'Bob', 'age': 25 })

# Insert multiple documents
collection.insert_many([
    { 'name': 'Carol', 'age': 27 },
    { 'name': 'Dave', 'age': 30 }
])

```
#### 8.3 Read (Query)
-python
```
# Find all documents
for user in collection.find():
    print(user)

# Find documents with a filter
for user in collection.find({ 'age': { '$gt': 25 } }):
    print(user)
```
#### 8.4 Update
- python
```
# Update one document
collection.update_one({ 'name': 'Bob' }, { '$set': { 'age': 26 } })

# Update multiple documents
collection.update_many({ 'age': { '$lt': 30 } }, { '$inc': { 'age': 1 } })

```
## 8.5 Delete
- python
```
# Delete one document
collection.delete_one({ 'name': 'Dave' })

# Delete multiple documents
collection.delete_many({ 'age': { '$gt': 28 } })

```
## 9. CRUD Operations in JavaScript (Node.js)
Below is a summary of how to perform CRUD operations in JavaScript using the MongoDB Node.js driver.

### 9.1 Connect to MongoDB
- javascript
```
const { MongoClient } = require('mongodb');

const uri = 'mongodb://localhost:27017/';
const client = new MongoClient(uri);

async function run() {
  await client.connect();
  const db = client.db('mydatabase');
  const collection = db.collection('users');

  // Perform operations here

  await client.close();
}
run().catch(console.dir);
```



### 9.2 Create (Insert)
- javascript
```
// Insert one document
await collection.insertOne({ name: 'Eve', age: 22 });

// Insert multiple documents
await collection.insertMany([
  { name: 'Frank', age: 24 },
  { name: 'Grace', age: 26 }
]);

```
### 9.3 Read (Query)
- javascript
```
// Find all documents
const cursor = collection.find();
await cursor.forEach(doc => console.log(doc));

// Find documents with a filter
const filteredCursor = collection.find({ age: { $gt: 23 } });
await filteredCursor.forEach(doc => console.log(doc));
```

### 9.4 Update
- javascript
```
// Update one document
await collection.updateOne({ name: 'Eve' }, { $set: { age: 23 } });

// Update multiple documents
await collection.updateMany({ age: { $lt: 25 } }, { $inc: { age: 1 } });
```
### 9.5 Delete
- javascript
```
// Delete one document
await collection.deleteOne({ name: 'Frank' });

// Delete multiple documents
await collection.deleteMany({ age: { $gt: 25 } });
```


## 10. Conclusion
You've now learned how to perform the following in MongoDB:

- Create, delete, and modify databases: Using use to switch/create and dropDatabase to delete.
- Create, delete, and modify collections (tables): Using createCollection, drop, and manipulating documents.
- Create, delete, update, and modify fields (columns): Using $set, $unset, and $rename operators.
- Store different data types: Storing integers, floats, strings, and understanding MongoDB's flexible data types.
- CRUD operations: Performing create, read, update, and delete operations on documents.

By comparing MySQL commands to MongoDB equivalents, you've leveraged your existing SQL knowledge to understand MongoDB's operations. Remember that MongoDB's flexibility allows for dynamic schemas, making it different from the rigid structure of MySQL.