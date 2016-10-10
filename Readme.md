# Node.js Style Guide

This is the migenius JavaScript style guide forked from 
[felixge/node-style-guide](https://github.com/felixge/node-style-guide).
Following this guide is mandatory for all JavaScript code generated within
migenius. It is possible that in the future the style guide will be enforced
either by svn pre-commit hooks or continuous integration builds. 

The `.eslintrc` file matched the style guide and can be used to test and fix
your code. Most modern editors will have add-ons to support eslint natively.
The current file is aimed more torwards node.js, configurations targetting other
engines will be created as needed. Instructions for installation can be found below.

This guide was created by [Felix Geisendörfer](http://felixge.de/) and is
licensed under the [CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/)
license. You are encouraged to fork this repository and make adjustments
according to your preferences.

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

## Table of contents

### Formatting
* [4 Spaces for indentation](#4-spaces-for-indentation)
* [Newlines](#newlines)
* [No trailing whitespace](#no-trailing-whitespace)
* [Use Semicolons](#use-semicolons)
* [120 characters per line](#120-characters-per-line)
* [Use single quotes](#use-single-quotes)
* [Opening braces go on the same line](#opening-braces-go-on-the-same-line)
* [Use braces on multi line blocks](#use-braces-on-multi-line-blocks)
* [Declare one variable per var statement](#declare-one-variable-per-var-statement)

### Naming Conventions
* [Use lower_snake_case for variables, properties and function names](#use-lower_snake_case-for-variables-properties-and-function-names)
* [Use UpperCamelCase for class names](#use-uppercamelcase-for-class-names)
* [Use UPPERCASE for Constants](#use-uppercase-for-constants)

### Variables
* [Object / Array creation](#object--array-creation)

### Conditionals
* [Use the === operator](#use-the--operator)
* [Prefer single-line ternary operator](#prefer-multi-line-ternary-operator)
* [Use descriptive conditions](#use-descriptive-conditions)

### Functions
* [Write small functions](#write-small-functions)
* [Return early from functions](#return-early-from-functions)
* [Name your closures](#name-your-closures)
* [No nested closures](#no-nested-closures)
* [Method chaining](#method-chaining)

### Comments
* [Use slashes for comments](#use-slashes-for-comments)

### Miscellaneous
* [Object.freeze, Object.preventExtensions, Object.seal, with, eval](#objectfreeze-objectpreventextensions-objectseal-with-eval)
* [Requires At Top](#requires-at-top)
* [Getters and setters](#getters-and-setters)
* [Do not extend built-in prototypes](#do-not-extend-built-in-prototypes)

### ESLint Setup
* [Sublime Setup](#sublime-setup)

## Formatting

You may want to use [editorconfig.org](http://editorconfig.org/) to enforce the formatting settings in your editor. Use the [Node.js Style Guide .editorconfig file](.editorconfig) to have indentation, newslines and whitespace behavior automatically set to the rules set up below.

### 4 Spaces for indentation

Use 4 spaces for indenting your code and swear an oath to never mix tabs and
spaces - a special kind of hell is awaiting you otherwise.

### Newlines

Use UNIX-style newlines (`\n`), and a newline character as the last character
of a file. Windows-style newlines (`\r\n`) are forbidden inside any repository.

### No trailing whitespace

Just like you brush your teeth after every meal, you clean up any trailing
whitespace in your JS files before committing. Otherwise the rotten smell of
careless neglect will eventually drive away contributors and/or co-workers.

### Use Semicolons

According to [scientific research][hnsemicolons], the usage of semicolons is
a core value of our community. Consider the points of [the opposition][], but
be a traditionalist when it comes to abusing error correction mechanisms for
cheap syntactic pleasures.

[the opposition]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[hnsemicolons]: http://news.ycombinator.com/item?id=1547647

### 120 characters per line

Limit your lines to 120 characters. Yes, screens have gotten much bigger over the
last few years, but your brain has not. Use the additional room for split screen,
your editor supports that, right?

### Use single quotes

Use single quotes, unless you are writing JSON.

*Right:*

```js
var foo = 'bar';
```

*Wrong:*

```js
var foo = "bar";
```

### Opening braces go on the same line

Your opening braces go on the same line as the statement.

*Right:*

```js
if (true) {
  console.log('winning');
}
```

*Wrong:*

```js
if (true)
{
  console.log('losing');
}
```

Also, notice the use of whitespace before and after the condition statement.

### Use braces on multi line blocks

Multi line control statements must always use braces. When the statement is on a single line braces may be ommitted.

*Right:*

```js
if (err) callback(err);

if (err) {
    callback(err);
}
if (err) {
    console.error(err);
    callback(err);
}
```

*Wrong:*

```js
if (err) 
  callback(err);
```

### Declare one variable per var statement

Declare one variable per var statement, it makes it easier to re-order the
lines. However, ignore [Crockford][crockfordconvention] when it comes to
declaring variables deeper inside a function, just put the declarations wherever
they make sense.

*Right:*

```js
var keys   = ['foo', 'bar'];
var values = [23, 42];

var object = {};
while (keys.length) {
  var key = keys.pop();
  object[key] = values.pop();
}
```

*Wrong:*

```js
var keys = ['foo', 'bar'],
    values = [23, 42],
    object = {},
    key;

while (keys.length) {
  key = keys.pop();
  object[key] = values.pop();
}
```

[crockfordconvention]: http://javascript.crockford.com/code.html

The exemption to this is when requiring modules when the following is allowable: 

```js
var ssh = require('ssh2'),
    https = require('https');
```

### Naming Conventions

### Use lower\_snake\_case for variables, properties and function names

Variables, properties and function names should use `lower_snake_case`.  They
should also be descriptive. Single character variables and uncommon
abbreviations should generally be avoided.

*Right:*

```js
var admin_user = db.query('SELECT * FROM users ...');
```

*Wrong:*

```js
var adminUser = db.query('SELECT * FROM users ...');
```

### Use Upper\_snake\_case for class names

Class names should be capitalized using `Upper_snake_case`.

*Right:*

```js
function Bank_account() {
}
```

*Wrong:*

```js
function BankAccount() {
}
```

## Use UPPERCASE for Constants

Constants should be declared as regular variables or static class properties,
using all uppercase letters.

*Right:*

```js
var SECOND = 1 * 1000;

function File() {
}
File.FULL_PERMISSIONS = 0777;
```

*Wrong:*

```js
const SECOND = 1 * 1000;

function File() {
}
File.fullPermissions = 0777;
```

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

## Variables

### Object / Array creation

Use trailing commas and put *short* declarations on a single line. Only quote
keys when your interpreter complains:

*Right:*

```js
var a = ['hello', 'world'];
var b = {
  good: 'code',
  'is generally': 'pretty',
};
```

*Wrong:*

```js
var a = [
  'hello', 'world'
];
var b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## Conditionals

### Use the === operator

Programming is not about remembering [stupid rules][comparisonoperators]. Use
the triple equality operator as it will work just as expected.

*Right:*

```js
var a = 0;
if (a !== '') {
  console.log('winning');
}

```

*Wrong:*

```js
var a = 0;
if (a == '') {
  console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

### Prefer single-line ternary operator

In general we prefer the ternary operator to be used on a single line when it only has simple operands.

*Right:*

```js
var foo = (a === b) ? 1 : 2;
```

*Wrong:*

```js
var foo = (a === b)
  ? 1
  : 2;
```

For complex operands the opposite applies. A complex operand is defined as any operand which contains an
operation

*Right:*


```js
var foo = (a === b)
  ? (a + 3)
  : 2;
```

*Wrong:*

```js
var foo = (a === b) ? (a + 3) : 2;
```


### Use descriptive conditions

Any non-trivial conditions should be assigned to a descriptively named variable or function:

*Right:*

```js
var isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if (isValidPassword) {
  console.log('winning');
}
```

*Wrong:*

```js
if (password.length >= 4 && /^(?=.*\d).{4,}$/.test(password)) {
  console.log('losing');
}
```

## Functions

### Write small functions

Keep your functions short. A good function fits on a slide that the people in
the last row of a big room can comfortably read. So don't count on them having
perfect vision and limit yourself to ~15 lines of code per function.

### Return early from functions

To avoid deep nesting of if-statements, always return a function's value as early
as possible.

*Right:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

*Wrong:*

```js
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

Or for this particular example it may also be fine to shorten things even
further:

```js
function isPercentage(val) {
  var isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```

### Name your closures

Feel free to give your closures a name. It shows that you care about them, and
will produce better stack traces, heap and cpu profiles.

*Right:*

```js
req.on('end', function onEnd() {
  console.log('winning');
});
```

*Wrong:*

```js
req.on('end', function() {
  console.log('losing');
});
```

### No nested closures

Use closures, but don't nest them. Otherwise your code will become a mess.

*Right:*

```js
setTimeout(function() {
  client.connect(afterConnect);
}, 1000);

function afterConnect() {
  console.log('winning');
}
```

*Wrong:*

```js
setTimeout(function() {
  client.connect(function() {
    console.log('losing');
  });
}, 1000);
```


### Method chaining

One method per line should be used if you want to chain methods.

You should also indent these methods so it's easier to tell they are part of the same chain.

*Right:*

```js
User
  .findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });
````

*Wrong:*

```js
User
.findOne({ name: 'foo' })
.populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });

User.findOne({ name: 'foo' }).populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' }).populate('bar')
  .exec(function(err, user) {
    return true;
  });
````

## Comments

### Use slashes for comments

Use slashes for both single line and multi line comments. Try to write
comments that explain higher level mechanisms or clarify difficult
segments of your code. Don't use comments to restate trivial things.

*Right:*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE', 'SOMETHING', 'VALUE']
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
function loadUser(id, cb) {
  // ...
}

var isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
  // ...
}
```

*Wrong:*

```js
// Execute a regex
var matches = item.match(/ID_([^\n]+)=([^\n]+)/);

// Usage: loadUser(5, function() { ... })
function loadUser(id, cb) {
  // ...
}

// Check if the session is valid
var isSessionValid = (session.expires < Date.now());
// If the session is valid
if (isSessionValid) {
  // ...
}
```

## Miscellaneous

### Object.freeze, Object.preventExtensions, Object.seal, with, eval

Crazy shit that you will probably never need. Stay away from it.

### Requires At Top

Always put requires at top of file to clearly illustrate a file's dependencies. Besides giving an overview for others at a quick glance of dependencies and possible memory impact, it allows one to determine if they need a package.json file should they choose to use the file elsewhere.

### Getters and setters

Do not use setters, they cause more problems for people who try to use your
software than they can solve.

Feel free to use getters that are free from [side effects][sideeffect], like
providing a length property for a collection class.

[sideeffect]: http://en.wikipedia.org/wiki/Side_effect_(computer_science)

### Do not extend built-in prototypes

Do not extend the prototype of native JavaScript objects. Your future self will
be forever grateful.

*Right:*

```js
var a = [];
if (!a.length) {
  console.log('winning');
}
```

*Wrong:*

```js
Array.prototype.empty = function() {
  return !this.length;
}

var a = [];
if (a.empty()) {
  console.log('losing');
}
```

## ESLint Setup

### Sublime Setup

Sublime text editor has a package called 'ESlint' that can be installed via the 
package manager.

#### Install Node.js and eslint

Before using this plugin, you must ensure that `eslint` is installed on your system.
To install `eslint`, do the following:

1. Install [Node.js][Node.js] (and [npm][npm] on Linux).

2. Install `eslint` globally by typing the following in a terminal:
   ```bash
   npm install -g eslint
   ```
#### Install plugin

Install this plugin by using Sublime Text [Package Control][Package Control].

1. Open **"Command Pallet"** <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>p</kbd> (<kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>p</kbd> on OSX)
2. Select **"Package Control: Install Package"**
3. Select **ESLint**
4. Download `.eslintrc` from this repository and use it as your config\_file as described below. 
#### Configuring ESLint

[ESLint][ESLint Official] allows you to specify the JavaScript language options you want to support by using `.eslintrc` file,
it will use the first `.eslintrc` file found traversing from the active file in Sublime Text up to your project's root.

You can configure ESLint options by specify `.eslintrc` file.
For more information, see the [ESLint docs][ESLint Official Configuration Docs].

#### Settings

Several settings are available to customize the plugin's behavior.
Those settings are stored in a configuration file, as JSON.

Go to "`Preferences` / `Package Settings` / `ESLint` / `Settings - User`" to add your custom settings.

##### node\_path

*Default: `""`*

The directory location of your `node` executable lives.
If this is not specified, then it is expected to be on Sublime's environment path.

##### node\_modules_path

*Default: `""`*

The directory location of global `node_modules` via `npm`.
If this is not specified, then it is expected to be on system environment variable `NODE_PATH`.

##### config\_file

*Default: `""`*

This option allows you to specify an additional configuration file for ESLint.
If not specified, follows the default config file hierarchy.
This option works same as ESLint `-c` or `--config` command line option.

#### Run ESLint

ESLint an active JavaScript file.


* Open the context menu (right-click), and Select **ESLint**,  
  Or Open "Command Pallet" and Select **ESLint**,  
  Or keyboard shortcut: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>e</kbd> (<kbd>Cmd</kbd> + <kbd>Option</kbd> + <kbd>e</kbd> on OSX)

* <kbd>F4</kbd> : Jump to next error row/column
* <kbd>Shift</kbd> + <kbd>F4</kbd> : Jump to previous error row-column

**Note:**
The <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>e</kbd> (<kbd>Cmd</kbd> + <kbd>Option</kbd> + <kbd>e</kbd> on OSX) shortcut changes the Build System on the current file to ESLint,
then Builds to run ESLint on the file and output any errors for jumping to within the file.
You could alternatively set the Build System to Automatic and <kbd>Ctrl</kbd> + <kbd>b</kbd> (<kbd>Cmd</kbd> + <kbd>b</kbd> on OSX) or <kbd>F7</kbd>,
but only on files that end with `.js`.