# Layr Web Application Developer Coding Exercise
The goal of this exercise is to code a service that resolves JavaScript module dependencies.

The service is already started for you in [src/steel.js](src/steel.js). For your coded solution, you need only edit the steel.js file. 

Use the included documentation and test suite to drive your development of steel.js. 

#### The Task
Clone or download the repository and add the appropriate logic to `window.steel = {}` in [src/steel.js](src/steel.js) to ensure that all the unit tests pass. The test file ([test/spec.js](test/spec.js)) explains all the unit tests in detail. Tests can be run by opening [test/index.html](test/index.html) in a browser (there is no need to host `index.html` with a webserver). The testing is done with qUnit which you can read more about at [qunitjs.com](http://qunitjs.com/).

### Notes

- steel.js should not do script loading, i.e. the html page should load all the necessary scripts with script tags in the &lt;head&gt; element.
- The "component" module requirement is slightly different than the others (app, factory, service), please read the documentation carefully.
- This exercise is inspired by TDD, and therefore all the tests have already been written, you just need to write the necessary code in [src/steel.js](src/steel.js) to pass the qUnit tests in [test/index.html](test/index.html)
- Your complete solution should be correctly described by the **Documentation** section below

This library was inspired by Angular's naming scheme, and by Require.js's production-ready resolver, Almond.js.

# Example Usage of the steel.js Library

The following example shows how the completed steel.js library could be used to resolve dependencies.

`/index.html`
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>steel.js</title>
    <script type="text/javascript" src="steel.js"></script>
    <script type="text/javascript" src="app.js"></script>
    <script type="text/javascript" src="automobile.js"></script>
    <script type="text/javascript" src="mechanic.js"></script>
  </head>
  <body>
  </body>
</html>
```

`/mechanic.js`
```js
steel.service('mechanic', function() {
  return function(name) {
    this.name = name;
    this.clockedIn = true;
  };
});
```

`/automobile.js`
```js
steel.factory('automobile', ['mechanic'], function(mechanic) {
  return {
    _types: ['car', 'truck', 'bus', 'motorcycle'],
    isAvailable: function(type) {
      return this._types.indexOf(type) >= 0;
    }
  };
});
```

`/app.js`
```js
steel.app(['mechanic', 'automobile'], function(mechanic, automobile) {
  
  // bootstrap

});
```

# Documentation

`steel.app()`, `steel.factory()` and `steel.service()` are all semantically identical, but exist for code organization.

## steel.app([name, ] [dependecies, ] module)

Create an app module.

#### `name`: String
Define a name for the module, required if referenced as a dependency by another module.

#### `dependencies`: Array
List dependencies to be injected into the `module` callback function.

#### `module`: Function
Callback function executed when all dependencies (if any) have executed. The function is executed once and the returned value is cached for any future injections.

## steel.factory([name, ] [dependecies, ] module)

Create an factory module. 

#### `name`: String
Define a name for the module, required if referenced as a dependency by another module.

#### `dependencies`: Array
List dependencies to be injected into the `module` callback function.

#### `module`: Function
Callback function executed when all dependencies (if any) have executed. The function is executed once and the returned value is cached for any future injections.

## steel.service([name, ] [dependecies, ] module)

Create an service module. 

#### `name`: String
Define a name for the module, required if referenced as a dependency by another module.

#### `dependencies`: Array
List dependencies to be injected into the `module` callback function.

#### `module`: Function
Callback function executed when all dependencies (if any) have executed. The function is executed once and the returned value is cached for any future injections.

## steel.component([name, ] [dependecies, ] module)

Create a component module.

#### `name`: String
Define a name for the module, required if referenced as a dependency by another module.

#### `dependencies`: Array
List dependencies to be injected into the `module` callback function.

#### `module`: Function
Callback function executed when all dependencies (if any) have executed AND the DOMready event has fired. The function is executed once and the returned value is cached for any future injections.
