
# Setting up a Node.js Server to Serve HTML Files 
## by JFL IT Lab

## Prerequisites

Make sure you have **Node.js** installed on your system. If Node.js is not installed, you can download and install it from [Node.js official website](https://nodejs.org/).

After installing Node.js, you can verify the installation by running the following command in your terminal or command prompt:

```bash
node -v
npm -v
```

These commands will display the installed versions of Node.js and npm (Node Package Manager).

## Steps to Set Up Node.js Server

Follow these steps to create a Node.js server that serves an HTML file:

### 1. Initialize a Node.js Project

1. Open your terminal and create a new directory for your project:

    ```bash
    mkdir nodejs-html-server
    cd nodejs-html-server
    ```

2. Initialize a new Node.js project:

    ```bash
    npm init -y
    ```

    This will create a `package.json` file in your project directory.

### 2. Create HTML File

Create a new file named `index.html` in the project directory with the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Node.js HTML Example</title>
</head>
<body>
    <h1>Hello from Node.js Server!</h1>
    <p>This is a static HTML file being served by Node.js.</p>
</body>
</html>
```

### 3. Create Node.js Server

Create a new file named `server.js` and add the following code to create a simple server using Node.js:

```js
const http = require('http');
const fs = require('fs');
const path = require('path');

const hostname = '127.0.0.1';
const port = 3000;

// Create the HTTP server
const server = http.createServer((req, res) => {
    if (req.url === '/') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/html');

        // Read and serve the HTML file
        fs.readFile(path.join(__dirname, 'index.html'), (err, data) => {
            if (err) {
                res.statusCode = 500;
                res.end('Error reading file');
            } else {
                res.end(data);
            }
        });
    } else {
        res.statusCode = 404;
        res.end('Page not found');
    }
});

// Start the server
server.listen(port, hostname, () => {
    console.log(`Server running at http://${hostname}:${port}/`);
});
```

### 4. Run the Node.js Server

To run the server, use the following command:

```bash
node server.js
```

### 5. Access the Server

Now, open your browser and go to `http://127.0.0.1:3000/`. You should see the HTML content being served by the Node.js server.

---

## Optional: Using Express.js

You can also use the `express` framework for more flexibility. Here's how to set it up:

### 1. Install Express.js

Run the following command to install `express`:

```bash
npm install express
```

### 2. Create an Express Server

Update your `server.js` file with the following code:

```js
const express = require('express');
const path = require('path');
const app = express();

const port = 3000;

// Serve static files from the project directory
app.use(express.static(path.join(__dirname)));

app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}/`);
});
```

### 3. Run the Express Server

Run the server:

```bash
node server.js
```

Access the server at `http://localhost:3000/index.html`.

more information www.facebook.com/jflitlab

---

That's it! You've successfully set up a simple Node.js server to serve HTML files.
