https://github.com/anil-sidhu/JavaScript-100-objective-based-questions

# JavaScript-100-objective-based-questions


**1. Can we connect JavaScript Directly with Actual Database. can you give reason of it ?**
```js
a) Yes;
b) No;
c) Sometime;
d) Some Database
```
<details>
	<summary><b>View Answer</b></summary>
<ul>
Answer: b) No

- No, JavaScript in the **browser** can’t connect directly to a database because of **security** and **protocol** restrictions — it would expose credentials and browsers can’t use database protocols.
Only **server-side JavaScript** (like **Node.js**) can safely connect to databases.

</ul>
</details>


**2. Which of the following is NOT a JavaScript data type?**
```js
a) String
b) Boolean
c) Float
d) Undefined
```

<details>
	<summary><b>View Answer</b></summary>
<ul>
Answer: c) Float
</ul>
</details>


**3. Which symbol is used for single-line comments in JavaScript?**
```js
a) //
b) /*
c) #
d) <!--
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) //
</ul>
</details>


**4. What will typeof null return?**
```js
a) "null"
b) "object"
c) "undefined"
d) "string"
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) "object"

- `typeof null` returns **`"object"`** ✅

👉 This is actually a **bug in JavaScript** — it dates back to the language’s early design and was never fixed for backward compatibility.

So even though `null` is **not** an object, `typeof null` still returns `"object"`.

</ul>
</details>



**5. How to make immutable object in JavaScript**
```js
a) final var ={name:'Anil'}
b) const user={name:'Anil'}
c) var  user={name:'Anil'}; Object.freeze(user);
c) There is no way to make immutable object
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) var  user={name:'Anil'}; Object.freeze(obj);
</ul>
</details>


**Operators & Expressions**

**6. What will 2 + "2" evaluate to?**
```js
a) 4
b) "22"
c) NaN
d) Error
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) "22"

- `2 + "2"` will evaluate to **`"22"`** ✅

👉 Reason:
The `+` operator with a **string** causes **type coercion** — JavaScript converts the number `2` into a string and performs **string concatenation**, not addition.

</ul>
</details>


**7.Which operator is used for strict equality in JavaScript?**
```js
a) ==
b) !==
c) =
d) !=
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) !==
</ul>
</details>



**8. What does !!"false" evaluate to?**
```js
a) true
b) false
c) undefined
d) Error
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) true

- `!!"false"` evaluates to **`true`** ✅

👉 Reason:

* `"false"` (in quotes) is a **non-empty string**, and all non-empty strings are **truthy** in JavaScript.
* The first `!` converts it to `false`.
* The second `!` negates that, giving **`true`**.

</ul>
</details>



**9. What is the result of 5 == "5"?**
```js
a) true
b) false
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) true

`5 == "5"` evaluates to **`true`** ✅

👉 Reason:
The `==` operator performs **type coercion**, so JavaScript converts the string `"5"` to a number before comparing — and both become `5`.

</ul>
</details>



**10. What is the result of type of  "5 " === " 5"?**
```js
a) true
b) false
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) false
</ul>
</details>



**11. Which loop is guaranteed to execute at least once?**
```
a) for loop
b) while loop
c) do-while loop
d) None of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) do-while loop
</ul>
</details>



**12. Output of this for loop loop**
```js 
for(;;) {
console.log("Loop")
}
```
```js
a) Infinit Loop 
b) Loop will not execute
c) Error
d) Only Run once 
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) Infinit Loop
</ul>
</details>


**13. What will console.log(typeof NaN); print?**
```js
a) "number"
b) "NaN"
c) "undefined"
d) "object"
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) "number"

`console.log(typeof NaN);` will print **`"number"`** ✅

👉 Reason:
`NaN` (Not-a-Number) is actually a **numeric value** in JavaScript — it represents an invalid number, but its **type is still `number`**.

</ul>
</details>


**14. Output of below statment**
```js
let x=null;
let y=null;
console.log(x+y) 
```
```js
a) null
b) object
c) 0
d) undefined
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) 0

The output will be **`0`** ✅

👉 Reason:

* Both `x` and `y` are `null`.
* When used in arithmetic operations, `null` is **converted to `0`**.
* So the expression becomes `0 + 0`, which equals **`0`**.

</ul>
</details>


**15. What will console.log(typeof function(){}); return?**
```js
a) "function"
b) "object"
c) "undefined"
d) "null"
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) "function"

`console.log(typeof function(){});` will return **`"function"`** ✅

👉 Reason:
In JavaScript, functions are **special objects**, and the `typeof` operator identifies them with the distinct type `"function"`.

</ul>
</details>


**16. What will console.log(typeof function(){}()); return?**
```js
a) "function"
b) "object"
c) "undefined"
d) "null"
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) "undefined"

✅ The output will be **`"undefined"`**

👉 Explanation:

```js
console.log(typeof function(){}());
```

* `function(){}()` defines an **anonymous function** and **immediately invokes** it (IIFE).
* The function has **no return statement**, so it returns **`undefined`**.
* Then `typeof undefined` → **`"undefined"`**.

</ul>
</details>

**17. What is the default return value of a function in JavaScript if no return statement is used?**
```js
a) null
b) undefined
c) false
d) 0
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) undefined

The default return value of a function in JavaScript, if no `return` statement is used, is **`undefined`** ✅

</ul>
</details>


**18. Which type of function executes immediately after its definition?**
```js
a) Anonymous function
b) Named function
c) IIFE (Immediately Invoked Function Expression)
d) Arrow function
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) IIFE

A **Immediately Invoked Function Expression (IIFE)** ✅

👉 Example:

```js
(function() {
  console.log("I run immediately!");
})();
```

🧠 It’s a function that’s **defined and executed instantly** — without being called separately.

</ul>
</details>


**19. Outpout of below statment** 
```js
 console.log(x);
 let x = 5; 
```
```js 
a) 5
b) undefined
c) ReferenceError
d) NaN
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) ReferenceError

❌ The output will be a **`ReferenceError`** ✅

👉 Explanation:

* `let` and `const` variables are **hoisted** but **not initialized**.
* They remain in the **Temporal Dead Zone (TDZ)** until the declaration line is executed.
* So when you try to access `x` before `let x = 5;`, JavaScript throws:

```
ReferenceError: Cannot access 'x' before initialization
```

</ul>
</details>


**20. How do you create an object in JavaScript?**
```js
a) let obj = {};
b) let obj = new Object();
c) Both a and b
d) None of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) Both a and b

You can create an object in JavaScript in several ways ✅

### 🧩 1. **Using Object Literal (most common)**

```js
const person = { name: "Alice", age: 25 };
```

### 🧱 2. **Using `new Object()`**

```js
const person = new Object();
person.name = "Alice";
person.age = 25;
```

### 🧰 3. **Using a Constructor Function**

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}
const p1 = new Person("Alice", 25);
```

### ⚙️ 4. **Using ES6 Class**

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}
const p1 = new Person("Alice", 25);
```

✅ **Most common and simplest way:**

```js
const obj = { key: "value" };
```

</ul>
</details>


**21. How do you access a property in an object?**
```js
a) obj[property]
b) obj.property
c) Both a and b
d) None of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) Both a and b
</ul>
</details>

**22. Which method is used to add a new element at the end of an array?**
```js
a) push()
b) pop()
c) shift()
d) unshift()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) push()

The **`.push()`** method ✅

👉 Example:

```js
const arr = [1, 2, 3];
arr.push(4);
console.log(arr); // [1, 2, 3, 4]
```

🧠 `.push()` adds one or more elements to the **end** of an array and returns the **new length** of the array.

</ul>
</details>


**23. What will console.log([1,2,3].length); return?**
```js
a) 2
b) 3
c) 4
d) undefined
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) 3

`console.log([1, 2, 3].length);` will return **`3`** ✅

👉 Reason:
The `.length` property of an array gives the **number of elements** in it.
Here, the array `[1, 2, 3]` has **3 elements**.

</ul>
</details>


**24. How do you remove first 2 element of an array?**
```js
a) pop()
b) shift()
c) unshift()
d) splice()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: d) splice()

You can remove the first 2 elements of an array using the **`splice()`** or **`slice()`** method ✅

