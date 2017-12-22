# The Node Package Manager

The NPM is the largest ecosystem of open-source libraries



### What is Semantic Versioning (semver)?

The basic concepts to know about semantic versioning is this. For instance the version is

**1.7.2**

This means:

- 1 - Major => Big changes, code may break
- 7 - Minor => Added some new features
- 2 - Patch => for bug fixes

For more information you can head to (semver website)[www.semver.org]

### What is package.json?

Package json is the metadata for your app. This will include all the dependencies of your app. 



### Installing packages

The line of code below is how to install moment.js. With the `--save` flag it includes this module in your `package.json` as a dependency.

`npm install --save moment`

`npm install` - to download all dependencies for project



#### Using moment.js

```javascript
var Moment = require('moment');
var now = new Moment();
console.log(now.format('ddd, h:mA'));
```



### Using jasmine.js DEV DEPENDENCY

`npm install jasmine-node --save-dev`

### Updating packages

`npm update`

