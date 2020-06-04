__Node Package Manager (npm)__ → command-line tool used by developers to share and control modules (or packages) of JavaScript code written for use with Node.js.

__package.json file__ → lists the package dependencies and other information about the project. Generated when starting a new project.

__node_modules__ → where the packages are saved.

## Packages
__Local packages__ → contained by a `node_modules` folder under our main project directory and will be accessible by only our project.\
__Global packages__ → installed at a single place in your system irrespective of the place where you execute your install command. Can be accessed by all projects.

Most developers prefer to install packages local to each project to create separation between the dependencies of different projects.

_Install a package:_
```
npm install [options] <package-name>
```
- `-g` → install package globally.
- `--dev` → install as a development dependency.

_Check how many global packages you have in your system:_
```
npm list -g --depth 0
```

_Uninstall a package:_
```
npm uninstall <package-name>
```
- `-g` → uninstall a global package.
- `--save` → update the`package.json` file.

## Other NPM commands
_Run a script:_
```
npm run <script-name>
```
Scripts are defined in the `package.json` file, under the `scripts` object. `start` is a special script that can be runned by typing `npm start`.

_Publish a module to npm:_
```
npm publish
```
It's required for you to have an account on [npmjs.com](https://npmjs.com)

# package.json
__*__ → file that stores information about the project. It's composed of a single JSON object. It should be stored in the our project's root.\
There are two required fields - `name` and `version` - but it's good practice to provide additional information as it could be useful to future users or maintainers.

## Field list
`name` → name of the project.\
`author` → string or object. Who created the project. Can provide contact details, or other details.\
`version` → string. The current version of the project. Should be in SemVer.\
`contributors` → string or object. The people who contributed for the project.\
`description` → string. Short, but informative description about the project. If you publish your project to npm, this is the string that should sell your idea to the user. It's also great way to summarize what a project does.\
`keywords` → array of strings. Used to describe your project using related keywords.\
`private` → boolean. If set to true prevents the app/package to be accidentally published on npm.\
`homepage` → string. Sets the package homepage.\
`main` → string. Points to the entry point/file of the application.\
`scripts` → object. Defines a set of node scripts you can run. Scripts are command line applications. You can run them by calling `npm run <script-name>`.\
`license` → string. Inform users of what they are allowed to do with your project.\
`dependencies` → object. Contains a key-value pair of the dependency and its version that the project requires. _e.g._ `"express": "4.14.0"`\
`devDependencies` → object. Dependencies that are used only in the development part of the app.\
`engines` → object. Sets which versions of Node this package/app works on.\
`browserslist` → array. It's used to tell which browsers (and their versions) you want to support. It's referenced by Babel, Autoprefixer, and other tools, to only add the polyfills and fallbacks needed to the browsers you target.\
`repository` → string. Specifies where this package repository is located. _e.g._ `"repository": "github:flaviocopes/testing"`\
`bugs` → string. URL and email where the bugs in the application should be reported.

## Dependencies Versions
`"2.15.0"` → only include a specific version of a package.\
`"~2.15.0"` → allows the dependency to update to the latest `PATCH` version.\
`"^2.15.0"` → allows the dependency to update to the latest `MINOR` and `PATCH` versions.\
`"*2.15.0"` → allows the dependency to update to the latest `MAJOR`, `MINOR` and `PATCH` versions.\
`>` → accept any version higher than the one you specify.\
`>=` → accept any version equal to or higher than the one you specify.\
`<=` → accept any version equal or lower to the one you specify.\
`<` → accept any version lower to the one you specify.\
`latest` → latest version available.

# Keywords
__package manager__ → helps developers to make sure they have all the correct dependencies of a project. The package manager will install everything for us.\
__Semantic Versioning (SemVer)__ → industry standard for software versioning. Everything published on npm should use SemVer. The format is `MAJOR.MINOR.PATCH`. `MAJOR` changes when making incompatible API changes, `MINOR` when adding functionality in a backwards-compatible mannner, and `PATCH` when making backwards-compatible bug fixes.