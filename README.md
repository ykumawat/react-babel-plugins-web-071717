# React Babel Plugins

## Overview

We'll explain what Babel does and how to use it for React development. 

## Objectives
1. Define and describe the benefits of using Babel plugins
2. Find Babel plugins and install them
2. Describe a few useful plugins for React development

## Babel recap
Babel is used to transform our ES2015 (and even newer) code to ES5 — the previous version of JavaScript that all browsers know and understand. Most of the ES2015 features are already present in browsers, but it's best to transpile your code using Babel anyway.

This ensures that _every_ browser can run your code, as well as giving you the possibility of writing even more modern code (using features that haven't been released yet). Babel, installed by itself, does _nothing_ to your code. It only starts transforming your code once you tell it which plugins to use.

## Plugins?
Plugins are small, composable dependencies that transform parts of our code. These plugins get applied to the code when compiling it with Babel, each doing their own little job and changing our code. For example, the `transform-es2015-destructuring` allows us to use ES2015 destructuring in our code:

```js
// Source code
const { foo, bar } = myLib;

// Gets transformed by the plugin to:
var _myLib = myLib;
var foo = _myLib.foo;
var bar = _myLib.bar;
```

Having small, separate plugins like this allows us to tweak our configuration to our heart's desire. However, installing every single plugin just to write ES2015 and React code seems like such a hassle... Luckily, there's a thing in Babel called plugin presets! These dependencies are basically a collection of plugins that are grouped together. For example, to transform the code we're writing in this course, we use `babel-preset-es2015` and `babel-preset-react`. Of course, if we want to add additional plugins, we can do so without any restriction!

## Using plugins and presets
Now that we know how plugins and presets work, let's take a look at how tell Babel to actually use them. We install them using `npm`, and then we use a file called `.babelrc` in the root of our project to configure Babel:

```json
{
  "presets": ["es2015", "react"],
  "plugins": ["an-example-plugin", "another-example-plugin"]
}
```

Now when Babel compiles our code, it'll use the presets and plugins we've defined above. Babel has a great [list of all available plugins](https://babeljs.io/docs/plugins/) that you can use to see if you'd like to add anything else.

## Notable plugins
While the following plugins are at an experimental stage, they're still worth checking out — they make the development of React applications even easier!

### Object rest & spread
Using the [`babel-plugin-transform-object-rest-spread`](http://babeljs.io/docs/plugins/transform-object-rest-spread/) plugin, we can use the spread operator for objects, much like you can already do in ES2015 with arrays. An example from the docs:

```js
// Rest properties
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
console.log(x); // 1
console.log(y); // 2
console.log(z); // { a: 3, b: 4 }

// Spread properties
let n = { x, y, ...z };
console.log(n); // { x: 1, y: 2, a: 3, b: 4 }
```

### Class properties
Using the [`babel-plugin-transform-class-properties`](http://babeljs.io/docs/plugins/transform-class-properties/) plugin, we can use class properties to declare our methods, alleviating the need to use `.bind()` in the constructor.

## Resources
- [Babel: Plugins](http://babeljs.io/docs/plugins/)
