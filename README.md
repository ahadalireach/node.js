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

### Request Messages

- Are what the user sending (url, web app). They also use HTTP request.

### Response Messages

- Sending the response is our responsibility. We'll have to set a proper server that sends a correct response.
