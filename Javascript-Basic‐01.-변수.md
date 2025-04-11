# 변수란?

변수는 값을 담기 위한 공간 입니다.

컵이 있습니다. 컵에는 물도 담을 수 있고 음료수를 담을수도 있고 안 쓰는 단추 같은것도 담을 수 있습니다.

변수의 이름은 유일해야 합니다. 그렇지 않으면 에디터에서 알아서 오류를 내보냅니다.

## 변수 선언

ES6 이전에는 다음과 같은 방법으로 변수를 선언했습니다.

```javascript
var myCup = 'water';
```

오늘날에는 변수를 다음과 같은 방법으로 선언합니다.

```javascript
const glassCup = 'vodka';
let plasticCup = 'Orange juice';
```
## 변수 종류 별 차이

javascript 변수의 종류는 var, let, const 3가지 입니다.

var 과 let은 변수에 할당한 값을 변경할 수 있습니다.

const 에 할당한 변수는 한번 선언되면 변경할 수 없습니다. 이를 `상수` 라고 부릅니다.

### var
myCup 변수에 제일 처음 할당 한 값은 water 입니다.

그 다음 동일한 변수에 juice 를 할당하면 myCup 의 값은 juice 로 변경됐습니다.

```javascript
var myCup = 'water';
console.log(myCup);
myCup = 'juice';
console.log(myCup);

// water
/// juice
```

아주 간편하게 var 하나로 값을 설정할 수 있습니다. 그러나 여기엔 큰 문제가 있습니다.

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

var 변수는 scope 의 개념이 없습니다.

liquid 같은 경우는 제일 상단에 선언했기 때문에 myCup 함수 안에서도 사용할 수 있습니다.

liquidInCup 변수는 myCup 함수 안에서만 사용돼야 하는데 함수 밖에서도 호출을 할 수 있습니다.

심지어 값도 바꿀 수 있습니다. 이는 프로그램 동작에 치명적인 영항을 줄 수 있습니다.

이에 등장한 것이 let과 const 입니다.

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

myCup 내부의 liquidInCup 는 잘 호출이 됩니다. 그러나 외부에서 호출한 liquidInCup 은 not defied 오류가 발생하는 것을 확인할 수 있습니다.

### const

```javascript
const pie = 3.14;
pie = 3.1456

// TypeError: Assignment to constant variable.
```

const 변수에 값을 재할당 하면 오류가 발생하는 것을 확인할 수 있습니다.

상수는 변하지 않는 값 이기 때문에 다음과 같이 사용할 수 있습니다.

```javascript
// 원의 넓이 구하기
// pie * r ^ 2
const pie = 3.14;
const radius = 10;
console.log(pie * (radius ^ 2));
```
