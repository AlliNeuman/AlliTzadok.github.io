---
layout: post
title:      "jS - Hoisting and Scope"
date:       2018-07-18 21:39:25 +0000
permalink:  js_-_hoisting_and_scope
---


### What is Hoisting?
Hoisting in and of itself is how declarations are moved to the top of our code file.  Even though they are not physically being moved, the function and variable declarations are being added into memory during the compiling process, to be retrieved for initializations and assignment later on.  If the initializations occur before declarations you would get an undefined because initializations are not hoisted.

```
console.log(foo);
var foo;
foo = 3;
```
Since declarations are stored in memory, they can be accessed, but the value would be undefined. In the example above, console.log would return an undefined because var foo was defined after foo was initialized.  If we moved console.log after the declaration then we would get 3 in console.

### var, let and const - what's the deal?
Declarations using var keyword declaration is hoisted. In terms of scope, var's scope is the entire function, whereas let and constant's scope are only the enclosing block of curly braces.  Since ```var``` scope is the entire function, you can access the variable before it is declared, although it will return undefined. On the other hand, ```let``` and ```const``` will through a reference error saying the variable has not been defined.  Both ```let``` and ```const``` cannot be used until they have been declared.

Just like the example above, if we changed the ```var``` to ```let```:
```console.log(foo);
let foo;
foo = 3;
```
This will throw an Uncaught Reference Error "foo is not defined". This is because the declaration does not happen until the actual line where it is declared and initialized.

It is best practice to declare your variables first, and use later. In terms of scope aspect, ```var``` becomes a global variable, which can cause problems with variable assignment.  With es6, ```let``` and ```const``` are better options, but ```const``` is the most preferred and is the most 'safe' because the variable cannot be reassigned.

### How hoisting affects functions
Hoisting only occurs for function declarations, not function expressions.  Here are some examples of what may happen, and the errors or outputs we may get after calling functions.

```
hoistedFunction();

function hoistedFunction() {
console.log("This function is hoisted and would output this sentence, because it's a function declaration and not an expression")
}

hoistedTypeErrorFunction();
var typeErrorFunction = function() {
console.log("This function is not hoisted and will throw a TypeError beecause the function is a function expression. The variable is hoisted, but the function definition is not defined ie. will throw the TypeError.")
}
```

How do these function declarations differ from a named function expression?

 A functions name doesn't get hoisted if it's part of a function expression. If you call a function before it is declared, it will return not defined. If you call a named function expression it will return the TypeError for undefined is not a function.
 
 ex:

```
refErrorFunction();
 
namedFunctionExpression(); 

 var namedFunctionExpression = function refErrorFunction()   {
 console.log("test");
 }
 ```
 In the above code, calling refErrorFunction() will throw a reference error because refErrorFunction is not defined yet.  namedFunctionExpression will also throw an error, but a TypeError because although it returns undefined, undefined is not a function.
 
### Scope of var, let and const

**Var declarations** are processed before any code is executed (hoisting). The scope of var is either the current scope, or for variables declared outside of the function, it would be global scope. If a varaible is not declared, it is always global scope.  Variables declared using var can be redefined within later code.

If a variable has a function scope, it can only be accessed within that function.   You would have to call on the particular function in order to have access to that variable.  If the variable is not being returned though, there is no direct access to it. 

```
function doSomething() {
var x = 5;
}					
console.log(x)
```
The above code will throw a ReferenceError because x is defined within doSomething and not outside the function.

**Let declarations** for varibles limit the scope to the block, function, statement, or expression of code in which the declaration happens.  The scope also includes any sub-blocks for where the variables declared by ```let``` are declared.

**Const declarations** are like let declarations in that they are also block scoped.  The difference between let and const is that const cannot be reassigned or redeclared.

### Arrow function scope - "this"?
In normal es5 functions, ```this``` refers to the particular object that the function is referring to.   ```this``` references the owner of the function that it is actually contained in.  With arrow functions though, ```this``` binds to the window object and not the actual object you are working with.  In these cases, you would need to turn your arrow function into a normal es5 function. 


