# Setting up an Express Server

Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications. It is widely used for building APIs and web servers in Node.js.

## Basic Server Setup

To set up an Express server, you need to install Express and create a basic server.

1. **Install Express**: Use npm to install Express in your project directory.
   ```bash
   npm install express
   ```

2. **Create a Basic Server**: Create a file named `app.js` and add the following code to set up a basic Express server.

```javascript
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

- **`app.get`**: Defines a route handler for GET requests to the root URL (`/`).
- **`app.listen`**: Starts the server and listens on the specified port.

# Creating Routes and Route Methods

Express provides various methods to define route handlers for different HTTP methods.

1. **GET Request**: Respond with "Hello World!" on the homepage.
   ```javascript
   app.get('/', (req, res) => {
     res.send('Hello World!');
   });
   ```

2. **POST Request**: Respond to POST request on the root route.
   ```javascript
   app.post('/', (req, res) => {
     res.send('Got a POST request');
   });
   ```

3. **PUT Request**: Respond to a PUT request to the `/user` route.
   ```javascript
   app.put('/user', (req, res) => {
     res.send('Got a PUT request at /user');
   });
   ```

4. **DELETE Request**: Respond to a DELETE request to the `/user` route.
   ```javascript
   app.delete('/user', (req, res) => {
     res.send('Got a DELETE request at /user');
   });
   ```

# Middleware

Middleware functions are functions that have access to the request object (`req`), the response object (`res`), and the next middleware function in the application’s request-response cycle.

1. **Using Middleware**:
   ```javascript
   app.use((req, res, next) => {
     console.log('Testing middleware');
     next();
   });
   ```
   - This middleware logs a message for every request to the server and then passes control to the next middleware function.

# Error Handling

Express provides a simple and flexible way to handle errors.

1. **User-Facing Error**:
   ```javascript
   app.get("/profile", (req, res, next) => {
     return next(new Error("Not Implemented"));
   });
   ```

2. **Developer-Facing Error**:
   ```javascript
   app.use((err, req, res, next) => {
     console.error(err.stack);
     res.status(500).send('Something broke!');
   });
   ```

# Dynamic Routing

Dynamic routes allow you to define routes with parameters.

1. **Dynamic Route Example**:
   ```javascript
   app.get("/profile/:username/:age", (req, res) => {
     res.send(`You requested the profile of ${req.params.username} who is ${req.params.age} years old`);
   });
   ```
This setup provides a robust starting point for building an Express server with various route methods, middleware, error handling, and dynamic routing.
