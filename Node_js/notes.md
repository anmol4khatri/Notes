# Node js

# Creating an HTTP Server in Node.js

```jsx
const http = require("http");

const server = http.createServer((req, res) => {
    console.log("connection request recived");
    
    res.statusCode = 200; // Set the status code to 200 (OK)
    res.setHeader('Content-Type', 'text/plain'); // Set the content type to plain text
    res.end("Hello, World!"); // Send a response to the client
});

server.listen(5000, () => {
    console.log("Server is running on port 5000");
});
```

```jsx
const http = require("http");

// Create the server
const server = http.createServer((req, res) => {
    console.log("connection request recived");
    
    res.statusCode = 200; // Set the status code to 200 (OK)
    res.setHeader('Content-Type', 'text/plain'); // Set the content type to plain text

    if (req.url === "/home") {
        res.end("Welcome to our home page");
    } else if (req.url === "/about") {
        res.end("Welcome to our about page");
    } else {
        res.end("404 page not found");
    }
});

// Listen to the server
server.listen(5000, () => {
    console.log("Server is working on port 5000");
});

```

# Working with Modules(Import/Export)

### CommonJS Modules

**file1.js**

```jsx
const personName = "Anmol"; // Module to be exported
module.exports = personName; // Export the module

```

**file2.js**

```jsx
const personName = require("./file1.js");
console.log(personName); // Output: Anmol

```

### ES Modules (ESM)

First, add `"type": "module"` to your `package.json`:

```json
{
  "type": "module"
}
```

**file1.js**

```jsx
const personName = "Anmol";
export default personName; // Default export

const personName2 = "MrsRandom2";
const personName3 = "MrsRandom3";
export { personName2, personName3 }; // Named exports
```

**file2.js**

```jsx
import personName from "./file1.js"; // Default import
import { personName2, personName3 } from "./file1.js"; // Named imports

console.log(personName);  // Output: Anmol
console.log(personName2); // Output: MrsRandom2
console.log(personName3); // Output: MrsRandom3
```

### Working with Built-in Modules

### `fs` Module

**Reading a File**

```jsx
import fs from 'fs';

fs.readFile("./index.html", "utf8", (err, data) => {
    if (err) {
        console.error(err);
        return;
    }
    console.log(data); // Outputs the content of index.html
});
```

### `os` Module

**Getting OS Information**

```jsx
import os from 'os';

console.log("Platform:", os.platform());
console.log("Architecture:", os.arch());
console.log("CPU Cores:", os.cpus().length);
console.log("Free Memory:", os.freemem());
console.log("Total Memory:", os.totalmem());
```

### `path` Module

**Working with File Paths**

```jsx
import path from 'path';

const filePath = "/user/local/bin/test.txt";

console.log("Directory:", path.dirname(filePath));
console.log("Base name:", path.basename(filePath));
console.log("Extension:", path.extname(filePath));
```

**Challenge:**
Managing multiple routes in a Node.js application can be difficult and cumbersome.

**Solution:**
Express js simplifies the process by allowing easy handling of routes, requests, and responses.
This enables the creation of robust and scalable applications. Additionally, Express allows you to split your application into multiple files, each managing different routes separately, improving organization and maintainability.