# 목차

* [동기? 비동기?](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async#%EB%8F%99%EA%B8%B0-%EB%B9%84%EB%8F%99%EA%B8%B0)
  * [동기 프로그래밍](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async#%EB%8F%99%EA%B8%B0-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)
  * [비동기 프로그래밍](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async#%EB%B9%84%EB%8F%99%EA%B8%B0-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)
* [Javascript 의 비동기](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async#javascript-%EC%9D%98-%EB%B9%84%EB%8F%99%EA%B8%B0)
  * [Callback](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async#callback-pattern)
  * [Promise](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async#promise)
  * [Async & Await](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async#async--await)
* [추가 - HTTP 상태 코드](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async#http-%EC%83%81%ED%83%9C-%EC%BD%94%EB%93%9C)

# 동기? 비동기? 

앞서 우리는 간단한 유저 관리를 할 수 있는 웹 페이지를 생성했습니다.

잘 따라와주셔서 정말 감사합니다.

여러가지 궁금한 점이 있을 것 같아 추가 보충 자료를 준비했습니다.

바로 동기, 비동기에 관한 내용 입니다.

`app.js` 에서 작성했던 코드 중 일부를 가져왔습니다.

```javascript
async function fetchUsers() {
  const response = await fetch(API_URL);
  const users = await response.json();
  displayUsers(users);
}

// Display User List
function displayUsers(users) {
  userList.innerHTML = '';
  for (const user of users) {
  // blabla~~
  }
```

위 코드를 보면 function 이나 변수 앞에 `async` 혹은 `await` 키워드를 볼 수 있습니다.

벌써부터 머리가 아프다면 정상입니다.

일단 위의 내용은 잊어버리고 처음부터 천천히 진행 해보겠습니다.

## 동기 프로그래밍

동기 프로그래밍이란 하나의 작업이 완료되기 전에 다음 작업을 수행할 수 없는 방식 입니다.

예를 들어보겠습니다.

```javascript
// Task1
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// Task2
console.log('Finish!');
```

보통 javascript는 특별한 명령어가 없다면 코드의 상단부터 하단까지 순서대로 한 줄씩 읽고 실행 합니다.

이를 인터프리터라고 합니다. 이는 컴퓨터 공학 관련 지식이기 때문에 나중에 기회가 된다면 찾아보시는 것도 좋을 것 같습니다.

예제 코드를 순서대로 해석하면 0, 1, 2, 3, 4 를 출력 후 마지막으로 Finish! 를 출력 할 것으로 예상이 됩니다.

`console.log('Finish!');` 는 for loop 가 완전히 끝나기 전 까진 실행할 수 없습니다.

쉽게 얘기하면, 동기 프로그래밍은 한번에 한가지 일 밖에 못합니다.

제일 위에 있는 Task1 이 끝난 후 밑에 있는 Task2 를 이어서 진행 합니다. 

작업 순서가 중요한 프로그램에서는 가장 확실한 방법 이지만, 앞의 작업이 끝나지 않으면 뒤의 작업은 계속 기다려야 합니다.

![sync](https://github.com/user-attachments/assets/42d0bd67-d47a-49e5-b968-8fceba392deb)

## 비동기 프로그래밍

비동기 프로그래밍이란 여러개의 작업을 순서대로 기다리지 않고 동시에 수행할 수 있습니다. 

예시 코드를 보겠습니다.

```javascript
setTimeout(() => {
  console.log('Hi~!');
}, 1000);

console.log('bye~!');
```
setTimeout은 javascript 내장 함수로, 작업을 지연 시킬 때 주로 사용하는 함수 입니다.

초 단위는 ms 로 표기하고 1000은 1초 입니다.

동기 프로그램이라면 Hi~! 가 먼저 출력되고 Bye~! 가 출력돼야 합니다.

그러나 위 코드를 실행하면 Bye~! 가 먼저 출력되고 1초 뒤에 Hi~! 이 출력됩니다.

![async](https://github.com/user-attachments/assets/9302da11-4c49-41ed-99f3-8e98c8297437)

### 비동기 프로그램의 이점

그러면 Youtube를  비유하여 설명해보겠습니다.

요즘 한국에서 유행하는 밈인 chill guy를 검색했습니다.

![async example](https://github.com/user-attachments/assets/a8571e20-f73f-4dd9-9f64-62068d472a7f)

제 예상으로는 chill guy 관련 Shorts 리스트를 가져오는 API 와 영상 리스트를 가져오는 API, 

구독 한 채널에서 chill guy 업데이트 정보를 가져오는 API 등등 수많은 request api 들이 있을겁니다. 

개발자 도구를 켜서 확인을 할 수 있으니 확인해보시면 좋을 것 같습니다.

이 수많은 요청들을 순서대로 가져온다고 하면 유튜브 시청자들은 답답함을 견디지 못하고 화를 내거나 앱을 꺼버릴 것 입니다.

이런 불상사를 방지하기 위해 사용하는 것이 비동기 프로그램입니다.

여러개의 요청을 한번에 실행하고 요청이 완료 된 것 부터 빠르게 보여줄 수 있습니다.

# Javascript 의 비동기

Javascript 에서의 비동기 역사를 짧게 설명해보겠습니다.

## Callback Pattern

과거 Promise 가 등장하기 전에 비동기 이벤트를 다룰 때 Callback 패턴을 사용했습니다.

콜백 패턴이란 비동기 작업이 완료된 후 호출되는 함수를 전달하는 방식 입니다.

작업이 많아질수록 코드가 복잡해지고 가독성이 떨어지는 콜백지옥이 발생합니다.

또한 에러 발생시 에러 처리도 어렵습니다.

```javascript
setTimeout(() => {
  console.log('Task 1 completed');
  setTimeout(() => {
    console.log('Task 2 completed');
    setTimeout(() => {
      console.log('Task 3 completed');
    }, 1000);
  }, 1000);
}, 1000);

```

## Promise

이에 나타난 것이 Promise 입니다.

비동기 작업의 완료 또는 실패를 나타내는 객체로 콜백 지옥을 피하기 위해 .then(), .catch()를 사용하여 비동기 작업을 정리합니다.

```javascript
function asyncTask(taskName, delay) {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log(`${taskName} completed`);
      resolve();
    }, delay);
  });
}

asyncTask('Task 1', 1000)
  .then(() => asyncTask('Task 2', 1000))
  .then(() => asyncTask('Task 3', 1000))
  .catch(err => console.error(err));
```

Callback 과는 확연히 가독성이 좋아지고 나름 쳬계적으로 비동기 작업을 관리할 수 있습니다.

## Async & Await

이것도 복잡해서 싫다! 더 간결한 것이 좋다!

그냥 제가 지어 본 말이고 프로미스를 좀 더 쉽게 사용하기 위해 등장한 ES2017의 문법 입니다.

비동기 코드를 동기 코드처럼 쉽게 작성할 수 있습니다.

```javascript
function asyncTask(taskName, delay) {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log(`${taskName} completed`);
      resolve();
    }, delay);
  });
}

async function executeTasks() {
  try {
    await asyncTask('Task 1', 1000);
    await asyncTask('Task 2', 1000);
    await asyncTask('Task 3', 1000);
  } catch (err) {
    console.error(err);
  }
}

executeTasks();
```

가독성이 향상됐고 `try-catch` block 을 사용하여 에러 처리를 더 깔끔하게 할 수 있습니다.

try 블록 내부에 여러가지 비동기 작업들을 추가하고 에러가 발생할 시 catch 블록에서 에러에 대한 제어를 할 수 있습니다.

웹 프로그래밍에서 반드시 해야 할 작업 입니다.

db.js 에서 작업했던 유저 정보를 조회하는 API 입니다.

```javascript
// Search User ID
app.get('/users/:id', async (req, res) => {
  try {
    const userId = new ObjectId(req.params.id);
    const user = await collection.findOne({ _id: userId });
    if (!user) {
      return res.status(404).json({ error: '❌ Not Found User.' });
    }
    res.status(200).json(user);
  } catch (err) {
    res.status(500).json({ error: '❌ Failed Found User', details: err.message });
  }
});
```

로직 내부를 보면 try 블록 내부는 유저의 id 를 몽고DB 에서 조회하고 유저가 있으면 status code 200과 유저 정보를, 

유저가 없으면 stat code 404과 'Not Found User.' 메세지를 보냅니다.

그 외에 예상치 못한 오류가 발생하면 stat code 500과 'Failed Found User' 및 detail error 메세지를 사용자에게 보냅니다.


# HTTP 상태 코드

가끔 웹페이지나 어떤 서비스를 사용할 때 페이지가 정상적으로 작동하지 않으면 404 Not Found 혹은 500 어쩌구 저쩌구 라는 화면을 볼 수 있습니다.

이는 HTTP 상태 코드로 요청에 대한 서버의 응답상태를 식별하기 위한 코드 입니다.

3자리 숫자로 구성되며, 1번째 숫자는 유형을 나타내고, 2번째 숫자는 자세 내용을 정의합니다.


## HTTP 상태 코드 유형

### 1xx: 안내 (Informational)

요청이 성공적으로 받았다는 안내를 제공.

다음 작업을 계속해야 할지 알릴 때 사용.

**예제**:

* 100 Continue: 계속해서 요청 바로 보내도 된다는 의미.

* 101 Switching Protocols: 서버가 프로토콜 변경을 수신하여 실행했다는 의미.

### 2xx: 성공 (Successful)

요청이 성공적으로 처리되었을 때 사용.

**예제**:

* 200 OK: 성공적으로 요청을 처리했다.

* 201 Created: 요청으로 새 자산이 성공적으로 생성되었다.

* 204 No Content: 성공적으로 처리되었지만 보내지는 내용이 없다.

### 3xx: 이동 (Redirection)

요청을 완료하기 위해 다른 위치로 이동을 안내.

**예제**:

* 301 Moved Permanently: 요청한 자산이  \uC 영구적으로 이동했다.

* 302 Found: 일시적으로 다른 위치에 상속이 있음.

* 304 Not Modified: 요청한 자산이 이미 최신이면, 자동으로 캐스팅 파일을 사용.

### 4xx: 해당 시 오류 (Client Error)

사용자의 요청에 문제가 있을 때 사용.

**예제**:

* 400 Bad Request: 요청 문서가 잘못되어 서버가 이해할 수 없다.

* 401 Unauthorized: 인증 필요. 사용자가 이미 인증되지 않음.

* 403 Forbidden: 인증이 되었지만 조회권한이 없어 작업을 수행할 수 없음.

* 404 Not Found: 요청한 자산을 찾을 수 없음.

### 5xx: 서버 오류 (Server Error)

서버가 요청을 처리하는 중 오류가 발생했을 때 사용.

**예제**:

* 500 Internal Server Error: 서버 내부 오류.

* 502 Bad Gateway: 서버가 올바르지 않은 응답을 받음.

* 503 Service Unavailable: 서버가 성능 부족로 요청을 처리할 수 없음.