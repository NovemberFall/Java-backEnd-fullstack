## JavaScript


- 1.Linking JavaScript file and html file
- 2.JavaScript Fundamentals
  - 2.1 Variables
  - 2.2 Data Types
  - 2.4 Functions
  - 2.5 Hoisting
  - 2.6 Closure

---


### 1.Linking JavaScript file and html file

- 1.1 Adding JavaScript into an HTML Document
  - You can add JavaScript code in an HTML document by employing the dedicated HTML tag 
    <script>that wraps around JavaScript code.
    Method 1: inline mode

![](img/2020-08-22-13-12-34.png)

- 这种模式不推荐

---


- Method 2: using <script>tag
  - 2.1 internal style
  - 2.2 external style (推荐)

![](img/2020-08-22-13-13-41.png)

---


### 2. JavaScript Fundamentals

- 2.1. Variables
  - 1. three ways of variable declaration: `let`, `var` and `const`.
    We use those three keywords to create variables in JavaScript.
    e.g. `let message;` or `var message;` or `const message;`

- Note:
  - 1. `var` variables are defined from the beginning of the function, no matter where 
    the definition is.（`var is function scope`）
  - 2.	`var` is function scope, so it has no `block scope`, but `let` and `const` are block scope.
  - 3. `var` can be declared many times, but `let` and `const` cannot in the same scope.


- 2.2 Data Types
  - JavaScript is “dynamically typed”, meaning that there are data types, but variables are not bound to 
    any of them. In JavaScript there are two types of data: `primitive` and `reference value`.

```js
//no error
let message = "hello";
message = 123456;
```

- Data types: Number, String, Boolean, Object, Function, `Null, Undefined`

```js
var = length = 16; //number
var lastName = 'Johnson';  //string
var lastName = "Johnson";  //string
var p = {firstName: 'John', lastName:'Doe'}; //object
var isGood = true; //booelan
var isPlenty = true; //booelan
var isGoodAndPlenty = true; //booelan
var arr = [1, 2, 3]; //array
var arr1 = [1, 2, 3, 'John', 'richard', 'bob']; //array

//function
function say(){
  return 'I am a function';
}
//function expression
var say = function(){
  return 'I am a function';
}

var u;
typeof u //undefined
```

---

#### Null & Undefined

- **null** is a special value meaning "no value". On the other hand, **undefined** means that the variable 
  has not been declared, or has not been given a value.


- object
  - Objects are used to store keyed collections of various data and more complex entities.


- Function
  - Functions are the main “building blocks” of the program. They allow the code to be called 
    many times without repetition.


- Function Declaration


```js
function showMessage(){
  alert('Hello everyone!');
}
```

- The function keyword goes first, then goes the name of the function, then a list of parameters between 
  the parentheses (empty in the example above) and finally the code of the function, also named 
  “the function body”, between curly braces.

![](img/2020-08-30-20-57-36.png)  


