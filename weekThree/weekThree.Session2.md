Truthy & Falsy Values in JavaScript

Before we begin looking at logical expressions,
which rely on the truthiness of statements to 
derive validity of the expression, we should 
have a solid understanding of what is truthy in 
JavaScript. Since JavaScript is loosely typed, 
values can be coerced into booleans to evaluate 
logical expressions. if conditions, &&, ||, and 
the part of a ternary statement preceding the 
question mark (_?_:_) all coerce their evaluated 
values into booleans. (Note that this doesn�t mean 
that they necessarily return a boolean from the operation.) 
The shortcut to knowing what is truthy is to know that 
there are only six falsy values � false, null, undefined,
 NaN, 0, and '' � and everything else is truthy. 
This means that [] and {} are both truthy.


We have a golbal place where we decalre all the varible and there is a place where we will write the equations
and there will be a place where we will do the constant.

/*G/Memory
num: 5
multiply: f
name: Milton
multi:
*/


const num = 5
function multilpy (input )
{
  const result = input * 2
  return result
}
const name = "Ali"
const multi = Multiply(1)
multilpy()

There are ways to declare a function. 

Checkout if you can come up with some functional declaration.
Variable Environmnent - 
When we com up from a ficntion, the javascript provides us a direction to let us know wehere
we are. This is called callstack. 
- It tells us where we are and what we can do from that point. Thats the job of callstack to tell where 
to go from that point. We took the golbal.
Global will come first.
AAny function that is going in that dictionary. Every place hasit local. 

```javascript
// console.log is the writer 
// console.log('Hello world!')

// Using the older variable syntax 
// var name = 'Milton'

// console.log(name)

// bla = 2
// var bla

// Let allows the variable to be changed and it will only take the latest variable
// with the variable name
let name = "Nelson"
name = "NZ"
name = "Milton"
console.log(name)

// 
const lastname = "Milton"
const firstname = "Ashkar"
console.log(lastname)
console.log(firstname)

// or to concatenate
console.log(firstname, lastname)

// Basic arithmetic
const numOne = 100.99
const numTwo = 56.97

const resultSubtract = numTwo - numOne
console.log(resultSubtract)

const resultAdd = numTwo + numOne
console.log(resultAdd)

const resultDivide = numTwo / numOne
console.log(resultDivide)

const resultMultiply = numTwo * numOne
console.log(resultMultiply)


// % is modular and gets the number of decimal places
const numThree = 12
const numFour = 5

const result = numThree % numFour
console.log(result)
```