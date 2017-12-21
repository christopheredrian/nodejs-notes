# Modules, Exports and Require

JavaScript (client side) under the hood does not allow you to package your code into modules and import them on the same js file. Node on the other hand supports this on the fly. Modules are the foundations of node and to know them is a must in order to code in node.



### What is a module?

A module is a reusable piece of code which does not impact other code. Node js implements modules using the **comonjs modules**. 



### What is Commonjs modules?

Is a standard for how modules should be structured.



### How do we build a module?

Here we will create a greet module

- Create a folder for your module (Let's say greet)
- Add a `index.js` file inside the `greet` folder which will require all the modules in that folder
- create greetings files (`english.js`, `kapampangan.js`)

```javascript
// greet/english.js

var greet = function(){
 console.log('How are you?'); 
};
module.exports = greet;
```

```javascript
// greet/kapampangan.js

var greet = function(){
 console.log('Komusta naka?'); 
};

modules.exports = { greet };
```

```javascript
// greet/index.js

var english = require('./english');
var kapampangan = require('./kapampangan');
module.exports = { 
	'english': english,
  	'kapampangan': kapampangan
};
```



Invoking the greet module in another file

```javascript
// app.js
var greet = require('./greet');
greet.english();
greet.kapampangan();
// This will print out:
// How are you?
// Komusta naka?
```



### The module patterns

These are the module patterns in order of preference.

1. ```javascript
   // reveal only the one that needs to be revealed
   /* Revealing module pattern */
   module.exports = {
     greet: greet
   }
   ```

2. `module.exports = Greetr;`

3. ```javascript
   // useful for singleton
   module.exports = new Greetr();
   ```

4. `module.exports = {}`

5. `module.exports.greet`



### How do you require native/core modules?

#### Using the utilities module

```javascript
var util = require('util');
console.log(util.isArray([]));
util.log(util.format('Hello %s', 'Chris'));
```



### ECMAScript 2015/ES6 Modules

```javascript
// greet.js
export function greet(){
  console.log('Hello!');
}

// app.js
import * as greeter from 'greet';
greeter.greet();

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



### `exports` vs `module.exports`

As we can see above the first parameter is the `module.exports` meaning `exports` is a short-hand for `module.exports`. But it is not recommended since what is returned is `module.exports`. Why? It does not work with the patterns noted above:  #2 and #4.

In sort **JUST USE `module.exports`**



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



### JSON

A way of writing data in text, so that other systems can understand your data



```json
// languages.json
{
  'en': 'How are you?',
  'ka': 'Komusta naka?'
}
```



You can also require `.json` files

```javascript
var json = require('./languages.json');
```



