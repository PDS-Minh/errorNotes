# What is a REST API?

When we browse web pages, we can see URL addresses separated by / in the address bar.

For example, on Google, I searched for `node.js`.

I could view the search results for `node.js`, and I noticed the URL address at the top of the screen had changed.

![image](https://github.com/user-attachments/assets/7332c449-6cff-4c4b-9be2-ccc96581eca9)

Before Search:
```
https://www.google.com
```


After Search:
```
https://www.google.com/search?q=node.js&newwindow=1&sca_esv=e993029fa676fbb3&sxsrf=ADLYWIK2OxMce_N5zoEuJgUmDXymFN_t6A%3A1736842647552&source=hp&ei=lx2GZ_ujH-60vr0PxOjHyAo&iflsig=AL9hbdgAAAAAZ4Yrpy5wOwYuOQYOsMGpkqJyShQaVjIR&ved=0ahUKEwi7y6SI4_SKAxVumq8BHUT0EakQ4dUDCBk&uact=5&oq=node.js&gs_lp=Egdnd3Mtd2l6Igdub2RlLmpzMgoQIxiABBgnGIoFMgoQABiABBgUGIcCMgUQABiABDIFEAAYgAQyBRAAGIAEMgUQABiABDIFEAAYgAQyBRAAGIAEMgUQABiABDIFEAAYgARIuiVQpRRYsiNwAngAkAEAmAGEAaABngaqAQMwLje4AQPIAQD4AQGYAgmgArcGqAIKwgIHECMYJxjqAsICDRAuGNEDGMcBGCcY6gLCAgQQIxgnwgIREC4YgAQYsQMY0QMYgwEYxwHCAgsQABiABBixAxiDAcICChAAGIAEGEMYigXCAgsQLhiABBixAxiDAcICCBAAGIAEGLEDwgIEEAAYA5gDB_EFc0wCkxLbBk6SBwMyLjegB7g7&sclient=gws-wiz
```

You can verify this information using the developer tools.

```
q: node.js
newwindow: 1
sca_esv: e993029fa676fbb3
sxsrf: ADLYWIKqyVzzD8u6Dy3lvCOu9PIpPRq8Ww:1736842654007
ei: nh2GZ4QU8qS-vQ-nsMPoBQ
ved: 0ahUKEwiE27CL4_SKAxVykq8BHSfYEF0Q4dUDCBA
oq: node.js
gs_lp: Egxnd3Mtd2l6LXNlcnAiB25vZGUuanNIAFAAWABwAHgBkAEAmAEAoAEAqgEAuAEMyAEAmAIAoAIAmAMAkgcAoAcA
sclient: gws-wiz-serp
```

To send a request to the server, you need to provide the correct path and data.

## 1. What is an API?
   API stands for Application Programming Interface, which is an interface that enables communication between programs.

An API is like a restaurant menu.

For example, when you go to a restaurant, you order food by looking at the menu. You don’t need to know how the food is prepared in the kitchen. Similarly, with APIs, we request the data (Request) we need and receive the results (Response).

## 2. What is REST?
   REST stands for Representational State Transfer. It is a set of principles and rules for exchanging data on the web.

### Key Principles of REST:

1. Resource-Based Design

* All data is treated as resources.
* For example, a user is a resource, and a post is another resource.

2. Using HTTP Methods

* REST APIs use HTTP methods to handle resources.
* Key methods include:
  * GET: Retrieve data (e.g., fetch a list of users)
  * POST: Create data (e.g., add a new user)
  * PUT: Update data (e.g., modify user details)
  * DELETE: Delete data (e.g., remove a user)

3. Using URIs to Represent Resources

* Each resource is identified by a unique URL.
* Examples:
  * User list: https://example.com/users
  * Specific user: https://example.com/users/123

4. Stateless

* The server does not store the client’s state.
* The client must include all necessary information in the request.

## 3. What is a REST API?
   A REST API is an API that follows REST principles.
   It is used to exchange data between a client and a server.

Example:
* Most websites and apps (e.g., shopping platforms, social media) use REST APIs.
* Client: Browser or app
* Server: Where the database and business logic reside

## 4. Example of REST API in Action
   ### Managing Blog Posts with a REST API
   * GET Request: https://example.com/posts
     → Retrieve all posts.

   * GET Request: https://example.com/posts/1
     → Retrieve the post with ID 1.

   * POST Request: https://example.com/posts
     → Add a new post (with the post content in the request body).

   * PUT Request: https://example.com/posts/1
     → Update the post with ID 1.

   * DELETE Request: https://example.com/posts/1
     → Delete the post with ID 1.

## 5. Why Use REST APIs?
   
1. Standardization
* All systems can exchange data in the same way, making integration easier.

2. Scalability
* Servers and clients can be developed independently.

3. Flexibility
* Compatible with various clients (browsers, mobile apps, etc.).

# Trying Out REST APIs
## 1. Installing Express

Express is a fast and simple web framework for Node.js that helps you easily create servers.

Open a new terminal in VS Code and run the following command to install the Express package: `npm i express
`
After installation, you can see Express listed in the dependencies section of package.json:

```json
{
  "dependencies": {
    "express": "^4.21.2"
  }
}
```

## 2. Running a Server

Let’s create a simple web server using Express.

Here’s an example from the official Express documentation:

[serverExpress.js]

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

Save this code in a file named serverExpress.js.

You can run the server by entering the following command in the terminal: node serverExpress.js Or, add a script to package.json:

[package.json]
```json

{
  "scripts": {
    "start:express": "node serverExpress.js"
  }  
}

```
start the scripts `start:express`.

```
Executing task: npm run start:express


> nodejs-guide@1.0.0 start:express
> node serverExpress.js

file:///D:/my-test/nodejs-guide/serverExpress.js:1
const express = require('express')
^

ReferenceError: require is not defined in ES module scope, you can use import instead
This file is being treated as an ES module because it has a '.js' file extension and 'D:\my-test\nodejs-guide\package.json' contains "type": "module". To treat it as a CommonJS script, rename it to use the '.cjs' file extension.
at file:///D:/my-test/nodejs-guide/serverExpress.js:1:17
at ModuleJob.run (node:internal/modules/esm/module_job:222:25)
at async ModuleLoader.import (node:internal/modules/esm/loader:316:24)        
at async asyncRunEntryPointWithESMLoader (node:internal/modules/run_main:123:5)
```

An error has occurred.

Let's read the message from the beginning without panicking.

node serverExpress.js So far, it's been executed, but the problem is the next line.

It kindly tells you where the error occurs.

``` javascript
const express = require('express')
                ^
```

Next, let's read the error message.

```
ReferenceError: require is not defined in ES module scope, you can use import instead
```
The requirement is not defined in the ES module, so import should be used instead of requirement.

Let's go modify the code content of serverExpress.js.

[serverExpress.js]
``` javascript
// const express = require('express')
import express from 'express';

...
```

Annotate or delete the require portion and call the package using import.

Then, you can run it again to verify that the server ran normally.

```
Executing task: npm run start:express 


> nodejs-guide@1.0.0 start:express
> node serverExpress.js

Example app listening on port 3000
```

### 3. Making API Requests
You can also use the Postman program to make API requests, but basically it's also possible in a browser, so let's open a blank browser.

The default url address is localhost, and the port can be set as desired.

The port number mainly used by the development server is 3000.

Type localhost:3000/ in the browser.

You can see that Hello World! text is displayed in your browser.

![image](https://github.com/user-attachments/assets/4de2dda4-1220-4b3d-b686-9a49ef141426)

Though this example is simple, with a database connection and CSS styling, you could eventually create something like Facebook!

## Node.js Start
- [Node.js start - 05. Information security](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-05.-information-security-en-US)