# CPE 1040 - Spring 2020

## JavaScript Classes (Level 2 - Intermediate)

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

The only way we want to change the base `game.LedSprite` is to add an _optional_ "halo" around it as it moves. The halo is just the surrounding 8 positions around the current position of the sprite, lit with lower brightness than the sprite itself. In terms of data, we need to add only two things to our derived class that don't exist in the base class: 
  1. `hasHalo` variable for whether the sprite has a halo or not, so just a `boolean`; and   
  2. `adjArr` for the description of the halo positions relative to the sprite position, so an array.   

The code for the `boolean` is straightforward:

```TypeScript
class BouncySprite extends game.LedSprite {
    hasHalo : boolean = false
  
}
```
We define the extra variable right inside the block statement (and scope) of the class.   

The array of halo positions is a _two-dimensional_ array, that is, an array of arrays. This doesn't change anything significant about the array, except that it will have a two array index operators `[][]` when we want a value from the inner arrays. Let's see the code:

```TypeScript
class BouncySprite extends game.LedSprite {
    hasHalo : boolean = false

    private adjArr = [
        [0, -1, 0.67],
        [0, 1, 0.67],
        [-1, 0, 0.67],
        [1, 0, 0.67],
        [-1, -1, 0.40],
        [-1, 1, 0.40],
        [1, -1, 0.40],
        [1, 1, 0.40]
    ]  
}
```
Each of the inner arrays contains, in this order, an additive x offset, a additive y offset, and a multiplicative brightness coefficient. They can be applied to any sprite at current position `(x, y)` and brightness `b` to light up one of the adjacent positions from the halo. For the first inner array, this will result in `(x, y - 1, b * 0.67)`. This is how we get the halo!  

### 3. Drawing the halo

The motion of the sprite is essentially plotting and unplotting LED positions along a line. This is done by the function `move` of the sprite base class. So, we need to draw the halo at each call to `move`. First, we need to define a new method in our derived class `BouncySprite` which encapsulates the drawing of the halo. Here's the code:

```TypeScript
class BouncySprite extends game.LedSprite {
    hasHalo : boolean = false

    private adjArr = [
        [0, -1, 0.67],
        [0, 1, 0.67],
        [-1, 0, 0.67],
        [1, 0, 0.67],
        [-1, -1, 0.40],
        [-1, 1, 0.40],
        [1, -1, 0.40],
        [1, 1, 0.40]
    ]  

    private halo() {
        // get the current position and brightness
        let x = this.get(LedSpriteProperty.X)
        let y = this.get(LedSpriteProperty.Y)
        let b = this.get(LedSpriteProperty.Brightness)
        
        // plot halo
        for (let i = 0; i < this.adjArr.length; i++)
            led.plotBrightness(x + this.adjArr[i][0],
                y + this.adjArr[i][1],
                b * this.adjArr[i][2])

        // ugly but otherwise halo is invisible
        basic.pause(5)
        
        // unplot halo
        for (let i = 0; i < this.adjArr.length; i++)
            led.unplot(x + this.adjArr[i][0],
                y + this.adjArr[i][1])
    }
}
```

The `halo` method is quite straightforward:
  1. First, it takes the current position and brightness level of the sprite.
  2. Then, it cycles through the adjacent halo positions and draws them. _Notice how we add the offsets to the coordinates and multiply the brightness with the coefficient._
  3. Finally, after a pause, it again cycles through the halo positions to turn them off. _This ensures that the halo follows the motion of the sprite and we don't have halos left behind along its trajectory._
  
The `halo` method declared `private`, which means that we don't want to allow code ourside the class to make direct calls to it. We only want to call it from inside, specifically in the `move` method.

The base class has a `move` method, so we need to _override_ it to draw the halo. This is what it looks like in the code:

```TypeScript
class BouncySprite extends game.LedSprite {
    hasHalo : boolean = false

    private adjArr = [
        [0, -1, 0.67],
        [0, 1, 0.67],
        [-1, 0, 0.67],
        [1, 0, 0.67],
        [-1, -1, 0.40],
        [-1, 1, 0.40],
        [1, -1, 0.40],
        [1, 1, 0.40]
    ]  

    private halo() {
        // get the current position and brightness
        let x = this.get(LedSpriteProperty.X)
        let y = this.get(LedSpriteProperty.Y)
        let b = this.get(LedSpriteProperty.Brightness)
        
        // plot halo
        for (let i = 0; i < this.adjArr.length; i++)
            led.plotBrightness(x + this.adjArr[i][0],
                y + this.adjArr[i][1],
                b * this.adjArr[i][2])

        // ugly but otherwise halo is invisible
        basic.pause(5)
        
        // unplot halo
        for (let i = 0; i < this.adjArr.length; i++)
            led.unplot(x + this.adjArr[i][0],
                y + this.adjArr[i][1])
    }
    
    move(z: number) {
        super.move(z)
        if (this.hasHalo) this.halo()
    }
}
```

We need to draw the halo after the sprite moves (that is, at the new location) but before the `move` method exits. So, in our `move` method we first call the one from the base class (aka called a _superclass_) with the keyword `super` and only then, if we are supposed to have a halo, call our method `halo`. From _inside_ a class block, we need to use the keyword `this` before every class datum we want to manipulate and every class method we want to call. Therefore, we have `if (this.hasHalo) this.halo()`.

### 4. Instantiating a class

Objects are variables of complex user-defined types. It is also said that they are _instantiations_ of a class. Remember how a class is _template_ for objects. So, objects are the actual products defined by the template. We use the `new` keyword to create a new `Bouncy Sprite` object. What does `new` do? It invokes the _constructor_ of the class to make a new object by calling the eponymous method:

```TypeScript
class BouncySprite extends game.LedSprite {
   // variables
   
   // methods
   
   constructor(x : number = 2, y : number = 2) {
      super(x, y)
   }
}
```

As you can see, `super` can be used on its own to call the base class constructor. In our case, that's all we do. If we wanted to initialize our `BouncySprite` with, say, a particular value for `hasHalo`, we would instead have the following constructor:

```TypeScript
class BouncySprite extends game.LedSprite {
   // variables
   
   // methods
   
   constructor(x : number = 2, y : number = 2, hasHalo : boolean = true) {
      super(x, y)
      this.hasHalo = hasHalo
   }
}
```

Notice the _default_ values that we declare in the constructor. This allows us to call it without any arguments, if we don't want different values, as follows:

```TypeScript
let sprite : BouncySprite = new BouncySprite()
```

This is just a variable declaration with type `BouncySprite` (remember, classes are user-define _types_), and an assignment to it of a newly constructor `BouncySprite` object at location (2, 2) and with a halo. How that we have a hallowed sprite (just kidding :D), we can use it just as the vanilla sprites from the base class:

```TypeScript
basic.forever(function () {
    sprite.move(1)
    sprite.ifOnEdgeBounce()
    basic.pause(50)
})
```

### 5. Turning the halo on and off

The halo of our `BouncySprite` can be turned on and off by assigning `true` or `false` to the sprite objects `hasHalo`, as we do in the event handler for the button B press:

```TypeScript
input.onButtonPressed(Button.B, function () {
    sprite.hasHalo = !sprite.hasHalo
})
```

In this case, we use button B to _toggle_ the halo on and off.

---

That's all, folks! Oink!

