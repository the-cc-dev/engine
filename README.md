# engine [![NPM version](https://badge.fury.io/js/engine.svg)](http://badge.fury.io/js/engine)

> Template engine based on Lo-Dash template, but adds features like the ability to register helpers and more easily set data to be used as context in templates.

This code is based on [Lo-Dash's](https://lodash.com/) `_.template` method, with a few additions, like the ability to register helpers and more easily control context.

## Install

Install with [npm](https://www.npmjs.com/)

```sh
$ npm i engine --save
```

## Table of contents

<!-- toc -->

* [Usage](#usage)
* [API](#api)
* [Related projects](#related-projects)
* [Running tests](#running-tests)
* [Contributing](#contributing)
* [Author](#author)
* [License](#license)

_(Table of contents generated by [verb](https://github.com/verbose/verb))_

<!-- tocstop -->

## Usage

```js
var engine = require('engine');

engine.helper('upper', function(str) {
  return str.toUpperCase();
});

engine.render('<%= upper(name) %>', {name: 'Brian'});
//=> 'BRIAN'
```

## API

### [Engine](index.js#L28)

Create an instance of `Engine` with the given options.

**Params**

* `options` **{Object}**

**Example**

```js
var Engine = require('engine');
var engine = new Engine();

// or
var engine = require('engine')();
```

### [.helper](index.js#L81)

Register a template helper.

**Params**

* `prop` **{String}**
* `fn` **{Function}**
* `returns` **{Object}**: Instance of `Engine` for chaining

**Example**

```js
engine.helper('upper', function(str) {
  return str.toUpperCase();
});

engine.render('<%= upper(user) %>', {user: 'doowb'});
//=> 'DOOWB'
```

### [.helpers](index.js#L98)

Register an object of template helpers.

**Params**

* `helpers` **{Object|Array}**: Object or array of helper objects.
* `returns` **{Object}**: Instance of `Engine` for chaining

**Example**

```js
engine.helpers({
 upper: function(str) {
   return str.toUpperCase();
 },
 lower: function(str) {
   return str.toLowerCase();
 }
});

// Or, just require in `template-helpers`
engine.helpers(require('template-helpers')._);
```

### [.data](index.js#L117)

Add data to be passed to templates as context.

**Params**

* `key` **{String|Object}**: Property key, or an object
* `value` **{any}**: If key is a string, this can be any typeof value
* `returns` **{Object}**: Engine instance, for chaining

**Example**

```js
engine.data({first: 'Brian'});
engine.render('<%= last %>, <%= first %>', {last: 'Woodward'});
//=> 'Woodward, Brian'
```

### [.compile](index.js#L186)

Creates a compiled template function that can interpolate data properties in "interpolate" delimiters, HTML-escape interpolated data properties in "escape" delimiters, and execute JavaScript in "evaluate" delimiters. Data properties may be accessed as free variables in the template. If a setting object is provided it takes precedence over `engine.settings` values.

**Params**

* `str` **{string}**: The template string.
* `opts` **{Object}**: The options object.
* `escape` **{RegExp}**: The HTML "escape" delimiter.
* `evaluate` **{RegExp}**: The "evaluate" delimiter.
* `imports` **{Object}**: An object to import into the template as free variables.
* `interpolate` **{RegExp}**: The "interpolate" delimiter.
* `sourceURL` **{string}**: The sourceURL of the template's compiled source.
* `variable` **{string}**: The data object variable name.
* `returns` **{Function}**: Returns the compiled template function.

**Example**

```js
var fn = engine.compile('Hello, <%= user %>!');
//=> [function]

fn({user: 'doowb'});
//=> 'Hello, doowb!'

fn({user: 'halle'});
//=> 'Hello, halle!'
```

### [.render](index.js#L303)

Renders templates with the given data and returns a string.

**Params**

* `str` **{String}**
* `data` **{Object}**
* `returns` **{String}**

**Example**

```js
engine.render('<%= user %>', {user: 'doowb'});
//=> 'doowb'
```

## Related projects

* [assemble](https://www.npmjs.com/package/assemble): Static site generator for Grunt.js, Yeoman and Node.js. Used by Zurb Foundation, Zurb Ink, H5BP/Effeckt,… [more](https://www.npmjs.com/package/assemble) | [homepage](http://assemble.io)
* [scaffold](https://www.npmjs.com/package/scaffold): Conventions and API for creating scaffolds that can by used by any build system or… [more](https://www.npmjs.com/package/scaffold) | [homepage](https://github.com/jonschlinkert/scaffold)
* [snippet](https://www.npmjs.com/package/snippet): CLI and API for easily creating, reusing, sharing and generating snippets of code from the… [more](https://www.npmjs.com/package/snippet) | [homepage](https://github.com/jonschlinkert/snippet)
* [template](https://www.npmjs.com/package/template): Render templates using any engine. Supports, layouts, pages, partials and custom template types. Use template… [more](https://www.npmjs.com/package/template) | [homepage](https://github.com/jonschlinkert/template)
* [verb](https://www.npmjs.com/package/verb): Documentation generator for GitHub projects. Verb is extremely powerful, easy to use, and is used… [more](https://www.npmjs.com/package/verb) | [homepage](https://github.com/verbose/verb)

## Running tests

Install dev dependencies:

```sh
$ npm i -d && npm test
```

## Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/engine/issues/new).

## Author

**Jon Schlinkert**

+ [github/jonschlinkert](https://github.com/jonschlinkert)
+ [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License

Copyright © 2015 Jon Schlinkert
Released under the MIT license.

***

_This file was generated by [verb-cli](https://github.com/assemble/verb-cli) on September 08, 2015._
