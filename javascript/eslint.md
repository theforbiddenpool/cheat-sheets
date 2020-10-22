__Lint/linter__ → tool that analyzes source code to flag programming errors, bugs, stylistic errors, and suspicious constructs. ESLint is one of the most popular JavaScript linters.

_Install ESLint dependency as a devDependency:_
```
$ npm install --save-dev eslint
```

_Install ESLint as a global dependency:_
```
$ npm install -g eslint
```

_Add the lint line to our package.json:_
```json
...
"scripts": {
  "lint": "eslint . --ext.js"
}
...
```
This means you will be running the linter on the entire project directory, on any file that has an extension of .js. You can change the flag to be more specific.

_Create a new file at the root of our project called .eslintrc.js:_
```javascript
module.exports = {};
```

We can also let ESLint to the configuration for us by running:
```
$ eslint --init
```
We'll be prompted different questions, and a *.eslintrc.js* will be created for us.

## Babel parser
ESLint allows us to specify a parses that allows the linting processing to look at the same code as your browser sees. In this case, we will be using Babel's ESLint parser. To install it:
```
$ npm install --save-dev babel babel-eslint
```

And update the .eslintrc.js config file with some new options:
```javascript
module.exports = {
  "env": {
    "browser": true,
    "node": true,
    "es6": true
  },
  "parser": "babel-eslint"
};
```

Here we are letting ESLint know that our environment will be run in node, inside the browser, and it will use ES6.

## Plugins
Plugins create and set rules for you. The React plugin takes care of linting the JSX. To install the dependency:
```
$ npm install --save-dev eslint-plugin-react
```

And update our .eslintrc.js file again:
```javascript
module.exports = {
  "settings": {
    "react": {
        "version": "detect"
    }
  },
  "env": {
    "browser": true,
    "node": true,
    "es6": true
  },
  "plugins": [
    "react"
  ],
  "parser": "babel-eslint"
};
```

The setting will automatically detect what React version we're using, and adding the react plugin.

## Rules
It's recommended that you enable ESLint's won recommended rules. And since we're running a React app, we need to add the plugin's rules. Add it to the .eslintrc.js config file:
```javascript
  // ...
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended"
  ]
```

_Run the linter:_
```
$ npm lint
```
- `--fix` → also fixes errors

#### Popular configurations for ESlint
- Airbnb's config
- Semistandard
- Google's JS Style Guide

#### Other linting tools to check out
- __JSHint__: an alternative to ESLint
- __Stylelint__: a linting tool for CSS and CSS-like syntaxes like Sass
- __Awesome ESLint__: a simple list of awesome configs, parsers, plugins, and other tools to boost your ESLint game
- __Webhint__: linting tool for accessibility, speed, and more website best practices
- __A11y JSX Plugin__: ESLint plugin for checking accessibility rules on JSX elements

# Sources
[What is linting and how can it save you time? - FreeCodeCamp](https://www.freecodecamp.org/news/what-is-linting-and-how-can-it-save-you-time/)