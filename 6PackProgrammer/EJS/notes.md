# Ejs

# Rendering Dynamic HTML

### Folder Structure

```
project/
│
├── views/
│   └── index.ejs
│
└── server.js

```

1. **Create `index.ejs` File**:
    
    ```html
    <!-- views/index.ejs -->
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <h1>Hello, <%= name %>!</h1>
    </body>
    </html>
    
    ```
    
2. **Create `server.js` File**:
    
    ```jsx
    // server.js
    import express from "express";
    const app = express();
    
    // Set the view engine to EJS
    app.set("view engine", "ejs");
    
    // Define a route to render the EJS template
    app.get("/", (req, res) => {
        res.render("index", { name: "Anmol" });
    });
    
    // Start the server
    app.listen(5000, () => {
        console.log("Server is running on port 5000");
    });
    
    ```
    

# Serving static HTML

Create a folder named as public under project which contains all the public file like HTML and CSS.

```
project/
│
├── public/
│   ├── index.html
│   └── styles.css
│
```

```jsx
import express from "express";
import path from "path";

const app = express();

//app.use(express.static(public));
app.use(express.static(path.join(path.resolve(),"public")));

app.set("view engine","ejs");

app.get("/", (req,res) => {
    res.send("index.html");
});

app.listen(5000, () => {
    console.log("Server is working at port 5000");
});
```