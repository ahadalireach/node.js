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
