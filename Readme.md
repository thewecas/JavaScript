# [33 JavaScript Concepts Every Developer Should Know 🤓️💯️](https://github.com/leonardomso/33-js-concepts)

## 1. Call stack, Heap, Queue, Execution Context, Event Loop

- ### Execution Context

  - Where Execution of code takes place
  - it has 2 components
    - Memory : where variables and functions are stored as key:value pair
    - Code : wh - ere execution of code happens

- ### Call Stack

  - Data structure for recording function calls
  - Max calls in chrome is 16,000 frames

- ### Heap

  - Memory allocation to variables and objects happens in Queue

- ### Queue

  - All the callback functions are stored here

- ### Event Loop

  - Continuously monitors Call stack and Queue,
  - If call stack becomes empty, it push the callback fn from Queue to call stack

## 2. Data Types

- ### Primitive types

  Stored in Stack memory, has fast access time & less storage

  - string : `"hello"`
  - number : `12, 3.1415`
  - boolean : `true, false`
  - undefined
  - null

- ### Reference/Non primitive types

  Stored in Heap memory, has low access time but more storage

  - Objects : `const person = { name: "vikas", age: 22 } ;`
    - Array : `let arr = [1, 2, 3, 4] ;`

- ### Variables

  - **let** : scope within current execution context i.e block and sub block have different scope

    ```js
    let x = 1;

    if (x === 1) {
      let x = 2;

      console.log(x); // 2
    }

    console.log(x); // 1
    ```

  - **var** : scope within the function i.e, within entire enclosing function

    ```js
    var x = 1;

    function foo() {
      var y = 2;

      console.log(x); // 1 (function `foo` closes over `x`)
      console.log(y); // 2 (`y` is in scope)
    }

    foo();

    console.log(x); // 1 (`x` is in scope)
    console.log(y); // ReferenceError, `y` is scoped to `foo`
    ```

  - **const** : block scope, value can't be changed once it's initiated.
    `const pi = 3.24;`

## 3. Value Types and Reference Types

- Primitives are copied/pass by their value

  ```js
  let number = 10;

  function foo(number) {
    number++;
  }

  foo(number);

  console.log(number); // 10;
  ```

- Objects are copied/pass by their reference

  ```js
  let obj = { value: 10 };

  function foo(obj) {
    obj.value = 22;
  }

  foo(obj);

  console.log(obj); // { value: 22 };
  ```

## 4. Coercion (Type Casting)

- Javascript attempting to coerce an unexpected value type to the expected type i.e converts value from one type to another.

  ```js
  "5" + 5; // 55 , number `5` in interpreted as a string
  "5" - 5; // 0 , string `5` is interpreted as a number, works same for *, /, %
  true + 5; // 6 , `true` is interpreted to value `1`
  false + 5; // 5 , `false` is interpreted as value `0`
  ```

- **Implicit vs Explicit Coercion**

  | Implicit Coercion                                          | Explicit Coercion                                                |
  | ---------------------------------------------------------- | ---------------------------------------------------------------- |
  | Values are converted between different types automatically | Developer converts between types by writing the appropriate code |
  | Example :`5 + '5'    // 55`                                | Example :` 5 + Number('5')    // 10`                             |

- Only 3 types of conversion can be done in js

  1. to String
     ```js
     String(123); // explicit
     123 + ""; // implicit
     ```
  2. to boolean
     ```js
      Boolean(2)          // explicit
      if (2) { ... }      // implicit
     ```
  3. to number
     ```js
     Number("123"); // explicit
     5 - "5"; // implicit
     ```

- **Type coercion for objects** :

  - Boolean conversion will always coerced the objects to `true`
  - String conversion can be done using `toString()`
  - Number conversion can be done using `valueOf()`

- **Nominal Typing** : Compatibility between objects determined based on their explicit type or name, rather than their structure.
- **Duck typing** : Compatibility of objects is determined by whether they possess certain methods or properties, rather than their specific type or class.
- **Structural typing** : A concept where the compatibility between objects is determined by their structure or shape, rather than their explicit type or name.

## 5. == vs === vs typeof

| ==                                                                                                                     | ===                                                                                                                                         | typeof                                                 |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| Checks if the values being compared are equal, performing type coercion if necessary.<br />Performs a loose comparison | Checks if the values being compared are equal and of the same type, without performing any type coercion.<br />Performs a strict comparison | Determine the type of a value or expression            |
| Returns boolean value                                                                                                  | Returns boolean value                                                                                                                       | Returns a string representing the type of the operand. |
| Example :<br />` 4 == '4'       // true`                                                                               | Example :<br />` 4 === '4'    // false`                                                                                                     | Example :<br />`typeof 'hi'    // 'string' `           |

## 6. Scope

- scope ~ availability

