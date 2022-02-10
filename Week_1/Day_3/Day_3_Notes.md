# W1D3 - Objects

## Objectives 
- [ ] primitive data types review 
- [ ] objects! 
- [ ] passing primitives and objects to functions 
- [ ] function as object methods 
- [ ] what is `this`
- [ ] object iteration with `for...in` loops

<br>

----- 
## Primitives Types 
There are 7 primitive types of data in JavaScript, to check the data type of a data, we can use the `.typeOf()` operator. Primitive types are immutable.

- Strings 
- Numbers 
  - `Number.MAX_SAFE_INTEGER`
    - the max number to be safely operate as an integer 
- Boolean 
- Undefined 
- Null 
- Symbol
  - often used along side objects 
  - to create a symbol...
    - `Symbol('')` : this variable is guaranteed to always be unique, even if compare using the strict equal operator "`===`".
- Bigint 
  - integer that is larger than `Number.MAX_SAFE_INTEGER`
  - by placing a "`n`" behind the integer 
  - DO NOT mix numbers with bigint 
  - large numbers will not be automatically convert to bigint

<br>

----- 
### `Objects`
We want to store values in JS that has properties instead of just numbers, which has certain attribute assigned to it. 

Anything that is `not a primitive value` in JS is considered an Object, including functions and arrays.

Objects are...
- Data structures that contain related data and functionality.
- Made up of key-value pairs where you can access the value from the key.
  - Keys are strings/values can be an type (primitive or object).

To call upon the attribute of an object 
- **dot notation** 
  -  `object.attricbute`
      - To grab an element from an array of attributes, we use the index `[i]` to grab specific elements 
- **bracket notation** 
  - `object['attribute']`
    - The string 'attribute' can be assigned to a `variable` and use the variable to call upon the attribute of an object
-  `console.log()` vs `console['log']`
    - We generally use the dot notation 
    - When we don't neccesarily know the key we're going to interact with, we would use the bracket notation 
      - Bracket notation is less prone to bugs but more time consuming to layout

To create a new attribute in an array, simply:
```javascript
object.newAttribute = newValue
object['newAttribute'] = newValue
```
<br>

----- 
## Passing Values 

### `global scope` vs. `local scope`

Primitive functions passing by `value`
- Global stays global 
- Local stays local
  - "here is a copy that you can use and manipulate..."

Primitive function passing by the `reference`.

For `Objects `... 

When changing the value of an global variable of an object within an function, the object value within the global scope will also be changed.
- Uses the good copy of the variable, so by changing the value it in terms mutates the primitive value 
- Objects values are `mutable` in JavaScript (const) 

<br>

----- 
  [PythonTutor](https://pythontutor.com/visualize.html#mode=edit) is a great tool used to visualize the function of your code, it breaks down the code into step by step process so it's easier to visualize. 

<br>

----- 
## Methods 

a function that belongs to an object, each method has their own unique function stored to the method 

  - `log` 
  - `slice` 
  - `join` 
  - `splice` 
  - `trim`

### To create a method: 
  - Create a `function` assinged to a key within an object 
    - Can also assign a function in the global scope to a key within the object 
  - If we invoke the function within the object instead of assigning the name of the function, the value of the function will be assigned instead of the function itself
    - The key will not be a method, instead it will just be storing a primitive value 

<br>

----- 
## Keyword `This`
the keyword `This` reference to the whole object
  -  Is a keyword that accesses the given scope's object.
  - Can use this keyword to replace the name of the object if it is called upon inside of the referred object 
  - Referencing the object to which it is called

<br>

----- 
## Object iteration with `for...in` looping

Objects are not ordered in any way, so.. what are we looping over? The `key names` will be looped through!
```javascript
for (const key in object) {
  console.log(object[key]);
} 
```
This will return the value of each key from the object!

Usually only use bracket notation since we dont explicitedly know what the value of `key` will be, so we cannot use dot notation in this situation. Dot notation does not take variables.

Can be pair with `if...` statements to filter out different conditions. 