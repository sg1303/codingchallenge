# Overview

steel.js is a lightweight module dependency manager for small, non-framework implementations. Each js file defines a module in the AMD format. The js script tags must be included in the HTML page itself or manually appended to the DOM. steel.js does not do script sourcing.


# Bright Channel Front-End Developer Coding Exercise

This repo purposefully has [src/steel.js](src/steel.js) left blank, and it is your task to add the appropriate logic to `window.steel = {}` to ensure that all the unit tests pass. Tests can be run by opening [test/index.html](test/index.html) in a browser (there is no need to host `index.html` with a webserver).


# Example Usage of the steel.js Library

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

Create an component module.

#### `name`: String
Define a name for the module, required if referenced as a dependency by another module.

#### `dependencies`: Array
List dependencies to be injected into the `module` callback function.

#### `module`: Function
Callback function executed after the DOMready event is fired. The function is executed once and the returned value is cached for any future injections.
