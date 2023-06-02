# [33 JavaScript Concepts Every Developer Should Know 🤓️💯️](https://dev.to/eludadev/33-javascript-concepts-every-beginner-should-know-with-tutorials-4kao#1-call-stack)


### 1. Call stack, Heap, Queue, Execution Context, Event Loop
 - Execution Context
   - Where Execution of code takes place
   - it has 2 components
     - Memory : where varibales and functions are stored as key:value pair
     - Code : where execution of code happens
 - Call Stack
   - Data structure for recording fuction calls
   - Max calls in chrome is 16,000 frames
 - Heap
   - Memory allocation to variables and objects happens in Queue
 - Queue
   - All the callback functions are stored here 
 - Event Loop
   - Continuously monitors Call stack and Queue, 
   - If callstack becomes empty, it push the callback fn from Queue to call stack
