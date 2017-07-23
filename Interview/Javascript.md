## Explain event delegation
Event propagation and bubbling :(http://javascript.info/bubbling-and-capturing)
Event delegation allows you to avoid adding event listeners to specific nodes. Instead, the event listener is added to one parent.

```javascript
<ul id="parent-list">
<li id="post-1">Item 1</li>
<li id="post-2">Item 2</li>
<li id="post-3">Item 3</li>
<li id="post-4">Item 4</li>
<li id="post-5">Item 5</li>
<li id="post-6">Item 6</li>
</ul>
```

When we need to add a click listener to each child element.
You could add an event listener to the parent `UL` element. When the event listener is triggered, check the event element to ensure it's type of element to react to.If it is an LI element, we have what we need!  If it's not an element that we want, the event can be ignored.Using the Element.matches API, we can see if the element matches our desired target.
In summary, the steps of event delegation are:
 - Add an event listener on some element enclosing all the elements where you want to simulate event handling (BODY)
 - In the handler, simulate bubbling and look for matching elements (all A tags)
 - When you find a matching element, set event.currentTarget to it and call subsequent handling code

The standard DOM Events describes 3 phases of event propagation:   
  * Capturing phase – the event goes down to the element.   
  * Target phase – the event reached the target element.   
  * Bubbling phase – the event bubbles up from the element.   
 ### Event Bubbling
 When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors.
 below are 3 nested elements FORM > DIV > P with a handler on each of them:

  ``` javascript
   <style>
    body * {
      margin: 10px;
      border: 1px solid blue;
    }
  </style>

  <form onclick="alert('form')">FORM
    <div onclick="alert('div')">DIV
      <p onclick="alert('p')">P</p>
    </div>
  </form>
  ```

So if we click on <p>, then we’ll see 3 alerts: p → div → form.
The process is called “bubbling”, because events “bubble” from the inner element up through parents like a bubble in the water.

## Explain how this works in JavaScript
`This` refers to itself, to its won object or global object.Using `this` are partitioned in 3 locations of code:
- In Functions:  `this` is an extra, often implicit, parameter.
  * Real functions ->  `this` is the global object in sloppy mode, undefined in strict mode
    ``` javascript
    sloppy mode:
    function sloppyFunc() {
            console.log(this === window); // true
    }
    sloppyFunc();
    strict mode:
    function strictFunc() {
            'use strict';
            console.log(this === undefined); // true
      }
      strictFunc();
    ```
  * Constructors -> `this` refers to the newly created instance
    ``` javascript
    var savedThis;
        function Constr() {
            savedThis = this;
        }
        var inst = new Constr();
        console.log(savedThis === inst); // true
      ```
  * Methods -> `this` refers to the receiver of the method call
    ``` javascript
      var obj = {
            method: function () {
                console.log(this === obj); // true
            }
        }
        obj.method();
      ```
-  in Outside functions ( in the top-level scope)  
`This` refers to the global object in browsers and to a module's exports in Node.js
-  in eval()  
eval is a function which evaluates a string as though it were an expression and returns a result
  `This` refers to the receiver of the method call
    * if `eval()` is called indirectly, `this` refers to the global object
    * if `eval()` is called directly, `this` remains the same as in surroundings of `eval()`.

## Explain how prototypal inheritance works
## What do you think of AMD vs CommonJS?
## Explain why the following doesn't work as an IIFE: function foo(){ }();.

## What needs to be changed to properly make it an IIFE?
- #### What is Immediately Invoked Function Expressions(IIFE)
An IIFE is an anonymous function that is created and then immediately invoked. It’s not called from anywhere else, but runs just after being created.   
Example:
```
(function () {
  console.log(5);
} ());
```
- #### Why we need IIFE
The primary reason to use an IIFE is to obtain data privacy. Because JavaScript's var scopes variables to their containing function, any variables declared within the IIFE cannot be accessed by the outside world.
``` javascript
(function () {
    var foo = "bar";
    console.log(foo);// Outputs: "bar"
})();
// ReferenceError: foo is not defined
console.log(foo);
```
- #### Pass arguments into the IIFE:
``` javascript
var foo = "foo";
(function (innerFoo) {
    console.log(innerFoo);// Outputs: "foo"
})(foo);
```

- #### Explain why the following doesn't work as an IIFE:
`function foo(){ }();`
because this function is defined with Normal function definition and not been called. To change it as an IIFE,
``` javascript
(function foo(){
  ...
}()); // returns ... immediately
```

## What's the difference between a variable that is: null, undefined or undeclared?
- `undefined`: A variable is undefined when it hasn't been defined yet. If you call a variable or function without having actually created it yet, the parser will give you an `not defined` error.
  ``` javascript
  var undefinedVariable;
  console.log(typeof(undefinedVariable)); // undefined
  ```
  To assign a value to the variable, use the equal sign:
  ``` javascript
  var numberVariable = 1;
  console.log(numberVariable); // 1
  ```

- `null`: A variable is null when it is defined and have null assigned to them.
  ``` javascript
  var nullVariable = null; // null
  typeof nullVariable // "object"
  ```

  When will following functions evaluate:
  ``` javascript
  if( value ) {
  }
  ```
  Value will evaluate to true if value is not: null /undefined / NaN/ empty string ("")/ 0/ false

- `undeclared`: A variable is undeclared when it does not sue the `var` keyword. undeclared variables do not exist until code assigning them is executed. Therefore, assigning a value to an undeclared variable implicitly creates it as a global variable when the assignment is executed. This means that, all undeclared variables are global variables.   

  ```javascript
  function hoist() {
    a = 20;
    var b = 100;
  }
  hoist();
  console.log(a);
  /*
  Accessible as a global variable outside hoist() function
  Output: 20
  */

  console.log(b);
  /*
  Since it was declared, it is confined to the hoist() function scope.
  We can't print it out outside the confines of the hoist() function.
  Output: ReferenceError: b is not defined
  */
```

## How would you go about checking for any of these states?
## What is a closure, and how/why would you use one?
Closures are functions that refer to independent (free) variables (variables that are used locally, but defined in an enclosing scope). In other words, these functions 'remember' the environment in which they were created.



```javascript
function f1(){
　　　　var n=999;
　　　　function f2(){
　　　　　　alert(n);
　　　　}
　　　　return f2;
　　}
　　var result=f1();
　　result(); // 999
```
## What's a typical use case for anonymous functions?
- #### what's anonymous functions?  
  An anonymous function is a function that was declared without any named identifier to refer to it. As such, an anonymous function is usually not accessible after its initial creation.
  - Normal function definition:
  ``` javaScript
  function hello() {
    alert('Hello world');
  }
  hello();
  ```
  - Anonymous function definition:
  ``` javaScript
  var anon = function() {
    alert('I am anonymous');
  };
  anon();
  ```
- #### What's a typical use case for anonymous functions?  
One common use for anonymous functions is as arguments to other functions. Another common use is as a closure.   
example:
``` javascript
     function takesACallback(callback) {
      return "The callback says: " + callback();
     }

    takesACallback(function() {
        return "I'm the callback!";
      }); // returns "The callback says: I'm the callback!"
 ```
## How do you organize your code? (module pattern, classical inheritance?)
## What's the difference between host objects and native objects?
- #### What's native object
    > Native objects are inherent to JS - they are available to you so long as you're using JS. The native objects are sometimes referred to as “global objects” since they are the objects that JavaScript has made natively available for use.  
    Below find the list of 9 native object constructors that come pre-packaged with JavaScript:  
    ✴ Number() ✴ String() ✴ Boolean() ✴ Object() ✴ Array() ✴ Function() ✴ Date() ✴ RegExp() ✴ Error()

- #### What's host object  
  >Host object includes Everything the environment gives you. Host objects can differ by environment (or host).   
  Example, browser environment supplies objects such as window. While a node.js/server environment supplies objects such as NodeList.

## Difference between: function Person(){}, var person = Person(), and var person = new Person()?
## What's the difference between .call and .apply?
The difference between call and apply. Both can be called on functions, which they run in the context of the first argument. In call the subsequent arguments are passed in to the function as they are, while apply expects the second argument to be an array that it unpacks as arguments for the called function.

While the syntax of this function is almost identical to that of call(), the fundamental difference is that call() accepts an argument list, while apply() accepts a single array of arguments.

```JavaScript

.apply(thisArg, [argsArray])
.call(thisArg, arg1, arg2, ...)


var person1 = {name: 'Marvin', age: 42, size: '2xM'};
var person2 = {name: 'Zaphod', age: 4200, size: '1xS'};

var sayHello = function(){
    alert('Hello, ' + this.name);
};

var sayGoodbye = function(){
    alert('Goodbye, ' + this.name);
};

sayHello.call(person1);
sayHello.apply(person1);

sayGoodbye.call(person2);
sayGoodbye.apply(person2);
```

## Explain Function.prototype.bind.
## When would you use document.write()?
```javascript
<script type="text/javascript">
document.write("<h1>Test comment！</h1>");
</script>
```
>mostly works like alert function

Definition and Usage
The write() method writes HTML expressions or JavaScript code to a document.

The write() method is mostly used for testing: If it is used after an HTML document is fully loaded, it will delete all existing HTML.

Note: When this method is not used for testing, it is often used to write some text to an output stream opened by the document.open() method.

It also can be used in initialize a new window with document.close().

```JavaScript
<script language="JavaScript">
  var newWindow
  function makeNewWindow(){
    newWindow = window.open("","","status,height=200,width=300")
  }

  function subWrite(){
    // make new window if someone has closed it
    if(newWindow.closed){
      makeNewWindow()
    }
    // bring subwindow to front
    newWindow.focus()
    // assemble content for new window
    var newContent = "<html><head><title>A New Doc</title></head>"
    newContent += "<body bgcolor='coral'><h1>This document is brand new.</h1>"
    newContent += "</body></html>"
    // write HTML to new window document
    newWindow.document.write(newContent)
    newWindow.document.close()    // close layout stream
  }
</script>
</head>

<body onLoad="makeNewWindow()">
  <form>
    <input type="button" value="Write to Subwindow" onClick="subWrite()">
  </form>
</body>
```
## What's the difference between feature detection, feature inference, and using the UA string?
## Explain Ajax in as much detail as possible.
## What are the advantages and disadvantages of using Ajax?
AJAX = Asynchronous JavaScript And XML.

AJAX is not a programming language.

The two major features of AJAX allow you to do the following:

Make requests to the server without reloading the page
Receive and work with data from the server

you can:

Update a web page without reloading the page
Request data from a server - after the page has loaded
Receive data from a server - after the page has loaded
Send data to a server - in the background

![alt tag](./images/ajax.gif)  

 What are the advantages and disadvantages of using Ajax?

 * Advantages

 >Better interactivity

 This is pretty much the most striking benefit behind why several developers and webmasters are switching to AJAX for their websites. AJAX allows easier and quicker interaction between user and website as pages are not reloaded for content to be displayed.

 >Easier navigation

 AJAX applications on websites can be built to allow easier navigation to users in comparison to using the traditional back and forward button on a browser.

 >Compact

 With AJAX, several multi purpose applications and features can be handled using a single web page, avoiding the need for clutter with several web pages. For our use of AJAX on goedkope-zomervakantie.com, it took just a few lines of code!

 >Backed by reputed brands

 Another assuring reason to use AJAX on your websites is the fact that several complex web applications are handled using AJAX, Google Maps is the most impressive and obvious example, other powerful, popular scripts such as the vBulletin forum software has also incorporated AJAX into their latest version.

 * Disadvantages

 >The back and refresh button are rendered useless

 With AJAX, as all functions are loaded on a dynamic page without the page being reloaded or more importantly a URL being changed (except for a hash symbol maybe), clicking the back or refresh button would take you to an entirely different web page or to the beginning of what your dynamic web page was processing. This is the main drawback behind AJAX but fortunately with good programming skills this issue can be fixed.  

 twitter solution

 >It is built on javascript

 While javascript is secure and has been heavily used by websites for a long period of time, a percentage of website surfers prefer to turn javascript functionality off on their browser rendering the AJAX application useless, a work around to this con is present as well, where the developer will need to code a parallel non-javascript version of the dynamic web page to cater to these users.

## Explain how JSONP works (and how it's not really Ajax).
## Have you ever used JavaScript templating? If so, what libraries have you used?
JavaScript templating refers to the client side data binding method implemented with the JavaScript language. This approach became popular thanks to JavaScript's increased use, its increase in client processing capabilities, and the trend to outsource computations to the client's web browser. Popular JavaScript templating libraries are `AngularJS`, `Backbone.js`, `Ember.js`, `Handlebars.js`, `Vue.js` and `Mustache.js`. A frequent practice is to use double curly brackets (i.e. {{key}}) to call values of the given key from data files, often JSON objects.

Normally, the js code is like:
```JavaScript
var html='<ul>';
for(var i=0;i<users.length;i++){
  html+='<li><a href=">'+users[i].url+'">'+users[i].name+'</a>';
}
html+='</ul>';

document.getElementById('results').innerHTML=html;
```
It works like this:
```JavaScript
<ul>
    <% for ( var i = 0; i < users.length; i++ ) { %>
         <li><a href="<%=users[i].url%>"><%=users[i].name%></a></li>
    <% } %>
</ul>
```

This is what we want:
```JavaScript
<ul>
  <li><a href="XXX">OOO</a></li>
  <li><a href="XXX">OOO</a></li>
  <li><a href="XXX">OOO</a></li>
</ul>
```

## Explain "hoisting".
The following is the JavaScript lifecycle and indicative of the sequence in which variable declaration and initialization occurs.It is however important to remember that in the background, JavaScript is religiously declaring then initializing our variables.All variable and function declarations are hoisted to the top of their scope.

  ![Image](./images/variablehoisting.png)

``` javascript
console.log(hoist); // Output: undefined
var hoist = 'The variable has been hoisted.';
```
JavaScript engine interprets code as:
``` javascript
var hoist;

console.log(hoist); // Output: undefined
hoist = 'The variable has been hoisted.';
```
Because of this, we can use variables before we declare them. However, we have to be careful because the hoisted variable is initialized with a value of undefined. The best option would be to declare and initialize our variable before use.

- #### Function Hoisting  
  As we mentioned before, all variable and function declarations are hoisted to the top of their scope. Since this is one of the eccentricities of how JavaScript handles variables, it is recommended to always declare variables regardless of whether they are in a function or global scope.
  ``` javascript
  function hoist() {
    console.log(message);
    var message='Hoisting is all the rage!'
  }
  hoist();
  ```
  this found should output `undefined`. The variable declaration, var message whose scope is the function hoist(), is hoisted to the top of the function.

  JavaScript engine interprets code as:
  ``` javascript
  function hoist() {
    var message;
    console.log(message);
    message='Hoisting is all the rage!'
  }
  hoist(); // Ouput: undefined
  ```
  To avoid this pitfall, we would make sure to declare and initialise the variable before we use it:
  ``` javascript
  function hoist() {
    message='Hoisting is all the rage!'
    console.log(message);
  }
  hoist(); // Ouput: Hoisting is all the rage!
  ```

## Describe event bubbling.
## What's the difference between an "attribute" and a "property"?
## Why is extending built-in JavaScript objects not a good idea?
## Difference between document load event and document DOMContentLoaded event?
## What is the difference between == and ===?
## Explain the same-origin policy with regards to JavaScript.
## Make this work:
## duplicate([1,2,3,4,5]); // [1,2,3,4,5,1,2,3,4,5]
## Why is it called a Ternary expression, what does the word "Ternary" indicate?
## What is "use strict";? what are the advantages and disadvantages to using it?
## Create a for loop that iterates up to 100 while outputting "fizz" at multiples of 3, "buzz" at multiples of 5 and "fizzbuzz" at multiples of 3 and 5
## Why is it, in general, a good idea to leave the global scope of a website as-is and never touch it?
## Why would you use something like the load event? Does this event have disadvantages? Do you know any alternatives, and why would you use those?
## Explain what a single page app is and how to make one SEO-friendly.
## What is the extent of your experience with Promises and/or their polyfills?
## What are the pros and cons of using Promises instead of callbacks?
## What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?
## What tools and techniques do you use debugging JavaScript code?
## What language constructions do you use for iterating over object properties and array items?
## Explain the difference between mutable and immutable objects.
## What is an example of an immutable object in JavaScript?
## What are the pros and cons of immutability?
## How can you achieve immutability in your own code?
## Explain the difference between synchronous and asynchronous functions.
## What is event loop?
## What is the difference between call stack and task queue?
## Explain the differences on the usage of foo between function foo() {} and var foo = function() {}
- #### Function Declarations
  ``` javascript
  var result = foo();
  function foo() {}
  ```

  It has the name `foo` directly after the word function and is what is called a function declaration.   
  Function declarations are actually hoisted up to the top of their scope, so you can define a function declaration after it is used in code without getting an error. Function declarations get hoisted to the top before executing, and the declaration actually includes the function.    

  JavaScript engine interprets code as:
  ``` javascript
  //compilation
  var result;
  function foo() {}
  //execution
  result = foo();
  ```

- #### Function Expressions
  ``` javascript
  var result = foo();
  var foo = function() {};
  ```
  this is called a function expression and doesn't require a name after the word function. Because of this, these functions are considered anonymous.Because function expressions are only referenced through a variable, only the variable declaration (var foo) is hoisted at runtime , and not the assignment (= function() {}).

  JavaScript engine interprets code as:
  ``` javascript
  //compilation
  var result;
  var foo;
  //execution
  result = foo(); // --> Error: foo is not a function
  foo = function() {};
  ```
