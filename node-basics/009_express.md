# Express.js

### Important Notes

```javascript
var port = process.env.PORT || 3000; 
app.use('url', callback); 		// Use Middlewares
app.set('view engine', 'ejs');	// Setting the view engine

// Body Parser
var bodyParser = require('body-parser');
var jsonParser = bodyParser.json();
var urlEncodedParser = bodyParser.urlencoded({ extended: false});

/* Request */
req.query.q			// Given /person/Chris?q=posts
req.url
req.ip
req.params.id 		// Given: /person/:id on route

```

## Sample App

```javascript
var express = require('express');
var app = express();
var bodyParser = require('body-parser');

// Middlewares
// log the request
app.use('/', function(req, res, next){
    console.log('Request URL: ' + req.url);
    console.log('Request URL: ' + req.ip);
    console.log('Request URL: ' + req.method);
    next();
});
// for static contents
app.use('/assets', express.static(__dirname + '/public'))
app.set('view engine', 'ejs');

// Body parser for posts
var jsonParser = bodyParser.json();
var urlEncodedParser = bodyParser.urlencoded({ extended: false});

// Simple route
app.get('/', function(req, res){
    res.render('index', {
        'header' : "Hello there!"
    })
});

// Using ther req.params
app.get('/person/:id', function(req, res){
    res.render('person', {
         'id': req.params.id ,
         q: req.query.q
        });
});

// Post route using bodyparser
app.post('/person', urlEncodedParser, function(req, res){
    res.send('Thank You!');
    console.log(req.body.firstName); // This is what is added by body-parser
    console.log(req.body.lastName); // This is what is added by body-parser
    
});

// Post but using json
app.post('/personJson', jsonParser, function(req, res){
    res.send('Thank You!');
    console.log(req.body.firstName); // This is what is added by body-parser
    console.log(req.body.lastName); // This is what is added by body-parser
    
});

// Response using JSON
app.get('/api', (req, res) => {
    res.json({
        'firstName': 'Cee',
        lastName : 'Espiritu'
    });
});


var port = process.env.PORT || 3000; 
// Run the http server
app.listen(port);
```



###  A cleaner approach

```javascript
// index.js/app.js
var express = require('express');
var app = express();

var webController = require('./controllers/webController');
var apiController = require('./controllers/apiController');

// Middlewares
// log the request
app.use('/', function(req, res, next){
    console.log('Request URL: ' + req.url);
    console.log('Request URL: ' + req.ip);
    console.log('Request URL: ' + req.method);
    next();
});
// for static contents
app.use('/assets', express.static(__dirname + '/public'))
app.set('view engine', 'ejs');

// Routing
webController(app);
apiController(app);


var port = process.env.PORT || 3000; 
// Run the http server
app.listen(port);
```

```javascript
// ./controllers/webController.js
var bodyParser = require('body-parser');
var urlEncodedParser = bodyParser.urlencoded({ extended: false});

module.exports = function(app){
    // Simple route
    app.get('/', function(req, res){
        res.render('index', {
            'header' : "Hello there!"
        })
    });

    // Using ther req.params
    app.get('/person/:id', function(req, res){
        res.render('person', {
            'id': req.params.id ,
            q: req.query.q
            });
    });

    // Post route using bodyparser
    app.post('/person', urlEncodedParser, function(req, res){
        res.send('Thank You!');
        console.log(req.body.firstName); // This is what is added by body-parser
        console.log(req.body.lastName); // This is what is added by body-parser
        
    });
}
```



```javascript
// ./controllers/apiController.js
var bodyParser = require('body-parser');
var jsonParser = bodyParser.json();
module.exports = function(app){
    
    // Post but using json
    app.post('/personJson', jsonParser, function(req, res){
        res.send('Thank You!');
        console.log(req.body.firstName); // This is what is added by body-parser
        console.log(req.body.lastName); // This is what is added by body-parser
        
    });

    // Response using JSON
    app.get('/api', (req, res) => {
        res.json({
            'firstName': 'Cee',
            lastName : 'Espiritu'
        });
    });
}
```



### Installing express

`npm i express --save`

### What is a middleware?

A piece of code that runs between two layers of software



### Using template engines?

`npm i --save ejs `

(EJS)[http://ejs.co/]



### What is REST?

REST stands for Representational State Transfer. It is a architecture that specifies that HTTP Verbs and URLs mean something.