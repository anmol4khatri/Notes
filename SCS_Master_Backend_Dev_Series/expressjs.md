# Setting up a Express Server

```jsx
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});
```

# Creating Routes and Route Method

```jsx
 //Respond with Hello World! on the homepage:
app.get('/', (req, res) => {
  res.send('Hello World!')
});//get: browser deafult

//Respond to POST request on the root route (/), the application’s home page:
app.post('/', (req, res) => {
  res.send('Got a POST request')
});

//Respond to a PUT request to the /user route:
app.put('/user', (req, res) => {
  res.send('Got a PUT request at /user')
});
    
//Respond to a DELETE request to the /user route:
app.delete('/user', (req, res) => {
  res.send('Got a DELETE request at /user')
});
```

# Middleware

```jsx
app.use((req, res, next) => {
    console.log('Testing middleware');
    next();
});
//Middleware runs each time the user requests on a route
```

# Error Handling

```jsx
//for users
app.get("/profile", (req,res,next) => {
		return next(new Error("Not Implemented"));
});
```

```jsx
//for devs
app.use((err,req,res,next) => {
    console.error(err.stack);
    res.status(500).send('Something broke!');
});
```

# Dynamic Routing

```jsx
app.get("/profile/:username/:age", (req, res) => {
    res.send(`You requested the profile of ${req.params.username} who is ${req.params.age} years old`);
});
```