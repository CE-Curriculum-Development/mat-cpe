# CPE 1040 - Spring 2020

## JavaScript Classes (Level 2 - Intermediate) (IN PROGRESS)

Author: Ivo Georgiev, PhD  
Last update: 2020-02-24  
Code: 6cee6577335b94d0ac3ffdf9b32e5d0c349d1b72    

In Week 6 we will introduce the following topics:
- [Transistor](https://docs.google.com/document/d/1KpK2u7tlg9IpjeqpNTxizabOwoFxsuq-k4WMEPzzcE4/) – The transistor is essentially a circuit-level switch
- [Classes](https://github.com/CE-Curriculum-Development/mat-cpe-1040/edit/master/CPE-Week06-Classes.md) - The programming language facility for user-defined data types and the heart of object-oriented programming

_**A note on the language:** Traditional mainstream JavaScript and TypeScript differ in their support of the so called classical or object-oriented class model. JavaScript has [**prorotype-based inheritance**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain). Support for explicit `class`-es has only been added in the latest ECMA standard and is still only syntactic sugar, while JS remains strictly prototype-based. TypeScript supports the [**object-oriented model**](https://www.typescriptlang.org/docs/handbook/classes.html), familiar to Java and C++ programmers, though it too ultimately compiles down to canonic JavaScript. The prototype approach is considered more powerful and indeed TS builds their `class`-es on top of it. Once again, as this is a micro:bit and MakeCode focused document, the rest of the document describes the TypeScript "classical" object-oriented inheritance style.

## Classes 

Classes are *templates* for complex data objects. They can be thought of as cookie cutters, where the cut cookies are the objects. A class is defined with special syntax by the programmer. It contains local data and methods. Thus, classes are *user-defined complex data types*. Therefore, we will use "class" and "type" interchangeably. There is quite a lot to be said about classes and objects, so we'll take it slow. 

The MakeCode JavaScript Reference has a separate page on [Classes](https://makecode.microbit.org/javascript/classes), which is quite good. The DevDocs JavaScript Reference has a short page on [Classes](https://devdocs.io/javascript/statements/class). The official TypeScript documentation has an extensive section on [Classes](https://www.typescriptlang.org/docs/handbook/classes.html).

## Demo 

These language features are best demonstrated in working code in a familiar environment. We have created an example on top of the Bouncing Sprite from Assignment 2.  

The code can be found on this Github [gist](https://gist.github.com/ivogeorg/be8b11ca24f118fd63c0407e93c81f81), and can be copy-pasted into the MakeCode JavaScript editor. Read the inline comments for clarification. Note that the simulator may not show the behavior correctly. Program your micro:bit and look at it in the dark. Press the buttons to see what they do. 

The demo video is on [Imgur](https://imgur.com/gallery/qysnAQG). 

## Walkthrough

Here we will show in detail how using classes and objects allowed us to create a sprite with a halo that can be turned on and off. For the uses of arrays and `for` loops in the demo, refer to the earlier document on [arrays and `for` loops](CPE-Week03-JavaScript-Arrays-Loops-Classes.md).

### 1. Inheritance: Extending a class

First of all, the `game.LedSprite` was already a class with most of the funcitonality that we needed. In fact, we only wanted to modify the sprite a little. A class declaration looks like this:

```TypeScript
class Sprite {

}
```
We just have the `class` keyword, the _capitalized_ class name, and the _block statement_. The latter should be familiar from the earlier document on [statements](CPE-Week04-JavaScript-Statements.md). Inside the block statement, the data and the methods of the type are defined. 

Because we don't want to redefine the whole class, we instead _extend_ the an already existing class. The declaration looks like this:

```TypeScript
class BouncySprite extends game.LedSprite {

}
```

Here, the _base_ (that is, the already existing) class which we are extending is `game.LedSprite`, while the _derived_ (that is, the extending) class is `BouncySprite`. Inside the block statement, we only define the additional features or feature modifications, while we _inherit_ all the rest of the functionality from the base class.

### 2. Defining the halo



