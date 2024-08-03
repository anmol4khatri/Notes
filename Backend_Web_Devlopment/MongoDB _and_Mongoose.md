# Setting up a MongoDB Server with Mongoose and Performing CRUD Operations

MongoDB is a popular NoSQL database that allows for flexible and scalable storage of data. Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js, which provides a straightforward, schema-based solution to model your application data.

# Define a Mongoose Model

A Mongoose model is a wrapper on the Mongoose schema. A schema defines the structure of the documents within a collection in MongoDB. A model provides an interface to the database for creating, querying, updating, deleting records, etc.

Create a file named `usermodel.js`:

```javascript
const mongoose = require('mongoose');

// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/mongopractice', { useNewUrlParser: true, useUnifiedTopology: true });

// Define the User Schema
const userSchema = mongoose.Schema({
    name: String,
    username: String,
    email: String,
});

// Export the User Model
module.exports = mongoose.model('user', userSchema);
```

- **Connecting to MongoDB**: The `mongoose.connect` function establishes a connection to the MongoDB server.
- **Defining a Schema**: The `userSchema` defines the structure of the user documents.
- **Creating a Model**: The `mongoose.model` function creates a model based on the schema, which is used to interact with the database.

# Performing CRUD Operations

CRUD operations are the basic operations for interacting with the database: Create, Read, Update, and Delete.

Create a file named `app.js` and set up Express routes to perform these operations.

### 1. Create Operation

To add a new document to the collection:

```javascript
const express = require('express');
const app = express();
const userModel = require('./usermodel');

// Create a New User
app.get('/create', async (req, res) => {
    let createdUser = await userModel.create({
        name: 'John Doe',
        username: 'johndoe',
        email: 'johndoe@outlook.com'
    });
    res.send(createdUser);
});

app.listen(3000, () => {
    console.log('Server running on port 3000');
});
```

### 2. Read Operation

To retrieve documents from the collection:

- **Read All Users**:

```javascript
app.get('/read', async (req, res) => {
    let users = await userModel.find();
    res.send(users);
});
```

- **Read Specific User**:

```javascript
app.get('/read-specific', async (req, res) => {
    let user = await userModel.find({ username: 'anmol__khatri' });
    res.send(user);
});
```

### 3. Update Operation

To modify an existing document in the collection:

```javascript
app.get('/update', async (req, res) => {
    let updatedUser = await userModel.findOneAndUpdate(
        { username: 'johndoe' }, 
        { username: 'anmol__khatri' },
        { new: true }
    );
    res.send(updatedUser);
});
```

### 4. Delete Operation

To remove a document from the collection:

```javascript
app.get('/delete', async (req, res) => {
    let deletedUser = await userModel.findOneAndDelete({ username: 'anmol__khatri' });
    res.send(deletedUser);
});
```

### Theory Behind Mongoose and CRUD Operations

#### **Mongoose**:
Mongoose provides a schema-based solution to model application data, enabling you to define the structure and constraints for the data being stored in MongoDB. It also provides a powerful API for database operations, including validation, typecasting, and middleware.

#### **CRUD Operations**:
CRUD operations are essential for managing data in any application. Each operation serves a specific purpose:

- **Create**: Adding new documents to the collection. This operation ensures that new data can be stored and accessed.
- **Read**: Retrieving documents from the collection. This operation allows you to fetch data based on specific criteria.
- **Update**: Modifying existing documents in the collection. This operation is crucial for maintaining and updating data as requirements change.
- **Delete**: Removing documents from the collection. This operation ensures that outdated or unnecessary data can be cleaned up.

By setting up a MongoDB server with Mongoose and performing CRUD operations, you can efficiently manage your application's data, ensuring both flexibility and robustness.
