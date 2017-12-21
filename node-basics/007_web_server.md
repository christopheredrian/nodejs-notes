# HTTP and Building a Web Server

### What is a protocol (TCP/IP)?

A protocol set of rules two sides agreed upon

Some terms to note are: 

**TCP/IP** is a protocol for the web specifically **HTTP**, it is understandable by the client and the server

**TCP**(Transmission Control Protocol) is a protocol of **HOW** the information is sent (by packets)

**IP**(Internet Protocol) is where to send the packets

**Sockets** are the medium for TCP

### What is HTTP?

It is how that information (from TCP/IP) is formatted.

HTTP can be either a **HTTP request** or a **HTTP response**. The HTTP request is composed of:

- Status
- Headers
- Body

### What is the HTTP Parser?

The HTTP Parser is a library (built in C) that is embedded inside of Node that parses HTTP requests (From text to something that we can utilize). It is also wrapped inside Node (From C to JavaScript).

The http module of node can only not parse http requests but it can also request from another http server. 

Note: In other languages such as Java or Php, your program needs have a container (server), in Node we also code our server.

### How to build a web server in Node?

Here's the basic HTTP Web server

```javascript
var http = require('http');

var server = http.createServer(function(req, res){
    res.writeHead(200, {
        'Content-Type': 'text/plain'
    });
    res.end("Hello World!\n");
});

server.listen(3000, '127.0.0.1');
```



### What is an API and endpoint?

API stands for Application Programming Interface and is a set of tools for building a software

A endpoint is a URL that is part of a web API

### How to output JSON?

Here is a snippet:

```javascript
var http = require('http');
var fs = require('fs');

var server = http.createServer(function(req, res){
    res.writeHead(200, {
        'Content-Type': 'application/json'
    });
    var obj = {
        firstName: 'John',
        lastName: 'Doe'
    }
    res.end(JSON.stringify(obj));
});

server.listen(3000, '127.0.0.1');
```

### What is routing?

Is essentially mapping http request URL to content

A basic router can be:

```javascript
var http = require('http');
var fs = require('fs');

var server = http.createServer(function(req, res){
    if(req.url === '/'){
        fs.createReadStream(__dirname + '/index.htm').pipe(res);
    }else if(req.url === '/api'){
        res.writeHead(200, {
            'Content-Type': 'application/json'
        });
        var obj = {
            firstName: 'John',
            lastName: 'Doe'
        }
        res.end(JSON.stringify(obj));
    } else{
        res.writeHead(404);
        res.end();
    }
  
});

server.listen(3000, '127.0.0.1');
```

