# Day 4 Notes 

## Lecute outline 
- *Functions as values* 
- *Function calling vs function passing vs function definitions*
- *Callbacks and higher order functions* 
- *Anonymous functions* 
- *Arrow functions* 
- *Make our own higher order function* 


--------------

### function as values 

functions can be passed with different values 
- string value 
- number value 
- function value 

a function needs to have 3 components, basically the minimal process of computing
  1. input 
  2. process 
  3. output

    const myFunctions = [func1, func2] {
    }

    function doActionFourTimes(action){
      for (let i = 0; i < 4; i++) {
        action(i);
      }
    }

-----------

### Passing functions 

    function processor(arg1, callback) {
      
      console.log('arg1', arg1)
      callback('monkey fuzz!');

    }

    processor(1, function(string){console.log('my sting is' + string)})
    
    // output = arg1 1 
    my string is monkey fuzz!

-----------

### Anonymous functions

    function product(a, b) {
      return a * b
    }; 

    const runDatabaseQuery = 
      function(action){
        action('Elise');
      };

    const sayHello = function(name){ console.log(`Hello, `, name);};

    runDatabaseQuery(sayHello); 
    //output: hello, Elise

    // this is an anonymous function 

------------

### Arrow Functions 

just anohter syntax for defining functions 

theyre way more compact, and they treat the variable `this` a little differently 

    // normal function call
    const runMyFunction = function(callback){
      callback('monkey fuzz!');
    }

    // arrow function call
    const runMyFunction2 = (callback) => {
      callback('monkey fuzz!');
    }

to call back an arrow function within a function... 

    runMyFunction( (string) => { console.log(string); return string;} );

    // output: monkey Fuzz!

*to simplify...*

if only have 1 parameter, we can drop the bracket and the curly braces, and we can dismiss the return value as well 


    runMyFunction( string => console.log(string) );


when `this` is utilized, the output will come out different based on what type of syntax choose to use... which we will not get into right now until we have more context... 

---------------------------

### Make your own higher function callback 

    const animalNoises = ['Oink', 'Moo', 'Meow', 'Bark'];

    animalNoises.forEach( (element) => {
      console.log(`monkey does not say ${element}`);
    } );

    //output: monkey does not say... 'element' x4

now lets do another one 

    const ourForEach = (arr, callback) => {

      for (let i = 0; i < arr.length; i++) {
        callback( arr[i] );
      }
    };

    ourForEach(animalNoises, (element) => {
      console.log('tada!', element);
    } )

    //output: tada! Oink, tada! Moo.... etc.