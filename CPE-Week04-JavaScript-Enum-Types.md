# CPE 1040 - Week 4
## JavaScript Enum Types (Level 1 - Novice)

Author: Ivo Georgiev, PhD  
Last edited: 2020-02-19  
Code: 76627b276fc903aac634e77db641b0d6743570ba    


In Week 4, we are introducing two fundamental topics in computer engineering, as well as more features of JavaScript: 
- [Binary number system](https://docs.google.com/document/d/1e9QTeYUYFm5DyQIz6qbM0OUYKsh8nf36WEvbQq3O8uk/edit#) – the number (aka numeral) system used in computing 
- [Electricity](https://docs.google.com/document/d/1rHwjfT52t8e8BeC3xgw7rdLXgL3fGsUDZzf24rT2oK4/edit#) – the natural phenomenon on which computing has been built 
- [Statements](CPE-Week04-JavaScript-Statements.md) - statements in programming languages are like the sentences in human speech
- [Enumerated types](CPE-Week04-JavaScript-Enum-Types.md) – JavaScript data types that are just collections of names (like the names of variables) 

### JavaScript `enum` types

_**A note on the language:** The [current version of JavaScript](https://www.ecma-international.org/publications/standards/Ecma-262.htm) does **not** have `enum` types. Since this is micro:bit-oriented material, we are talking about the [subset of TypeScript](https://makecode.com/language) which is implemented for the micro:bit. TypeScript supports [`enum`](https://www.typescriptlang.org/docs/handbook/basic-types.html#enum)._

Enumerations (aka enums) are collections of names. Contrary to the distinction between variable name and values, with enum types the name **is** the value. One of the most popular and intuitive example for an enum type is:

```JavaScript
enum Color { Red, Green, Blue, Cyan, Magenta, Yellow, Black }

let carColor : Color = Color.Cyan                               // Gaudy! I bet it's a Cadillac :D
```
The type's name is `Color` and the values are `Red`, `Green`, etc. Note their use in a variable declaration. Note also that the following declaration is illegal:

```JavaScript
let carColor : Color = Cyan                                     // Which "Cyan" are we talking about???
```

#### micro:bit enums

The JavaScript (ahem, TypeScript) of the MakeCode environment makes extensive user of `enum` types. Here are some examples:
```JavaScript
let icon : IconNames = IconNames.Heart
let jest : Gesture = Gesture.Shake
let butt : Button = Button.A
let vcc : DigitalPin = DigitalPin.P0
let sig : AnalogPin = AnalogPin.P1
```

#### Integers underneath

Enum type values resolve to integers. Unless assigned explicitly, they start at 0 and continue to n-1, where n is the number of values in the particular type, and going in order. Run this fun example on your micro:bit to get your feet wet:

```JavaScript
// Full program - can run on its own

// Enumerated type definition (just a bunch of arbitrary names)
// Conventionally, both the type name and the individual "values"
// are capitalized
enum Bench { Flat, DoubleDeck, Park }               // Flat resolves to 0, DoubleDeck to 1, and Park to 2

// Global variables
let sittingPlace: Bench = Bench.DoubleDeck          // Variable of type Bench (resolves to 1)
let playThings: Bench[] = [                         // Array with base type Bench (resolve to 1, 2, 0, in this order)
    Bench.DoubleDeck,
    Bench.Park,
    Bench.Flat]

// Forever loop
basic.forever(function () {
    if (Math.randomBoolean()) {                     // see the explanation of randomBoolean() in the text below
        basic.showNumber(sittingPlace)              // shows 1
    } else {
        basic.showNumber(playThings[sittingPlace])  // shows 2 (why?)
    }
})
```
##### `Math.randomBoolean()`

This function returns `true` or `false` at random. This does not mean strict alternation like `true`, `false`, `true`, `false`, `true`, etc. Instead, you can may see sequences of 2 or more repeated values. This is not hard to spot as you look at what is shown on the LED matrix. The guarantee of `Math.randomBoolean()` is that over a sufficiently long period of time the number of `true` and `false` values returned will be roughly the same.
