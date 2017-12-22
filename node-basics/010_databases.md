# Databases

### How to integrate node and mysql?

Here is a basic snippet which connects to my local wamp server

```javascript
var mysql = require('mysql');

var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'root',
  password : '',
  database : 'fs-2017'
});
connection.query('SELECT * FROM accounts', function(err, rows){
  if(!err){
    console.log(rows[0]);
  }
});
```

### How to use MongoDB  and Mongoose for Node?

You can either install MongoDB locally or use a cloud MongoDB server such as: (MongoLab)[https://mlab.com/]

```javascript
var mongoose = require('mongoose');

mongoose.connect('mongodb://admin:123password123@ds157653.mlab.com:57653/addressbook');

var Schema = mongoose.Schema;

var personSchema = new Schema({
    firstName: String,
    lastName: String,
    address: String
});

var Person = mongoose.model('Person', personSchema);
var chris = Person({
    firstName: 'Chris',
    lastName: 'Esp',
    address: 'Baguio City'
});

chris.save(function(err){
    if(err) throw err;
    console.log('person saved!');
});

// To get all rows

Person.find({}, function(err, users){
  if(err) throw err;
  console.log(users);
})
```



