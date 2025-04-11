# What is a variable?

Variables are spaces to contain values.

There are cups. They can hold water, drinks, and buttons that you don't use.

The name of the variable must be unique, otherwise the editor will export the error on its own.

## Declaration of Variables

Prior to ES6, variables were declared in the following ways.

```javascript
var myCup = 'water';
```

Today, variables are declared in the following ways.

```javascript
const glassCup = 'vodka';
let plasticCup = 'Orange juice';
```
## Differences by variable type

There are three types of javascript variables: var, let, and const.

The var and let can change the value assigned to the variable.

You cannot change the variable you assigned to const once it is declared, which is called a 'constant'.

### var
The first value assigned to the myCup variable is water.

If you then assign juice to the same variable, the value of myCup is changed to juice.

```javascript
var myCup = 'water';
console.log(myCup);
myCup = 'juice';
console.log(myCup);

// water
/// juice
```

It's very easy to set the value with just one var, but there's a big problem here.

```javascript
var liquid = 'vodca';
console.log('liquid =>', liquid);

function myCup() {
  liquid = 'water';
  var liquidInCup = 'water';
  console.log('myCup() liquid=> ', liquid);
  console.log('myCup() liquidInCup=> ', liquidInCup);
}

myCup();
liquidInCup = 'vodca'
console.log('liquidInCup =>', liquidInCup);


// liquid => vodca
// myCup() liquid=> water
// myCup() liquidInCup=> water
// liquidInCup => vodca
```

Var variable has no concept of scope.

In the case of liquid, it can be used within myCup function because it is declared at the top.

The liquidInCup variable must be used only within the myCup function, but can also be called outside the function.

You can even change the value, which can have a devastating effect on program behavior.

And it's the let and const.

### let

```javascript
let liquid = 'vodca';
console.log('liquid =>', liquid);

function myCup() {
  liquid = 'water';
  let liquidInCup = 'water';
  console.log('myCup() liquid=> ', liquid);
  console.log('myCup() liquidInCup=> ', liquidInCup);
}

myCup();
console.log('liquidInCup =>', liquidInCup);

// liquid => vodca
// myCup() liquid=> water
// myCup() liquidInCup=> water
// ReferenceError: liquidInCup is not defined

```

The liquidInCup inside myCup is well called, but you can see that the external called liquidInCup is experiencing a not defied error.

### const

```javascript
const pie = 3.14;
pie = 3.1456

// TypeError: Assignment to constant variable.
```

Reassigning a value to a const variable can confirm that an error occurs.

Because the constant is an unchanging value, you can use it as follows.

```javascript
// Finding the area of a circle
// pie * r ^ 2
const pie = 3.14;
const radius = 10;
console.log(pie * (radius ^ 2));
```
