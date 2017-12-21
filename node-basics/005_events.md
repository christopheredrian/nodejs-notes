# Events and Event Emitter

Events and the Event Emitter object ...

## What are events?

Something that happened in an app that we can respond to, and there are two different kinds of events:

- System Events - these came from the C++ core (libuv). Examples are:
  - Finish reading a file
  - I got the data from the Internet
  - Things that JavaScript does not have
- Custom Events - these are completely different, lives in **JavaScript Core** specifically the Event Emitter


## How to use the built-in Node Event Emitter

Usually this is how you use the EventEmitter

```javascript
// app.js
var Emitter = require('events');
var emtr = new Emitter();

emtr.on('greet', () => {
    console.log('someone greeted!');
});

emtr.on('greet', () => {
    console.log('Ating meg greet!');
});
emtr.emit('greet');
```

A better approach would be to use a different pattern:

```javascript
// config.js
module.exports = {
    events: {
        GREET: 'greet',
        FILESAVED: 'filesaved'
    }
}
```

and then on app

```javascript
// app.js
var Emitter = require('events');
var eventConfig = require('./config').events;
var emtr = new Emitter();

emtr.on(eventConfig.GREET, () => {
    console.log('someone greeted!');
});

emtr.on(eventConfig.GREET, () => {
    console.log('Ating meg greet!');
});
emtr.emit(eventConfig.GREET);
```



#### Creating our own custom EventEmitter

```javascript
/* emitter.js */
function Emitter(){
    this.events = {};
}

/**
 * Appends a listener to a type
 * @param {string} type 
 * @param {function} listener 
 */
Emitter.prototype.on = function(type, listener) {
    this.events[type] = this.events[type] || [];
    this.events[type].push(listener);
};

/**
 * Emit the event
 * @param {string} type 
 */
Emitter.prototype.emit = function(type){
    if(this.events[type]){
        // execute for all listeners
        this.events[type].forEach(listener => {
            listener();
        });
    }
};

module.exports = Emitter;

```

```javascript
/* app.js */
var Emitter = require('./emitter');
var emtr = new Emitter();
emtr.on('greet', () => {
    console.log('someone greeted!');
});

emtr.on('greet', () => {
    console.log('Ating meg greet!');
});
emtr.emit('greet');
```



### Inheriting from the Event Emitter

There is a function in the `util` library that can help us with this

```javascript
// app.js
var EventEmitter = require('events');
var util = require('util');

function Greeter(){
    // Adds on properties and methods to the newly created object
    // AKA the super constructor
    EventEmitter.call(this);
    this.greeting = "Hello!";
}

// The important line - will just connect the prototype and not the properties
util.inherits(Greeter, EventEmitter);

Greeter.prototype.greet = function(){
    console.log('greeting');
    this.emit('greet');
};

var greeter1 = new Greeter();
greeter1.on('greet', function(){
    console.log('someone greeted');
});

greeter1.greet();
```



# Important Aspects

### Arrays and functions

```javascript
var myFunctions = [];
myFunctions.push(function(){
  console.log("Hello World 1");
});
myFunctions.push(function(){
  console.log("Hello World 2");
});
myFunctions.push(() => {
  console.log("Hello World 3");
});

myFunctions.forEach((func) => {
    func();
});

```

### Node and ES6

This is the new standard in JavaScript and it is optional to use them

###### jsonfig.json - for VSCode 

###### Template Literal Syntax 

​	a way of concatenating strings

`	console.log(${name} and the age is ${age});`

###### ES6 Classes

It is important to know that under the hood the `class` syntax still uses the prototypal inheritance method. In a way it is just a syntactical sugar for the new ES6 feature.

```javascript
'use strict';

class Person{
  // The constructor
  constructor(firstName, lastName){
    this.firstName = firstName;
    this.lastName = lastName;
  }
  // Methods
  greet(){
    console.log(`Hello ${ this.firstName } ${ $this.lastName }`);
  }
  
}

```



### Call and Apply

These are both functions for invoking functions

```javascript
// Create an object
var obj = {
  name: 'Chris',
  greet: function(){
    console.log("The name is " + name);
  }
};

```

First by using `.call`

```javascript
obj.greet.call({ name: 'Johnny' }, param1, param2);
```

This will replace the ones in the this keyword

Then by apply

```javascript
obj.greet.apply({'name': 'Johnny'}, [param1, param2]);
```

