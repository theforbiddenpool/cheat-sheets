__Transpilers__, or __source-to-source compilers__ → tools that read source code written in one programming language, and produce the equivalent code in another language. They are the only reliable way to use features from ES2015 and beyond.

__compile-to-JS languages__ → languages that transpile to JavaScript, *e.g.* TypeScript, CoffeeScript.

Every browser uses a different JavaScript engine. Each has different performance characteristics, and implements a different subset of ES2015 features. We are making progress, however it's still not the time to write ES2015 directly. Instead, we let transpilers do the work to translate our code to vanilla ES5 that works in *every* browser.

Transpilers also play an important role in guiding the decisions of the TC39 committee. They can contribute directly to the inclusion of a feature in the standard. But the most valuable contribution is the feedback from its users.

# Setting Up Babel
Install the Babel tool, along with the presets and plugins we'll be using:
```
$ npm install -D babel-cli babel-preset-es2015 babel-plugin-transform-async-to-generator
```
- `babel-preset-es2015` → collection of plugins enabling all the ES2015 features Babel supports.
- `babel-plugin-transform-async-to-generator` → plugin that allows the use of ES7 `async` functions.

The configuration file is called *.babelrc*.
```json
{
  "presets": ["es2015"],
  "plugins": ["transform-async-to-generator"]
}
```

We can use the Babel CLI tool to transpile our file every time we save changes:
```
$ babel index.js --out-file index.transpiled.js --source-maps --watch
```
However using the CLI tool isn't always viable for larger project. We can use tools like [Grunt](https://gruntjs.com/), and [Gulp](https://gulpjs.com/), or bundlers and module loaders like [Webpack](https://webpack.js.org/), and [Browserify](http://browserify.org/) to automate this process.

# Resources
[Babel Handbook – GitHub](https://github.com/jamiebuilds/babel-handbook), by Jamie Kyle

# Sources
[JavaScript Transpilers: What They Are & Why We Need Them – Scotch](https://scotch.io/tutorials/javascript-transpilers-what-they-are-why-we-need-them)