### ✅ Using `splice()` (modifies original array)

```js
const arr = [1, 2, 3, 4, 5];
arr.splice(0, 2); // removes first 2 elements
console.log(arr); // [3, 4, 5]
```

### ✅ Using `slice()` (creates a new array)

```js
const arr = [1, 2, 3, 4, 5];
const newArr = arr.slice(2); // skips first 2 elements
console.log(newArr); // [3, 4, 5]
```

</ul>
</details>


**25. Which keyword allows block-scoped variable declarations?**
```js
a) var
b) let
c) const
d) Both b and c

```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: d) Both b and c

The keywords **`let`** and **`const`** allow **block-scoped** variable declarations ✅

👉 Example:

```js
{
  let a = 10;
  const b = 20;
}
// a and b are not accessible outside this block
```

</ul>
</details>

**26 Which of the following is true about const variables?**
```js
a) Their values cannot be changed
b) They cannot be reassigned
c) They are always immutable
d) All of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) They cannot be reassigned

✅ **Correct answer:** **b) They cannot be reassigned**

👉 Explanation:

* `const` **prevents reassignment** of the variable itself.
* However, if the value is an **object or array**, its **contents can still be changed** (mutated).

Example:

```js
const obj = { name: "Alice" };
obj.name = "Bob"; // ✅ allowed — object property changed
obj = {};         // ❌ Error — reassignment not allowed
```

</ul>
</details>


**27. What is the output of console.log(typeof([]));?**
```js
a) "object"
b) "array"
c) "undefined"
d) "null"
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) "object"

`console.log(typeof([]));` will output **`"object"`** ✅

👉 Reason:
In JavaScript, **arrays are special kinds of objects**, so the `typeof` operator returns `"object"` for arrays.

*(To check if something is truly an array, use `Array.isArray([])` → `true`)*

</ul>
</details>


**28. What is a template literal in JavaScript?**
```js
a) A type of array
b) A string enclosed in backticks (` `)
c) A special function
d) A new ES6 data type
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) A string enclosed in backticks (` `)

A **template literal** in JavaScript is a way to create strings that can include **variables** and **expressions** easily using **backticks (`)** ✅

### 🧩 Example:

```js
const name = "Alice";
const message = `Hello, ${name}!`;
console.log(message); // Hello, Alice!
```

### ✨ Features:

* Use **backticks** instead of quotes: `` ` ``
* Supports **multi-line strings**
* Allows **interpolation** with `${expression}`

Example:

```js
const a = 5, b = 10;
console.log(`Sum is ${a + b}`); // Sum is 15
```

</ul>
</details>


**29. What will console.log(..."Hello"); output?**
```js
a) "H e l l o"
b) ["H", "e", "l", "l", "o"]
c) Syntax Error
d) undefined
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) "H e l l o"

`console.log(..."Hello");` will output:

```
H e l l o
```

✅

👉 Explanation:

* The **spread operator (`...`)** expands an iterable (like a string or array) into individual elements.
* `"Hello"` is a string, so it gets spread into its characters: `H`, `e`, `l`, `l`, `o`.

</ul>
</details>


**30. How do you define an arrow function?**
```
a) const add = (a, b) => a + b;
b) const add = function(a, b) { return a + b; };
c) Both a and b
d) None of the above
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) const add = (a, b) => a + b;
</ul>
</details>



**31 What does the spread operator ... do in JavaScript?**
```js
a) Combines arrays
b) Expands iterable elements
C) All of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: C) All of the above

The **spread operator (`...`)** in JavaScript is used to **expand** (or “spread”) elements of an **iterable** (like an array, string, or object) into **individual elements** ✅

### 🧩 Examples:

#### 1. **In Arrays**

```js
const arr = [1, 2, 3];
const newArr = [...arr, 4, 5];
console.log(newArr); // [1, 2, 3, 4, 5]
```

#### 2. **In Objects**

```js
const obj = { a: 1, b: 2 };
const newObj = { ...obj, c: 3 };
console.log(newObj); // { a: 1, b: 2, c: 3 }
```

#### 3. **In Function Calls**

```js
const nums = [1, 2, 3];
console.log(Math.max(...nums)); // 3
```

👉 **In short:** The spread operator **unpacks** elements from arrays or objects.

</ul>
</details>


**32. What will console.log([...new Set([1, 2, 2, 3])]); return?**
```js
a) [1, 2, 3]
b) [1, 2, 2, 3]
c) Set {1, 2, 3}
d) {1, 2, 3}
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) [1, 2, 3]

`console.log([...new Set([1, 2, 2, 3])]);` will return **`[1, 2, 3]`** ✅

👉 **Explanation:**

* `new Set([1, 2, 2, 3])` creates a **Set**, which automatically removes **duplicate values** → `{1, 2, 3}`
* The **spread operator (`...`)** converts the Set back into an **array** → `[1, 2, 3]`

</ul>
</details>


**33. Which statement about arrow functions is true?**
```js
a) They do not bind this
b) They can be used as constructors
c) They have a prototype property
d) They support arguments keyword
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) They do not bind this

✅ **Correct answer:** **a) They do not bind `this`**

👉 **Explanation:**

* Arrow functions **do not have their own `this`** — they inherit it **lexically** from the surrounding scope.
* They **cannot** be used as constructors (`new` keyword ❌).
* They **don’t** have a `prototype` property.
* They **don’t** support the `arguments` keyword (use rest parameters instead).

</ul>
</details>


**34. Output of follow code?**
```js
function tryFruits(...fruits)
{
console.log(...fruits)
}

tryFruits('apple','banana','grapes')
```
```js
a) ['apple', 'banana', 'grapes']
b) {'apple', 'banana', 'grapes'}
c) 'apple 'banana grapes'
d) 'apple'
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) 'apple 'banana grapes'

✅ **Correct answer:** **c) `'apple banana grapes'`**

👉 **Explanation:**

* The rest parameter `...fruits` collects the arguments into an array → `['apple', 'banana', 'grapes']`.
* Inside `console.log(...fruits)`, the **spread operator** expands that array into individual values — so it prints them separated by spaces.

🧩 Output:

```
apple banana grapes
```

</ul>
</details>


**35. What is the purpose of JavaScript Promises?**
```js
a) Handle synchronous code
b) Handle asynchronous operations
c) Block execution until resolved
d) Replace all callbacks
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) Handle asynchronous operations

The purpose of **JavaScript Promises** is to **handle asynchronous operations** more cleanly and efficiently ✅

### 🧠 In simple terms:

A **Promise** represents a **value that will be available in the future** — it can be:

* **Pending** (still working),
* **Fulfilled** (completed successfully), or
* **Rejected** (failed with an error).

### ✨ Example:

```js
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Data received"), 1000);
});

promise.then(result => console.log(result)); // "Data received"
```

👉 **Purpose:**

* Avoids **callback hell**
* Makes asynchronous code easier to read and manage
* Works well with modern syntax like **`async/await`**

</ul>
</details>


**36. Which state is NOT valid for a Promise?**
```js
a) Pending
b) Fulfilled
c) Rejected
d) Running
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: d) Running

✅ **Correct answer:** **d) Running**

👉 **Explanation:**
A JavaScript **Promise** has only **three valid states**:

1. **Pending** – initial state (operation not completed yet)
2. **Fulfilled** – operation completed successfully
3. **Rejected** – operation failed

There’s **no “Running”** state in Promises.

</ul>
</details>


**37. Use of Await keyword ?**
```js
a) wait for an asynchronous operation to finish before continuing the execution
b) make promise
c) atop execution  
d) all of above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) wait for an asynchronous operation to finish before continuing the execution

The **`await`** keyword is used to **pause** the execution of an **async function** until a **Promise** is **resolved** or **rejected** ✅

### 🧩 Example:

```js
async function getData() {
  const data = await fetch("https://api.example.com/data");
  console.log("Data fetched!");
}
```

👉 **What it does:**

* `await` **waits** for the Promise returned by `fetch()` to resolve.
* The rest of the code inside the function runs **only after** the Promise is settled.
* It makes asynchronous code look and behave **like synchronous code**, improving readability.

⚠️ **Note:**
`await` can be used **only inside** an `async` function.

