# Node.js

## What is Node.js

- Node.js is an environment to run JavaScript outside the browser.
- It was built in 2009 using Chrome's V8 engine.

## JavaScript Browser vs Node.js

### JavaScript Browser

- Works with the Document Object Model (DOM).
- Utilizes the Window object.
- Primarily for interactive applications (GUI).
- Lacks access to the filesystem.
- Faces potential fragmentation, requiring bug fixes and feature adjustments.

### Node.js

- Does not work with the DOM.
- Does not have a Window object.
- Used for server-side applications (pure logic).
- Provides access to the filesystem (information about the operating system and networks).
- Offers stable versions, reducing the need for frequent updates.

#### -------------------------------------------------------------------------------------------------------------------------------------------- ####
#### -------------------------------------------------------------------------------------------------------------------------------------------- ####

## Express

### HTTP Messages

![HTTP Messages](https://github.com/bfmahad/Node_JS/assets/115062995/ed0c227e-e4e6-4845-8141-4d8a84bef677)

- Express utilizes HTTP Messages, not the HTTP protocol directly.
- Analogy: Does a cloud still function when it's raining?
    - Yes, a cloud represents a network of servers and computers designed to maintain accessibility regardless of external conditions.

#### Request Messages

- Are what the user sending (url, web app). They also use HTTP request.

#### Response Messages

- Sending the response is our responsibility. We'll have to set a proper server that sends a correct response.

![Screenshot 2024-02-12 041913](https://github.com/bfmahad/Node_JS/assets/115062995/d7b66e95-dfe8-428b-b146-bf72a5616566)

### HTTP Basics

- `res.end()` ends the response, which means nothing will be sent to the browser (the HTTP request-response cycle is finished).
- `res.send()` returns a string to the browser.

```js
const http = require("http");
const { hostname } = require("os");
const PORT = 111;

const server = http.createServer((req, res) => {
      console.log(req.method);
      res.send('Hello World');
      res.end();
});

server.listen(PORT,hostname, () => {
  console.log(`Server listening on port http://${hostname}:${PORT}/`);
});
```

### HTTP Headers

- In Node.js, `write` and `writeHead` are two methods provided by the `http.ServerResponse` class, which is used to send a response back to the client during an HTTP request.

- `writeHead:`
  - The writeHead method is used to send the response header to the client.
  - It takes in three parameters: statusCode, statusMessage, and an optional headers object.
  - Here's the breakdown:
      - `StatusCode (required): It represents the HTTP status code of the response, indicating the outcome of the request (e.g., 200 for success, 404 for not found, etc.).
      - StatusMessage (optional): It allows you to provide a custom status message that corresponds to the status code. If not provided, a default message will be sent based on the status code.
      - Headers (optional): It is an object containing additional headers to be sent with the response.

  - The writeHead method must be called before any call to write or end. It sets the response status code and headers. For example, to send a 200 OK response with a custom header:
  
    ```js
    res.writeHead(200, { "content-type": "text/html" });
    ```

- The `write` method is used to send the response body (i.e., the content) to the client. It takes a single parameter, which is the content to be sent. You can call write multiple times to send data in chunks.
  
```js
res.write(homePage);
```

### HTTP Request Object

- It will give us the information about request metadata.

```js
console.log(req.method)
```

- `req.url` give us the information that user passes.

### HTTP HTML File

- The `fs.readFileSync()` method is an inbuilt application programming interface of the fs module which is used to read the file and return its content.
- `fs.readFileSync( path, options )`
- Parameters:  
    - `Path:` It takes the relative path of the text file. The path can be of URL type. The file can also be a file descriptor. If both the files are in the same folder just give the filename in quotes.
    - `Options:` It is an optional parameter that contains the encoding and flag, the encoding contains data specification. Its default value is null which returns the raw buffer and the flag contains an indication of operations in the file. Its default value is ‘r’.
    - `Return Value:` This method returns the content of the file.

- `const { readFileSync } = require("fs");
const homePage = readFileSync("path");`


#### Example

- Browser perform request for every file or resource which is present in `index.HTML` file.
- Every loaded module must be compiled into JavaScript code before being available in Node.js applications.

```js
const http = require("http");
const { readFileSync } = require("fs");
const { hostname } = require("os");
const PORT = 8080;

// get all files
const homePage = readFileSync("./navbar-app/index.html");
const homeStyles = readFileSync("./navbar-app/styles.css");
const homeImage = readFileSync("./navbar-app/logo.svg");
const homeLogic = readFileSync("./navbar-app/browser-app.js");

const server = http.createServer((req, res) => {
  const url = req.url;
  // home page
  if (url === "/") {
    res.writeHead(200, { "content-type": "text/html" });
    res.write(homePage);
    res.end();
  }
  // about page
  else if (url === "/about") {
    res.writeHead(200, { "content-type": "text/html" });
    res.write("<h1>about page</h1>");
    res.end();
  }
  // styles
  else if (url === "/styles.css") {
    res.writeHead(200, { "content-type": "text/css" });
    res.write(homeStyles);
    res.end();
  }
  // image/logo
  else if (url === "/logo.svg") {
    res.writeHead(200, { "content-type": "image/svg+xml" });
    res.write(homeImage);
    res.end();
  }
  // logic
  else if (url === "/browser-app.js") {
    res.writeHead(200, { "content-type": "text/javascript" });
    res.write(homeLogic);
    res.end();
  }
  // 404
  else {
    res.writeHead(404, { "content-type": "text/html" });
    res.write("<h1>page not found</h1>");
    res.end();
  }
});

server.listen(PORT, hostname, () => {
  console.log(`Server listening on port http://${hostname}:${PORT}/`);
});
```

### Express Basics

- Minimal flexible Node.js web app framework designed to make web apps and api's much faster and easier.
- Ways of importing express:
    - `const app = require('express')();`
    - *Or*
    - `const express = require('express');
      const app = express();`
- `app` methods:
    - `app.use();
    app.get();
    app.post();
    app.put();
    app.delete();
    app.all();
    app.listen();`
- By default browsers perform get request.
- `app.all()` method can be used for all types of routings of a HTTP request, i.e., for POST, GET, PUT, DELETE, etc., requests that are made to any specific route.
- `app.use()` is responsible for middleware. If we can't find response.
- ![Screenshot 2024-02-17 055619](https://github.com/bfmahad/Node_JS/assets/115062995/01252273-a353-42c0-a97c-5b855fa5f3f6)
-`express` do the great work with status code. But we include it `explicitly` so that way we have more control what we sent back.

```js
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.status(200).send("Home Page");
});

app.get("/about", (req, res) => {
  res.status(200).send("About Page");
});

app.all("*", (req, res) => {
  res.status(404).send("<h1>Page Not Found!</h1>");
});

app.listen(8080, () => {
  console.log(`Server is listening on 8080`);
});
```

#### Example

- `path` module provides a way of working with directories and file paths.
- `var path = require('path');`
- `static` are the assests that server would not need to change. Therefore all the assests and resources that we do by ourself in `node` `express` will handle it.