| Global scope                                                                  | Function scope                                                          | Block scope                                               |     |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------------------- | --------------------------------------------------------- | --- |
| Variables declared outside of any functions or blocks.                        | Variables declared within a function                                    | Variables declared within block (defined by curly braces) |     |
| accessed from anywhere within the code, including other functions and blocks. | only accessible within that function and any nested functions inside it | only accessible within the block.                         |     |

## 7. Expression vs Statement

| Expression                              | Statements                                      |
| --------------------------------------- | ----------------------------------------------- |
| Expressions evaluates to a single value | Statements are the instructions to perform task |
| Example :`2+3*5` will evaluates to 17   | Example :`if (true) console.log("hi")`          |

- **Function expression :**
  - function as part of an expression
  - Example : `let sum = funciton(){...}`

## 8. IIFE, Modules and Namespaces

- ### IIFE (Immediately Invoked Function Expression)

  - It's a self-executing anonymous function.
  - Variables & functions inside the IIFE are have local scope.
  - Prevents global scope pollution
  - Syntax :

    ```js
    (function () {
      //code
    })();
    ```

  - Example :

    ```js
    (function () {
      let value = 10;
    })();
    ```

- ### Modules

  - Allows to organize code in separate files.
  - helps in writing reusable & maintainable code.
  - a module may contain variable, function or classes
  - **Exporting Module**

    - `export` keyword is used for named export
    - `export default ` keyword is used to default export
    - Example :

      ```js
      //module.js

      export default name = "vikas";

      export function greet() {
        console.log("Hi everyone");
      }
      ```

  - **Importing Module**

    - `import` keyword can be used for importing
    - Example :

      ```js
      //main.js

      import guestName from "/module.js"; //imports default export. i.e, name variable

      import { greet } from "/module.js"; //imports greet from module

      console.log(guestName + "says " + greet());
      ```

- ### Namespaces

  - Containers uses to group & organize the related variables, functions and objects.
  - Helps in avoiding naming conflicts.
  - Namespaces are not built into js. but it can be achieved using objects
  - It can be accessed using the dot operator.
  - Example :

    ```js
    var marksNamespace = {
      mark1: 34,
      mark2: 45,
      avg: function () {
        return (this.mark1 + this.mark2) / 2;
      },
    };

    console.log(marksNamespace.mark1); //accessing the mark1 namespace
    console.log(marksNamespace.avg()); //accessing the avg namespace, which calls the associated function
    ```

## 9. Message Queue and Event Loop

- When asynchronous operations such as netwwork request or timer is encountered, it's associated callback is placed in the queue in a fifo fashion,
- After the execution of synchronous code, the event loop process the queue.
- Event loop looks for pending task in queue, if yes then puts that task inside the stack.
- Asynchronous operations may include `eventlisteners` , `setTimeout` or any api request etc

## 10. setTimeout, setInterval and requestAnimationFrame

- ### setTimeout vs setInterval

  | setTimeout                                                                                                                | setInterval                                                                                      |
  | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
  | Executes a specified piece of code or a function once after a given delay.                                                | Executes a specified piece of code or a function repeatedly at a given interval.                 |
  | Syntax :`setTimeout(callback_fn, delay, ...parameters)`                                                                   | Syntax :`setInterval(callback_fn, delay, ...parameters)`                                         |
  | Example :`setTimeout(function(){console.log("hello");},1000)` will print `hello` once after 1 second of program execution | Example :`setInterval(function(){console.log("hello");},1000)` will print `hello` every 1 second |
  | Execution can be terminated with `clearTimeout()`                                                                         | Execution can be terminated with `clearInterval()`                                               |

- ### requestAnimationFrame

  - used to schedule a function to execute before updating visual elements in the webpage (called repainting)
  - Syntax : `requestAnimationFrame(callback_fn)`

## 11. JavaScript Engines

- for running Js, we need a Js runtime environment.
- Js runtime environment consist of JS Engine, API, event loop, queues....
- v8 engine (written in c++) is most famously used js engine, in chrome & node js
- 3 process happens inside the js engine

  - PARSING : code -> token -> abstract syntax tree,
  - COMPILATION (JIT) : AST-> byte code & optimize
  - EXECUTION : uses memory heap & call stack in the process

- Mark & sweep algorithm is used for garbage collection

## 12. Bitwise Operators

- performs operations on bits (0's and 1's)
- **NOT `~`** :
  - works on single bit, replaces 0 with 1 and 1 with 0
  - Example : `~5` -> `~ (101) `->`010`
- **OR `|`** :
  - either of the bit is 1 => result 1
  - Example : `5 | 6` -> `101 | 110` -> `111` -> `7`
- **AND `&`** :
  - both bits are `1` =>result 1
  - Example : `7 & 6 `->`111 & 110 `->`110 `->`6`
- **XOR `^`** :
  - one bit is `1` & other bit is `0` -> result `1`
  - Exmple : `5 ^ 6` -> `101 ^ 110` -> `011` ->`3`
- **Leftshift `<<`** :
  - shifts the number to left by specified number, works on single bit
  - Example : `5<<2` -> `0000 0101` -> `0001 0100` ->20
