# here is How mysql user can learn fast the mongodb


## 3.1 Create a Database
### MySQL Equivalent:
`CREATE DATABASE mydatabase;
USE mydatabase;
`
### MongoDB:

In MongoDB, you switch to a database using the use command. The database is created when you first store data in it.

MongoDB Shell
- javascript
`
use mydatabase
`
- Python
`
from pymongo import MongoClient
client = MongoClient('mongodb://localhost:27017/')
db = client['mydatabase']
`
- JavaScript (Node.js)
javascript
`
const { MongoClient } = require('mongodb');
const uri = 'mongodb://localhost:27017/';
const client = new MongoClient(uri);
async function run() {
  await client.connect();
  const db = client.db('mydatabase');
  // Proceed with operations
}
run();

`
## 3.2 Delete a Database
MySQL Equivalent:

sql
Copy code
DROP DATABASE mydatabase;
MongoDB:

MongoDB Shell
javascript
Copy code
use mydatabase
db.dropDatabase()
Python
python
Copy code
client.drop_database('mydatabase')
JavaScript (Node.js)
javascript
Copy code
await client.db('mydatabase').dropDatabase();
