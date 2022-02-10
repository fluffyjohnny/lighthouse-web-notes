# W2D2 - Asynchronous Control Flow

## <u> Review of how functions are defined </u> 

today we learn about how JavaScript handle asynchronous computing. 

all computing can be broken down into input, computing and output. 




## <u>Why do we want to use callbacks?</u>

* to abstract out the actual computation
* with asynchronous code, you **_cannot_** retrieve the return value

## <u>Robot</u>

```Javascript

```
## how is javascript ran?
1. **the main thread**
  - goes and find the file
2. **the event loop** 
  - does not start until the main thread is finished 
  - the event loops processes functions/callbacks (actions, activities, morsels of computation, processes... etc.) as they were `scheduled` to happen 
  - you can use callbacks as a way of gathering OUTPUTS from anonymous functions on the event loop 
  

## <u>what is asynchronicity </u>
able to to still access and manipulate the program while running the program, basically the main frame is ran and every actions are scheduled

## <u>Events </u>
a callback in reaction to a certain event that happened on the event loop

## <u>Nesting </u>
