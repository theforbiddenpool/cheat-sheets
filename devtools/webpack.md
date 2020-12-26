__Webpack__ → unifies all the different sources and module types to produce a shippable output.

```
$ npm i webpack webpack-cli webpack-dev-server --save-dev
```

Some basic scripts to add `package.json` file:
```json
"scripts": {
  "dev": "webpack --mode development",
  "start": "webpack-dev-server --mode development --open",
  "build": "webpack --mode production"
}
```

We also will need to create the an entry point, *src/index.js*.

## Configurations
Since v4.0, we can run Webpack with no configuration. However we'll hit its limit pretty soon.

To configure webpack, create a `webpack.config.js` file in the project's folder.

Webpack runs on top on a headless JavaScript environment, using Common JS export.
```javascript
module.exports = {
  //
};
```

#### Entry & Output Point
```javascript
const path = require('path');

module.exports = {
  entry: { 
    index: path.resolve(__dirname, "source", "index.js")
  },
  output: {
    path: path.resolve(__dirname, "build")
  }
};
```

### Plugins
#### HTML
Install the HTML plugin:
```
$ npm i html-webpack-plugin --save-dev
```

This plugin loads our HTML files and injects the bundle(s) in the same file.

Load an HTML template from *src/index.html*:
```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');

module.exports = {
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__diname, "src", "index.html")
    })
  ]
};
```

### Loaders
The configuration of a loader follows the structure:
```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.extension$/,
        use: ["loader-b", "loader-a"]
      }
    ]
  },
}
```
Each loader is listed inside `rules`. `use` defines what loaders are applied to the file. The order of the loaders matter – webpack loaders are loaded from right to left.

#### CSS
Install the CSS loaders:
```
$ npm i css-loader style-loader --save-dev
```

```javascript
...
rules: [
  {
    test: /\.css$/,
    use: ["style-loader", "css-loader"]
  }
]
...
```

#### SCSS
Install the CSS + SCSS loaders:
```
$ npm i css-loader style-loader sass-loader sass --save-dev
```

```javascript
...
rules: [
  {
    test: /\.scss$/,
    use: ["style-loader", "css-loader", "sass-loader"]
  }
]
...
```

#### JavaScript
Webpack by itself doesn't know how to transform JavaScript code. We use Babel for this. There are three main packages we install: **babel core**, the actual engine, **babel preset env**, for compiling modern JavaScript down to ES5, and finally babel loader for webpack.
```
$ npm i @babel/core babel-loader @babel/preset-env --save-dev
```

We then have to configure Babel, in *babel.config.json*.
```javascript
{
  "presets": [
    "@babel/preset-env"
  ]
}
```
All the presets we use should be in that array. For React projects, we'll also need *@babel/preset-react*.

And then the loader:
```javascript
...
rules: [
  ...
  {
    test: /\.js$/,
    exclude: /node_modules/,
    use: ['babel-loader']
  }
]
...
```
When working with React projects, in the regex string we should also add the `.jsx` extension, *e.g.* `\.(js|jsx)$`

So that in `import` statemens we don't have to keep putting the JavaScript files extension, we can use the `resolve` property.
```javascript
module.exports {
  //...
  resolve: {
    extensions: ['.js', '.jsx']
  },
}
```

#### ESLint
ESLint will tell us if we have any Syntax errors, and can help us keep a consistent code style between different team members. This loader will check for any mistakes, and display them in the console.
```
$ npm install --dev eslint eslint-loader 
```

Add then add the loader in Webpack's config file:
```javascript
//...
rules: [
  //...
  {
    test: /\.js$/,
    exclude: /node_modules/,
    use: ['eslint-loader']
  }
],
//...
```

## Code splitting
Code splitting aims to avoid big bundles and avoid dependencies duplication. The webpack community considers **200KB** to be the maximum for the inital bundle.

There are three main ways to activate code splitting in webpack:
1. multiple entry points → works well for smaller projects.
2. `optimization.splitChunks` → chunks are split according to certain conditions.
3. dynamic imports → in the code itself.

# Keywords
__Entry point__ → the starting point from which all the dependencies are collected. These dependencies from a **dependency graph**. The default v4.0+ is `src/index.js`. We can have multiple entry points.

__Output__ → where the resulting files go after the build process. The default since v4.0+ is `dist/`.

__Bundle__ → the unified JavaScript files.

__Loaders__ → third-party extensions that help webpack deal with various file extensions.

__Plugins__ → third-party extensions that can alter how webpack works.

__Mode__ → **development** and **production**. Production code applies minification and other optimizations to our JavaScript code.

__Code splitting__ or __lazy loading__ → optimization technique for avoiding larger bundles. Blocks of JavaScript are only loaded in response to some user interaction.

__Chunk__ → piece of code that's splitted.

# Sources
[A mostly complete guide to webpack (2020) – Valentino Gagliardi](https://www.valentinog.com/blog/webpack/)\
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie
