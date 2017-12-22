# The Mongo, Express, Angular, Node (MEAN) stack



### Angular code

```html
<!-- index.html -->
<html ng-app="TestApp">
    <head></head>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.7/angular.min.js"></script>
    <body ng-controller="MainController as vm">
    <h1>Angular</h1>
    <input type="text" ng-model="vm.message">
    {{ vm.message }}
    <ul>
        <li ng-repeat="person in vm.people">
            {{ person.name }}
        </li>
    </ul>
    </body>
    <script src="/assets/js/app.js"></script>
</html>
```

```javascript
 // app.js
angular.module('TestApp',[]);
angular.module('TestApp')
.controller('MainController', ctrlFunc);

function ctrlFunc(){
    this.message = "hello!";
    this.people = [
        {  name: 'John Smith' },
        {  name: 'Glen Frey' },
        {  name: 'Johnny Bravo' },
    ];
}
```