</ul>
</details>


**38. Which method selects an element by ID?**
```
a) document.getElementofId()
b) document.getElementById()
c) document.selectElementById()
d) document.selectById()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) document.getElementById()
</ul>
</details>



**39. Which event is triggered when an input field loses focus?**
```js
a) click
b) blur
c) focus
d) change
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) blur
</ul>
</details>


**40. Which method adds an event listener to an element?**
```js
a) element.addEventListener()
b) element.attachEvent()
c) element.onEvent()
d) element.setEventListener()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) element.addEventListener()
</ul>
</details>


**41. What does event.preventDefault() do?**
```js
a) Stops the default action of an event
b) Stops event propagation
c) Prevents event from being attached
d) None of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) Stops the default action of an event
</ul>
</details>

**43. What is localStorage used for?**
```js
a) Storing session data
b) Storing data persistently in the browser
c) Making API requests
d) Caching images
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) Storing data persistently in the browser

✅ **Answer:**
`localStorage` is used to **store data in the browser permanently** (until manually cleared).

### 🧩 Key Points:

* Stores **key–value pairs** as **strings**.
* Data **persists even after page reload or browser restart**.
* Has a **storage limit** of about **5–10 MB** (depending on browser).

### 🧠 Example:

```js
localStorage.setItem("name", "Alice");
console.log(localStorage.getItem("name")); // "Alice"
localStorage.removeItem("name");
```

👉 Use `localStorage` for saving things like user preferences, theme settings, or small app data.

</ul>
</details>


**44 Which method converts a JavaScript object into a JSON string?**
```js
a) JSON.stringify()
b) JSON.parse()
c) toJSON()
d) parseJSON()
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) JSON.stringify()

✅ **Answer:** `JSON.stringify()`

👉 **Example:**

```js
const obj = { name: "Alice", age: 25 };
const jsonString = JSON.stringify(obj);
console.log(jsonString); // '{"name":"Alice","age":25}'
```

🧠 **Explanation:**
`JSON.stringify()` converts a **JavaScript object** into a **JSON-formatted string**, which is useful for storing or sending data.

</ul>
</details>


**45 What will console.log(parseInt("10px")) return?**
```js
a) 10
b) NaN
c) "10px"
d) Error
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) 10

`console.log(parseInt("10px"))` will return **`10`** ✅

👉 **Explanation:**

* `parseInt()` reads a string from **left to right** and converts the initial numeric part into an integer.
* It stops parsing when it encounters a **non-numeric character** (`p` in this case).
* So `"10px"` → **`10`**

</ul>
</details>


**46. Which method executes a function repeatedly with a time interval?**
```js
a) setInterval()
b) setTimeout()
c) repeat()
d) setLoop()
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) setInterval()

✅ **Answer:** `setInterval()`

👉 **Example:**

```js
setInterval(() => {
  console.log("Hello!");
}, 1000);
```

🧠 **Explanation:**
`setInterval()` repeatedly executes a given function **at fixed time intervals** (in milliseconds) until it’s stopped using `clearInterval()`.

</ul>
</details>



**47. How do you check if a variable is an array?**
```js
a) typeof x === "array"
b) x.isArray()
c) Array.isArray(x)
d) x instanceof Object
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) Array.isArray(x)

✅ **Correct answer:** **c) Array.isArray(x)**

👉 **Explanation:**
`Array.isArray(x)` returns **true** if `x` is an array, otherwise **false**.
Other options are incorrect because:

* `typeof x === "array"` ❌ → `typeof` returns `"object"` for arrays.
* `x.isArray()` ❌ → no such method exists.
* `x instanceof Object` ❌ → true for many things, not just arrays.

</ul>
</details>




**48. What is a closure in JavaScript?**
```js
a) A function inside another function that has access to its parent’s scope
b) A block of code that runs automatically
c) A way to define private variables
d) Both a and c
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: d) Both a and c

✅ **Correct answer:** **d) Both a and c**

👉 **Explanation:**
A **closure** is:

* **(a)** A function **inside another function** that has access to the **parent’s variables** even after the parent function has finished executing.
* **(c)** This behavior allows creation of **private variables**, since those inner variables aren’t accessible from outside.

### 🧩 Example:

```js
function outer() {
  let count = 0; // private variable
  return function inner() {
    count++;
    console.log(count);
  };
}

const counter = outer();
counter(); // 1
counter(); // 2
```

Here, `inner()` forms a **closure** over `count`.

</ul>
</details>



**49. Which of the following is true about closures?**
```js
a) Closures have access to their own scope
b) Closures have access to their parent function's scope
c) Closures have access to global scope
d) All of the above
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: d) All of the above

✅ **Correct answer:** **d) All of the above**

👉 **Explanation:**
A **closure** in JavaScript has access to:

1. **Its own scope** (local variables inside the function)
2. **Its parent function’s scope** (variables defined in the outer function)
3. **The global scope** (variables defined globally)

### 🧩 Example:

```js
let globalVar = "Global";

function outer() {
  let outerVar = "Outer";
  return function inner() {
    let innerVar = "Inner";
    console.log(innerVar, outerVar, globalVar);
  };
}

outer()(); // Inner Outer Global
```

✅ The inner function (closure) can access all three scopes.

</ul>
</details>

**50.What will this code output?**
```js
function outer() {
    let count = 0;
    return function inner() {
        count++;
        console.log(count);
    };
}
const counter = outer();
counter();
counter();
```

```js
a) 1 2
b) 0 1
c) 1 1
d) Error
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) 1 2

✅ **Output:**

```
1
2
```

👉 **Explanation:**

* `outer()` runs once and returns the `inner()` function.
* The variable `count` is defined in `outer()` and preserved by the **closure**.
* Each time `counter()` (which is `inner`) is called, it increments and logs `count`.
* Since the same `count` variable is remembered between calls:

  * First call → `count = 1`
  * Second call → `count = 2`

  ----

  # Detailed explanation — why the output is

```
1
2
```

Let's walk through the code step-by-step and show what happens in memory:

```js
function outer() {
  let count = 0;
  return function inner() {
    count++;
    console.log(count);
  };
}
const counter = outer();
counter();
counter();
```

### 1) When `outer()` is called

* A new execution context for `outer` is created.
* Inside that context a variable `count` is created and initialized to `0`.
* The function `inner` is created as a **function object** that has a reference to its *lexical environment* — i.e., it remembers the scope where it was defined (the `outer` scope). That reference is what we call a **closure**.
* `outer()` returns the `inner` function object.

**Memory snapshot after `const counter = outer();`**

* Global scope: `counter → <function inner>`
* Heap / closed-over environment: `{ count: 0 }` — this environment is kept alive because `inner` references it.

Even though the `outer` call has finished, the `{ count: 0 }` environment is not garbage-collected because `counter` (the returned `inner`) still holds a reference to it.

### 2) First call `counter()`

* When `inner` runs, it looks up `count` in its closure (the outer environment).
* `count++` increments `count` from `0` to `1`.
* `console.log(count)` prints `1`.

### 3) Second call `counter()`

* The same `inner` function runs again, using the *same* closed-over environment.
* `count` is currently `1`, so `count++` makes it `2`.
* `console.log(count)` prints `2`.

### Why `count` persists between calls

* The inner function closes over the `count` variable (it captures the *environment*, not a one-time value).
* Because `inner` holds a reference to that environment, `count` lives on the heap and retains its updated value across multiple calls.
* If you call `outer()` again and assign to a different variable, you get a new independent `count`.

### Quick demo to show independent counters

```js
const c1 = outer();
const c2 = outer();
c1(); // 1
c1(); // 2
c2(); // 1   <-- separate `count`
```

### Summary

* The code logs `1` then `2` because the inner function forms a closure over `count`, allowing `count` to persist and be incremented across calls.


</ul>
</details>


**51. Which statement about var and let is true?**
```js
a) Both are function-scoped
b) var is function-scoped, let is block-scoped
c) Both are block-scoped
d) var allows redeclaration, let doesn’t
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) var is function-scoped, let is block-scoped
</ul>
</details>


**52. What will console.log(x); var x = 10; output?**
```js
a) 10
b) undefined
c) ReferenceError
d) NaN
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) undefined

