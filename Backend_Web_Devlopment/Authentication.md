Authentication is a critical part of any web application, ensuring that only authorized users can access certain resources. This involves the use of cookies, password hashing (with bcrypt), and JSON Web Tokens (JWT). Here's a detailed overview with corresponding code examples in Node.js:
# What are Cookies?
Cookies are small pieces of data stored on the client-side (in the browser) that are sent to the server with each request. They are used for various purposes, including session management, user tracking, and storing user preferences.

# How to Send a Cookie in Express

To send a cookie in Express, you can use the `res.cookie` method. Here's an example:

```javascript
const express = require('express');
const app = express();
const cookieParser = require('cookie-parser');

app.use(cookieParser());

app.get('/set-cookie', (req, res) => {
    res.cookie("Name", "Anmol");
    res.send("Cookie Saved");
});

app.listen(3000, () => {
    console.log('Server running on port 3000');
});
```

# Nature of Cookies

Cookies created on any route will be sent with every subsequent request to the server. This behavior allows the server to access the cookies regardless of the endpoint being requested.

```javascript
app.get('/read-cookie', (req, res) => {
    console.log(req.cookies);
    res.send(req.cookies);
});
```

# Why Cookies are Used

Cookies are primarily used to maintain stateful information between requests. This includes:
- Storing session identifiers to keep users logged in.
- Storing user preferences and settings.
- Tracking user activity for analytics.

# Bcrypt for Password Hashing

Storing plain text passwords is insecure. Bcrypt is a library that helps securely hash passwords before storing them in the database. Hashing converts the password into a fixed-size string that is not reversible, enhancing security.

How It Works:

Salt Generation: Bcrypt generates a unique salt for each password, adding randomness to the hashing process.

Hashing: The plaintext password is combined with the salt and hashed multiple times to produce a hash.

Verification: When a user logs in, the entered password is hashed with the stored salt and compared to the stored hash. If they match, the password is correct.


### Hashing a Password

```javascript
const bcrypt = require('bcrypt');
const saltRounds = 10;
const myPlaintextPassword = 'mySecretPassword';

app.get('/hash-password', (req, res) => {
    bcrypt.genSalt(saltRounds, (err, salt) => {
        bcrypt.hash(myPlaintextPassword, salt, (err, hash) => {
            if (err) throw err;
            // Store hash in your password database.
            res.send(`Hashed Password: ${hash}`);
        });
    });
});
```

### Checking a Password

```javascript
const hashedPassword = '$2b$10$...'; // Example hashed password

app.get('/check-password', (req, res) => {
    bcrypt.compare(myPlaintextPassword, hashedPassword, (err, result) => {
        if (err) throw err;
        res.send(result ? 'Password match' : 'Password does not match');
    });
});
```

# JWT (JSON Web Token)

JWT is a compact, URL-safe means of representing claims to be transferred between two parties. It consists of three parts: Header, Payload, and Signature.

### Generating a JWT

```javascript
app.get('/generate-token', (req, res) => {
    const token = jwt.sign({ email: "anmolkhatri04@outlook.com" }, "secretKey");
    res.cookie("token", token);
    res.send("JWT Saved in Cookie");
});
```

### Verifying a JWT

```javascript
app.get('/verify-token', (req, res) => {
    const token = req.cookies.token;
    jwt.verify(token, "secretKey", (err, data) => {
        if (err) {
            res.send('Invalid Token');
        } else {
            console.log(data);
            res.send(data);
        }
    });
});
```

## Summary

- **Cookies** are used to store session data on the client-side and are sent with every request to the server.
- **Bcrypt** is used to hash passwords securely before storing them in the database.
- **JWT** is a standard for creating access tokens that assert some number of claims, typically used for authorization.

These mechanisms together form the foundation of user authentication and session management in web applications.
