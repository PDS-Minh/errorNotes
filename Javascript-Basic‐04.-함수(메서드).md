# 함수(메서드)

함수란?

중,고등학교 때 수학시간을 잠시 떠올려봅시다.

`x + y = z` 나 원의 넓이를 구하기 위해  `π * r²` 공식을 외웠던 기억이 있을겁니다.

이처럼 계산하고자 하는 값을 입력하고 원하는 결과값을 출력하도록 하는 것이 **함수** 입니다.

## 함수 살펴보기

함수의 구조는 다음과 같습니다.

```javascript
function 함수이름(매개변수) {
  return 반환값;
}
```

### function

변수에서 var, let, const 를 사용하여 변수를 선언했듯이 함수도 function 키워드를 앞에 붙여야 합니다.

### 함수이름

함수 이름은 camelCase 형태로 선언 해줍니다.

camelCase 는 단어 그대로 낙타의 혹과 같은 모양으로 표현하는 방법입니다.

두 개 이상의 단어를 조합할 때 첫번째 단어는 소문자로, 그 뒤의 문자들의 첫 글자는 대문자로 표현합니다.

이렇게 표현하는 이유는 해당 함수가 어떤 기능을 하는지 명확하게 표현을 해서 

본인이나 다른 사람이 봤을때 이 메서드가 어떤 기능을 하는지 표현하기 위함입니다.

ex) 유저의 리스트를 보여주기

```javascript
function showUserList() {}
```

### 매개변수

매개변수는 전달 할 값이 없으면 비워도 되고 1개 이상 전달할 수 있습니다.

매개변수는 다양한 타입을 전달할 수 있습니다.

```javascript
function showUser(name, age, address, hobby) {
  console.log(`My name is ${name}`);
  console.log(`My age is ${age}`);
  console.log(`My address is ${address}`);
  console.log(`My hobby is ${hobby}`);
}

showUser('Hwang', 36, 'South Korea', 'Running');
```

매개변수가 너무 많아지면 코드가 지저분해질 수 있으니 전재구문이란 방법을 사용하여 축약할 수 있습니다.

```javascript
function showUser(...userInfo) {
  // 배열의 인덱스에 바로 접근
  console.log(userInfo) // Array ["Hwang", 36, "South Korea", "Running"]
  
  console.log(`My name is ${userInfo[0]}`);
  console.log(`My age is ${userInfo[1]}`);
  console.log(`My address is ${userInfo[2]}`);
  console.log(`My hobby is ${userInfo[3]}`);
  
  // Tip. 배열의 순서대로 변수를 할당하는 방법
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

### 반환값

반환값은 전달한 매개변수를 토대로 계산을 하고 결과값을 반환할 때 사용합니다.

반환값이 있는 경우도 있고 없는 경우도 있는데 반환값이 없을때는 `void` 라고 표현합니다.

보통 javascript 에서는 반환 타입을 생략하지만 typescript 는 반환 타입을 지정해줘야 합니다.

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

## 함수를 사용해야 하는 이유

극단적인 예시를 들어보겠습니다. 

구구단을 출력하려고 합니다.

```javascript
console.log('1 x 1 = 1');
console.log('1 x 2 = 2');
console.log('1 x 3 = 3');
// ... 
console.log('9 x 9 = 81');
```

위와 같은 방법으로 직접 타이핑으로 할 수도 있지만 프로그래밍을 배운 입장으로써 너무나 비효율적입니다.

구구단을 모두 출력하기 위해 81라인을 소비해야 하니 말이죠.

여기서는 함수를 이용한 방법으로 표현해보겠습니다.

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

## 이름 없이 사용하는 함수 표현식

함수의 기본에 대해 알아봤습니다.

함수를 선언할 때 함수의 이름을 지정해 줘야 하는데 이름을 할당하지 않고 사용할 수 있는 함수가 있습니다.

### 익명함수

**익명함수**는 말 그대로 함수 이름이 없습니다.

위에서는 함수의 이름을 할당해줘야 하는데 함수의 이름이 없으면 어떻게 할까요?

바로 변수에 함수를 할당하는 것 입니다.

```javascript
let sum = function(a, b) {
  return a + b;
}

console.log(`sum result => ${sum(1, 2)}`); // 3
```

### 즉시 실행 함수

위 에서의 방법은 변수로 할당하고 필요할 때 마다 호출하는 방법입니다.

즉시실행함수는 한번만 실행 할 함수를 따로 선언할 수 있는데 이를 **즉시 실행 함수** 라고 합니다.

```javascript
(function(a, b) {
  let sum = a + b;
  console.log(`sum result => ${sum}`); // 3
} (1, 2));

// "sum result => 3"
```

### 화살표 함수

화살표 함수는 ECMAScript2015 버전부터 등장한 함수를 좀 더 간단하게 선언하기 위한 표현식 입니다.

화살표 함수를 사용하면 보다 간결하고 축약된 형태로 표현할 수 있습니다.

`function` 카워드는 사라지고 매개변수와 중괄호({}) 사이에 `=>` 를 추가하면 끝 입니다.

`(매개변수) => { 함수 내용 }`

위에서 선언했던 익명함수 sum 을 화살표 표현식으로 바꾸면 다음과 같습니다.

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

### 콜백함수

콜백함수는 다른 함수의 인수로 사용하는 함수를 말합니다.

쉽게 말하면 함수의 매개변수에 다른 함수를 넣어서 2중 호출을 한다고 생각하시면 될 것 같습니다.

복잡한 개념일 수 있지만 간혹 사용되는 개념이니 지금은 알아만 두시는게 좋을 것 같습니다.

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

### 재귀 함수

재귀란 어떠한 것을 정의할 때 자기 자신을 참조하는 것을 뜻 합니다.

함수가 자기 자신을 호출하는 개념이라고 보면 될 것 같습니다.

유명한 예시로는 수학시간에 배웠던 팩토리얼이 있습니다.

팩토리얼은 n 이 자연수일 때, 1 부터 n 까지의 모든 자연수의 곱을 의미합니다.

10 팩토리얼은 다음과 같습니다.

`10! = 10 * 9 * 8 * 7 * ... * 1 => 3628800`

이를 loop 로도 표현할 수 있겠지만 재귀함수를 사용하여 표현할 수 있습니다.

```javascript
function factorial(num) {
  if (num <= 1) { // base case
    return 1
  }
  return num * factorial(num - 1) // recursive case
}
console.log(factorial(10)) //결과값 3628800
```