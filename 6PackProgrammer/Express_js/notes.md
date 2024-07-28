# Express js

# Creating an HTTP Server with Express.js

## Setting Up

1. **Install Express.js:**
    
    ```bash
    npm install express
    
    ```
    
2. **Import Express:**
    
    ```jsx
    import express from "express";
    
    ```
    

## Creating a Basic HTTP Server

### Step 1: Initialize Express App

```jsx
import express from "express";

const app = express();

```

### Step 2: Define Routes

### Plain Text Response

```jsx
app.get("/", (req, res) => {
    res.send("Hi");
});

```

### Error Response

```jsx
app.get("/nice", (req, res) => {
    res.status(500).send("Something went wrong!");
});

```

### Step 3: Start the Server

```jsx
app.listen(5000, () => {
    console.log("Server is working at port 5000");
});

```

### Full Code

```jsx
import express from "express";

const app = express();

app.get("/", (req, res) => {
    res.send("Hi");
});

app.get("/nice", (req, res) => {
    res.status(500).send("Something went wrong!");
});

app.listen(5000, () => {
    console.log("Server is working at port 5000");
});

```

## Sending JSON Data

```jsx
import express from "express";

const app = express();

app.get("/products", (req, res) => {
    res.json({
        success: true,
        products: [],
    });
});

app.listen(5000, () => {
    console.log("Server is working at port 5000");
});

```

## Serving Static HTML Files

### for `“type": "module",`

```jsx
import express from "express"
import path from "path"

const app = express();

app.get("/products", (req,res) => {
    const pathlocation = path.resolve();
    res.sendFile(path.join(pathlocation, "./index.html"));
});

app.listen(5000, () => {
    console.log("Server is working at port 5000");
});

```

### for `“type”: "commonjs",`

```jsx
import express from "express";
import path from "path";
import { fileURLToPath } from "url";

const app = express();

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

app.get("/products", (req, res) => {
    res.sendFile(path.join(__dirname, "index.html"));
});

app.listen(5000, () => {
    console.log("Server is working at port 5000");
});

```

**Challenge:**
Serving static HTML pages in Express.js is straightforward, but it becomes complex when we need to render dynamic, variable-based HTML.

**Solution:**
EJS (Embedded JavaScript) is a package built on top of Express.js that addresses this challenge.
It allows us to render dynamic HTML pages with embedded JavaScript variables, making it easier to create flexible and data-driven web pages.