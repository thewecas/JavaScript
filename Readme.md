# [33 JavaScript Concepts Every Developer Should Know 🤓️💯️](https://dev.to/eludadev/33-javascript-concepts-every-beginner-should-know-with-tutorials-4kao#1-call-stack)

## 1. Call stack, Heap, Queue, Execution Context, Event Loop

- ### Execution Context

  - Where Execution of code takes place
  - it has 2 components
    - Memory : where varibales and functions are stored as key:value pair
    - Code : wh - ere execution of code happens

- ### Call Stack

  - Data structure for recording fuction calls
  - Max calls in chrome is 16,000 frames

- ### Heap

  - Memory allocation to variables and objects happens in Queue

- ### Queue

  - All the callback functions are stored here

- ### Event Loop

  - Continuously monitors Call stack and Queue,
  - If callstack becomes empty, it push the callback fn from Queue to call stack

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

    ```
    let x = 1;

    if (x === 1) {
      let x = 2;

      console.log(x); // 2
    }

    console.log(x); // 1
    ```

  - **var** : scope within the function i.e, withinn enitire enclosing function

    ```
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

  - **const** : blcok scope, value can't be changed once it's initiated.
    `const pi = 3.24;`

## 3. Value Types and Reference Types

- Premitives are copied/pass by their value

  ```
  let number = 10;

  function foo(number) {
      number++;
  }

  foo(number);

  console.log(number);   // 10;
  ```

- Objects are copied/pass by their reference

  ```
  let obj = { value: 10 };

  function foo(obj) {
      obj.value = 22;
  }

  foo(obj);

  console.log(obj);   // { value: 22 };
  ```

## 4. Coercion (Type Casting)

- Javascript attempting to coerce an unexpected value type to the expected type i.e converts value from one type to another.

  ```
  '5' + 5        // 55 , number `5` in interpreted as a string
  '5' - 5        // 0 , string `5` is interpreted as a number, works same for *, /, %
  true + 5       // 6 , `true` is interpreted to value `1`
  false + 5      // 5 , `false` is interpreted as value `0`
  ```

- **Implicit vs Explicit Coercion**

  | Implicit Coercion                                          | Explicit Coercion                                                |
  | ---------------------------------------------------------- | ---------------------------------------------------------------- |
  | Values are converted between different types automatically | Developer converts between types by writing the appropriate code |
  | Example :`5 + '5'    // 55`                                | Example :` 5 + Number('5')    // 10`                             |

- Only 3 types of conversion can be done in js

  1. to String
     ```
       String(123)        // explicit
       123 + ''           // implicit
     ```
  2. to boolean
     ```
      Boolean(2)          // explicit
      if (2) { ... }      // implicit
     ```
  3. to number
     ```
     Number('123')        // explicit
     5 - '5'              // implicit
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
| Example :<br />` 4 == '4'       // true`                                                                               | Example :<br />` 4 === '4'    // fasle`                                                                                                     | Example :<br />`typeof 'hi'    // 'string' `           |

## 6. Scope

- scope ~ availabiltiy

| Global scope                                                                  | Function scope                                                          | Block scope                                               |     |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------------------- | --------------------------------------------------------- | --- |
| Variables declared outside of any functions or blocks.                        | Variables declared within a function                                    | Variables declared within block (defined by curly braces) |     |
| accessed from anywhere within the code, including other functions and blocks. | only accessible within that function and any nested functions inside it | only accessible within the block.                         |     |

## 7. Expression vs Statement

| Expression                              | Statements                                     |
| --------------------------------------- | ---------------------------------------------- |
| Expressions evaluates to a single value | Statemets are the instructions to perform task |
| Example :`2+3*5` will evaluates to 17   | Example :`if (true) concole.log("hi")`         |

- **Function expression :**
  - function as part of an expresion
  - Example : `let sum = fucniton(){...}`

## 8. IIFE, Modules and Namespaces

- ### IIFE (Immediately Invoked Function Expression)

  - It's a self-executing anonymous function.
  - Variables & functions inside the IIFE are have local scope.
  - Prevents global scope pollution
  - Syntax :

    ```
    (function () {
        //code
    })()
    ```

  - Example :

    ```
    (function () {
        let value = 10;
    })()
    ```

- ### Modules

  - Allows to organize code in separate files.
  - helps in writing reusable & maintainable code.
  - a module may contain variable, function or classes
  - **Exporting Module**

    - `export` keyword is used for named export
    - `export default ` keyord is used to default export
    - Example :

      ```
      //module.js

      export default name = "vikas";

      export function greet() {
          console.log("Hi everyone");
      }
      ```

  - **Importing Module**

    - `import` keyword can be used for importing
    - Example :

      ```
      //main.js

      import guestName from "/module.js"   //imports default export. i.e, name varibale

      import { greet } from "/module.js"     //imports greet from module

      console.log(guestName + "says " + greet());
      ```

- ### Namespaces

  - Containers uses to group & oragnize the related variables, functions and objects.
  - Helps in avoiding naming conflicts.
  - Namspaces are not built into js. but it can be achieved using objects
  - It can be accessed using the dot operator.
  - Example :

    ```
    var marksNamespace = {
        mark1: 34,
        mark2: 45,
        avg: function () {
            return (this.mark1 + this.mark2) / 2;
        }
    }

    console.log(marksNamespace.mark1);      //accessing the mark1 namespace
    console.log(marksNamespace.avg());      //accessing the avg namespace, which calls the associated function
    ```

- [x] closure
- [x] hoisting
