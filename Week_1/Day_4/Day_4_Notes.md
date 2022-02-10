# W1D4 - Callbacks

## Lecute outline 
- Functions as values
- Calling a function vs. passing a function
- Callbacks!
- Anonymous functions
- Arrow functions
- Higher order functions

<br>

--------------
<br>

## Function as values 

Functions can be passed with different values 
- String value 
- Number value 
- Function value 

A function needs to have 3 components, basically the minimal process of computing
  1. Input 
  2. Process 
  3. Output
```javascript
const myFunctions = (`Input`) => {
  `Process`
  return `Output`;
};

function doActionFourTimes(action){
  for (let i = 0; i < 4; i++) {
    action(i);
  }
};
```
<br>

-----------
<br>

## Passing functions 
Functions can be passed as arguments to other functions
```javascript
const processor = (arg1, callback) => {
  console.log('arg1', arg1);
  callback('monkey fuzz!');
};

processor(1, (string) => {
  console.log('my sting is' + string)
});
    
/* 
output = arg1 1 
my string is monkey fuzz!
*/
```
Functions that are passed to functions are called callbacks. In other words, a callback is a function that gets passed to another function to be invoked in a function.

<br>

-----------
<br>

## Anonymous functions
We don't have to pass a function variable to a higher order function as a callback but instead, we can pass an unnamed (anonymous) function directly inline.
```javascript
function product(a, b) {
  return a * b
}; 

const runDatabaseQuery = function(action) {
    action('Elise');
  };

const sayHello = function(name){ console.log(`Hello, `, name);};

runDatabaseQuery(sayHello); 
//output: hello, Elise
```

<br>

-----------
<br>

## Arrow Functions 

Arrow functions give us a syntactic alternative to using the function keyword, they are way more compact, and they treat the variable `this` a little differently 
- Arrow functions are often used as callbacks because they are shorter/cleaner to type
```javascript
// normal function call
const runMyFunction = function(callback){
  callback('monkey fuzz!');
};

// arrow function call
const runMyFunction2 = (callback) => {
  callback('monkey fuzz!');
};
```
To call back an arrow function within a function... 
```javascript
runMyFunction( (string) => { console.log(string); return string;} );

// output: monkey Fuzz!
```
*To simplify more...*

If only have 1 parameter, we can drop the bracket and the curly braces, and we can dismiss the return value as well 

```javascript
runMyFunction(string => console.log(string));
```

When `this` is utilized, the output will come out different based on what type of syntax choose to use... which we will not get into right now until we have more context... 

<br>

---------------------------
<br>

## Make your own higher function callback 
```javascript
const animalNoises = ['Oink', 'Moo', 'Meow', 'Bark'];

animalNoises.forEach( (element) => {
  console.log(`monkey does not say ${element}`);
} );

//output: monkey does not say 'element' x4
```

```javascript
const ourForEach = (arr, callback) => {
  for (let i = 0; i < arr.length; i++) {
    callback(arr[i]);
  }
};

ourForEach(animalNoises, (element) => {
  console.log('tada!', element);
});

//output: tada! Oink, tada! Moo.... etc.
```