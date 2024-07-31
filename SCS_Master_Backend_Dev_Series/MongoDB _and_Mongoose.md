# Setting up a MongoDB Server

`usermodel.js`

```jsx
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost:27017/mongopractice');

const userSchema = mongoose.Schema({
    name: String,
    username: String,
    email: String,
});

module.exports = mongoose.model('user', userSchema);

```

# CRUD Operations

`app.js`

### Create

```jsx
app.get('/create', async (req, res) => {
    let createduser = await userModel.create({
        name: 'John Doe',
        username: 'johndoe',
        email: 'johmdoe@outlook.com'
    });
    res.send(createduser);
});
```

### Read

`find();` //to read all the users

```jsx
app.get('/read', async (req, res) => {
    let users = await userModel.find();
    res.send(users);
});
```

`find( {key:value} );` //to read specific user

```jsx
app.get('/read', async (req, res) => {
    let users = await userModel.find({username: 'anmol__khatri'});
    res.send(users);
});
```

```jsx
//find() : gives array
//findOne() : gives object
```

### Update

```jsx
app.get('/update', async (req, res) => {
    let updateduser = await userModel.findOneAndUpdate({username: 'johndoe'},{username: 'anmol__khatri'},{new: true});
    res.send(updateduser);
});

//syntax:
//findOneAndUpdate({to_find},{to_update},{new: true});
```

### Delete

```jsx
app.get('/delete', async (req, res) => {
    let users = await userModel.findOneAndDelete({username: 'anmol__khatri'});
    res.send(users);
});
```
