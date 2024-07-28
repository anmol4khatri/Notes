# MongoDB / Mongoose

# How To Connect to MongoDB Server

### Method : 1

```jsx
//npm install mongoose 

//require mongoose module
const mongoose = require(mongoose);

//Define the MongoDB connection URL
const mongoURL = 'mongodb://localhost:27017/mydatabaseName'
//Recplace the mydatabaseName with name of your database

//Set up MongoDB connection
mongoose.connect(mongoURL, {
    useNewUrlParser: true,
    useUnfiedTopology: true
});

//Get the deafult connection
//MongoDB maintains a deafult connection object representing the MongoDB connection
const db= mongoose.connection;

// Define event listeners for database connection
db.on('connected', () => {
    console.log("Connected to MongoDb server");
});

db.om('error', (err) => {
    console.error("MongoDB connection error : ",err);
});

db.on('disconnected', () => {
    console.log("MongoDB disconnected");
});

//Export the database connection
module.exports = db;
//or
export default db; 
```

### Method : 2

```jsx
import mangoose from "mangoose";

mangoose.connect("mongodb://localhost:27017/", {
    dbName: "backend" //name of the database
}).then(() => console.log("Database Connected")).catch((e) => console.log(e));

export default db;
```

# How to Create Schema

```jsx
import { Schema, model } from 'mongoose';

//Define the Person Schema
const personSchema = new Schema({
    name: {
        type: String,
        required: true
    },
    age: {
        type: Number
    },
    work: {
        type: String,
        enum: ['chef', 'waiter', 'manager'],
        required: true
    },
    mobile: {
        type: String,
        required: true
    },
    email: {
        type: String,
        required: true,
        unique: true
    },
    address: {
        type: String,
        required: true
    },
    salary: {
        type: Number,
        required: true
    }
});

//Create Person model
const Person = model('Person', personSchema);
modeule.exports = Person;
```