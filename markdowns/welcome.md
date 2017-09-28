# Part1 - Introduction to this weird Language called Javascript!

![](https://cdn-images-1.medium.com/max/800/1*1DWxwYJJcq-Id4D3HbJkIw.png)

This article is Part 1 for the Series **“Modern ES6+ Javascript for those who know only a little about that old Javascript.”**

_Please note that this article assumes that you have little knowledge about JavaScript. Just a little… string, numbers, booleans… knowledge of variables will be good!_

JavaScript is (by far) the most popular language on the web and open-source ecosystem. Created by Brendan Eich, though JavaScript’s popularity and significance can be regarded due to its interconnection with the browsers and JavaScript Engines, Google’s V8 (Chrome) and Mozilla’s SpiderMonkey(Firefox) engines are just so extremely optimized monsters.

> The gift of Eich, relegated for such a long time,  
> Will descend upon the great iron,  
> When the magical abilities of its scrolls  
> Become apparent to the Elixir Worshippers and the Gemstone Alchemists.

But hey in Modern Javascript, it’s not only about browser. Although web browsers are still the most widely used platforms for JavaScript, but modern databases such as MongoDB use JavaScript as their scripting and query language. But the main thing which has made everyone nuts is that JavaScript is now providing a powerful platforms for apps to develop scalable **server** environments. Yes server, you listened it right! Wait, when I started I heard that HTML CSS JS is client and you use things like PHP for server. No ? Yes but things have changed now as all hail the NODE in this new era.

JavaScript is a very loosely-typed language and has been built around functions, dynamic objects, prototypal inheritance, and a powerful object literal notation. Like all other languages, it was built on very sound design principles but the problem was that unlike other languages, it had to evolve along with the browser. Web browsers support various features and standards and thus it tried to accommodate all the ideas that browsers made and unfortunately ended up making some very bad design decisions. These weird parts has overshadowed the good parts of the language for most people. Even now, this hasn’t changed even after the evolution of the web and JavaScript. Developer’s have written bad code, and other developer’s have had frightening experience trying to fix up that bad code and thus as a result, JavaScript got a very bad reputation. [Douglas Crockford](http://javascript.crockford.com/javascript.html) have termed it as one of the most misunderstood programming languages.

## Functions in Javascript

Functions are a base to JavaScript. If you can understand functions, then you just got the single most important weapon in your arsenal. The most important fact about functions is that in JavaScript, functions are first-class objects. They are treated like any other JavaScript object. Just like other JavaScript data types, they can be assigned to variables, array entries, and properties of other objects, declared with literals, be returned as values from functions, possess dynamically created properties and even passed as function parameters. They are the primary unit of execution and are the pieces where you would wrap all your code and is declared using a function literal. Here is a small example that will demonstrate how a function is declared.

```javascript runnable
function add (harry, larry) {  
 return harry + larry;  
}

const result = add(1993, 1973);  
console.log(result); //prints 3966
```

It all starts with a `function` keyword followed by the function name. Cool part is that the function name is optional and if there is no name given, it is said to be anonymous. Then there is `harry` and `larry`, they are actually parameters of the function which are wrapped in parentheses. These parameter’s are in the set of zero or more and has to be separated by commas. These names are defined as variables within the function, and instead of being initialized to undefined, they are initialized to the arguments supplied when the function is invoked.

And then there is `return harry + larry` wrapped in curly braces. That statement is actually body of the function and are executed when the function is invoked. This method is also known as **function statement**. When you are declaring functions like this, the content of the function get’s compiled and an object with the same name as the functions name is created. An another way of function getting declared is through **function expressions.**

```javascript runnable
var add = function (harry, larry) {  
  return harry + larry;  
};

const result = add(1973, 1993);  
console.log(result);  //prints 3966
```

As discussed, if there is no name given then that is an anonymous function. This anonymous function is getting assigned to an `add` variable and this variable is used to invoke the function same like in the earlier example. The problem with this style is that you can’t have recursive calls. Oh, Big word alert… Recursion! Recursion is a smart coding paradigm where the function calls itself. Back to the problem, Named function expressions can be used to to solve this limitation. For example,

```javascript runnable
var result = function factorial(n) {  
 if (n <= 1) {  
 return 1;  
 }  
 return n * factorial(n - 1);  
};  
console.log(result(4));
```

As you can see that instead of creating an anonymous function, you will create a named function and as the function has a name, now it can call himself recursively. But the cool part I love about is the Self Invoked Functions. Here’s an example…

```javascript runnable
(function greet() {  
  console.log("Hello all from inside.");  
})(); //=> Self invoked!
```

Please note that you can also self invoking functions like this.

```javascript runnable
(function greet() {  
  console.log("Hello all from inside.");  
}()); //=> I am Self invoked too!
```

Did, you saw that difference `(function greet(){…})();` instead of `(function greet(){…}());`. I hope you did, once defined, a function can be called in other JavaScript functions too. As the body of the function is executed, that code which get’s called and execute the function continues to execute. Funny enough, you can also pass a function as a parameter to an another function.

```javascript runnable
//=> Change to uppercase, gets executed with an `execute` function!

function changeToUpperCase(value) {  
 return value.toUpperCase();  
}

//=> `a` parameter is the string that get’s converted to uppercase  
//=> `passToAnother` get's referenced to the `changeCase()` function

function execute(a, passToAnother) {  
 console.log(passToAnother(a));  
}

execute('harry', changeToUpperCase); //=> HARRY
```

As, you can see that here we are passing a function reference as an argument to another function. Isn’t this cool? This function may or may not return a value. In above examples, we used an `add` function that returned a value through the code that is getting called up. Instead of returning a value at the end of the function, calling a `return` allows you to conditionally return from a function in an accurate manner.

```javascript runnable
var omit5FromLoop = function(x){  
 if (x % 5 === 0) return;  
 console.log(x);  
};

for(var i = 1; i < 10; i++){  
 omit5FromLoop(i);  
}
```

This will return a loop like this below. If you see carefully there is no **5\.** When the `if (x % 5 === 0)`condition is requested and returns true, the code simply returns from the function and the rest of the code is not called.

![](https://cdn-images-1.medium.com/max/800/1*p1199PyyvasBulTmQP4zBA.png)

## Passing functions as Data

Let’s start from scratch and create a variable `validateData` which will validate if the person’s age is less than 1 or greater than 99? If yes, the function will return true or else, will return false.

```javascript
var validateData = function(data) {  
 person = data();  
 console.log(person);  
 if (person.age < 1 || person.age > 99) return true;  
 else return false;  
};
```

Then we will create an error handler, so that this process a request if there is an error coming from validation.

```javascript
var errorHandler = function(error) {  
 console.log(“Error while processing age”);  
};
```

Then, we will create a request parser which will take three functions as arguments, these arguments are responsible for attaching the specifics together: the data, validator, and error handler.

```javascript
function parseRequest(data,validateData,errorHandler) {  
 var error = validateData(data);  
 if (!error) console.log(“no errors”);  
 else errorHandler();  
}
```

Now, we will generate a human and a robot which will be responsible for creating an object data through functions. In this example, the name is typed as a static term, whereas age is getting counted from a random number between 1 to 99.

```javascript
var generateHuman = function() {  
  return {  
    name: 'Harry Manchanda',  
    age : Math.floor(Math.random() * (100 - 1)) + 1,  
  };  
};

var generateRobot = function() {  
  return {  
    name: 'Robot Singh Sidhu',  
    age : Math.floor(Math.random() * (100 - 1)) + 1,  
  };  
};
```

Now let’s parse the request and execute the functions

```javascript
parseRequest(generateHuman, validateData, errorHandler);  
parseRequest(generateRobot, validateData, errorHandler);
```

Now let's run all of this code:

```javascript runnable
var validateData = function(data) {  
 person = data();  
 console.log(person);  
 if (person.age < 1 || person.age > 99) return true;  
 else return false;  
};

var errorHandler = function(error) {  
 console.log("Error while processing age");  
};

function parseRequest(data,validateData,errorHandler) {  
 var error = validateData(data);  
 if (!error) console.log("no errors");  
 else errorHandler();  
}

var generateHuman = function() {  
  return {  
    name: 'Harry Manchanda',  
    age : Math.floor(Math.random() * (100 - 1)) + 1,  
  };  
};

var generateRobot = function() {  
  return {  
    name: 'Robot Singh Sidhu',  
    age : Math.floor(Math.random() * (100 - 1)) + 1,  
  };  
};

parseRequest(generateHuman, validateData, errorHandler);  
parseRequest(generateRobot, validateData, errorHandler);
```

Here is the result that I got from the log, please note that age will vary in your result due to random function inside the `age` key of an object function.

```bash
{ name: 'Harry Manchanda', age: 16 }  
no errors  
{ name: 'Robot Singh Sidhu', age: 10 }  
no errors
```

Please note that `parseRequest()` function is fully extendable and in fact can be customised, will be invoked in every request, and because of that there is a single, clean debugging point. I hope by now you would have started to applause the power that JavaScript functions possess like a demon.

## Scoping in JavaScript

If you want to work efficiently with JavaScript, understanding scope is very important. But the problem is that it’s slightly confusing. That said, I will try to resolve your doubts. Though these concepts may seem straight forward thanks to other languages but hey REMINDER, this is JavaScript! There are some subtle changes that must be understood so that you can master the concept. In JavaScript, the scope refers to the current context of code.

A variable’s scope is the context in which the variable exists. The scope help’s you to specify from where you can access a variable and whether you have access to the variable in that context or not? Scopes can be defined globally or locally.

**Global Scope**

Any variable that you declare by default is been defined in global scope. Yes yes, this is one of the most stupid language design based decision taken within JavaScript. A global variable is visible in all other scopes and can be modified by any scope. Unfortunately, a global variable is visible in all other scopes and can be modified by any scope thus making it harder to run the loosely combined sub-programs within the same program. If the sub-programs have one or more global variables that share the same name(s), then they will get involved with each other and likely fail, mostly in an unrecognizable manner and is known as namespace clash.

**Local Scope**

JavaScript doesn’t have block-level scope aka the variables scoped to surrounding curly brackets instead, the language have a function-level scope. The variables declared in a function are simply local variables and is only accessible within that function or by functions inside that function.

```javascript runnable
var myName = 'Harman Singh Manchanda'; // Global Variable  
function twitter () {  
  var myName = 'Harry Manchanda'; // local variable  
  console.log (myName);   
}  
console.log (myName); //prints - Global  
twitter();         //prints – Local
```

## Function-level scope versus block-level scope

The JavaScript variables are scoped at function level. Think of this as a small bubble being created which prevents the variable to be visible from outside this bubble. Function creates such a bubble for variables declared inside the function.

```asciidoc
-GLOBAL SCOPE---------------------------------------------|
var g =0;                                                 |
function foo(a) { -----------------------|                |
    var b = 1;                           |                |
    //code                               |                |
    function bar() { ------|             |                |
        // ...             |ScopeBar     | ScopeFoo       |
    }                ------|             |                |
    // code                              |                |
    var c = 2;                           |                |
}----------------------------------------|                |
foo();   //WORKS                                          |
bar();   //FAILS                                          |
----------------------------------------------------------|

//=> Source: Mastering Javascript 
```

As you can see the language uses the so called “scope chains” to establish the scope for a given function. That mean’s that there is typically one global scope, and each function defined below has its own nested scope. A function that defined in an another function has a local scope which is getting used up by linking up to an outer function. **It’s always the position in the source that defines the scope.** When it tries to resolve a variable, the language starts at the innermost scope and searches outwards.

Within the visual, you can easily see that the `foo()` function has been defined in the global scope. The `foo()` function has its own local scope and get’s accessed to the `g` variable because it's in the global scope. But`a`, `b`, and `c` variables are available in the local scope as they are defined inside the function scope. The `bar()`function is also declared inside the function scope and thus is also available within the `foo()` function. So, as you can see once the function scope is over, the `bar()` function is just not available. You can’t see or call the `bar()` function from outside the `foo()` function—[#aScopeBubble](https://twitter.com/search?f=tweets&q=%23aScopeBubble). As you can see that now, the `bar()` function also has its own function scope (bubble), I ask you what’s available ? The answer is that the `bar()`function have an access to the `foo()` function and all the variables been created in the parent scope of the `foo()` function—`a`, `b`, and `c`. The `bar()` function also has access to the global scoped variable, `g`.

Believe it or not but this is powerful. Please take a moment to think about it. We have just discussed how restricted and out of control global scope have gone in the language. What about if we take an random piece of code and wrap it around within a function? We will be able to hide and create a scope bubble around this piece of code. No? Creating the correct scope using function wrapping will only help us create correct code and prevent those difficult to detect bugs. An another advantage through this is that you are hiding variables and functions within this scope and thus, you can avoid those collisions between two identifiers. The following example shows such a bad case:

```javascript 
function foo() {  
 function bar(a) {  
 i = 2; // changing the ‘i’ in the enclosing scope’s for-loop  
 console.log(a+i);  
 }  
 for (var i=0; i<10; i++) {  
 bar(i); // infinite loop… run at your own risk  
 }  
}  
foo();
```

In this `bar()` function, we are accidentally modifying the value of `i=2` and thus, when we are looking to call `bar()` from within the `for` loop, value of the `i` variable is set to `2` and just never come out of an infinite loop. This won’t be wrong if i call this a bad case of namespace collision.

So far, we thought that using functions as a scope is a great way to achieve modularity and correctness within the language. Well, though this technique works, it’s not really not a great one. The first problem we are facing is that we must create a named function. If we keep on creating such functions just to introduce the function scope, we are polluting the global scope or the parent scope. Additionally, we will have to keep calling such functions. This introduces a lot of boilerplate code, which makes it hard for the code to be read properly as time passes by.

```javascript runnable
var a = 1;  
//=> 1. Add a named function foo() into the global scope

function foo() {   
 var a = 2;  
 console.log( a ); // Print's 2  
}

//=> 2. Now call the named function foo()

foo();  
console.log( a ); // Print's 1
```

We just introduced the function scope by creating a new function `foo()` to the global scope and later on, called this function to execute the code.  
As discussed little above, we can solve both these problems by creating functions that immediately get executed.

```javascript runnable
var a = 1;  
//=> 1. Add a named function foo() into the global scope

(function foo() {   
 var a = 2;  
 console.log( a ); // Print’s 2  
 }) (); //=> 2\. this function `foo()` executes immediately  
console.log( a ); // Print’s 1
```

You would notice that the wrapping function statement is starting with a `function`. This means that instead of treating this function as a standard declaration, this function has been treated as a function expression. The `(function foo(){ ... })` statement as an expression meant that the identifier `foo` is to be found only in the scope of the `foo()` function, and not in the outer scope. By hiding the name `foo` in itself would mean that it does not pollute the enclosing scope unnecessarily. This is so useful and far better. Thus we add `()` after the function expression to invoke it immediately. This pattern is the so called, **Immediately Invoked Function Expression** or **IIFE.** Mostly developer’s remove the function name whenever they use IIFE as the primary use of IIFE is to introduce function-level scope, and thus function naming is not required, really!

## Block scopes

Please note that JavaScript just does not have the concept of block scopes. Developer’s coming from other languages such as Java or C can find this very odd and uncomfortable. **ES6** introduces the **let** and **const** keywords to introduce traditional block scope. This is so incredibly convenient that in modern JavaScript, thanks to tools like babel, you are supporting ES6, and thus you should always use the `let` or `const` keyword. We will discuss `let` and `const` instead of `var`. That being said, this is not the right time to discuss that. It can soon go off the topic, we will discuss it in upcoming parts of this series. That being said, find an example of it below:

```javascript runnable
var foo = true;
if (foo) { 
  let bar = 42; //variable bar is local in this block { } 
  console.log( bar );
}
console.log( bar ); // ReferenceError
```

## Hoisting in Javascript

Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution. In layman’s term that simply means that no matter where your functions and variables are declared, they will be moved to the top of their scope regardless of whether their scope is global or local. It is a very strong feature in the language. It provides high flexibility to the language, if used properly and carefully. Please note that, having a strong understanding of scoping within the language can help you to avoid many common mistakes.

Let’s test you out, without running can you answer what this below code will print out to the console?

```javascript runnable
var video = 'HTML5 is the present!';  
if(true) {  
  var video = 'Long live Flash';  
}  
console.log(video);
```

If you said, ‘Long live Flash’… then good luck you either know hoisting, or you guessed it right. For other fellow’s I would like to tell that this is happening due to the function-level scoping in JavaScript within a variable declaration (using `var` keyword). It is very important to remember that only the declarations themselves are hoisted, while any assignments or other executable logic are left in place. For example,

```javascript runnable
var video;  
console.log(video); //=> undefined

video = 'HTML5 is the present!';  
if(true) {  
 var video = 'Long live Flash';  
}

console.log(video); //=> Long live Flash
```

But hey, as told earlier that variables that are declared (using `var` keyword) are function-level scoped and the block-level scoping with loops and conditionals ( `if,for, while, switch` blocks) just does not determine the limits of the scope.

## ES6, you are awesome!

```javascript runnable
var structure = 'HTML5 is the best!';  
let interactivity = 'ES6 Rules';  
if (true) {  
 var structure = 'Long live Flash'; //=> scope is global  
 let interactivity = 'ES5 Sucks'; //=> scope is (local) block-level  
 console.log(structure); //=> Print's 'Long live Flash' 
 console.log(interactivity); //=> Print's 'ES5 Sucks'  
}  
console.log(structure); //=> Print's 'Long live Flash'  
console.log(interactivity); //=> Print's 'ES6 Rules'
```

Part 2 is all about this. Check back soon!

## Function declarations versus function expressions

Functions can be defined in two ways, as Function declarations or function expressions and they both serve identical purposes but there is a difference between these two types of declarations.

Here is an example of Function expression, which returned a type error.

```javascript runnable
functionOne();  
//=> TypeError: functionOne is not a function

var functionOne = function() {  
 console.log('Hey I am function no. 1');  
};
```

Here is an example of **Function declaration**, which printed out the logic.

```javascript runnable
functionTwo();  
//=> Prints - functionTwo

function functionTwo() {  
  console.log('Hey I am function no. 1');  
}
```

As you can see, a function declaration is processed when the execution enters the context in which it appears and before any step-by-step code is called. The function that it creates has been given a proper name `functionTwo()` and we are putting this name in the scope in which the declaration will appear. As it isprocessed before any step-by-step code in the same context, calling `functionTwo()` before defining it works without any error. But, `functionOne()` is an anonymous function expression, and is being assessed when it reaches the step-by-step execution of the code (also being called the runtime execution) and thus we have to declare it before we can invoke it. In layman terms, the function declaration of `functionTwo()` was hoisted while the function expression of `functionOne()` was executed when line-by-line execution encountered it.

But hey, if there is a thing to remember in this scenario then that is that you should never use function declarations conditionally. This behaviour is non-standardised and thus may behave differently across platforms. The following example shows such a scenario where we are trying to use function declarations conditionally by assigning different function body to function `sayHello()` but please remember that such a conditional code is not guaranteed to work across all browsers and mostly results in an unpredictable results.

```javascript
if (true) {  
 function sayHello() {  
 return ‘Harry is awesome!’;  
 }  
}  
else {  
 function sayHello() {  
 return ‘Harry is stupid!’;  
 }  
}  
```

Never do this, different browsers will behave differently in this case. A function declaration should never be placed in the block. You should be using an function expression as it’s perfectly safe and in-fact a smart choice.

```javascript
if (true) {  
 sayHello = function () {  
 return 'Harry is awesome!';  
 };  
}  
else {  
 sayHello = function () {  
 return 'Harry is stupid!';  
 };  
}  
```

The thing with declarations is that they are only allowed to appear within the program or function body. They cannot appear in a block `{ ... }`. Weird, No? Yes but that’s just how JavaScript goes, the blocks are only allowed contain statements and not function declarations. Thus Function expressions, are very popular due to this weird stuff. The common pattern among JavaScript developer’s is that they fork the function definitions based on some kind of a condition. These forks usually happen in the same scope and thus is almost always necessary to use function expressions.

## Arguments Parameter

An argument parameter is a collection of all the arguments passed to the function. A collection has a property named `length` that would contain the count of arguments, and the individual argument values can be obtained by using an array indexing notation. But hey, arguments parameter is not a JavaScript array and if you would try to use array methods on arguments, GOOD LUCK! Think of arguments as an array-like structure which is helping it to write functions that can take an unspecified number of parameters. See the below example:

```javascript runnable
var sum = function () {   
 var i, total = 0;  
 for (i = 0; i < arguments.length; i += 1)   
 total += arguments[i];  
 return total;  
};  
console.log(sum(1,2,3,4,5,6,7)); // print’s 28  
console.log(sum(1,2,3,4)); // print’s 10
```

Though, the arguments parameter is not really an array but it is possible to convert it to an array like below and once converted, you can manipulate the list as you wish.

```javascript
var args = Array.prototype.slice.call(arguments);
```

### The this parameter

Yes `this`, if you can say that you know the `this` keyword very well then Great, because I ain’t the one who can say that. But still I will try to explain in this context. Whenever a function is invoked, apart from parameters that represent the detailed arguments that were provided on the function call, an implicit (indirect) parameter named `this` is also passed to the function. This refers to an object that’s implicitly associated with the function invocation, commonly termed as a **function context.**

**Invocation as a function:** If a function is not invoked as a method, or as a constructor, or through`apply()` or `call()`, then this is simply been invoked as a function. With this pattern, `this` is bound to the global object. I have heard a lot from many developer’s that this is a bad design choice. Of-course, this is natural to assume that `this` would be bound to the parent context. If would only say that if you are in a same situation, just capture the value of `this` in an another variable.

**Invocation as a method:** A method is basically a function tied to a property on an object. For methods, `this` is bound to the object on invocation as shown in example below. As you can see, `this` is bound to the person object when invoked by`greet` because `greet` is the method of person.

```javascript runnable
var person = {  
  name: 'Harry Manchanda',  
  age: 24,  
  greet: function () {  
    console.log(this.name + ', ' + this.age);  
  }  
};

person.greet();
```

**Invocation as a constructor: Constructor** functions get’s declared just like any other functions. No, there is nothing special about them. But, the way in which they are invoked is very different. To invoke the function as a constructor, we precede the function invocation with the **new** keyword. When this happens, `this` is bound to the new object. We will discuss about prototypal inheritance later but for now, just jot down that these contructor functions are designed to be called with the `new` prefix. For easier distinction, they are named using **PascalCase** as opposed to **camelCase**.

In below example, notice how the `greet` function uses this to access the `name` property. The `this` parameter is bound to `Person`.

```javascript runnable
var Person = function (name) {  
  this.name = name;  
};

Person.prototype.greet = function () {  
  return this.name;  
};

var zuck = new Person('Mark Zuckerberg');  
console.log(zuck.greet());
```

**To be continued…**

## Thanks a lot…

* **_If you liked my article and also my passion for teaching, please don’t forget to follow me and also Codeburst by clicking the links below._**
* **_If you would like to hire me for your next cool project, or just want to say hello… my twitter handle is_ **[**_@harmanmanchanda_**](http://bit.ly/tw-harry)** _for getting in touch with me! My DM’s are open to the public so just hit me up._**
