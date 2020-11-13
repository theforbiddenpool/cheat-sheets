__yarn__ → it was build by Facebook, Google, Exponent, and Tilde with the purpose of solving a handful of problems that these teams faced with npm.

Yarn differs from npm in two main things:
- yarn.lock file
- parallel instalation of packages, which makes installation faster;
- cleaner output.

## Commands
_Start a new project:_
```
yarn init
```

_Add a dependency:_
```
yarn add <package>[@<version>]
```
- `--dev` → install as a `devDependency`.
- `--peer` → install as a `peerDependency`.
- `--optional` → install as a `optionalDependency`.

_Upgrade a package:_
```
yarn upgrade <package>[@<version>]
```

_Remove a package:_
```
yarn remove <package>
```

_Install all dependencies of the project:_
```
yarn install [package]
```
`yarn install` only installs the dependencies listed in `yarn.lock' or `package.json`, in that order.

_List the licenses of all installed packages:_
```
yarn licenses ls
```

_Generate a disclaimer containing the contents of all of the packages' licenses:_
```
yarn licenses generate-disclaimer
```

_Figure out why a given package is installed in our project:_
```
yarn why <package>
```

_Generate a `yarn.lock` file based on the dependencies set in `package.json`_:
```
yarn generate-lock-entry
```
`yarn.lock` is generated and updated automatically when adding or upgrading dependencies via `yarn add` and `yarn upgrade`.


# Sources
[Yarn docs](https://classic.yarnpkg.com/lang/en/docs/getting-started/)\
[sitepoint - Yarn vs npm: Everything You Need to Know](https://www.sitepoint.com/yarn-vs-npm/)