✅ **Output:**

```
undefined
```

👉 **Explanation:**

* Variables declared with `var` are **hoisted** to the top of their scope.
* During hoisting, only the **declaration** is moved, not the **initialization**.

So JavaScript treats your code like this internally:

```js
var x;          // declaration hoisted
console.log(x); // x exists but is undefined
x = 10;         // initialization happens here
```

Hence, the output is **`undefined`** (not an error).

</ul>
</details>


**53. Which statement is used for error handling in JavaScript?**
```js
a) try...catch
b) throw
c) finally
d) All of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: d) All of the above

✅ **Correct answer:** **d) All of the above**

👉 **Explanation:**
In JavaScript, **error handling** is done using all three:

1. **`try...catch`** – to handle runtime errors
2. **`throw`** – to manually throw an error
3. **`finally`** – to execute code after `try`/`catch`, no matter what happens

### 🧩 Example:

```js
try {
  throw new Error("Something went wrong!");
} catch (err) {
  console.log(err.message); // "Something went wrong!"
} finally {
  console.log("Always runs");
}
```

</ul>
</details>


**54. What happens if an error occurs inside the try block?**
```js
a) The script stops execution
b) The error is caught in the catch block
c) The script crashes
d) The error is ignored
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) The error is caught in the catch block

✅ **Correct answer:** **b) The error is caught in the catch block**

👉 **Explanation:**
When an error occurs inside the **`try`** block:

* JavaScript **immediately jumps** to the **`catch`** block (if present).
* The **`catch`** block handles the error without stopping the entire script.

### 🧩 Example:

```js
try {
  throw new Error("Something went wrong!");
} catch (err) {
  console.log("Caught error:", err.message);
}
```

🖨️ Output:

```
Caught error: Something went wrong!
```

</ul>
</details>


**55. What will console.log(x); inside a try block with no catch or finally do?**
```js
a) Print undefined
b) Print null
c) Throw a ReferenceError
d) Nothing
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) Throw a ReferenceError

If you run this code:

```js
try {
  console.log(x);
}
```

✅ **Output:**

```
ReferenceError: x is not defined
```

👉 **Explanation:**

* The `try` block executes, and `console.log(x)` throws a **ReferenceError** because `x` is not defined.
* Since there’s **no `catch`** or **`finally`** block to handle the error,
  the error **is not caught** and will **stop script execution**.

💡 In short — the error **escapes the try block** and behaves as if there were no `try` at all.

</ul>
</details>


**56. Which method is used to generate a custom error?**
```js
a) throw new Error()
b) console.error()
c) generateError()
d) raiseError()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) throw new Error()

✅ **Correct answer:** **a) `throw new Error()`**

👉 **Explanation:**
You can generate (or “throw”) a custom error in JavaScript using the `throw` statement with the `Error` constructor.

### 🧩 Example:

```js
throw new Error("This is a custom error!");
```

🧠 **Details:**

* `throw` is the keyword that raises the error.
* `new Error()` creates a new **Error object** with a custom message.
* The error can then be **caught** using a `try...catch` block.

</ul>
</details>


**57. What will finally do in a try-catch-finally block?**
```js
a) Execute only if no error occurs
b) Execute only if an error occurs
c) Always execute
d) None of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) Always execute

✅ **Correct answer:** **c) Always execute**

👉 **Explanation:**
The **`finally`** block in JavaScript **always runs**,
no matter whether:

* an error occurs or not,
* the error is caught or uncaught,
* there’s a `return`, `break`, or `throw` inside the `try` or `catch`.

### 🧩 Example:

```js
try {
  throw new Error("Oops!");
} catch (err) {
  console.log("Error caught!");
} finally {
  console.log("Finally always runs!");
}
```

🖨️ **Output:**

```
Error caught!
Finally always runs!
```

</ul>
</details>


**58. OOP (Object-Oriented Programming) in JavaScript
Which keyword is used to create a class in JavaScript?**
```js
a) class
b) function
c) Class
d) new Class

```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) class

✅ **Correct answer:** **a) `class`**

👉 **Explanation:**
In JavaScript, the **`class`** keyword (introduced in ES6) is used to create classes — a blueprint for creating objects.

### 🧩 Example:

```js
class Person {
  constructor(name) {
    this.name = name;
  }
  
  greet() {
    console.log(`Hello, ${this.name}!`);
  }
}

const p1 = new Person("Alice");
p1.greet(); // Hello, Alice!
```

🧠 The `class` syntax is just **syntactic sugar** over JavaScript’s existing **prototype-based inheritance** system.

</ul>
</details>

**59. What is the purpose of the constructor method in a class?**
```js
a) To create private variables
b) To initialize object properties
c) To call another class
d) None of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) To initialize object properties

✅ **Correct answer:** **b) To initialize object properties**

👉 **Explanation:**
The **`constructor`** method in a JavaScript class is a **special function** that runs **automatically** when a new object is created from that class using `new`.

### 🧩 Example:

```js
class Person {
  constructor(name, age) {
    this.name = name; // initialize properties
    this.age = age;
  }
}

const p1 = new Person("Alice", 25);
console.log(p1.name); // Alice
```

🧠 The constructor is mainly used to **set up initial values** (object properties) for each instance of the class.

</ul>
</details>



**60. Which keyword is used for inheritance in JavaScript?**
```js
a) implements
b) extends
c) inherits
d) prototype
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) extends

✅ **Correct answer:** **b) `extends`**

👉 **Explanation:**
The **`extends`** keyword in JavaScript is used for **class inheritance**, allowing one class to inherit properties and methods from another.

### 🧩 Example:

```js
class Animal {
  speak() {
    console.log("Animal speaks");
  }
}

class Dog extends Animal {
  bark() {
    console.log("Dog barks");
  }
}

const dog = new Dog();
dog.speak(); // Animal speaks
dog.bark();  // Dog barks
```

🧠 The `extends` keyword enables **reusability** and **hierarchical relationships** between classes.

</ul>
</details>



**61. Which method in a class is used to call the parent class constructor?**
```js
a) parent()
b) super()
c) this()
d) constructor()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) super()

✅ **Correct answer:** **b) `super()`**

👉 **Explanation:**
In JavaScript, the **`super()`** method is used inside a subclass’s constructor to **call the parent class’s constructor**.

### 🧩 Example:

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // calls parent (Animal) constructor
    this.breed = breed;
  }
}

const dog = new Dog("Buddy", "Labrador");
console.log(dog.name);  // Buddy
console.log(dog.breed); // Labrador
```

🧠 **Note:**
You must call `super()` **before using `this`** in a subclass constructor.

</ul>
</details>


**62 Which statement about JavaScript classes is true?**
```js
a) They support multiple inheritance
b) They are syntactic sugar over prototypes
c) They can be redeclared
d) They do not support inheritance
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) They are syntactic sugar over prototypes

✅ **Correct answer:** **b) They are syntactic sugar over prototypes**

👉 **Explanation:**
JavaScript **classes** (introduced in ES6) are not a new object model — they are just **syntactic sugar** over the existing **prototype-based inheritance** system.

### 🧩 Example:

```js
class Person {
  greet() {
    console.log("Hello!");
  }
}

const p = new Person();
p.greet(); // Hello!
```

Under the hood, this is equivalent to:

```js
function Person() {}
Person.prototype.greet = function() {
  console.log("Hello!");
};
```

🧠 So classes make code **cleaner and easier to read**, but they still use **prototypes internally**.

---

Excellent question 👏 — let’s break it down clearly and simply:

---

### 🧠 **Meaning of “Syntactic Sugar”**

**Syntactic sugar** means a **nicer, easier-to-read syntax** that doesn’t add new functionality — it just makes existing behavior simpler or cleaner to write.

So when we say:

> JavaScript classes are *syntactic sugar* over prototypes,

we mean that **classes don’t create a new inheritance model** — they just provide a **cleaner syntax** for the **prototype-based system** JavaScript already had.

---

### 🧩 Example Without Class (Using Prototypes)

Before ES6, you would write something like this:

```js
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(`Hello, ${this.name}!`);
};

const p1 = new Person("Alice");
p1.greet(); // Hello, Alice!
```

