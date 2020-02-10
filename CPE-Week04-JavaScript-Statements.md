# CPE 1040 - Week 4
## JavaScript (Level 1 - Novice) (IN PROGRESS)

Author: Ivo Georgiev, PhD  
Last edited: 2020-02-10  
Code: 61aa792860768aa6d3a18481e2d0b9a5bc4b3082  


In Week 4, we are introducing two fundamental topics in computer engineering, as well as more features of JavaScript: 
- Binary – the number (aka numeral) system used in computing 
- Electricity – the natural phenomenon on which computing has been built 
- Statements - statements in programming languages are like the sentences in human speech
- Enumerated types – data types that are collection of names (like the names of variables) 

### JavaScript statements

One can think of JavaScript statements as the sentences of human language, but programming languages are much more strict and unambigious than human speech. While the latter has almost infinite variation and many nuances of expression, statements in JavaScript, a representative programming language, have each strict syntax and specific purpose. There are two major reasons why it is beneficial for a programmer to think of a program as a collection of statements:
1. Once the programmer learns the syntax of all statement types in a language, it becomes much easier for them to navigate even a large program and quickly spot the code they need to modify, add to, or fix.
2. It becomes much easier to write syntactically correct code and spot errors, leaving more time for functionality design and implementation details.

The concise micro:bit JavaScript reference contains a section on [Statements](https://makecode.microbit.org/javascript/statements).

_**A note on the language:** The language in which one programs for the micro:bit in the [MakeCode](https://makecode.microbit.org/) environment, is [TypeScript](https://www.typescriptlang.org/docs/home.html). TypeScript is a superset of JavaScript, which means that it has all features of JavaScript, and also has additional features. Most notably, TypeScript allows for static typing, which roughly means that you can declare the exact [type](https://makecode.microbit.org/javascript/types) of all the variables in your program and expect the language environment to warn you when you are assigning the wrong value type to a typed variable, or even error out. In JavaScript, the type of the variable is transparent. Further, the micro:bit TypeScript is only a subset of the full TypeScript, with many advanced features not implemented. All this means that the programmer should have a language reference handy to make sure that a feature in the chosen language is [supported](#references). In this document, we'll keep to the JavaScript language for the micro:bit in MakeCode._

Of the statements in the reference, we have already encountered the variable and constant declarations with `let` and `const`, the block statement `{}` which encapsulates multiple lines of code, the conditional `if...else`, and the non-infinite loop `for (;;)` statement. In addition, we have seen the infinite loop, whose canonical form is `while (true)`, in the form of the `forever` function.

#### Declarations

In JavaScript, you can delcare _variables_, _constants_, _functions_, and _classes_ with appropriate statements. Here is a brief explanation and an example declaration of each:
1. Variables. Variables are named data in computer memory. The values of the data can change throughout the program via _assignments_.
```JavaScript
let speed : number = 40          // a variable declaration with an assignment of an initial value
let isAwake : boolean = true
let greeting : string = "Hallo"
```
2. Constants. Constants are named data in computer memory, which can only be assigned once.
```JavaScript
const PI : number = 3.14159265359
const MSU_NAME : string = "Metropolitan State University of Denver" // constant names are usually all-caps
```
3. Functions. Functions are named encapsulation of statements. Functions can be called multiple times throught the program. Functions can take in data in the form of arguments, and can also return data. In JavaScript, functions are _first-class_ objects, which roughly means that one can do with them what one does with variables, e.g., pass them in as arguments to other fuctions, return them from functions, make arrays of them, etc.
```JavaScript
function greet(name : string) {                                        // named function with 
    return greeting + ", " + name + "!"
}
input.onButtonPressed(Button.A, function () { isAwake = ! isAwake; })  // anonymous function passed in as argument to an event handler
input.onButtonPressed(Button.A, () => { isAwake = ! isAwake; })        // popular alternative syntax for anonymous functions
```
4. Classes. Classes are encapsulations of data and functions. They are the primary method for creating user-defined data types. The functions that are part of a class, aka _methods_, are the only ones that can be applied to objects of the given class (aka type). This limitation is an important part of the user-defined type definition. For example, if I have a class `Wumpus` and wumpuses cannot fly, it would be illegal to call `wumpus.fly()` :D.
```JavaScript
class RainDrop {
    x : number                                                // the data of the RainDrop class and objects
    y : number
    speed : number
    constructor(x : number, y : number, speed : number) {     // every class has a constructor to initialize objects when "new" is called
        this.x = x
        this.y = y
        this.speed = speed
    }
    
    fall() {                                                  // a method
        this.move(this.speed)                                 // can call another method
    }
    
    move(d : number) {
        this.y += number                                      // "this" selects the data of the particular object
    }
}
        
let drop : RainDrop = new RainDrop(2, 0, 2)                   // "drop" is an object of type RainDrop, at position (2, 0) and speed 2

drop.fall()                                                   // calling a method on an object
```

### References

1. [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript).
2. [TypeScript](https://www.typescriptlang.org/docs/home.html).
3. [MakeCode](https://makecode.com/language) [TypeScript](https://makecode.microbit.org/javascript).

