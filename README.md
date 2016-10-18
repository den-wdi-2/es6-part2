# ES6 Part 2

### Concise Object Properties and Methods (5 / 75)

ES6 allows us to shorten method definitions from:

```js
var car = {
  drive: function(){
    console.log("vroom")
  }
}
```

to

```js
let car = {
  drive(){
    console.log("vroom")
  }
}
```

And for properties where the key is the same as the variable storing the value:

```js
// es5
let x = 1
let y = 2
let obj = {x:x, y:y}

// vs
//es6

let obj = {x,y}
```

#### You do: Concise methods and properties practice (5 / 80)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/07-concise-properties-and-methods.js

### Template Literals (5 / 85)

Remember string interpolation from ruby? We've been able to semi-accomplish this
with string concatenation in javascript:

```js
var name = "Inigo Montoya"
var killee = "father"
var prepareTo = "die"

console.log("Hello. My name is "+ name + ". You killed my " + killee +". Prepare to " + prepareTo)
```

In ES6, we can interpolate variables using template literal syntax: `\``

```js
let name = "Inigo Montoya"
let killee = "father"
let prepareTo = "die"

console.log(`Hello. My name is ${name}. You killed my ${killee}. Prepare to ${prepareTo}`)

```

#### You do: Template Exercise (5 / 90)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/09-templates.js

### Arrow Functions (15 / 105)

Arrow functions are a new shorthand syntax for defining anonymous functions:

```js
let foods = ["pizza","mac n cheese","lasagna"]
foods.forEach( food => console.log(`I love ${food}`) )

// vs the old

foods.forEach(function(food){
  console.log("I love " + food)
})
```

If there is more than one argument to the anonymous function, wrap
them in parens:

```js
let foods = ["pizza","mac n cheese","lasagna"]
foods.forEach( (food,i) => console.log(`My #${i} favorite food is ${food}`) )
```

Arrow functions also have the benefit of not changing the value of `this`:

```js
var pizza = {
  temperature: 0,
  toppings: ["cheese", "ham", "pineapple"],
  bake() {
    setInterval(function(){
      this.temperature++ // doesnt work because this is GLOBAL. The setInterval function belongs to the window object.
    }, 1000)
  }
}

// vs ES6

var pizza = {
  temperature: 0,
  toppings: ["cheese", "ham", "pineapple"],
  bake() {
    setInterval( () => {
      this.temperature++
    }, 1000)
  }
}
```

Additionally, the `return` statement is not needed with single line arrow functions. There is an implicit return.

```js
let add = (x, y) => x + y
```

If the function is multi-line, you need to explicitly return:

```js
let add = (x,y) => {
  return x + y
}
```

Though the single line return can be faked by wrapping the expression in parentheses:

```js
let add = (x,y) => (
  x + y
)
```

#### You do: Arrow functions (10 / 115)

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/11-arrow-functions.js


## Legacy Browser Support (5 / 120)

Support for ES6 is great! - https://kangax.github.io/compat-table/es6/

If you need to support a legacy browser, check out the following tools:
- [Traceur](https://github.com/google/traceur-compiler/wiki/Getting-Started)
- [Babel](https://babeljs.io/)

## Bonus

### Spread operator

The spread operator `...` allows an expression to be expanded into multiple elements.

This is useful for separating an array into individual elements:

```js
var dimensions = [10, 5, 2];
var volume = function(height, width, length){
  return height * width * length;
}
volume(...dimensions);

// versus

volume(dimensions[0], dimensions[1], dimensions[2])
```

This also makes it very easy to create copies of an array in functions where
mutation occurs:

```js
var days = ["monday","tuesday","wednesday","thursday","friday","saturday","sunday"]
function reversedDays(arr){
  return arr.reverse()
}
console.log(reversedDays(days))
// but now days is no longer in order
console.log(days)

// To deal with this, we can either:

function reversedDays(arr){
  var newArray = []
  for(let i = 0; i < arr.length; i++){
    newArray.push(arr[i])
  }
  return newArray.reverse()
}
console.log(reversedDays(days))
console.log(days)

// or... (<- pun)

function reversedDays(arr){
  return [...arr].reverse()
}
console.log(reversedDays(days))
console.log(days)
```

#### You do: Spread Practice

1. https://github.com/ga-wdi-exercises/es6-exercises/blob/master/03-spread-practice.js

## Keep Going

There are lots more features of ES6 that we have not covered:

- [Symbols](http://es6-features.org/#SymbolType)
- [Iterator & for..of operator](http://es6-features.org/#IteratorForOfOperator)
- [Generators](https://davidwalsh.name/es6-generators)
- [Proxies](https://ponyfoo.com/articles/es6-proxies-in-depth)
- [Reflection and meta-programming](http://www.2ality.com/2011/01/reflection-and-meta-programming-in.html)

## Resources

- [You Don't Know ES6](https://github.com/getify/You-Dont-Know-JS/tree/master/es6%20%26%20beyond)
- [Block Scope](https://www.sitepoint.com/joys-block-scoping-es6/)
- [Destructuring](http://www.2ality.com/2015/01/es6-destructuring.html)
- [Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_template_literals)