---

### 🧩 Example With Class (Using Syntactic Sugar)

Now, using ES6 `class` syntax:

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hello, ${this.name}!`);
  }
}

const p1 = new Person("Alice");
p1.greet(); // Hello, Alice!
```

---

### ⚙️ Internally — Both Do the Same Thing!

Both versions:

* Create a **constructor function** (`Person`).
* Attach methods (`greet`) to **Person.prototype**.
* Use the **prototype chain** for inheritance.

The `class` syntax just hides the messy prototype setup and makes it easier for developers to read and maintain.

---

### ✅ **In short**

> “Syntactic sugar over prototypes” means **classes are just a cleaner way to use the existing prototype-based inheritance system** in JavaScript — no new behavior, just simpler syntax.


</ul>
</details>

**Web APIs & Asynchronous JavaScript**

**63 Which API is used for making HTTP requests in JavaScript?**
```
a) XMLHttpRequest
b) Fetch API
c) Axios
d) All of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: d) All of the above

✅ **Correct answer:** **d) All of the above**

👉 **Explanation:**
All three can be used to make **HTTP requests** in JavaScript — but they differ in usage and modernity:

1. **`XMLHttpRequest`** — the **old, traditional** way (used before ES6).
2. **`Fetch API`** — the **modern built-in** way (promise-based, cleaner syntax).
3. **`Axios`** — a **third-party library** built on top of `XMLHttpRequest`, providing an easier and more powerful interface.

### 🧩 Example with Fetch API:

```js
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

🧠 Today, the **Fetch API** is the most common choice for modern JavaScript applications.

</ul>
</details>


**64. Which method sends a GET request using Fetch API?** 
```js
a) fetch(url)
b) fetch(url, { method: 'GET' })
c) Both a and b
d) None of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) Both a and b
</ul>
</details>


**65. What does navigator.geolocation.getCurrentPosition() do?**
```js
a) Gets user’s IP address
b) Gets user’s location
c) Opens a Google Maps page
d) None of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) Gets user’s location

✅ **Correct answer:** **b) Gets user’s location**

👉 **Explanation:**
`navigator.geolocation.getCurrentPosition()` is a **Web API** that retrieves the **user’s current geographic location** (latitude and longitude) — **with their permission**.

### 🧩 Example:

```js
navigator.geolocation.getCurrentPosition(
  position => {
    console.log(position.coords.latitude, position.coords.longitude);
  },
  error => {
    console.error(error);
  }
);
```

🧠 **Note:**

* It requires the user to **allow location access**.
* Works only in **secure contexts** (`https` or localhost).

</ul>
</details>


**66. Which storage API stores data persistently?**
```js
a) localStorage
b) sessionStorage
c) cookies
d) All of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) localStorage

✅ **Correct answer:** **d) All of the above**

👉 **Explanation:**
All three can store data **persistently**, but with different scopes and lifetimes:

| Storage Type       | Persistence                                             | Scope                        | Storage Limit |
| ------------------ | ------------------------------------------------------- | ---------------------------- | ------------- |
| **localStorage**   | ✅ **Persistent** — remains even after browser is closed | Per origin (domain)          | ~5–10 MB      |
| **sessionStorage** | ⚠️ **Temporary** — cleared when the tab is closed       | Per tab/session              | ~5 MB         |
| **cookies**        | ✅ **Persistent (if expiry set)**                        | Sent with every HTTP request | ~4 KB         |

### 🧠 Summary:

* `localStorage` → Long-term storage
* `sessionStorage` → Per-tab short-term storage
* `cookies` → Can persist (if not session cookies) and are also sent to the server

</ul>
</details>


**67. How can you set an interval in JavaScript?**
```js
a) setTimeout()
b) setInterval()
c) setRepeat()
d) Interval()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) setInterval()

✅ **Correct answer:** **b) `setInterval()`**

👉 **Explanation:**
`setInterval()` is used to **repeatedly execute** a function at a fixed time interval (in milliseconds).

### 🧩 Example:

```js
setInterval(() => {
  console.log("Hello every 2 seconds!");
}, 2000);
```

🧠 **Tip:**
To stop it, use **`clearInterval()`** with the interval’s ID:

```js
const id = setInterval(...);
clearInterval(id);
```

</ul>
</details>



**68 Which method removes an element from an array?**
```js
a) splice()
b) slice()
c) remove()
d) delete()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) splice()

✅ **Correct answer:** **a) `splice()`**

👉 **Explanation:**
The **`splice()`** method is used to **add or remove** elements from an array **in place** (i.e., it changes the original array).

### 🧩 Example:

```js
const arr = [1, 2, 3, 4];
arr.splice(1, 1); // removes 1 element at index 1
console.log(arr); // [1, 3, 4]
```

### ⚙️ Other options:

* `slice()` → ❌ returns a **shallow copy**, does **not** modify the array.
* `remove()` → ❌ not a valid JavaScript array method.
* `delete()` → ⚠️ removes the element but leaves an **empty slot** (undefined index).

</ul>
</details>


**69. Which JavaScript engine is used in Google Chrome?**
```js
a) SpiderMonkey
b) V8
c) Chakra
d) Nitro
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) V8

✅ **Correct answer:** **b) V8**

👉 **Explanation:**
The **V8 JavaScript engine**, developed by **Google**, is used in:

* **Google Chrome** 🟢
* **Node.js** 🟢

### 🧠 Additional info:

* **SpiderMonkey** → used in **Mozilla Firefox**
* **Chakra** → used in **Microsoft Edge (legacy)**
* **Nitro** → used in **Apple Safari**

</ul>
</details>

**70. Which method converts a string into a number?**
```js
a) parseInt()
b) Number()
c) + (unary plus)
d) All of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: d) All of the above

✅ **Correct answer:** **d) All of the above**

👉 **Explanation:**
All three can convert a **string** into a **number** in JavaScript:

### 🧩 Examples:

```js
parseInt("42");     // 42       → converts to integer
Number("42");       // 42       → converts to number (int or float)
+"42";              // 42       → unary plus operator converts to number
```

### 🧠 Notes:

* `parseInt()` stops at non-numeric characters → `parseInt("10px")` → `10`
* `Number()` and `+` will return `NaN` if the entire string isn’t numeric.

</ul>
</details>


**71. Which function generates a random number between 0 and 1?**
```js
a) Math.random()
b) random()
c) generateRandom()
d) Math.rand()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) Math.random()

✅ **Correct answer:** **a) `Math.random()`**

👉 **Explanation:**
`Math.random()` returns a **floating-point number** between **0 (inclusive)** and **1 (exclusive)**.

### 🧩 Example:

```js
console.log(Math.random()); // e.g. 0.348192734
```

🧠 **Tip:**
You can scale it to a range, for example 1–10:

```js
const num = Math.random() * 10;  // 0–9.999...
console.log(Math.floor(num) + 1); // 1–10
```

</ul>
</details>



**72. Which of the following is a falsy value in JavaScript?**
```js
a) "false"
b) "0"
c) undefined
d) "undefined"
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) undefined

✅ **Correct answer:** **c) `undefined`**

👉 **Explanation:**
In JavaScript, **falsy values** are values that evaluate to `false` in a Boolean context.

### 🧩 List of falsy values:

1. `false`
2. `0`
3. `""` (empty string)
4. `null`
5. `undefined` ✅
6. `NaN`

### ⚠️ Note:

* `"false"` → truthy (non-empty string)
* `"0"` → truthy (non-empty string)
* `"undefined"` → truthy (non-empty string)

</ul>
</details>


**73. What will console.log([] == false); return?**
```js
a) true
b) false
c) undefined
d) Error
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) true

✅ **Correct answer:** **a) true**

👉 **Explanation:**
When using the **loose equality (`==`)**, JavaScript performs **type coercion** before comparison.

Let’s break it down 👇

```js
[] == false
```

1. The empty array `[]` is converted to a **primitive** — `""` (empty string).
2. Then `""` (empty string) is converted to a **number** → `0`.
3. `false` is also converted to a **number** → `0`.
4. Now comparison is `0 == 0`, which is **true** ✅

🧠 **Note:**
If you use **strict equality (`===`)**, it returns `false` because types differ:

