# TypeScript

> TypeScript is a free and open source high-level programming language developed and maintained by Microsoft. It is a strict syntactical superset of JavaScript and adds optional static typing to the language. It is designed for the development of large applications and transpiles to JavaScript. As it is a superset of JavaScript, existing JavaScript programs are also valid TypeScript programs.
>
> -- <cite>Wikipedia</cite>

## The workflow

First, if not already installed, we need to install `Node.js`. See [Chapter Development Tools](../01_developmenttools/#node-js).

Next, we install TypeScript globaly:

```bash
npm install -g typescript
```

TypeScript will be used in *npm* projects. Later on we will already be in a npm project, for now we can just start a new *npm* project by opening a new terminal and execute the following command:

```bash
npm init -y
```

Now we can install TypeScript:

```bash
npm install typescript --only=dev
```

Next we need to start our Typescript project:

```bash
tsc --init
```

This will start our TypeScript project by creating a *tsconfig.json* file inside our projectfolder. This is a compiler settings file. Here, you can define the target, which JavaScript libraries will be available on the development, the target ECMAScript version, the module generation, and much more.

Now, let's create our index.ts file with the following content:

```typescript
function sum (a: number, b: number) : number {
    return a + b;
}

const firstNumber: number = 10;
const secondNumber: number = 20;

console.log(sum(firstNumber,secondNumber));
```

Dont worry about the code for now. Let's just compile this to a JavaScript file:

```bash
tsc ./index.ts
```

After compilation, we can see the final file in *index.js*. If we look inside the file, the final code will be similar to this:

```js
function sum (a, b) {
    return a + b;
}

const firstNumber = 10;
const secondNumber = 20;

console.log(sum(firstNumber,secondNumber));
```

You may be wondering: *where are my types?* As ECMAScript is a dynamic language, the types of TypeScript exiist only at the superset level, and won't be passed down to the JavaScript file.

## Understanding TypeScript

TypeScript is a typed-based language. Much of its power comes with the ability to use static code analysis with JavaScript. This is possible thanks to the tools that excist inside the TypeScript environment.

### Types

The main feature we get from using TypeScript is the **types**. 

#### String

All the textual data on JavaScript will be treated as a **string**. To declare a string, we always need to surround it with double " or single ' quotes, or the ` grave accent, commonly known as a template string.

Declaring template strings inside text is not a problem with TypeScript. Template strings are a feature in ECMAScript that made it possible to add a variable inside a string without the need for concatenation:

```typescript
const myText: string = 'My Simple Text';
const myTextAgain: string = "My Simple Text";
const greeting: string = `Welcome back ${myName}!`;
```

#### Number

In JavaScript, all numbers are floating-point values. In TypeScript, it's the same. Those numbers get a **number** type. In addition to the hexadecimal and decimal numbers, the binary and octal literals that were introduced in ECMAScript 2015 are treated like numbers too:

```typescript
const myAge: number = 54;
const hexNumber: number = 0xf010d;
const binaryNumber: number = 0b1011;
const octalNumber: number = 0o744;
```

#### Boolean

The most basic type in the programming languages is the **boolean** values, a simple 1 or 0, and true or false.

```typescript
const isTaskDone: boolean = false;
const isGreaterThen: boolean = 10 > 5;
```

#### Arrays

A group of elements in most of the languages is commonly called an **array**. In TypeScript we can declare it in two different ways.

The most simple way is just to declare the type of the element followed by [ ] to denote that it is an array of the declared type:

```typescript
const primeNumbers: number[] = [1,3,5,7,11];
```

Or, you can declare generically, using the `Array<type>` declaration. This is not the most common way used, but, depending on the code you are developing, you may need to use it:

```typescript
const switchInstructions: Array<boolean> = [true, false, false, true];
```

#### Tuple

**Tuples** are a type of variable that has a specific structure. Structurally, a tuple is an array of two elements; both are a known type by the compiler and the user, but those elements don't need to have the same type.

```typescript
let person: [string, number];
person = ['Ronny', 54];
console.log(`My name is ${person[0]} and I am ${person[1]} years old`);
```

#### Enum

**Enums** are similar to JavaScript objects, but they have some special attributes that help in the development of your application. You can have a friendly name for numeric values or a more controlled environment for the constants on the variables a function can accept.

A numeric enum can be created without any declaration. By doing this, it will start with the initial values of 0 and finish with the value of the final index number; or, you can get the name of the enum, passing the index of the enum value:

```typescript
enum ErrorLevel {
    Info,
    Debug,
    Warning,
    Error,
    Critical,
}

console.log(ErrorLevel.Error);  // 3
console.log(ErrorLevel[3]); // Error
```

Or, an enum can be declared with values. It can be an initial declaration that the TypeScript compiler will interpret the rest of the elements as an increment of the first one, or an individual declaration.

```typescript
enum Color {
    Red = '#FF0000',
    Blue = '#0000FF',
    Green = '#00FF00',    
}

enum Languages {
    JavaScript = 1,
    PHP,
    Python,
    Java = 10,
    Ruby,
    Rust,
    TypeScript,
}

console.log(Color.Red); // '#FF0000'
console.log(Language.TypeScript) // 13
```

#### Any

As JavaScript is a dynamic language, TypeScript needed to implement a type that has no defined value, so it implemented the **any** type. The most used case for the any type any is when using values that came from a third-party library. In that case, we know that we are dropping the type checking:

```typescript
let maybeIs: any = 4;
maybeIs = 'a string?';
maybeIs = true;
```

The main use of the any type is when you are upgrading a legacy JavaScript project to TypeScript, and you can gradually add the types and validations to the variables and functions.

#### Void

As the opposite of any, **void** is the absence of the type at all. The most used case is with functions that won't return any values:

```typescript
function logThis(str: string) : void {
    console.log(str);
}
```

Using void to type a variable is useless because it only can be assigned to undefined and null.

#### Objects

An **object** in TypeScript has a special form of declaring because it can be declared as an interface, as a direct object, or as a type of its own.

Declaring an object as an interface, you have to declare the interface before using it, all the attributes must be passed, and the types need to be set:

```typescript
interface IPerson {
    name: string;
    age: number;
}

const person: IPerson = {
    name: 'Ronny',
    age: 54,
};
```

Using objects as direct inputs is sometimes common when passing to a function:

```typescript
function greetingUser(user: {name: string, lastName: string}) {
    console.log(`Hello, ${user.name} ${user.lastName}`);
}

```

And finally, they are used for declaring a type of object and reusing it:

```typescript
type Person = {
    name: string,
    age: number,
};

const person: Person = {
    name: 'Ronny',
    age: 54,
};

console.log(`My name is ${person.name}, I am ${person.age} years old`);
```

### Functions

In TypeScript, one of the most diffucult types to declare is a **function**. It can get very complex in a just simple concatenation of the functional chain.

Declaring a function in TypeScript is a composition of the parameters that the function will receive and the final type that the function will return.

You can declare a simple function inside a constant, like this:

```typescript
const sumOfValues: (a:number, b:number): number = (a: number, b:number): number => a + b;
```

A more complex function declared inside a constant can be declared like this:

```typescript
const complexFunction: (a:number) => (b:number) => number = (a:number):(b:number) => number => (b:number): number => a + b;
```

When declaring a function as a normal function, the way to type it is almost the same as in a constant way, but you don't need to declare that the functions are a function. Here is an example:

```typescript
function foo(a: number, b:number): number{
    return a + b;
}
```

### Interfaces

TypeScript checks that the values of variables are the correct type and the same principle is applied to classes, objects, or contracts between your code. This is commonly known as "duck typing" or "structural sub-typing". Interfaces exist to fill this space and define these contracts or types.

Let's try to understand an **interface** with this example:

```typescript
function greetingStudent(student: {name: string}) {
    console.log(`Hello ${student.name}`);
}

const newStudent = {name: 'Ronny'};

greetingStudent(newStudent);
```

The function will know that the object has the property name on it and that it's valid to call it.

We can rewrite it with the interface type for better code management:

```typescript
interface IStudent {
    name: string;
    course?: string;
    readonly university: string;
}

function greetingStudent(student: IStudent) {
    console.log(`Hello ${student.name}`);
    if(student.course){
        console.log(`Welcome to the ${student.course} semester`);
    }
}

const newStudent: IStudent = {name: 'Ronny', university: 'VIVES'};

greetingStudent(newStudent);
```

As you can see, we have a new property called *course* that has a *?* declared on it. This symbolizes that this property can be nulled or undefined. It's called an optional property.

There is a property with a read-only attribute declared. If we try to change after it's declared on the variable creation, we will receive a compile error because it makes the property read-only.

## Object Oriented Programming in TypeScript

When writing a class inside a TypeScript file, we first need to have in mind what this class will do, what this class can be for, how it can be extended by another class through inheritance, and how it can be affected in the process.

Imagine that we have a basic *Animal* class. This class can have some basic properties such as its *name*, whether it produces a *sound*, its *family*, and the basic *food chain* this animal eats.

1. Let's start with the basic of the process, the *food chain*. We need to make sure that it's an innumerable list, and that each file that is using it will have the same value and the end. We just need to call a constant variable:
    ```typescript
    export enum FoodChainType{
        Carnivorous = 'carnivorous',
        Herbivorous = 'herbivorous',
        Omnivorous = 'omnivorous',
    }
    ```

2. Now, we want to make the basic *interface* for our animal. We know that our animal has a *name*, can produce a *sound*, can be part of a *family*, and be in a *food chain* category. Using an interface in a class, we make a contract between the class and what will be exposed, helping in the development process:

    ```typescript
    interface IAnimal {
        name: string;
        sound?: string;
        family: string;
        foodChainType: FoodChainType;
    }
    ```

3. With all that settled, we can make our *Animal* class. Each class can have its constructor. The class constructor can be simple, containing just some variables as arguments, or can be more complex and have an object as an argument. If your constructor will have any parameters, an interface or declaring the type of each parameter is needed. In this case, our constructor will be an object and will have only one parameter that is the same as the *Animal*, so it will extend the *IAnimal* interface:

    ```typescript
    interface IAnimalConstructor extends IAnimal {

    }
    ```

4. Now, to make our class, we have declared the interfaces and enums that will be used. We will start by declaring that the class will implement the *IBasicAnimal* interface. To do this, we need to add som public elements that our class will have and declare those too. We will need to implement the functions to show what animal it is and what sound it makes. Now, we have a basic class that includes all the attributes for our animal. It has seperate interfaces for the class and the constructors. The enum for the food chain is declared in a human-readable way, so the JavaScript imports of this library can execute without any problems.

```typescript
interface IBasicAnimal extends IAnimal {
    whoAmI: () => void;
    makeSound: () => void;
}

export class Animal implements IBasicAnimal {
    public name: string;
    public sound: string;
    public family: string;
    public foodChainType: FoodChainType;

    constructor(params: IAnimalConstructor) {
        this.name = params.name;
        this.sound = params.sound || '';
        this.family = this.family;
        this.foodChainType = params.foodChainType;
    }
}

public whoAmI(): void {
    console.log(`I am a ${this.name}, my family is ${this.family}. My diet is ${this.foodChainType}.`);
    if(this.sound){
        console.log([...Array(2).fill(this.sound)].join(', '));
    }
}

public makeSound(); void {
    console.log(this.sound);
}

```

5. Let's extend this class with a few lines of code and transform this *Animal* into a *Dog*:

```typescript
import (Animal, FoodChainType) from './Animal';

class Dog extends Animal {
    constructor() {
        super({
            name: 'Dog',
            sound: 'Wof!',
            family: 'Canidae',
            foodChainType: FoodChainType.Carnivorous,
        });
    }n
}
```

This is a simple way of extending a parent class and using the parent's definition of the child to compose a new class with almost the same interface as the parent.