- **Rightshift `>>`** :
  - shifts the number to left by specified number, works on single bit
  - Example `20>>2` -> `001 0100` -> `0000 0101` ->5

## 13. DOM

- Document Object Model is a tree like representation of html document
- Each element is a node. HTML element is the root of the DOM
- `console.dir(document)` will print all the element & their properties
- ### Selectors

  | Selector   | CSS          | Js                                                                                            | JQuery            |
  | ---------- | ------------ | --------------------------------------------------------------------------------------------- | ----------------- |
  | Id         | `#id`        | `document.getElementById('id')` <br />`document.querySelector('#id')`                         | `$('#id')`        |
  | Class name | `.className` | `document.getElementsByClassName('className')` <br />`document.querySelectorAll('className')` | `$('.className')` |
  | Tag name   | `tagName`    | `document.getElementsByTagName(tagName)`<br />`document.querySelectorAll(tagName)`            | `$('tagName')`    |

  - `querySelector()` returns the first element
  - `querySelectorAll()` returns NodeList of elements
  - pseudo classes like `:nth-child()` , `::before` , `::placeholder` can also be used with selectors for selecting the html elements

- ### Node methods

  `parentNode()` , `parentElement()` , `childNodes()` , `children()` , `firstChild()` , `firstElementChild()` , `lastChild()` , `lastElementChild()` , `nextSibling()` , `nextElementSibling()` , `previousSibling()` , `previousElementSibling()`

  - methods that have the keyword `Element` returns only Element nodes,
  - methods without keyword `Element` returns all kind of nodes i.e Element node, text node, comment node etc.

- Create Element : `createElement(tagName)`
- Create text node : `createTextNode('text')`
- Add element to the document : `appendChild()` , `prependChild()`

## 14. Factory functions

- Functions that create & return object, Always use camel case
- Syntax :

  ```js
  function fnName( <params> ) {
    return { obj };
  }
  ```

- Example

  ```js
  function createCircle(radius) {
    return {
      radius: radius,
      circumference: () => {
        return 2 * 3.14 * radius;
      },
    };
  }

  const circle1 = createCircle(2); // creates a circle object
  console.log(circle1.circumference()); //12.56
  ```

## 14. this(), call(), apply(), bind()

### this

- references an object in the current execution context
- current execution context refers to,

  - global environment of the browser or nodejs

    ```js
    console.log(this); //prints the global object
    ```

  - when used inside a function, the object thats calling the function

    ```js
    function getObj() {
      console.log(this);
    }

    const user = {
      name: "thewecas",
      getObj,
    };

    user.getObj(); // prints user object
    ```

### bind

- used to explicitly set the reference of `this`

  ```js
  function getObj() {
    console.log(this);
  }

  const user = {
    name: "thewecas",
  };

  const myUser = getObj.bind(user);

  myUser(); //prints {name : "thewecas" }
  ```

### call

- call a function with different `this` context/value
- can pass additional arguments separated by comma
- ` fn.call( obj, param1, param2...)`

  ```js
  function getObj() {
    console.log(this);
  }

  const user = {
    name: "thewecas",
  };

  getObj.call(user); //prints {name : "thewecas" }
  ```

### apply

- similar to call ,but the second argument should be an array
- ` fn.apply( obj, [param1, param2 .... ] )`

  ```js
  function getObj() {
    console.log(this);
  }

  const user = {
    name: "thewecas",
  };

  getObj.apply(user); //prints {name : "thewecas" }
  ```

> `arguments` is a collection of arguments that are being passed to the function
>
> ```js
> function fn() {
>   console.log(arguments);
> }
> fn(1, 2, 3); // prints [1,2,3]
> ```

## 16. new, constructor, instanceof and Instances

- **constructor** is used for creating & initializing the object
- **new** keyword is used to invoke the constructor & create instance of a class

  ```js
  class Circle {
    constructor(radius) {
      this.radius = radius;
      this.draw = function () {
        console.log("Draw");
      };
    }
  }
  const myCircle = new Circle(5);
  ```

- use Pascal notation for naming constructor functions

  ```js
  function Circle(radius) {
    this.radius = radius;
    this.draw = function () {
      console.log("Draw");
    };
  }

  const myCircle = new Circle(1);
  ```

- **instance** is a unique object created from a class or constructor function
- **instanceof** keyword is used to check whether the object is an instance of a class or a constructor function

  ```js
  const name = new String("thewecas");
  console.log(name instanceof String); // true
  ```

## 17. Prototype Inheritance and Prototype Chain

- A prototype is a template for the object
- prototype property belongs to constructor functions or classes
- `Object.create()` is used to create an object from a prototype.

  - Example

  ```js
  const food = {
    // Prototype
    init: function (type) {
      this.type = type;
    },
    eat: function () {
      console.log("you ate the " + this.type);
    },
  };

  //creating the bread object  from the food prototype
  const bread = Object.create(food);
  ```

### Prototype Inheritance