```js
[] === false  // false
```

</ul>
</details>



**74. Which of the following is NOT a primitive data type in JavaScript?**
```js
a) Number
b) String
c) Object
d) Symbol
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) Object

✅ **Correct answer:** **c) Object**

👉 **Explanation:**
**Primitive data types** in JavaScript are:

1. `Number`
2. `String`
3. `Boolean`
4. `Undefined`
5. `Null`
6. `BigInt`
7. `Symbol`

🧠 **`Object`** is **not primitive** — it’s a **reference type** that can hold multiple values and properties.

</ul>
</details>

**75. How do you deep clone an object in JavaScript?**
```js
a) Object.assign({}, obj)
b) JSON.parse(JSON.stringify(obj))
c) obj.clone()
d) obj.copy()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) JSON.parse(JSON.stringify(obj))

✅ **Correct answer:** **b) `JSON.parse(JSON.stringify(obj))`**

👉 **Explanation:**
`JSON.parse(JSON.stringify(obj))` creates a **deep clone** of an object — it copies **all nested properties** by converting the object to a JSON string and then parsing it back into a new object.

### 🧩 Example:

```js
const obj = { name: "Alice", details: { age: 25 } };
const clone = JSON.parse(JSON.stringify(obj));

clone.details.age = 30;

console.log(obj.details.age);   // 25  (original unchanged)
console.log(clone.details.age); // 30
```

### ⚠️ Note:

* This method **does not clone functions**, `undefined`, or special objects like `Date`, `Map`, or `Set`.
* For complex objects, use libraries like **Lodash’s `_.cloneDeep()`**.

</ul>
</details>


**76. What is the output of console.log(2 + "2" - 1);?**
```js
a) "21"
b) 21
c) "22"
d) 1
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) 21

✅ **Correct answer:** **b) `21`**

👉 **Step-by-step Explanation:**

```js
console.log(2 + "2" - 1);
```

1. `2 + "2"` → JavaScript performs **string concatenation**, not addition → `"22"`
2. `"22" - 1` → The `-` operator forces **numeric conversion** → `22 - 1 = 21`

✅ Final output: **`21`**

</ul>
</details>



**77. Which method is used to filter elements from an array?**
```js
a) map()
b) filter()
c) reduce()
d) slice()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) filter()

✅ **Correct answer:** **b) `filter()`**

👉 **Explanation:**
The **`filter()`** method creates a **new array** containing all elements that **pass a test (condition)** provided by a callback function.

### 🧩 Example:

```js
const numbers = [1, 2, 3, 4, 5];
const even = numbers.filter(num => num % 2 === 0);
console.log(even); // [2, 4]
```

🧠 **Note:**

* `map()` → transforms elements
* `reduce()` → reduces to a single value
* `slice()` → copies part of an array

</ul>
</details>



**78 Which function combines array elements into a single value?**
```js
a) reduce()
b) map()
c) join()
d) concat()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) reduce()

✅ **Correct answer:** **a) `reduce()`**

👉 **Explanation:**
The **`reduce()`** method executes a reducer function on each element of the array, resulting in a **single accumulated value**.

### 🧩 Example:

```js
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((acc, curr) => acc + curr, 0);
console.log(sum); // 10
```

🧠 **Note:**

* `map()` → transforms each element
* `join()` → combines elements into a **string**
* `concat()` → merges **arrays**, not elements

</ul>
</details>



**79. What does the following code return?**
```js
console.log([1, 2, 3].map(num => num * 2));
```
```js
a) [2, 4, 6]
b) [1, 4, 9]
c) [1, 2, 3]
d) [2, 3, 4]
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) [2, 4, 6]

✅ **Correct answer:** **a) [2, 4, 6]**

👉 **Explanation:**
The **`map()`** method creates a **new array** by applying a function to **each element** of the original array.

### 🧩 Example:

```js
[1, 2, 3].map(num => num * 2);
// Each element is doubled → [2, 4, 6]
```

🧠 The original array `[1, 2, 3]` remains **unchanged**.

</ul>
</details>


**80. Which of the following is NOT an immutable operation?**
```js
a) map()
b) filter()
c) splice()
d) concat()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) splice()

✅ **Correct answer:** **c) `splice()`**

👉 **Explanation:**

* **`splice()`** is a **mutable** operation — it **changes (modifies)** the original array by adding or removing elements.

### 🧩 Example:

```js
const arr = [1, 2, 3, 4];
arr.splice(1, 2); // removes 2 elements starting at index 1
console.log(arr); // [1, 4]  ← original array changed
```

### 🧠 Immutable methods (do **not** modify original array):

* `map()`
* `filter()`
* `concat()`

</ul>
</details>


**81. What is the event loop in JavaScript?**
```js
a) A process that handles function calls
b) A mechanism that allows async operations
c) A feature that prevents infinite loops
d) A method to execute code
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) A mechanism that allows async operations

✅ **Correct answer:** **b) A mechanism that allows async operations**

👉 **Explanation:**
The **event loop** in JavaScript is a **mechanism** that allows asynchronous (non-blocking) code — like `setTimeout`, Promises, or I/O operations — to run **without stopping** the main thread.

### 🧩 How it works (simplified):

1. JavaScript runs **synchronously** in a single thread.
2. Asynchronous tasks (like timers, fetch calls) are sent to the **Web APIs**.
3. When completed, their callbacks are pushed to the **callback queue**.
4. The **event loop** constantly checks:

   * If the **call stack** is empty → it moves the next callback from the **queue** to the stack and executes it.

### 🧠 In short:

> The **event loop** manages the execution of **synchronous and asynchronous code**, ensuring JavaScript remains **non-blocking and responsive**.

</ul>
</details>


**82. Which of the following executes first in the event loop?**
```js
a) setTimeout()
b) setInterval()
c) Promise.resolve().then()
d) console.log()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: d) console.log()

✅ **Correct answer:** **d) `console.log()`**

👉 **Explanation:**
The **event loop** executes **synchronous code first**, before handling asynchronous tasks.

Here’s the **order of execution** in JavaScript’s event loop:

1. **Synchronous code** → runs immediately (e.g. `console.log()`)
2. **Microtasks** → Promises (`.then()`, `catch`, `finally`)
3. **Macrotasks** → `setTimeout()`, `setInterval()`, I/O callbacks

### 🧩 Example:

```js
console.log("A");

setTimeout(() => console.log("B"), 0);
Promise.resolve().then(() => console.log("C"));

console.log("D");
```

**Output:**

```
A
D
C
B
```

🧠 So `console.log()` runs **first** because it’s **synchronous**.

</ul>
</details>



**83. Which queue does setTimeout() use in JavaScript?**
```js
a) Microtask queue
b) Callback queue
c) Event loop queue
d) Execution stack
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) Callback queue

✅ **Correct answer:** **b) Callback queue**

👉 **Explanation:**
`setTimeout()` schedules its callback to run **after the specified delay**, and the callback is placed into the **callback queue** (also known as the **macrotask queue**).

### 🧩 Event loop order:

1. **Synchronous code** runs first.
2. Then, **microtasks** (e.g., `Promise.then()`).
3. Finally, **macrotasks** from the **callback queue** (e.g., `setTimeout`, `setInterval`, I/O).

### 🧠 Example:

```js
setTimeout(() => console.log("Timeout"), 0);
Promise.resolve().then(() => console.log("Promise"));
console.log("Start");
```

**Output:**

```
Start
Promise
Timeout
```

✅ `setTimeout()` → **callback queue (macrotask)**
✅ `Promise.then()` → **microtask queue**

</ul>
</details>


**84. What will be the output of this code?**
```js
console.log("A");
setTimeout(() => console.log("B"), 0);
console.log("C");
```
```js
a) A B C
b) A C B
c) B A C
d) C A B
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) A C B

✅ **Correct answer:** **b) A C B**

👉 **Explanation:**
Let’s break it down step-by-step 👇

```js
console.log("A");
setTimeout(() => console.log("B"), 0);
console.log("C");
```

### 🧩 Execution flow:

1. `console.log("A")` → runs immediately → prints **A**
2. `setTimeout(..., 0)` → schedules callback for later (goes to **callback queue**)
3. `console.log("C")` → runs immediately → prints **C**
4. After the main thread finishes, the **event loop** picks up the callback (`console.log("B")`) from the **callback queue** → prints **B**

### ✅ Final Output:

```
A
C
B
```

</ul>
</details>

**85. Which of the following is a best practice in JavaScript?**
```js
a) Using == instead of ===
b) Avoiding global variables
c) Using var instead of let
d) Nesting loops as deep as possible
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) Avoiding global variables

