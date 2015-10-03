# JavaScript Patterns and Single-page Applications
## Single Page Application
* A single-page application (SPA) is a web application that fits on a single web page
  * Page resources are retrieved either at page load or loaded in response to user actions
  * The page does not reload at any point
* SPA apps can contain multiple fake pages
  * Not real pages, but ones that look like a page
* A SPA application is build from some layers to meet the "separation of concerns"
  * UI layer
    * Contains Views (HTML, CSS and UI logic)
  * Data layer
    * A way to communicate with the server (mainly HTTP requests)
  * Business layer
    * The layer that connects the Data with the UI
    * Contains controllers or view-models 

## Architectural Patterns  in JavaScript 
* Many design patterns exist that solve the separation of concerns
* The most used patterns are the MV* patterns
  * Model-View-*
  * The * contains the business logic of the app
* MV* has three concrete implementations:
  * MVC (Model-View-Controller)
  * MVVM (Model-View-ViewModel)
  * MVP (Model-View-Presenter)

## What is AngularJS?
* AngularJS is a full-featured SPA framework
* What make AngularJS so popular:
  * Two-way data binding
  * Templates 
  * Model-View-Whatever
  * Dependency injection
  * Open Source
  * Comprehensive
  * Testable
  * …

## Controllers and $scope
* Controllers in Angular
  * Have all the logic about a page
  * Control the $scope object
* $scope object
  * Two-way bound to the view
  * Tracks any changes in view and updates itself
  * Tracks any changes in JS and updates the view

```javascript
class MyController {
  constructor() {
    this.hello = "Hi, guys!";
  }
}
```

```html
<div ng-app="myApp">
  <div ng-controller="MyController as ctrl">
    <h1>{{ctrl.hello}}</h1>
  </div>
</div>
```

## Constants and Values

```javascript
myApp.value('someValue', {
  name: 'Lionel',
  number: 5,
  date: new Date()
});
myApp.constant('PI', 3.14);
```

## Why Using Services
* Services are:
  * Reusable
  * "SOLID"
  * Dependency Injection
  * Testable
* Three types
  * Factory – the returned value
  * Service – returns instance of the function
  * Provider – can be configured
* Built-in Services
 * $http – AJAX request
 * $resource – AJAX with restfull services
 * $q – Promise library
 * $anchorScroll – Scrolls to element
 * $cacheFactory – cache service (key-value pair)
 * $compile – compiles element with directives
 * $parse – parses expressions
 * $locale – localization of dates, numbers
 * $timeout – timeout with compiling
 * $exceptionHandler – handling exceptions
 * $filter – access to filter functions
 * $cookieStore – cookie sessions usage
* Custom Service

```javascript
class MyService {
  /* @ngInject */
  constructor($http) {
    $http.get('api/products').then(response => this.data = response.data);
  }
}

angular.module('myApp').service('MyService', MyService);
```

## What Is a Route
* Path to part of the SPA
* Not mapped URL to specific file or resource
* Descriptive for the end user
* Provides history and copy-paste functionality
* Create Routes per module

* ngRoute is too simple

```javascript
angular.module('mstore', ['ngRoute'])
.config(/* @ngInject */($routeProvider) => {
  $routeProvider
  .when('/', {
    templateUrl: 'app/components/home/home.html',
    controller: 'HomeControler',
    controllerAs: 'home'
  })
  .otherwise({ redirectTo: '/' });
});
```

* Angular 1.4 router

```javascript
class AppController {
  /* @ngInject */
  constructor($router) {
    $router.config([
      { path: '/home', component: 'home' },
      { path: '/', redirectTo: '/home' }
    ]);
  }
}

angular.module('mstore', ['ngNewRouter'])
.controller('AppController', AppController)
.controller('HomeController', HomeController)
.config(/* @ngInject */($componentLoaderProvider) => {
  $componentLoaderProvider.setTemplateMapping(name => `components/${name}/${name}.html`);
});

```

## Directives
* Extends HTML
* Make it easier for "dynamic" pages
* Easier to read document
* Domain specific tags

```html
<address-name name="my address name"></address-name>
```

```javascript
class AddressNameController {
  upperName() { return this.name.toUpperCase(); }
}
const addressName = () => {
  return {
    replace: true,
    scope: true,
    bindToController: {
      name: '@'
    },
    controller: AddressNameController,
    controllerAs: 'addressName',
    template: '<div>Address Name: {{ addressName.upperName() }}</div>'
  };
}

angular.module('mstore').directive('addressName', addressName);
```

## Data binding
* One-time binding with ```{{ ::obj.field }}```
  * Better performance with immutable data
  * Reduces the need for custom directives

```html
<div ng-repeat="prod in ::products.data track by prod.id">
  <h4 ng-bind="::prod.name"></h4>
</div>
```


## Frameworks and performance
* Framework should be fast
* Framework should help developers be fast
* So Angular 2 is fast from the start
  * Performance-first design
  * Applications are fast by default

## AngularJS 2.0
* AngularJS 1.x is built for current browsers while AngularJS 2.0 is being built for the browsers of the future.
* Full support for Web Components
  * 1 Class + 2 @Annotations = 1 Web Comp.
* Full support for ES6
* Better performance
* Better tooling support
* First-class mobile support
* Concepts Eliminated in 2.0
  * Controllers
  * Directive Definition Object
  * $scope
  * angular.module
  * jqLite

```html
<address-name name="my address name"></address-name>
```

```javascript
class AddressName {
  upperName() { return this.name.toUpperCase(); }
}
@Component({
  selector: 'address-image',
  bind: {
    name: 'name'
  }
});
@Template({
  inline: <div>Address Name: {{ upperName() }}</div>
});
```