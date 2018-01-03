## What is ES6?
Es6 or ECMASCRIPT 2015 is sixth major release of ECMAScript language which comes with a lot of new features and syntax for writing web applications in javascript. As currently, not all browsers support ES6, they support pre-versions of ES6. so to write web applications in ES6 that will support all Browsers we needed tools like Babel and Webpack.

## List some new features of ES6.
Check out the [examples](http://es6-features.org)
- Support for constants (also known as “immutable variables”)
- Block-Scope support for both variables, constants, functions
- Arrow Functions
- Extended Parameter Handling
- Template Literals
- Extended Literals
- Enhanced Regular Expression
- Enhanced Object Properties
- Destructuring Assignment
- Modules , Classes, Iterators , Generators
- Support for Map/Set & WeakMap/WeakSet
- Promises, Meta-Programming ,Internationalization & Localization

## What is Babel?
Babel is the one of the most popular javascript transpiler and becomes the industry standard. It allows us to write ES6 code and convert it back in pre-Es6 javascript that browser supports.

## What are template literals in Es6?
Template literals are the string with embedded code and variables inside.Template literal allows concatenation and interpolation in much more comprehensive and clear in comparison with prior versions of Ecma script.
```JavaScript
let a="Hello";
let b="John";
let c=`${a} ${b}`;
console.log(c); //outputs Hello John;
```

## What is Spread Operator in ES6?
Spread Operator provides a new way to manipulate array and objects in Es6. A Spread operator is represented by `…` followed by the variable name.

Example:
```JavaScript
let a =[7,8,9];
let b=[1,2,3,...a,10];
console.log(b); // [1,2,3,7,8,9,10]
```

## Explain Destructuring Assignment in ES6?
Destructing assignment in another improvement in Es6. It allows us to extract data from array and objects into separate variables.

Example:
```JavaScript
let full_name =['John','Deo'];

let [first_name,last_name]=full_name;

console.log(first_name,last_name);
// outputs John Deo
```

## How to create a Javascript class in ES6?
```JavaScript
class User{
    constructor(name,age) {
        this.name  = name;
        this.age = age;
    }

    getData() {
        console.log(this.name + " is " + this.age + " years old !");
    }
}

var user = new User("foo", 7);
s1.getData();
```