✅ **Correct answer:** **b) Avoiding global variables**

👉 **Explanation:**
Avoiding **global variables** is a key **best practice** in JavaScript because:

* They can be **accessed and modified anywhere**, leading to **naming conflicts** and **hard-to-track bugs**.
* They **pollute the global scope**, making code less modular and harder to maintain.

### 🧠 Other options:

* **a)** ❌ Use `===` (strict equality) instead of `==` to avoid type coercion errors.
* **c)** ❌ Prefer `let` and `const` over `var` for block scoping.
* **d)** ❌ Deeply nested loops make code harder to read and less efficient.

✅ **Best practice summary:**

> Use `let` / `const`, `===`, modular functions, and avoid global variables.

</ul>
</details>


**86. What does "debouncing" do in JavaScript?**
```js
a) Delays function execution until a pause in events
b) Executes a function immediately
c) Runs a function continuously
d) None of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) Delays function execution until a pause in events

✅ **Correct answer:** **a) Delays function execution until a pause in events**

👉 **Explanation:**
**Debouncing** is a technique used to **limit how often a function runs**, especially during events that fire repeatedly — like `scroll`, `resize`, or `keyup`.

It ensures the function executes **only after a specified delay** **once the event stops firing**.

### 🧩 Example:

```js
function debounce(func, delay) {
  let timer;
  return function(...args) {
    clearTimeout(timer);
    timer = setTimeout(() => func.apply(this, args), delay);
  };
}

const log = () => console.log("Input stopped!");
const debouncedLog = debounce(log, 500);

window.addEventListener("keyup", debouncedLog);
```

👉 In this example:
If you keep typing, the function keeps getting delayed.
It runs **only once** you stop typing for **500ms**.

🧠 **In short:** Debouncing helps **improve performance** and **reduce unnecessary function calls**.

</ul>
</details>


**87. What does "throttling" do?**
```js
a) Executes a function only at fixed intervals
b) Prevents a function from running
c) Removes unnecessary function calls
d) Stops event propagation
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) Executes a function only at fixed intervals

✅ **Correct answer:** **a) Executes a function only at fixed intervals**

👉 **Explanation:**
**Throttling** ensures that a function is **executed at most once** every specified time interval — even if an event (like `scroll`, `resize`, or `mousemove`) fires **continuously**.

It’s useful for **rate-limiting** performance-heavy functions.

---

### 🧩 Example:

```js
function throttle(func, limit) {
  let inThrottle;
  return function(...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}

const log = () => console.log("Scrolled!");
const throttledLog = throttle(log, 1000);

window.addEventListener("scroll", throttledLog);
```

---

🧠 **Difference from Debouncing:**

| Technique    | When function runs                              |
| ------------ | ----------------------------------------------- |
| **Debounce** | After the event stops firing for a delay        |
| **Throttle** | At regular, fixed intervals during event firing |

So throttling = “limit how often” ✅

</ul>
</details>


**88. Which of the following improves JavaScript performance?**
```js
a) Minifying JavaScript files
b) Using lazy loading
c) Avoiding unnecessary DOM manipulations
d) All of the above
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: d) All of the above

✅ **Correct answer:** **d) All of the above**

👉 **Explanation:**
All these techniques help **optimize and speed up** JavaScript performance 👇

### 🧩 1. **Minifying JavaScript files**

* Removes spaces, comments, and unnecessary characters.
* Reduces **file size**, improving **load time**.

### 🧩 2. **Using lazy loading**

* Loads resources (like images, components, or scripts) **only when needed**.
* Reduces **initial load time** and improves **page responsiveness**.

### 🧩 3. **Avoiding unnecessary DOM manipulations**

* Frequent DOM updates are expensive; minimize reflows and repaints.
* Use techniques like **document fragments**, **virtual DOM**, or **batch updates**.

🧠 **In short:**

> Optimize code, defer non-critical work, and minimize DOM operations for best JavaScript performance.

</ul>
</details>


**89. What is the best way to check if a variable is null or undefined?**
```js
a) if (x == null)
b) if (typeof x === "null")
c) if (x === null || x === undefined)
d) if (x == undefined)
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) if (x === null || x === undefined)

The best answer is **a) `if (x == null)`**

Here's why:

## The `==` null check (Option a)

```js
if (x == null)
```

This is the most concise and idiomatic way because **`== null` checks for both `null` AND `undefined`** due to JavaScript's type coercion rules. It's specifically designed for this purpose.

```js
null == undefined  // true
null == null       // true
undefined == undefined  // true
```

## Why the other options are less ideal:

**b) `if (typeof x === "null")`** - This is **incorrect**. The `typeof` operator never returns the string `"null"`. It returns `"object"` for null (a famous JavaScript quirk) and `"undefined"` for undefined.

**c) `if (x === null || x === undefined)`** - This works perfectly but is more verbose than option a. Use this if you want to be explicit or if your linting rules require strict equality.

**d) `if (x == undefined)`** - This works the same as option a (it catches both null and undefined), but checking against `null` is more common by convention.

## Best Practice

Use `if (x == null)` when you want to check for both null and undefined. This is one of the rare cases where using `==` instead of `===` is actually recommended. If you only want to check for one specific value, use strict equality (`===`).
</ul>
</details>


**90. What does document.createElement('div') do?**
```js
a) Creates and appends a div
b) Creates a div but does not append it
c) Selects an existing div
d) Deletes all div elements
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) Creates a div but does not append it

✅ **Correct answer:** **b) Creates a div but does not append it**

👉 **Explanation:**
`document.createElement('div')` creates a **new `<div>` element** in memory, but it’s **not added to the DOM** yet.

You must append it manually to make it visible on the page.

### 🧩 Example:

```js
const div = document.createElement('div'); // creates the element
div.textContent = "Hello!";
document.body.appendChild(div); // appends it to the document
```

🧠 **Summary:**

* Creates a new element ✅
* Doesn’t appear on the page until appended ❌

</ul>
</details>


**91. Which API is used to create animations in JavaScript?**
```js
a) WebGL
b) requestAnimationFrame()
c) animateCSS()
d) window.setInterval()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) requestAnimationFrame()

✅ **Correct answer:** **b) `requestAnimationFrame()`**

👉 **Explanation:**
The **`requestAnimationFrame()`** API is used to create **smooth, efficient animations** in JavaScript by syncing them with the browser’s **refresh rate (usually 60fps)**.

### 🧩 Example:

```js
function moveBox() {
  const box = document.getElementById("box");
  let pos = 0;

  function animate() {
    pos++;
    box.style.left = pos + "px";
    if (pos < 100) requestAnimationFrame(animate);
  }

  requestAnimationFrame(animate);
}

moveBox();
```

🧠 **Why use it:**

* More efficient than `setInterval()`
* Automatically pauses when the tab is inactive (saving resources)
* Provides smoother animations that align with the display’s refresh rate

</ul>
</details>



**92. Which function removes whitespace from both ends of a string?**
```js
a) trim()
b) slice()
c) removeSpace()
d) strip()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) trim()

✅ **Correct answer:** **a) `trim()`**

👉 **Explanation:**
The **`trim()`** method removes **whitespace** (spaces, tabs, newlines) from **both ends** of a string.

### 🧩 Example:

```js
const str = "   Hello World!   ";
console.log(str.trim()); // "Hello World!"
```

🧠 **Note:**

* `trimStart()` → removes from the **start only**
* `trimEnd()` → removes from the **end only**

</ul>
</details>


**93. Which method removes the last element from an array?**
```js
a) pop()
b) shift()
c) splice()
d) removeLast()
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) pop()

✅ **Correct answer:** **a) `pop()`**

👉 **Explanation:**
The **`pop()`** method removes the **last element** from an array and **returns it**. It also **modifies** the original array.

