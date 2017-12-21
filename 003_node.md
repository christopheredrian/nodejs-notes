# Node JS



### What is a client and what is a server?

A **client **is some entity (browser, bot, other computer) that makes a request to a server, and a **server** on the other hand receives a request and from that request it generates a __response__ 

### What is a Web Server?

An implementation of the client-server architecture but specifically for the Web (http). In a web server the request and the response are wrapped into a special http request and http response.

### What is the best example of a Web client?

The best example of a web client is a web browser

### Where can we use JavaScript?

The norm was JavaScript was usually used only in the client - a web browser. But with the advent of Node.js, now you can also use JavaScript in the server side. Hence, one programming language for both the client and the server.

### What does JavaScript needs to manage a server?

There are numerous things that JavaScript needs before it can manage a web server, some notable things are:

- Better ways to organize code into modules (importing them later on)
- File Management
- Database integration
- Communicate to the Internet
- Ability to accept requests and generate responses
- Deals with work that takes a long time (threading in java, event loop in Node

All of these things Node.js already integrates.

#### What is Node.js built with?

Node.js is built with C++. Making a JavaScript layer on top of the C++ libraries.

### Is Node all written in C++? 

No, JavaScript is used in most of the libraries in Node. There are hooks (bindings) with Node that binds with the C++. For instance the **util** library is just a collection of JavaScript utilities which you can code yourself, but is already there for you to use is written all in JavaScript.



### What is io.js?

Node started its development in the company Joyent, some of the developers are not happy with the current pace of the development so they forked node and have a new project called io.js. They continued working on it up into version 3. But later on the node js team and the io.js team managed to agree to merge all of their changes into one and to not confuse the versioning they ported it to version 4. So version 4 onwards is a merge of both Node js and Io.js.







