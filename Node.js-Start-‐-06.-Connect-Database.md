# 목차

* [Node.js 에서 MongoDB 사용하기](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-06.-Connect-Database#nodejs-%EC%97%90%EC%84%9C-mongodb-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)
  * [Postman 프로그램 설치](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-06.-Connect-Database#postman-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8-%EC%84%A4%EC%B9%98)
  * [DB 설정 파일 분리](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-06.-Connect-Database#db-%EC%84%A4%EC%A0%95-%ED%8C%8C%EC%9D%BC-%EB%B6%84%EB%A6%AC)
  * [mongodb 연결 & 종료 설정](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-06.-Connect-Database#mongodb-%EC%97%B0%EA%B2%B0--%EC%A2%85%EB%A3%8C-%EC%84%A4%EC%A0%95)
  * [users.js 파일 생성 및 DB 작업 API 생성](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-06.-Connect-Database#usersjs-%ED%8C%8C%EC%9D%BC-%EC%83%9D%EC%84%B1-%EB%B0%8F-db-%EC%9E%91%EC%97%85-api-%EC%83%9D%EC%84%B1)

본격적으로 MongoDB를 사용한 웹 프로그램을 시작해보겠습니다.

MongoDB 가이드도 추가했으니 먼저 가이드를 확인해주세요.

Link => [MongoDB-Guide](https://github.com/pmirnc-dev/pds-welcome/wiki/MongoDB-Guide)

# Node.js 에서 MongoDB 사용하기

Node.js 와 MongoDB 를 연결하기 위해 npm 에서 mongodb package를 설치해야합니다.

1. vscode를 열어줍니다.

2. Terminal 을 열고 `npm i mongodb` 를 입력하여 mongodb 를 설치합니다.

![image](https://github.com/user-attachments/assets/2154fed4-e55b-4fa9-a27d-a1085b844294)

## Postman 프로그램 설치

Postman 이란 REST API 통신을 테스트 할 수 있는 프로그램 입니다.

Link => [https://www.postman.com/downloads/](https://www.postman.com/downloads/)

설치 방법은 간단합니다. 

1. 각자 운영체제에 맞는 버전을 다운로드를 합니다.

![image](https://github.com/user-attachments/assets/c9ccc00d-ae7d-4bd8-b7ad-a4d44c74b6de)

2. 다운로드가 완료되면 설치 파일을 실행합니다.

![image](https://github.com/user-attachments/assets/986251d4-ea48-483f-97a0-6569c507da12)

설치 장면을 보여드리고 싶은데 저는 이미 프로그램이 설치돼어있어서 업데이트가 됐네요...

## DB 설정 파일 분리

db 관련 설정 파일을 생성하겠습니다.

하나의 파일에서 mongodb 를 연결하고 사용할 수 있지만, 설정 파일을 분리함으로써 코드 가독성을 높이고 유지보수에 용이합니다.

db.js 파일을 생성합니다.

## mongodb 연결 & 종료 설정

앞서 .env 를 사용하여 비밀 정보를 감추기로 했습니다.

.env 파일에 Database 이름과 Collection 이름을 추가해줍니다.
```
...
DB_NAME=mydatabase
COLLECTION_USERS=users
```

그리고 db.js에 아래와 같이 db 설정 코드를 작성합니다.
```javascript
// db.js
import { MongoClient } from 'mongodb';
import dotenv from 'dotenv';

dotenv.config();

// Setting MongoDB and URL
const dbHost = process.env.DB_HOST;
const dbPort = process.env.DB_PORT;
const dbName = process.env.DB_NAME;
const dbUrl = `mongodb://${dbHost}:${dbPort}/`;

// Create MongoDB Client
const client = new MongoClient(dbUrl);

// Database Connection Methon
export async function connectDB() {
  try {
    await client.connect();
    console.log("✅ Success to MongoDB Connection!");
    const db = client.db(dbName);
    return db;
  } catch (err) {
    console.error("❌ Failed to MongoDB Connection:", err);
    throw err;
  }
}

// Database Connection Close Methon
export async function closeDB() {
  try {
    await client.close();
    console.log("🔒 Close MongoDB Connection.");
  } catch (err) {
    console.error("❌ Failed to Close MongoDB Connection:", err);
  }
}



```

```javascript
const dbUrl = `'mongodb://${dbHost}:${dbPort}'`;
```

> 💡Tip
> 
> 위 코드에서 **backtick(``)** 은 새로운 문자열을 만들 때 좀 더 편리하게 사용할 수 있습니다. 
> 예시로, .env 에서 가져온 dbHost, dbPort 를 가져와 dbUrl을 만들려고 합니다. 
> 새로운 문자열 생성 방식을 비교해보겠습니다.

```javascript
// Old
const dbUrl = 'mongodb://' + dbHost + ':' + dbPort;

// New
const dbUrl = `'mongodb://${dbHost}:${dbPort}'`; 

// result => mongodb://localhost:27017
```

> 💡Tip
>
> connectDB 와 closeDB 메서드 앞에 있는 **export** 는 외부 파일에서 해당 메서드 혹은 변수에 접근할 수 있게 만드는 키워드입니다.
> 
> 사용 방법은 밑에 있습니다.


## users.js 파일 생성 및 DB 작업 API 생성

### users.js 파일 생성

기존에 만들었던 serverExpress.js 파일을 복사 후, users.js 라는 새로운 이름으로 변경해줍니다.

그리고 이 코드들을 제외한 나머지 내용들은 지워줍니다.

```javascript
import express from 'express';
import dotenv from 'dotenv';

dotenv.config();

const app = express();
const port = 3000;
```

### MongoDB 연결, 종료 메서드 가져오기

4 에서 추가한 MongoDB 연결, 종료 메서드를 가져오겠습니다. 

MongoDB 에서 ObjectId 값을 조회하기 위해 ObjectId 도 추가하겠습니다.

```javascript
...
import { connectDB, closeDB } from './db.js';
import { ObjectId } from 'mongodb';
```

port 변수 밑에 `app.use(express.json());` 를 추가합니다.

이 코드를 선언하면 Express 에서 JSON 형태의 요청을 파싱하기 위해 추가해줘야 합니다.

```javascript
app.use(express.json());
```

### Express & MongoDB Server Start

Express 서버를 실행할 때 MongoDB 연결을 시도하겠습니다.

```javascript
async function startServer() {
  try {
    const dbName = process.env.DB_NAME;
    db = await connectDB();
    collection = db.collection(dbName);
    
    app.listen(port, () => {
      console.log(`🚀 Running on http://localhost:${port}!`);
    });
  } catch (err) {
    console.error('❌ Server Start Error:', err);
  }
}
```

### Create & Find User
Compass 가 아닌 웹서버를 사용하여 유저를 추가해보겠습니다.

Node.js 가이드의 REST API 파트에서 설명했던 REST API 가 등장 할 차례입니다.

Link => [REST API](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-04.-REST-API#2-rest%EB%9E%80)

새로운 유저를 생성하기 위해 POST API 를 사용해야 합니다.

Express 를 사용하여 간편하게 REST API 를 설계할 수 있습니다.

```javascript
app.post('/users', async (req, res) => {
  try {
    const newUser = req.body;
    const result = await collection.insertOne(newUser);
    res.status(201).json({ message: '📥 Success Create User!', userId: result.insertedId });
  } catch (err) {
    res.status(500).json({ error: '❌ Failed Create User', details: err.message });
  }
});

```

app.메소드명 을 사용하여 GET, POST 등 메서드를 구분할 수 있고 

그 뒤에는 어떤 주소로 받을것인지 경로를 설정합니다.

외부에 노출 되더라도 어떤 작업을 하는지 알 수 없게 짧게 이름을 짓는게 좋습니다.

예시) **Create**
* ❌: POST /create/users
* ✅: POST /users

예시) **Read**
* ❌: GET /find/users?id=myid1234
* ✅: GET /users or /users?id=myid1234

예시) **Delete**
* ❌: DELETE /delete/users/id
* ✅: DELETE /users/id

아래와 같이 데이터를 저장하는 POST 와 조회하는 GET API를 추가해봅니다.

```javascript
import express from 'express';
import dotenv from 'dotenv';
import { connectDB, closeDB } from './db.js';
import { ObjectId } from 'mongodb';

dotenv.config();

const app = express();
const port = 3000;

app.use(express.json());

let db;
let collection;

async function startServer() {
  try {
    const users = process.env.COLLECTION_USERS;
    db = await connectDB();
    collection = db.collection(users);

    app.listen(port, () => {
      console.log(`🚀 Running on http://localhost:${port}!`);
    });
  } catch (err) {
    console.error('❌ Server Start Error:', err);
  }
}

// Create User
app.post('/users', async (req, res) => {
  try {
    const newUser = req.body;
    const result = await collection.insertOne(newUser);
    res.status(201).json({ message: '📥 Success Create User!', userId: result.insertedId });
  } catch (err) {
    res.status(500).json({ error: '❌ Failed Create User', details: err.message });
  }
});

// Search All User
app.get('/users', async (req, res) => {
  try {
    const users = await collection.find().toArray();
    console.log(users);
    res.status(200).json(users);
  } catch (err) {
    res.status(500).json({ error: '❌ Failed Search User', details: err.message });
  }
});

startServer();
```

```text
D:\my-test\nodejs-guide> node users.js
✅ Success to MongoDB Connection!
🚀 Running on http://localhost:3000!
```

### Test - Create

앞서 설치했던 Postman 프로그램을 실행합니다.

좌측 메뉴에서 + 버튼을 누르고 REST API basics 를 누르면 편리하게 REST API 테스트 템플릿이 생성됩니다.

![image](https://github.com/user-attachments/assets/5b22d94e-c562-414b-a444-44b7a43a029f)

위 사진과 같이 Variables에 공용 변수들을 세팅할 수 있습니다.

Initial value 와 Current Value 를 localhost:3000 으로 바꿔주고 `Ctrl + S` 를 눌러 변경사항을 저장해줍니다.

![image](https://github.com/user-attachments/assets/f8d00b3e-877c-405c-9c6f-aeea2f86e6ee)

1. Post 를 테스트하기 위해 좌측에서 Post data 를 클릭합니다.

2. 기본 설정되어 있는 주소를 지우고 `{{base_url}}/users` 로 수정해줍니다.

3. Body 를 클릭합니다.

4. raw 를 클릭합니다.

5. 입력 칸에 저장하고자 하는 정보를 JSON 형태로 입력합니다.
```json
{
	"name": "Jhon",
    "age": 31,
    "phone": "010-5555-6666",
    "hobby": [
        "youtube"
    ]
}
```
6. 우측에 send 버튼을 클릭하면 하단에 테스트 결과가 나타납니다.

![image](https://github.com/user-attachments/assets/23500df1-3a16-40db-be4a-f2889c999fff)

Compass 에서도 Jhon 이 추가 된 것을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/465e1826-d276-4968-bea3-bd395bb7133d)


### Test - Read

GET 메서드도 테스트 해봅시다.

1. 좌측에서 Get data 를 클릭하고 {{base_url}}/users 를 입력해줍니다.

2. Send 버튼을 클릭하면 하단에 유저 리스트가 나타납니다.

![image](https://github.com/user-attachments/assets/4bd692fc-8ee2-4464-bd2d-a543d601669a)


### nodemon 패키지 설치

터미널에서 실행한 서버를 Ctrl + C 를 눌러 종료시킬 수 있습니다.

서버 코드를 변경할때마다 계속 껐다 키는 일은 매우 귀찮으므로 새로운 패키지를 설치하여 

코드가 변경될 때 마다 서버를 재시작 할 수 있습니다.

1. Termianl 에 `npm install --save-dev nodemon` 을 입력하여 nodemon 패키지를 설치합니다.
2. 서버를 실행할 때 `nodemon users.js` 로 실행시킬 수 있습니다.
3. package.json 의 scripts 에는 다음과 같이 추가할 수 있습니다.

```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server.js",
    "start:express": "node serverExpress.js",
    "start:dev": "nodemon users.js"
  },
```

4. Terminal 에 npm run start:dev 를 입력하면 서버가 실행됩니다.

```
npm run start:dev

> nodejs-guide@1.0.0 start:dev
> nodemon users.js

[nodemon] 3.1.9
[nodemon] to restart at any time, enter `rs`
[nodemon] watching path(s): *.*
[nodemon] watching extensions: js,mjs,cjs,json
[nodemon] starting `node users.js`

✅ Success to MongoDB Connection!
🚀 Running on http://localhost:3000!
```

### 특정 유저 찾기

매번 전체 유저를 조회하기엔 서버 자원 낭비가 심하므로 Unique 값을 사용하여 유저를 찾아보겠습니다.

바로 _id 값이 기본으로 MongoDB 에서 생성해주는 Unique 값 입니다.

따로 Unique 값을 만들지 않을거라면 _id 를 사용하는게 간편합니다.

이 _id 는 특수한 상황이나 시간 값을 조합하여 암호화 한 값을 나타냅니다.

새로운 GET API 를 추가하겠습니다.

```javascript
// Search User ID
app.get('/users/:id', async (req, res) => {
  try {
    const userId = new ObjectId(req.params.id);
    // console.lod(req);
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

`/users/:id` 에서 `:id` 는 해당 위치에 id 값을 보내준다는 약속 입니다.

테스트를 할 때 `/users/67a023f6e4037912b6c68462` 로 GET 요청을 하면 `req.params.id` 에 `67a023f6e4037912b6c68462` 값이 담겨있는것을 확인할 수 있습니다.

`console.lod(req);` 를 추가하면 req 내부에 수많은 값이 있는 것을 확인할 수 있습니다.

1. Postman 에서 Get data 에 오른쪽에 ... 을 누릅니다.

![image](https://github.com/user-attachments/assets/0422a6a7-28d2-4d2c-ba38-f3413c959033)

2. Duplicate 를 누르면 해당 API 가 복사됩니다.

![image](https://github.com/user-attachments/assets/6add931f-d5db-4175-8fc0-136770d3dd15)

3. 이름을 바꾸고 저장합니다.

![image](https://github.com/user-attachments/assets/b249c57e-2000-43f0-96b9-f34a3817ef34)

4. api path의 내용을 바꾸고 Send 를 클릭하면 조회 결과를 볼 수 있습니다.

![image](https://github.com/user-attachments/assets/89f04817-10d1-4fe6-b0f1-f4111c46387f)

> 💡Tip
>
> Postman은 자동 저장기능이 있지만 베타버전이라 변경사항이 발생하면 수동 저장을 해줍시다.


### 유저 정보 수정

```javascript
// Update User Info
app.put('/users/:id', async (req, res) => {
  try {
    const userId = new ObjectId(req.params.id);
    const updateData = { $set: req.body };
    const result = await collection.updateOne({ _id: userId }, updateData);
    if (result.matchedCount === 0) {
      return res.status(404).json({ error: '❌ Not Found User' });
    }
    res.status(200).json({ message: '✏️ Success Patch User Info!' });
  } catch (err) {
    res.status(500).json({ error: '❌ Failed Patch User', details: err.message });
  }
});
```

PUT 메서드는 정보 갱신에 사용하는 메서드 입니다.

위 코드를 추가하고 Postman에서 Update data 를 열어줍니다.

Create 에서와 같이 Body > raw 를 선택해주고 JSON 형태로 수정하고자 하는 데이터를 입력해줍니다.

저는 Jhon 의 취미 데이터를 수정해주겠습니다.

수정 할 데이터를 JSON 형태로 넣어주고 PATH 를 수정 후 Send를 클릭합니다.

![image](https://github.com/user-attachments/assets/8bd22318-7e9f-4d41-9f7e-1f0275b78b4c)

Compass로 조회를 하면 Jhon 의 정보가 바뀐것을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/9b3e7bc0-1c99-4797-8a34-2cb01b822be9)

### 유저 정보 삭제

지금은 테스트이니 Hard Delete를 해보겠습니다.

Jhon 유저가 탈퇴를 했습니다. 이에 Jhon 의 정보를 삭제해야 합니다.

```javascript
// Delete User Info
app.delete('/users/:id', async (req, res) => {
  try {
    const userId = new ObjectId(req.params.id);
    const result = await collection.deleteOne({ _id: userId });
    if (result.deletedCount === 0) {
      return res.status(404).json({ error: '❌ Not Found User for Delete.' });
    }
    res.status(200).json({ message: '🗑️ Success Delete User!' });
  } catch (err) {
    res.status(500).json({ error: '❌ Failed Delete User', details: err.message });
  }
});
```

위 코드를 추가하고 Postman 에서 Delete data 를 선택합니다.

Path 정보를 수정해주고 send 를 클릭합니다.

![image](https://github.com/user-attachments/assets/71df3b82-b986-424b-857a-cc7fa550f33d)

삭제가 성공했으면 Compass 에서도 Jhon 의 정보가 사라진 것을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/e1f588b0-e3ee-495b-b6df-1199bbb12591)

