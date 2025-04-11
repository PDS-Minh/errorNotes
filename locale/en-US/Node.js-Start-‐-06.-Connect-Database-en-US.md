# Index

* [Using MongoDB in Node.js](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-06.-Connect-Database-en-US#using-mongodb-in-nodejs)
    * [Install Postman](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-06.-Connect-Database-en-US#install-postman)
    * [Separating DB Configuration Files](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-06.-Connect-Database-en-US#separating-db-configuration-files)
    * [Setting mongodb connection & disconnection
](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-06.-Connect-Database-en-US#setting-mongodb-connection--disconnection)
    * [Create a user.js file and create a DB action API
](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-06.-Connect-Database-en-US#create-a-userjs-file-and-create-a-db-action-api)

Let's start a web program using MongoDB in earnest.

I've also added a MongoDB guide, so please check the guide first.

Link => [MongoDB-Guide](https://github.com/pmirnc-dev/pds-welcome/wiki/MongoDB-Guide-en-US)

# Using MongoDB in Node.js

To connect Node.js and MongoDB, you must install the Mongodb package at npm.

1. Open vscode.

2. Open Terminal and type npm i mongodb to install mongodb package.

![image](https://github.com/user-attachments/assets/2154fed4-e55b-4fa9-a27d-a1085b844294)

## Install Postman

Postman is a program that can test REST API communication.

Link => [https://www.postman.com/downloads/](https://www.postman.com/downloads/)

The installation is simple.

1. Download the appropriate version for each operating system.

![image](https://github.com/user-attachments/assets/c9ccc00d-ae7d-4bd8-b7ad-a4d44c74b6de)

2. When the download is complete, run the installation file.

![image](https://github.com/user-attachments/assets/986251d4-ea48-483f-97a0-6569c507da12)

I want to show you the installation scene, but I already have the program installed, so it's been updated...

## Separating DB Configuration Files

Create a DB-related configuration file.

You can connect and use mongodb in one file, but by separating the configuration file, it increases code readability and facilitates maintenance.

Create a db.js file.

## Setting mongodb connection & disconnection

Earlier, we decided to use the .env file to hide the secret information.

Add the Database and Collection names to the .env file.
```
...
DB_NAME=mydatabase
COLLECTION_USERS=users
```

And write db setup code in db.js as below.

```javascript
// db.js
import { MongoClient } from 'mongodb';
import dotenv from 'dotenv';

dotenv.config();

// Setting MongoDB and URL
const dbHost = process.env.DB_HOST;
const dbPort = process.env.DB_PORT;
const dbName = process.env.DB_NAME;
const dbUrl = `mongodb://${dbHost}:${dbPort}/`;

// Create MongoDB Client
const client = new MongoClient(dbUrl);

// Database Connection Methon
export async function connectDB() {
  try {
    await client.connect();
    console.log("✅ Success to MongoDB Connection!");
    const db = client.db(dbName);
    return db;
  } catch (err) {
    console.error("❌ Failed to MongoDB Connection:", err);
    throw err;
  }
}

// Database Connection Close Methon
export async function closeDB() {
  try {
    await client.close();
    console.log("🔒 Close MongoDB Connection.");
  } catch (err) {
    console.error("❌ Failed to Close MongoDB Connection:", err);
  }
}



```

```javascript
const dbUrl = `mongodb://${dbHost}:${dbPort}`;
```

> 💡Tip
>
> In the code above, the **backtick(``)** is more convenient when creating new strings.
> As an example, I want to get dbHost, dbPort from .env and make dbUrl.
> Let's compare the new string generation method.

```javascript
// Old
const dbUrl = 'mongodb://' + dbHost + ':' + dbPort;

// New
const dbUrl = `mongodb://${dbHost}:${dbPort}`; 

// result => mongodb://localhost:27017
```

> 💡Tip
>
The **export** before the > connectDB and closeDB methods is a keyword that makes the method or variable accessible from an external file.
>
> How to use it is at the bottom.


## Create a user.js file and create a DB action API

### Create a users.js file.

Copy the previously created serverExpress.js file and change it to a new name: users.js.

And erase the rest of the contents except for these codes.

```javascript
import express from 'express';
import dotenv from 'dotenv';

dotenv.config();

const app = express();
const port = 3000;
```

### Get MongoDB connection and exit methods

I'll get the MongoDB connection, shutdown method I added in 4.

I will also add ObjectId to query the ObjectId value in MongoDB.

```javascript
...
import { connectDB, closeDB } from './db.js';
import { ObjectId } from 'mongodb';
```

Add `app.use(express.json());` under the port variable.

If you declare this code, Express will need to add a request in JSON form to parse it.

```javascript
app.use(express.json());
```

### Express & MongoDB Server Start

I will try to connect to MongoDB when running Express server.

```javascript
async function startServer() {
  try {
    const dbName = process.env.DB_NAME;
    db = await connectDB();
    collection = db.collection(dbName);
    
    app.listen(port, () => {
      console.log(`🚀 Running on http://localhost:${port}!`);
    });
  } catch (err) {
    console.error('❌ Server Start Error:', err);
  }
}
```

### Create & Find User
Let's try adding users using a web server instead of Compass.

It is time for the REST API described in the REST API part of the Node.js guide to appear.

Link => [REST API](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-04.-REST-API-en-US)

You must use the POST API to create new users.

You can easily design REST APIs using Express.

```javascript
app.post('/users', async (req, res) => {
  try {
    const newUser = req.body;
    const result = await collection.insertOne(newUser);
    res.status(201).json({ message: '📥 Success Create User!', userId: result.insertedId });
  } catch (err) {
    res.status(500).json({ error: '❌ Failed Create User', details: err.message });
  }
});

```

The app.method name can be used to distinguish methods such as GET, POST, etc

After that, set the path to which address you want to receive it.

Even if you're exposed to the outside, it's better to name it short so that you don't know what you're doing.

Example) **Create**
* ❌: POST /create/users
* ✅: POST /users

Example) **Read**
* ❌: GET /find/users?id=myid1234
* ✅: GET /users or /users?id=myid1234

Example) **Delete**
* ❌: DELETE /delete/users/id
* ✅: DELETE /users/id

I will add POST that stores data and GET API that inquires as below.

```javascript
import express from 'express';
import dotenv from 'dotenv';
import { connectDB, closeDB } from './db.js';
import { ObjectId } from 'mongodb';

dotenv.config();

const app = express();
const port = 3000;

app.use(express.json());

let db;
let collection;

async function startServer() {
  try {
    const users = process.env.COLLECTION_USERS;
    db = await connectDB();
    collection = db.collection(users);

    app.listen(port, () => {
      console.log(`🚀 Running on http://localhost:${port}!`);
    });
  } catch (err) {
    console.error('❌ Server Start Error:', err);
  }
}

// Create User
app.post('/users', async (req, res) => {
  try {
    const newUser = req.body;
    const result = await collection.insertOne(newUser);
    res.status(201).json({ message: '📥 Success Create User!', userId: result.insertedId });
  } catch (err) {
    res.status(500).json({ error: '❌ Failed Create User', details: err.message });
  }
});

// Search All User
app.get('/users', async (req, res) => {
  try {
    const users = await collection.find().toArray();
    console.log(users);
    res.status(200).json(users);
  } catch (err) {
    res.status(500).json({ error: '❌ Failed Search User', details: err.message });
  }
});

startServer();
```

```text
D:\my-test\nodejs-guide> node users.js
✅ Success to MongoDB Connection!
🚀 Running on http://localhost:3000!
```

### Test - Create

Run the previously installed Postman program.

Press the + button in the left menu and press REST API basics to conveniently create REST API test templates.

![image](https://github.com/user-attachments/assets/5b22d94e-c562-414b-a444-44b7a43a029f)

You can set common variables in Variables as shown in the picture above.

Change the initial and current values to localhost:3000 and press `Ctrl + S` to save your changes.

![image](https://github.com/user-attachments/assets/f8d00b3e-877c-405c-9c6f-aeea2f86e6ee)

1. Click Post data on the left to test the Post.

2. Clear the preconfigured address and modify it to '{{base_url}}/users'.

3. Click Body.

4. Click raw.

5. Enter the information you want to store in the input box in JSON format.

```json
{
	"name": "Jhon",
    "age": 31,
    "phone": "010-5555-6666",
    "hobby": [
        "youtube"
    ]
}
```
6. Click the send button on the right to display the test results at the bottom.

![image](https://github.com/user-attachments/assets/23500df1-3a16-40db-be4a-f2889c999fff)

You can also see that Jhon has been added in Compass.

![image](https://github.com/user-attachments/assets/465e1826-d276-4968-bea3-bd395bb7133d)


### Test - Read

Let's test the GET method as well.

1. Click Get data on the left and type {{base_url}}/users.

2. Click the Send button to see a list of users at the bottom.

![image](https://github.com/user-attachments/assets/4bd692fc-8ee2-4464-bd2d-a543d601669a)


### Install the nodemon package

You can shut down the server that you run on the terminal by pressing `Ctrl + C`.

It's very annoying to keep turning it off and on every time you change the server code, so install a new package

You can restart the server whenever the code changes.

1. In Termianl, type `npm install -- save-dev nodemon` to install the nodemon package.
2. When you run the server, you can run it with `nodemon users.js`.
3. You can add the following to the scripts in package.json.

```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server.js",
    "start:express": "node serverExpress.js",
    "start:dev": "nodemon users.js"
  },
```

4. If you enter npm run start:dev in Terminal, the server will run.

```
npm run start:dev

> nodejs-guide@1.0.0 start:dev
> nodemon users.js

[nodemon] 3.1.9
[nodemon] to restart at any time, enter `rs`
[nodemon] watching path(s): *.*
[nodemon] watching extensions: js,mjs,cjs,json
[nodemon] starting `node users.js`

✅ Success to MongoDB Connection!
🚀 Running on http://localhost:3000!
```

### Test - Find a specific user

It is a waste of server resources to check the entire user every time, so I will use the Unique value to find the user.

The _id value is the unique value generated by MongoDB by default.

If you don't want to create a unique value, it's easier to use _id.

This _id represents a value encrypted by combining special circumstances or time values.

I will add a new GET API.

```javascript
// Search User ID
app.get('/users/:id', async (req, res) => {
  try {
    const userId = new ObjectId(req.params.id);
    // console.lod(req);
    const user = await collection.findOne({ _id: userId });
    if (!user) {
      return res.status(404).json({ error: '❌ Not Found User.' });
    }
    res.status(200).json(user);
  } catch (err) {
    res.status(500).json({ error: '❌ Failed Found User', details: err.message });
  }
});
```

In `/user/:id`, `:id` is a promise to send an id value to that location.

When testing, if you make a GET request with `/user/67a023f6e4037912b6c68462`, 

you can see that the value `67a023f6e4037912b6c68462` is contained in `req.params.id`.

If you add `console.lod(req);` you can see that there are a lot of values inside the req.

1. In Postman, in Get data, click ... to the right.

![image](https://github.com/user-attachments/assets/0422a6a7-28d2-4d2c-ba38-f3413c959033)

2. Press Duplate to copy the API.

![image](https://github.com/user-attachments/assets/6add931f-d5db-4175-8fc0-136770d3dd15)

3. Change name and save.

![image](https://github.com/user-attachments/assets/b249c57e-2000-43f0-96b9-f34a3817ef34)

4. You can view the query results by changing the contents of the app path and clicking Send.

![image](https://github.com/user-attachments/assets/89f04817-10d1-4fe6-b0f1-f4111c46387f)

> 💡Tip
>
> Postman has an automatic save function, but it's a beta version, so if there's a change, let's save it manually.


### Test - Update User info

```javascript
// Update User Info
app.put('/users/:id', async (req, res) => {
  try {
    const userId = new ObjectId(req.params.id);
    const updateData = { $set: req.body };
    const result = await collection.updateOne({ _id: userId }, updateData);
    if (result.matchedCount === 0) {
      return res.status(404).json({ error: '❌ Not Found User' });
    }
    res.status(200).json({ message: '✏️ Success Patch User Info!' });
  } catch (err) {
    res.status(500).json({ error: '❌ Failed Patch User', details: err.message });
  }
});
```

The PUT method is a method used to update information.

Add the above code and open the Update data in Postman.

Select Body > raw as in Create and enter the data you want to modify in JSON format.

I will revise Jhon's hobby data.

Put the data you want to modify in JSON format, modify PATH, and click Send.

![image](https://github.com/user-attachments/assets/8bd22318-7e9f-4d41-9f7e-1f0275b78b4c)

You can check that Jhon's information has changed if you look it up with Compass.

![image](https://github.com/user-attachments/assets/9b3e7bc0-1c99-4797-8a34-2cb01b822be9)

### Test - Delete User info

This is a test, so let's do Hard Delete.

Jhon user has left, so you need to delete Jhon's information.

```javascript
// Delete User Info
app.delete('/users/:id', async (req, res) => {
  try {
    const userId = new ObjectId(req.params.id);
    const result = await collection.deleteOne({ _id: userId });
    if (result.deletedCount === 0) {
      return res.status(404).json({ error: '❌ Not Found User for Delete.' });
    }
    res.status(200).json({ message: '🗑️ Success Delete User!' });
  } catch (err) {
    res.status(500).json({ error: '❌ Failed Delete User', details: err.message });
  }
});
```

Add the above code and select Delete data from Postman.

Modify the Path information and click send.

![image](https://github.com/user-attachments/assets/71df3b82-b986-424b-857a-cc7fa550f33d)

If the deletion was successful, Compass can also verify that Jhon's information has disappeared.

![image](https://github.com/user-attachments/assets/e1f588b0-e3ee-495b-b6df-1199bbb12591)

