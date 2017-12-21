# Asynchronous code, libuv, the event loop, streams and more...



### Is JavaScript synchronous or asynchronous?

Node is asynchronous while JavaScript and the V8 engine is designed synchronous.

**Note: ** Asynchronous means code is executed at the same time while synchronous is one at a time.



### What is a callback?

A callback is something that is called when a code finishes something. For instance:

```javascript
setTimeout(function(){
  console.log('This code will be called after 2 seconds');
}, 2000);
```

### What is libuv?

There are two types of events the events for the JavaScript Core/Custom events  (EventEmitter) and the events from the C++ Core/ System events (libuv). Libuv is embedded inside node and is a C library for handling events that are from the operating system. It is important to note that inside Node we have several libraries namely v8, libuv, zlib, etc.

libuv library - [www.libuv.org]

#### Important things to note about libuv

1. Libuv request to the Operating system
2. Once the request is done it is send out to the Queue as an event
3. The event loop constantly checks when something is in the queue
4. Once the event loop sees that something is finish, it processes that and it invokes a callback
5. That callback is passed onto the V8

This is called an event-driven non-blocking I/O in V8 JavaScript

A detailed explanation of the the Event-Driven Non-Blocking architecture can be found on the link below 

Node-JS Architecture - [https://www.journaldev.com/7462/node-js-architecture-single-threaded-event-loop]

### What is a buffer?

A buffer is a temporary spot for data being moved from its source to its destination. Think of it as a shopping cart for your grocery, without it you would have to go grab the item, go the cashier, grab the item go to the cashier... until you have all you needed.

### What is a stream?

A stream is a sequence of data made available over time. Think of it as the stream of a river, data is flowing over a stream.

It is important to note that **the stream object in node inherits from the Emitter object**

`		util.inherits(Stream, EE)`

Also, a stream object in Node is abstract.

This implies that we can use event emitters for the stream.

The types of a stream:

- Stream.Readable - can only read
- Stream.Writable - can only send data to stream
- Stream.Duplex - both read and write
- Stream.Transform - can only change
- Stream.PassThrough

### What is the difference between character sets and character encoding?

A character set is the representation of a **character ** into numbers (UTF, Unicode, etc.) whereas a character encoding is the representation of **numbers** into binary.



### How do we typically use the Buffer library in Node?

```javascript
var buffer = new Buffer('Hello', 'utf8');
// This will output the binary data
console.log(buffer);
console.log(buffer.toJSON());
console.log(buffer.toString());
console.log(buffer[1]);
buffer.write('World');
console.log(buffer.toString());
```

### How do I read a file in Node? 

**!NOTE: For big files use a stream (Below)**

Here is a snippet:

```javascript
var fs = require('fs');
fs.readFile(__dirname + '/config.js', 'utf8', function(err, data){
    if(!err){
        console.log(data);
    }
});
```

Using streams

```javascript
var fs = require('fs');
var readable = fs.createReadStream(__dirname + '/bigfile.txt',{
    encoding: 'utf8',
    highWaterMark: 32*1024
});
var writable = fs.createWriteStream(__dirname + '/bigfile_copy.txt');
readable.on('data', function(chunk){
    console.log(chunk);
    writable.write(chunk);
    console.log(chunk.length);
    
});

readable.on('end', function(data){
    console.log("Finish");
})
```



### What are pipes?

A pipe is a way of connecting two streams by reading it on one stream and writing something on the other

###### Stream 1 output > Pipe > Stream 2 input

With the same function as above:

```javascript
var fs = require('fs');
var readable = fs.createReadStream(__dirname + '/bigfile.txt');
var writable = fs.createWriteStream(__dirname + '/bigfile_copy.txt');
readable.pipe(writable);
```

It is important to note that this is not limited to file to file piping, consider the example below. It converts a file into a zip.

```javascript
var fs = require('fs');
var zlib = require('zlib');
var gzip = zlib.createGzip();

var readable = fs.createReadStream(__dirname + '/bigfile.txt');
var writable = fs.createWriteStream(__dirname + '/bigfile_copy.txt');
var compressed = fs.createWriteStream(__dirname + '/bigfile_copy.txt.gz');
readable.pipe(writable);
// Chaining pipes
readable.pipe(gzip).pipe(compressed);

```

