# CPE 1040 - Spring 2020

## JavaScript Arrays, Loops, and Classes (Level 1 - Novice) (IN PROGRESS)

Author: Ivo Georgiev, PhD  
Last updated: 2020-02-20  
Code: 65801a904490f552039bb84995234c57c26cd7dd  

In Week 3, we are introducing the following topics:
- Arrays - one of the most useful _data structures_ in programming
- Loops - the programming language facility for repeated execution
- Classes - the programming language facility for user-defined data types and the heart of object-oriented programming

## Arrays 

Arrays are named sequential ordered indexable sets of data elements of the same base type. Let's unpack this mouthful: 

1. *Named* means that an array is a variable. It's definition and initialization has a special syntax. 

2. *Sequential* means that the data elements in the array are contiguous (that is, one after the other) in memory. 

3. *Ordered* means that an array's data elements come in the order in which they were defined and that order doesn't change. 

4. *Indexable* means that each data element's position in the array order is its *index*, from 0 (the first index) to ARRAY_LENGTH – 1 (the last index), and there is a special syntax to access a specific array data element. 

 

The MakeCode JavaScript Reference has a tiny blurb about arrays under the [Types](https://makecode.microbit.org/javascript/types) section. The DevDocs JavaScript Reference has a much more extensive entry on [Arrays](https://devdocs.io/javascript/global_objects/array). Note that the examples can be copy-and-pasted into the MakeCode editor to play with. *Don't forget the "forever" loop is needed to see things happen many times! :D* 

## *Code Example*
This program will randomly light up the LED array in an interesting way


```TypeScript
//Hurray for Arrays!
//Arrays are a simple yet powerful way to deal with
//a single variable that is used to store different elements
//for example

let brightness: number[] = [0, 5, 15, 40, 120, 200]
//"brightness" is our array
//the array called "brightness" has 6 elements 0,5,15...etc
//in this case our elements are numbers because we defined it with the ":number"
//but arrays can hold any data type including strings and other arrays

let flash: number = 0 //this variable is going to help us choose an element from our array
let xPos: number = 0 //xPos is going to be used to pass our X coordinate to the plotBrightness function
let yPos: number = 0 //yPos is going to be used to pass our Y coordinate to the plotBrightness function

basic.forever(function () {
    xPos = Math.randomRange(0, 4) //assigned a random number from 0-4 to xPos
    yPos = Math.randomRange(0, 4) //assigned a random number from 0-4 to yPos
    flash = Math.randomRange(0, 5) //assigned a random number from 0-5 to flash

    led.plotBrightness(xPos, yPos, brightness[flash])
    //each time we run through the loop
    //we send a random x,y coordinate and pick at random one of the six brightness values in our array
    //example. bright[1] returns the value 5 because 5 is stored in element 1
    //example. bright[flash] could return any value from our array 
    //example. since flash is randomly changing values from 0-5


})


```


## for loops 

The for loop is a handy language statement for repeated execution which gives the programmer control over the number of times to execute a block of statements. It has specific syntax and various capabilities for stopping, skipping, and indexing.  

 

The MakeCode JavaScript Reference has the for loop included in the [Statements](https://makecode.microbit.org/javascript/statements) section. It just refers to the DevDocs Reference page on the [for](https://makecode.microbit.org/javascript/statements)[ loop](https://makecode.microbit.org/javascript/statements). Note that some examples can be executed in-place in the browser page. *You might need to scroll down in the example box to see the Run and Reset buttons.* 

 

## Classes 

Classes are *templates* for complex data objects. They can be thought of as cookie cutters, where the cut cookies are the objects. A class is defined with special syntax by the programmer. It contains local data and methods. Thus, classes are *user-defined complex data types*. There is quite a lot to be said about classes and objects, so we'll take it slow. 

 

The MakeCode JavaScript Reference has a separate page on [Classes](https://makecode.microbit.org/javascript/classes), which is quite good. The DevDocs JavaScript Reference has a short page on [Classes](https://devdocs.io/javascript/statements/class). 

 

## Demo 

These language features are best demonstrated in working code in a familiar environment. We have created an example on top of the Bouncing Sprite from Assignment 2.  

 

The code can be found on this Github [gist](https://gist.github.com/ivogeorg/be8b11ca24f118fd63c0407e93c81f81), and can be copy-pasted into the MakeCode JavaScript editor. Read the inline comments for clarification. Note that the simulator does not show the behavior correctly. Program your micro:bit and look at it in the dark. Press the buttons to see what they do. 

 

The demo video is on [Imgur](https://imgur.com/gallery/qysnAQG). 

 

We'll discuss the code in class this week.  

 

The example and demo are meant to show you some powerful JavaScript functionality that might help with screensavers for Assignment 3. 

