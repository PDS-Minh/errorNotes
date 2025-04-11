# Function(method)

What is Function?

Let's think about math class in middle and high school for a while.

`x + y = z` I remember memorizing the formula `π * r²` to find the area of the circle.

The **function** is to enter the value you want to calculate and output the desired result.

## Look at the function

The structure of the function is as follows.

```javascript
function functionName (parameter) {
  return value;
}
```

### Function

A function must precede the function keyword, just as a variable is declared using var, let, and const in the variable.

### FunctionName

The function name declares it in camelCase form.

CamelCase is literally a way of expressing the shape of a camel's hump.

When combining two or more words, the first word is in lowercase and the first letter of the following letters is in capital letters.

The reason why I express it like this is because it clearly expresses the function of the function

This is to express what this method does from the perspective of yourself or others.

ex) Showing a list of users

```javascript
function showUserList() {}
```

### parameter

Parameters can be empty if there is no value to pass, or more than one can be passed.

Parameters can carry different types.

```javascript
function showUser(name, age, address, hobby) {
  console.log(`My name is ${name}`);
  console.log(`My age is ${age}`);
  console.log(`My address is ${address}`);
  console.log(`My hobby is ${hobby}`);
}

showUser('Hwang', 36, 'South Korea', 'Running');
```

Too many parameters can make the code messy, which can be abbreviated using a method called a preposition.

```javascript
function showUser(...userInfo) {
  //Direct access to the index of the array
  console.log(userInfo) // Array ["Hwang", 36, "South Korea", "Running"]
  
  console.log(`My name is ${userInfo[0]}`);
  console.log(`My age is ${userInfo[1]}`);
  console.log(`My address is ${userInfo[2]}`);
  console.log(`My hobby is ${userInfo[3]}`);
  
  // Tip. To assign variables in order of array
  const [name, age, address, hobby] = userInfo;
  console.log(`My name is ${name}`);
  console.log(`My age is ${age}`);
  console.log(`My address is ${address}`);
  console.log(`My hobby is ${hobby}`);
}

showUser('Hwang', 36, 'South Korea', 'Running');

/**
 Array ["Hwang", 36, "South Korea", "Running"]
 "My name is Hwang"
 "My age is 36"
 "My address is South Korea"
 "My hobby is Running"
   
 "My name is Hwang"
 "My age is 36"
 "My address is South Korea"
 "My hobby is Running"
 */
```

### Return

The return value is used to calculate based on the parameters passed and to return the result.

There are some cases where there is a return value and there is no return value, but when there is no return value, it is expressed as 'void'.

Normally, javascript omits the return type, but typescript must specify the return type.

```javascript
function addNumbers(num1, num2) { // type: number
  return num1 + num2;
}

function isCorrect(num1, num2) { // type: boolean
  return num1 === num2;
}

function showNumbers() { // type: number[]
  return [1, 2, 3, 4, 5, 6, 7, 8, 9]
}

function showUser(name, age, address, hobby) { // type: x => void
  console.log(`My name is ${name}`);
  console.log(`My age is ${age}`);
  console.log(`My address is ${address}`);
  console.log(`My hobby is ${hobby}`);
}
```

## Why should I use a function

Let me give you an extreme example.

You want to output a multiplication table.

```javascript
console.log('1 x 1 = 1');
console.log('1 x 2 = 2');
console.log('1 x 3 = 3');
// ... 
console.log('9 x 9 = 81');
```

You can type directly in the same way as above, but it is too inefficient for a position where you have learned programming.

You have to spend 81 lines to output all the multiplication tables.

Here, we're going to use a function to express it.

```javascript
function multiplicationValue(num1, num2) {
  return num1 * num2;
}

for (let i = 1; i <= 9; i++) {
  for (let j = 1; j <= 9; j++) {
    console.log(`${i} x ${j} = ${multiplicationValue(num1, num2)}`)
  } 
}
```

## Function expressions used without a name

We've learned the basics of functions.

When declaring a function, you must name the function, but some functions can be used without assigning a name.

### Anonymous function

**Anonymous function** literally does not have a function name.

Above, you need to assign the name of the function, but what if the name of the function is not there?

It's allocating a function to a variable.

```javascript
let sum = function(a, b) {
  return a + b;
}

console.log(`sum result => ${sum(1, 2)}`); // 3
```

### immediate execution function

The above method is to assign as a variable and call it whenever necessary.

An immediate execution function can declare a function to be executed only once, which is called **immediate execution function**.

```javascript
(function(a, b) {
  let sum = a + b;
  console.log(`sum result => ${sum}`); // 3
} (1, 2));

// "sum result => 3"
```

### Arrow function

The arrow function is a more straightforward expression for declaring functions that have appeared since ECMAScript2015.

The arrow function allows you to express it in a more concise and abbreviated form.

The 'function' Coward disappears and ends when you add '=>' between the parameter and the brace ({}.

'(parameter) => {function content}'

If you replace the anonymous function sum declared above with the arrow expression, it is as follows.

```javascript
// before
let sum = function(a, b) {
  return a + b;
}

// after
let sum = (a, b) => {
  return a + b;
}

console.log(`sum result => ${sum(1, 2)}`); // 3
```

### callback function

A callback function refers to a function that is used as an argument for another function.

Simply put, you can think of double calling by adding another function to the parameters of the function.

It may be a complicated concept, but it's an occasional concept, so you'd better keep that in mind for now.

```javascript
function display(a, b) {
 console.log(`a + b = ${a + b}`);
}

function getData(callback) {
  const num1 = 10;
  const num2 = 15;
  callback(num1, num2);
}

getData(display);
// "a + b = 25"
```

### recursive function

Recursion means referring to yourself when defining something.

You can think of it as a concept in which a function calls itself.

A famous example is a factual that I learned in math class.

Factorial means the product of all natural numbers from 1 to n when n is a natural number.

The 10 Factorial is as follows.

`10! = 10 * 9 * 8 * 7 * ... * 1 => 3628800`

It can also be expressed as a loop, but it can be expressed using a recursive function.

```javascript
function factorial(num) {
  if (num <= 1) { // base case
    return 1
  }
  return num * factorial(num - 1) // recursive case
}
console.log(factorial(10)) //result 3628800
```