### 🧩 Example:

```js
const fruits = ["apple", "banana", "mango"];
const last = fruits.pop();

console.log(last);    // "mango"
console.log(fruits);  // ["apple", "banana"]
```

🧠 **Note:**

* `shift()` → removes the **first** element
* `splice()` → can remove elements from **any position**
* `removeLast()` → ❌ not a valid JavaScript method

</ul>
</details>

**94. What is the output of the following code?**
```js
console.log(myFunc);
function myFunc() {
    return "Hello";
}
```
```
A) undefined
B) ReferenceError: myFunc is not defined
C) [Function: myFunc]
D) TypeError: myFunc is not a function

```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: c) ƒ myFunc() { return "Hello"; }

✅ **Correct answer:** **C) [Function: myFunc]**

👉 **Explanation:**
In JavaScript, **function declarations are hoisted** to the top of their scope **along with their definitions**.

So this code:

```js
console.log(myFunc);
function myFunc() {
  return "Hello";
}
```

is interpreted by the JavaScript engine like this:

```js
function myFunc() {
  return "Hello";
}
console.log(myFunc);
```

Hence, when the `console.log()` runs, `myFunc` is already defined — it logs the **function definition** itself (something like `[Function: myFunc]` or `ƒ myFunc() { return "Hello"; }`, depending on the environment).

✅ **Output:**

```
[Function: myFunc]
```

*(or equivalent function representation in browser console)*

</ul>
</details>

**95. Which of the following is an example of a higher-order function?**
```js
a) A function that returns another function
b) A function with a return type of void
c) A function that has a loop inside
d) A function that only contains if-else statements
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) A function that returns another function

✅ **Correct answer:** **a) A function that returns another function**

👉 **Explanation:**
A **higher-order function (HOF)** is a function that does **either or both** of the following:

1. **Takes another function as an argument**, or
2. **Returns another function** as its result.

### 🧩 Example:

```js
function greet(message) {
  return function(name) {
    return `${message}, ${name}!`;
  };
}

const sayHello = greet("Hello");
console.log(sayHello("Alice")); // "Hello, Alice!"
```

Here, `greet()` is a **higher-order function** because it **returns another function**.

🧠 **Common higher-order functions in JavaScript:**

* `map()`, `filter()`, `reduce()`, `forEach()`, `setTimeout()`, etc.

</ul>
</details>

**96. Which method is used to handle asynchronous functions in JavaScript?**
```js
a) setTimeout()
b) Promise.then()
c) async/await
d) All of the above
```

<details>
	<summary><b>View Answer</b></summary><ul>
Answer: d) All of the above

✅ **Correct answer:** **d) All of the above**

👉 **Explanation:**
All three can be used to **handle asynchronous operations** in JavaScript, but in different ways 👇

### 🧩 1. `setTimeout()`

Schedules a function to run **after a delay**, making it asynchronous.

```js
setTimeout(() => console.log("After 2s"), 2000);
```

### 🧩 2. `Promise.then()`

Handles the result of a **Promise** once it’s resolved or rejected.

```js
fetch("https://api.example.com")
  .then(res => res.json())
  .then(data => console.log(data));
```

### 🧩 3. `async/await`

Provides a **cleaner syntax** for working with Promises.

```js
async function getData() {
  const res = await fetch("https://api.example.com");
  const data = await res.json();
  console.log(data);
}
getData();
```

🧠 **In short:**

> All three methods help manage asynchronous code — but `Promises` and `async/await` are the **modern, preferred** approaches.

</ul>
</details>

 **97. Which of the following is NOT true about closures?**
 ```js
 a) A closure allows a function to retain access to variables from its outer scope.
b) Closures are created every time a function is invoked.
c) Closures help in data encapsulation.
d) Closures cannot access global variables.
 ```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: d) Closures cannot access global variables.

✅ **Correct answer:** **d) Closures cannot access global variables.**

👉 **Explanation:**
This statement is **NOT true** because **closures *can* access global variables** — just like any other function in JavaScript.

### 🧠 What’s true about closures:

* **(a)** ✅ A closure allows a function to **retain access to variables from its outer scope**, even after that outer function has finished executing.
* **(b)** ✅ Closures are created **every time a function is defined**, not necessarily every time it’s *invoked*.
* **(c)** ✅ Closures are useful for **data encapsulation** and creating **private variables**.

### 🧩 Example:

```js
let globalVar = "Global";

function outer() {
  let localVar = "Local";
  return function inner() {
    console.log(globalVar, localVar); // ✅ Can access both
  };
}

const fn = outer();
fn(); // Output: Global Local
```

✅ Hence, **closures can access global variables**, making **option (d)** the incorrect statement.


</ul>
</details>

**98. What will be the output of the following code?**
```js
const obj = {
    value: 42,
    getValue: () => {
        return this.value;
    }
};
console.log(obj.getValue());
```
```js
a) 42
b) undefined
c) ReferenceError
d) null
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) undefined

✅ **Correct answer:** **b) `undefined`**

👉 **Explanation:**
In this code:

```js
const obj = {
  value: 42,
  getValue: () => {
    return this.value;
  }
};
console.log(obj.getValue());
```

The method **`getValue`** is defined using an **arrow function** (`=>`), and **arrow functions do not have their own `this`**.
Instead, they **inherit `this` from their surrounding (lexical) scope** — which, in this case, is the **global scope**, *not* the `obj`.

---

### 🧩 Step-by-step:

* `this` inside the arrow function **does not refer to `obj`**.
* In the **global scope** (or module scope in strict mode), `this` is **`undefined`** in Node.js or **`window`** in browsers.
* Therefore, `this.value` → `undefined`.

---

### ✅ Output:

```
undefined
```

🧠 **Fix:** Use a regular function to bind `this` to the object:

```js
const obj = {
  value: 42,
  getValue() {
    return this.value;
  }
};
console.log(obj.getValue()); // 42
```

</ul>
</details>

**99 What will be the output of the following asynchronous function?**
```js
async function foo() {
    return "Hello";
}
console.log(foo());
```
```js
a) "Hello"
b) Promise { "Hello" }
c) undefined
d) Error
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: b) Promise { "Hello" }

✅ **Correct answer:** **b) `Promise { "Hello" }`**

👉 **Explanation:**
In JavaScript, any function declared with the **`async`** keyword **automatically returns a Promise**.

So this code:

```js
async function foo() {
  return "Hello";
}
console.log(foo());
```

### 🧩 Step-by-step:

1. The function `foo()` is called.
2. Since it’s an **async function**, it **wraps the return value ("Hello") inside a resolved Promise**.
3. `console.log(foo())` logs that Promise — **not the value inside it**.

---

### ✅ Output:

```
Promise { 'Hello' }
```

🧠 **To get the actual value**, use `await` or `.then()`:

```js
foo().then(result => console.log(result)); // "Hello"
```

or

```js
(async () => console.log(await foo()))(); // "Hello"
```

</ul>
</details>

**100. What is currying in JavaScript?**
```js
a) A technique where a function is transformed into a sequence of unary (one-argument) functions.
b) A method to execute functions asynchronously.
c) A way to cache function results for optimization.
d) A technique to convert a function into a class.
```
<details>
	<summary><b>View Answer</b></summary><ul>
Answer: a) A technique where a function is transformed into a sequence of unary functions.	

✅ **Correct answer:** **a) A technique where a function is transformed into a sequence of unary (one-argument) functions.**

👉 **Explanation:**
**Currying** is a **functional programming technique** in JavaScript where a function that takes multiple arguments is **broken down into a series of functions**, each taking **one argument at a time**.

---

### 🧩 Example:

```js
function add(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    };
  };
}

console.log(add(2)(3)(4)); // 9
```

Here:

* `add(2)` → returns a function waiting for `b`
* `add(2)(3)` → returns another function waiting for `c`
* `add(2)(3)(4)` → finally returns `9`

---

🧠 **Why use currying?**

* Makes functions **more reusable** and **modular**.
* Enables **function composition** and **partial application**.

✅ **In short:**

> Currying transforms `f(a, b, c)` into `f(a)(b)(c)`.

</ul>
</details>
