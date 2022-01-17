# W2D1 Notes - Testing 

## Manual Testing 

```javascript 
const sayHello = (name) => {
  console.log(`hello there ${name}`);
};
```

should always have an expectation of waht your code will output 

very time consuming and expensive to do manual testing

its much easier to test a return value than console logging a value, because we can assign return value to a variable 

```javascript 
if we change the console.log() to return, we can... 

const output = sayHello('name');
```

## Object assert
assertion is a forceful faction belief

```javascript 
const assert = require('assert').strict

// recommending strict equal, will only allow the strict equal keys inside of the assert object
```

why is assert better than console logging? 
- we want to see what is going on with the code and see if there are any errors, instead of just seeing the log

we want to seperate the testing codes from the production codes, should have different directories from the production files and the testing code files

```javascript 
module.exports = file

// allows us to export code lines and import them into other files without pasting the codes 
```
```javascript
// to import...

const variable = require('../filename');

// within require(), we use relative file location
``` 
make sure to double check what you're exporting and what youre importing 

## node wrapper function 

before a module's code is executed, node.js will wrap it with a function wrapper 

```javascript
(function(exports, reuqire, module, __filename, __dirname) {
  //module code actually lives here
});
```
## NPM - node package manager 

a place where programmers can submit their open-source package 

Will probably want to look at the reviews or weekly downloads to presume if the package is functional or not 

all these packages are hosted by github

*Three ways to install things*
* `npm install <package>`  
  * install the package as a dependency
  * required for the package 
* `npm install --global <package>`  
  * install the package globally 
* `npm install --save-dev <package>`  
  * install as a dev dependency 
  * just for the developement purpose
  * all the testings should be done in the dev environment 

## describe 

```javascript
// describe groups test together 

describe('I group tests together', () => {
  it(...);
  it(...);
});
```

you can also have describe inside of a discribe statement

## notes 
never add node_module to our github, if user wants to clone our file, they can go into our package.JSON to see our version dependency, user can then go download those themselves from npm/github

we use `gitignore` to ignore certain files from being push into our repository 

## chai 

we use it for the chai assert library, which we will be focusing on mostly `assert`, which they have more than enough options for us to test different cases of asserts  

