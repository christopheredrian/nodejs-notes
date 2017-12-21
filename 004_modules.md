# Modules, Exports and Require

JavaScript (client side) under the hood does not allow you to package your code into modules and import them on the same js file. Node on the other hand supports this on the fly. Modules are the foundations of node and to know them is a must in order to code in node.



### What is a module?

A module is a reusable piece of code which does not impact other code. Node js implements modules using the **comonjs modules**. 



### What is Commonjs modules?

Is a standard for how modules should be structured.



### How do we build a module?

Here we will create a greet module



```javascript
// greet.js

var greet = function(){
 console.log('Hi there!'); 
};

modules.exports = { greet };
```

Invoking the greet module in another file

```javascript
// app.js
var greet = require('./greet.js');
```



### How do module really works?

Essentially

​	Your Code >  Node Wrapped as a function expression > V8 Engine > Returns module.exports

``` module.export ``` is what is returned by `require()`



The wrapper is actually like this

```javascript
(function(exports, require, module, __filename, __dirname){
  // Module code here, for instance greet.js
  var greet = function(){
   console.log('Hi there!'); 
  };
  module.exports = greet;	
  
});
// The it is invoked
fn(module.exports, require, module, __filename, __dirname);
return module.exports;
```

As we can see the return value is anything inside `module.exports`





## Important Aspects

#### Functions

Functions in JavaScript are first-class. This means they are like your typical primitive data-types meaning they can be assigned to a variable (**function expressions**), passed into functions as arguments and more.

```javascript
var helloFunction = function(){
  console.log('Hello World!');
}
```

As you can see in the code above we assigned a **function** in a variable called `helloFunction`, and you invoke (run) this using this line:

```javascript
helloFunction();
```



Consider this code:

```javascript
function runFunc(theFunction){
  // We INVOKED the passed function
  theFunction();
}

var helloFunction = function(){
  console.log('Hello World!');
}

// Here we called runFunc and passed it the variable helloFunction
runFunc(helloFunction);
// Outputs: Hello World!

// We can also do this (Anonymous functions)
runFunc(function(){
  console.log("Hello again!");
});
```



On the code above we passed a function inside a function, this is one case of functions as first class. Many programming languages out there do not support this feature, but on the fly JavaScript is built with this architecture.



#### Object

An JavaScript object is simply a collection named value pairs

```javascript
var person = {
  'name': 'John Smith',
  age: 32,
  address: {
    number: '1',
    street: 'Avelino St.',
    city: 'Baguio City'
  }
  printPerson: function(){
	console.log(this.name, ' ', this.age );
  }
};

// accessing the properties
var name = person.name;
var name = person['name'];

console.log(name);
```



#### Prototypal Inheritance

How do we create objects in JavaScript? Either using the literal syntax, but we can also use protypal inheritance

##### Function Constructors

A function constructor is a function that is used to construct an object

```javascript
// The convention is to capitalize the word
function Person(firstName, lastName){
  this.firstName = firstName;
  this.lastName = lastName;
}

Person.prototype.greet = function(){
  console.log('Hello ' + this.firstName);
};

var me = new Person('Chris', 'Espiritu');
console.log(me.firstName);
```



#### Passing by Reference vs by Values

- Reference - passing the variable as an object
- Value - passing the variable as a primitive (not an object: string, number)



#### How do we Immediately Invoke function Expressions (IIFEs)

This is a fundamental technique on how module works. Things to note are:

- What is a scope?



Here is an example of a IIFE

```javascript
var firstName = 'Jenny';

(function(){
  var firstName = 'Johny';
  console.log(firstName);
})();

console.log(firstName);
```



