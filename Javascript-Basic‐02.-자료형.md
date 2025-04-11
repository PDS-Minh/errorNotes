# 자료형

자바스크립트의 자료형은 크게 원시유형"pirmitive type" 과 객체 "object" 로 나뉘어집니다.

원시유형은 하나의 값만 저장하는 자료형으로 숫자, 문자, 논리형, undefined, null symbol 유형이 있습니다.

원시 유형 외에는 모두 객체 입니다.

## typeof

자바스크립트에서 자료형을 확인하는 방법은 다음과 같습니다.

```javascript
let hello='Hello~!';
console.log(typeof hello);

// result
// "string"
```

## 숫자형

모든 프로그래밍에서 기초가 되는 자료형 입니다. 자바스크립트에서는 정수와 실수를 함께 묶어서 숫자형으로 인식합니다.

자바스크립트는 정밀한 실수 계산에 적합하지 않으니 주의하세요!

```javascript
console.log(0.1+0.2);
// expect: 0.3
// result: 0.30000000000000004
```

정밀한 소수점 계산을 할 때는 `toFixed()` 나 `Math 함수` 를 적극 사용하는 것을 권장합니다.

## 문자형

자바스크립트에서 문자형은 작은 따옴표(') 나 큰 따옴표(") 로 묶은 데이터를 의미합니다.

### 특수기호 표시하기

문자열에는 종종 특수기호를 사용하여 줄 바꿈이나 탭 처럼 문서에서 기능을 수행할 수 있습니다.

```
\\ 백 슬래시 문자
\' 작은 따옴표 문자
\" 큰 따옴표 문자
\b 백스페이스 문자
\f 폼 피드 문자
\n 줄 바꿈 문자
\r 캐리지 리턴 문자
\t 탭 문자

console.log('\"Hi~\" \n nice to meet you! \tPMI!')
// result:  '"Hi~" nice to meet you! PMI!'
```

### 템플릿 리터럴

템플릿 리터럴은 문자열과 변수, 식을 섞어서 하나의 문자열을 만드는 방법 입니다.

백틱(``) 사이에 표현하고자 하는 문자열을 조합할 수 있습니다.

변수를 대입할때는 `${변수명}` 으로 입력할 수 있습니다.

또한 ${} 사이에 숫자 계산 같은 식도 가능합니다.

```javascript
const hello = 'Hello';
const world = 'World!'
const name = 'Inho';

console.log(`${hello} ~ ${world} ${name} -> ${new Date()}`);
// result:  "Hello ~ World! Inho -> Wed Feb 12 2025 12:53:57 GMT+0900 (한국 표준시)"

console.log(`2 X 3 = ${ 2 * 3 }`);
// result: "2 X 3 = 6"
```

## 논리형

논리형의 값은 true 와 false 만 있습니다.

조건식이 참, 거짓이냐를 구분할 때 주로 사용합니다.

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
undefined는 값이 할당되지 않았을 때 변수의 초기값 입니다. undefined는 값이면서 자료형 입니다.
```javascript
let user;
console.log(user);
// undefined
```

### null

null도 값이면서 동시에 자료형 입니다.

null은 값이 없거나 유효하지 않는 상태를 표현합니다.

그러나 웬만한 프로그래밍에서 null 사용을 기피해야 합니다.

JAVA 의 유명한 NullPointerException 오류가 있죠.

사람이 코드를 개발하는 이상 모든 오류에 대해 예측을 할 순 없지만,

예상치 못한 상황에 대비하기 위한 장치들은 있으니 이런 것들을 적극 활용해도 좋을 것 같습니다.

javascript 에는 옵셔널 채이닝이 있습니다.

```javascript

// 3항 연산자를 이용한 null 체크
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
console.log(car?.model ?? 'ok'); // null 병합 연산자
console.log(car?.model || 'ok'); // or 연산자

```

## 객체

javascript 에서 객체란, 여러 개의 원시 유형을 하나로 묶어놓은 것 이라고 볼 수 있습니다.

### 객체란?

객체는 하나의 변수에 다양한 정보를 담을 수 있는 자료형 입니다. 

중괄호({}) 안에 모든 정보를 담는데 키 와 값으로 여러개의 쌍을 만들 수 있습니다.

값에는 모든 자료형이 들어갈 수 있습니다. 함수도 들어갈 수 있습니다.

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

객체의 요소에 접근하여 값을 바꿀때는 `객체명.키이름` 이나 `객체명['키이름']` 으로 접근할 수 있습니다.

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

### 배열

배열도 하나의 변수에 여러개의 값을 저장할 수 있으므로 객체입니다. 

실제로 typeof 를 사용하여 배열의 타입을 확인하면 object로 출력되는 것을 확인할 수 있습니다.

```javascript
let alphabet = ['a', 'b', 'c', 'd', 'e'];
console.log(typeof alphabet); // object
```

인덱스를 통해 배열의 원하는 요소에 빠르게 접근 할 수도 있고 loop 함수를 사용하여 다양하게 응용할 수 있습니다.

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

## 심벌

심벌은 ECMAScript2015에 새롭게 추가된 원시 유형의 자료형으로, 위의 자료형들과는 다른 특성을 갖고 있습니다.

심벌의 가장 큰 특징은 유일성을 보장합니다.

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

# 자료형 변환

javascript의 장점이자 단점은 바로 자료형 검사가 느슨합니다.

아래 예시와 같이 자료형이 달라도 덮어씌울 수 있습니다.

```javascript
let userId = 'userId01'; // 문자형
userId = 123455; // 숫자형
```

후에 Typescript 라는 대안이 나와서 타입에 대한 설정이 한층 더 강력해집니다.

javascript 에서 자료형 변환은 다음과 같이 할 수 있습니다.

## 숫자형

문자형에서 숫자형으로 타입을 변환하는 방법은 크게 세가지가 있습니다.

1. 직접 숫자형으로 변환
2. Number() 함수
3. parseInt(), parseFloat() 함수

### 직접 숫자형으로 변환

위에서 언급했듯이 javascript 의 장점이자 단점이 느슨한 타입검사 입니다.

다음과 같이 직접 숫자형을 변환할 수 있습니다.

```javascript
let str2num = '10';
console.log(+str2num);
```

### Number()

Number()는 숫자 객체를 생성하는 생성자 함수 입니다.

```javascript
let str2num = '10';
console.log(Number(str2num));
```

### parseInt(), parseFloat()

parse 함수는 문자열 타입의 매개변수를 정수, 실수로 변환하는 함수 입니다.

Number 와 달리 parse 함수에는 두번 째 매개변수 옵션을 통해 2진수 부터 36 까지 다양한 진수로 변환할 수 있습니다.

기본은 10진수 입니다.

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

## 문자형

문자열이 아닌 값을 문자열로 변환할 때 사용합니다. 크게 3가지 방법이 있습니다.

1. 간단한 방법 (숫자 + '')
2. toString() 함수
3. String() 함수

### 숫자 + 빈 문자열

제일 간편한 방법이지만 추천하지 않습니다.

```javascript
let num2str = 10;
console.log(num2str + '');
```

### toString() 함수

toString 함수는 undefined 와 null 을 제외한 나머지 자료형을 모두 문자형으로 변환합니다.

```javascript
let num2str = 10;
console.log(num2str.toString());
```
### String() 함수

String 함수는 undefined 와 null 을 포함한 모든 자료형을 문자형으로 변환합니다.

```javascript
let num2str = 10;
console.log(String(num2str));
```

## 논리형

Boolean() 함수를 이용하여 다른 유형의 데이터를 논리형 데이터로 변환할 수 있습니다.

값이 0 이거나 비어있을 땐 false, 그 외에는 true 를 반환합니다.

```javascript
Boolean(1); // true
Boolean(0); // false
Boolean('1'); // true
console.log(Boolean('')) // false
Boolean(undefined); // false
```