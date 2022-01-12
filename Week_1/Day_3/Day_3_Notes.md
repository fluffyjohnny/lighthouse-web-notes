# Notes for W1D3

## Objects 

----

### Objectives 
- [ ] primitive data types review 
- [ ] objects! 
- [ ] passing primitives and objects to functions 
- [ ] function as object methods 
- [ ] what is `this`
- [ ] object iteration with `for...in` loops

-----

### 7 Primitives data types 
To check the data type of a data, we can use the `.typeOf()` operator.
- strings 
- numbers 
  - `Number.MAX_SAFE_INTEGER`
    - the max number to be safely operate as an integer 
- boolean 
- undefined 
- null 
- symbol
  - often used along side objects 
  - to create a symbol 
    - Symbol('')
    - this variable is guaranteed to always be unique
      - even if compare using the strict equal operator `===`
- bigint 
  - integer that is larger than `Number.MAX_SAFE_INTEGER`
  - by placing a "`n`" behind the integer 
  - DO NOT mix numbers with bigint 
  - large numbers will not be automatically convert to bigint

-------

### Objects 
we want to store values in JS that has properties instead of just numbers, which has certain attribute assigned to it. 

anything that is not a primitive value in JS is considered an Object. 

to call upon the attribute of an object 
- dot notation 
  -  `object.attricbute`
  - to grab an element from an array of attributes, we use the index `[i]` to grab specific elements 
- bracket notation 
  - `object['attribute']`
  - the string 'attribute' can be assigned to a `variable` and use the variable to call upon the attribute of an object
-  `console.log()` vs `console['log']`
    - we generally use the dot notation 
    - when we don't neccesarily know the key we're going to interact with, we would use the bracket notation 
      - bracket notation is less prone to bugs but more time consuming to layout

to create a new attribute in an array, simply:

    object.newAttribute = newValue

-----

### Passing Values 

`global scope` vs. `local scope`

primitive functions passing by `value`
- Global stays global 
- Local stays local
  - "here is a copy that you can use and manipulate..."

`Objects `

when changing the value of an global variable of an object within an function, the object value within the global scope will also be changed.

primitive function passing by the `reference` 
- uses the good copy of the variable, so by changing the value it in terms mutates the primitive value 
- objects values are `mutable` in JavaScript (const) 

[PythonTutor](https://pythontutor.com/visualize.html#mode=edit) is a great tool used to visualize the function of your code, it breaks down the code into step by step process so it's easier to visualize. 

-------
### Methods 

a function that belongs to an object, each method has their own unique function stored to the method 

  - `log` 
  - `slice` 
  - `join` 
  - `splice` 
  - `trim`

to create a method: 
  - create a `function` assinged to a key within an object 
    - can also assign a function in the global scope to a key within the object 
      - If we invoke the function within the object instead of assigning the name of the function, the value of the function will be assigned instead of the function itself
      - the key will not be a method, instead it will just be storing a primitive value 

----

### Keyword `This`
the keyword `This` reference to the whole object 
  - can use this keyword to replace the name of the object if it is called upon inside of the referred object 
  - referencing the object to which it is called 

----- 

### Object iteration with `for...in` looping

objects are not ordered in any way, so.. what are we looping over? 
the `key names` will be looped through

    for (const key in object) {
      console.log(object[key]);
    } 
this will return the value of each key from the object!

Usually only use bracket notation since we dont explicitedly know what the value of `key` will be, so we cannot use dot notation in this situation. Dot notation does not take variables.

can be pair with `if...` statements to filter out different conditions 