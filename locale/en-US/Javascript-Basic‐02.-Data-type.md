# Data type

JavaScript's data types are largely divided into raw type "preliminary type" and object "object".

The raw type is a data type that stores only one value, including numeric, letter, logical, undefined, and null symbol types.

All but raw type are objects.

## typeof

Here's how to check the data type in JavaScript.

```javascript
let hello='Hello~!';
console.log(typeof hello);

// result
// "string"
```

## Number type

It is a data type that is the basis of all programming. In JavaScript, integers and real numbers are grouped together and recognized as numeric.

Javascript is not suitable for precise mistake calculations, so be careful!

```javascript
console.log(0.1+0.2);
// expect: 0.3
// result: 0.30000000000000004
```

It is recommended that you actively use 'toFixed()' or 'Mat function' when performing precise decimal calculations.

## Character type

In JavaScript, letter type means data in small quotation marks (') or large quotation marks (').

### To display special symbols

Strings often use special symbols to perform functions in a document, such as line breaks or tabs.

```
\\ Back slash characters
\' lower quotation marks
\" double quotation marks
\b Backspace Characters
\fform feed character
\n a line-changing character
\r carriage return character
\t Tab Characters

console.log('\"Hi~\" \n nice to meet you! \tPMI!')
// result:  '"Hi~" nice to meet you! PMI!'
```

### Template Literals

Template literal is a way to create one string by mixing strings, variables, and expressions.

You can combine the strings you want to express between the backticks (``).

When substituting variables, you can enter '${variable name}'.

You can also do numerical calculations between ${}.

```javascript
const hello = 'Hello';
const world = 'World!'
const name = 'Inho';

console.log(`${hello} ~ ${world} ${name} -> ${new Date()}`);
// result:  "Hello ~ World! Inho -> Wed Feb 12 2025 12:53:57 GMT+0900 (한국 표준시)"

console.log(`2 X 3 = ${ 2 * 3 }`);
// result: "2 X 3 = 6"
```

## logical type

The logical type has only true and false values.

It is usually used to distinguish whether a conditional expression is true or false.

```javascript
const isUse = true;

if (isUse === true) { // or if (isUse)
  console.log('Using...')
} else {
  console.log('Not Using...')
}
```

## undefined, null

### undefined

undefined is the initial value of a variable when no value is assigned. undefined is both a value and a data type.

```javascript
let user;
console.log(user);
// undefined
```

### null

Null is also a value and a data type.

null represents a state in which no value exists or is invalid.

However, you should avoid using null in most programming.

JAVA's famous null PointerException error.

As long as a person develops a code, they can't predict every error,

There are devices to prepare for unexpected situations, so I think it would be good to use these things actively.

The javascript has an optional chaining.

```javascript
// Null check with 3-term operator
let user = null;
console.log(user ? 'Tom' : 'No User!');

// 옵셔널 체이닝
let car = {
  door: 'ok',
  engine: 'ok',
  tire: 'ok',
  bettery: 'ok'
};

console.log(car?.model); // undefiend
console.log(car?.model ?? 'ok'); // null merge operator
console.log(car?.model || 'ok'); // or operator

```

## Object

In javascript, an object is a combination of multiple raw types.

### What is an object?

An object is a data type that can contain various information in one variable.

You can create multiple pairs of keys and values to contain all the information in brackets ({}.

The value can contain any datatype. It can also contain functions.

```javascript
function startingVehicle() {
  console.log('Driving is ready');
}

let car = {
  door: 'ok',
  engine: 'ok',
  tire: 'ok',
  bettery: 'ok',
  isFuelFull: false,
  km: 12384,
  starting: startingVehicle()
};

console.log(car.starting); // Driving is ready

```

When you access an element of an object and change its value, you can access it by `object name.key name` or `'object name ['key name']`.

```javascript
let car = {
  door: 'ok',
  engine: 'ok',
  tire: 'ok',
  bettery: 'ok',
  isFuelFull: false,
  km: 12384,
};

car.isFuelFull = true;
car['km'] = 12544;

```

### Array

Arrays are also objects because they can store multiple values in a variable.

In fact, if you use typeof to check the type of array, you can see that it is output as an object.
```javascript
let alphabet = ['a', 'b', 'c', 'd', 'e'];
console.log(typeof alphabet); // object
```

Indexes provide quick access to the desired elements of an array, or loop functions can be used to provide a variety of applications.

```javascript
let alphabet = ['a', 'b', 'c', 'd', 'e'];
console.log(alphabet[1]) // b

alphabet[1] ='f'
console.log(alphabet[1]) // f

for (const content of alphabet) {
  console.log(content)
  /*  
  result 
  a
  b
  c
  d
  e
   */
}

```

## Symbol

The symbol is a raw data type newly added to ECMAScript2015 and has different characteristics from the above data types.

The biggest feature of the cymbal is to ensure its uniqueness.

```javascript
let id = Symbol();
const user = {
    name: 'Hwang',
    [id]: 123456
};

console.log(user);
// {name: 'Hwang', Symbol(): 123456}
console.log(user[id]);
// 123456

user.id = 56789;

console.log(user);
// {name: 'Hwang', id: 56789, Symbol(): 123456} 
```

# Data type conversion

The advantage and disadvantage of javascript is that data-type tests are loose.

As in the example below, it can be overwritten even if the data type is different.

```javascript
let userId = 'userId01'; // 문자형
userId = 123455; // 숫자형
```

Later, an alternative called Typescript comes out, making the settings for the types even more powerful.

In javascript, data type conversion can be done as follows.

## Number type

There are three main ways to convert types from letter type to numeric type.

1. Direct conversion to numeric type
2. Number() function
3. parseInt(), parseFloat() function

### Direct conversion to numeric type

As mentioned above, the advantage and disadvantage of javascript is a loose type test.

You can convert the numeric type directly as follows.

```javascript
let str2num = '10';
console.log(+str2num);
```

### Number()

Number() is a generator function that generates numeric objects.

```javascript
let str2num = '10';
console.log(Number(str2num));
```

### parseInt(), parseFloat()

The parse function is a function that converts the parameters of string type into integers, real numbers.

Unlike Number, the path function can be converted to a variety of integers, from binary to 36, with the second parameter option.

The default is decimal.

```javascript
let str2num = '10';
console.log(parseInt(str2num)); // 10
console.log(parseInt(str2num, 2)); // 2
console.log(parseInt(str2num, 16)); // 16

let str2num = 'F';
console.log(parseInt(str2num)); // NaN
console.log(parseInt(str2num, 2)); // NaN
console.log(parseInt(str2num, 16)); // 15
```

## Character type

Use to convert non-string values into strings. There are three main ways.

1. Simple method (number + '') or '${}'
2. toString() function
3. String() function

### numeric + empty string

It's the easiest way, but I don't recommend it.

```javascript
let num2str = 10;
console.log(num2str + '');
console.log(`${num2str}`);
```

### toString() function

The toString function transforms all data types into characters except undefined and null.

```javascript
let num2str = 10;
console.log(num2str.toString());
```
### String() function

The String function transforms all data types, including undefined and null, into characters.

```javascript
let num2str = 10;
console.log(String(num2str));
```

## logical type

You can use the Boolean() function to convert other types of data into logical data.

Returns false if the value is 0 or empty, and true otherwise.

```javascript
Boolean(1); // true
Boolean(0); // false
Boolean('1'); // true
console.log(Boolean('')) // false
Boolean(undefined); // false
```