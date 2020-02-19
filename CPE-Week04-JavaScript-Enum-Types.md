# CPE 1040 - Week 4
## JavaScript Enum Types (Level 1 - Novice) (IN PROGRESS)

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

Enumerations (aka enums) are collections of names. Contrary to the distinction between variable name and values, with enum types the name is the value.

#### Integers underneath

Enum type values resolve to integers. Unless assigned explicitly, they start at 0 and continue to n-1, where n is the number of values in the particular type, going in order.


```JavaScript
// Enumerated type definition (just a bunch of arbitrary names)
// Conventionally, both the type name and the individual "values"
// are capitalized
enum Bench { Flat, DoubleDeck, Park }

// Global variables
let sittingPlace: Bench = Bench.DoubleDeck  // Variable of type Bench
let playThings: Bench[] = [                 // Array with base type Bench
    Bench.DoubleDeck,
    Bench.Park,
    Bench.Flat]
let foos = [                                // Array of functions
    heart,
    diamond,
    duck]

// Function definitions
function heart() {
    basic.showIcon(IconNames.Heart)
}

function diamond() {
    basic.showIcon(IconNames.Diamond)
}

function duck() {
    basic.showIcon(IconNames.Duck)
}

// Forever loop
basic.forever(function () {
    // the following three calls are equivalent (that is, call the same function)
    heart()                                     // Call a function (note the parentheses)
    foos[0]()                                   // Call the function from array (again,
    // note the parentheses)
    foos[playThings.indexOf(sittingPlace)]()    // Call the function from array 
    // at the same index as the value 
    // of sittingPlace is in the 
    // playThings array, effectively
    // matching (or mapping) the two
    // arrays elementwise
})
```


