# Make Node.js Web Server

before [Node.js Guide](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Guide) briefly described the server on the page

The way to create Node.js Web Server is to create a more scalable project using your own http module and npm init.

## About HTTP?

before using server, let's learn about Http, the basis of the web. 

HTTP(Hypertext Transfer Protocol) is a **rule** designed to transfer information between network devices.

It consists of Request/Response and sends documents such as HTML.

Here's how servers and clients work.

Users make requests that conform to the rules through clicks or keyboard events in a web browser.

The server receives the request and forwards processed documents such as html, css, and image to the user.

![](https://mdn.github.io/shared-assets/images/diagrams/http/overview/fetching-a-page.svg)

The content on HTTP is huge, so it's hard to explain everything, and it will be helpful to read the document when you have time.

Link => https://developer.mozilla.org/ko/docs/Web/HTTP

## Create a full-fledged server - using the http module

In the explorer window, create a server.js file and enter the code.

```
const http = require('http');

http.createServer(function(req, res) {
  res.write('<h1>Hello world</h1>');
  res.end('<p>Hello Node.js Server!</p>');
}).listen(8080, function () {
  console.log('listening on 8080');
});
```

Enter `node server.js` In the Terminal.

When server is running, print message `listening on 8080` 

![image](https://github.com/user-attachments/assets/e3bd49c7-e083-430e-b895-a0e958041d9b)

This message mean, server is waiting on 8080 port.

Port is the entry number for data coming into a specific service or application from the server.

I'll make an easy analogy.

The URL is your home address and port number is door lock password.

**Address: Seocho-gu, Seoul, Republic of Korea 00, 00gil**

  <img src="https://github.com/user-attachments/assets/d7ab5f78-194d-469b-a52f-8e1b350254f2" alt="network" width="50%" />

**Port: 8080**

  <img src="https://github.com/user-attachments/assets/a5dbaacc-992b-4bdf-a093-b37c6228a8d7" alt="network" width="50%" />

And let's request the web server

Open the new tab in browser and enter thr url:port address.

```
http://localhost:8080
```

You can see that the html tag that you entered in server.js appeared on the screen.


![image](https://github.com/user-attachments/assets/d41b5980-3792-4b73-9e39-f579def0b133)

## Using npm

before introduce, npm is Node Package Manager. 

A variety of node.js development related packages are available.


I will continue to explain it on the next page.

## Node.js Start
- [Node.js Start - 03 npm](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-03.-npm-en-US)
- [Node.js start - 04. REST API](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-04.-REST-API-en-US)
- [Node.js start - 05. Information security](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-05.-information-security-en-US)


