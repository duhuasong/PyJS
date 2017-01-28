# PyJS

A minimal Python interpreter written in JavaScript. This is my project for the course *Principles of Programming Languages* at Zhejiang University. Do not use it for serious business.

## Usage

PyJS can be installed using NPM:

```sh
npm install yzyzsun/PyJS
```

Then you can use `./node_modules/.bin/PyJS` to interpret Python code file, which will also generate a Lisp-like syntax tree file in the same directory. You can access the interpreter programmatically from CommonJS module too:

```javascript
const interpreter = require('PyJS').interpreter;
const source = require('fs').readFileSync('test.py', 'utf8');
interpreter.interpret(source);
```

## Specification

PyJS accepts a simplified version of Python 3, but there are also subtle differences between them. It supports the novel features of Python such as indentation levels, `__*__` methods, LGB scoping rules, etc.

Its supported built-in types include `int`, `float`, `bool`, `str`, `list`, `dict`, `set`, `object` and `NoneType`, together with special types like `function` and `type`. Arithmetic, bitwise and boolean operations, comparisons and conditional expressions (a.k.a. ternary operator) work and their corresponding methods will be respected. For example, the floor division operator `//` will call `__floordiv__()` internally. Simple statements including assignments, `pass`, `del`, `return`, `break`, `continue` and compound statements including `if-elif-else`, `while`, `for`, function and class definitions are also accepted.

For a detailed specification, see [docs/grammar.txt](docs/grammar.txt).

## Hierarchy

- `src/`:
  - `parser.jison`: The grammar file used by [Jison](https://github.com/zaach/jison)
  - `interpreter.js`: The main part of interpretation
  - `object.js`: Python object model
  - `error.js`: Error definitions used by interpreter
  - `cli.js`: Command line interface
  - `docs.js`: Entry point for webpack, used to generate `docs/bundle.js`
- `docs/`: Public directory for GitHub Pages
- `.babelrc`: Babel configuration file, used to transcompile ES2015+ to ES5
- `package.json`: NPM configuration file
- `webpack.config.js`: Webpack configuration file, used to bundle scripts and stylesheets into `docs/bundle.js`
- `yarn.lock`: Yarn lockfile

## Demo

http://blog.yzyzsun.me/PyJS/
