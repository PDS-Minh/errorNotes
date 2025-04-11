# 목차

* [웹 화면 만들기](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-07.-Create-Web-Page#%EC%9B%B9-%ED%99%94%EB%A9%B4-%EB%A7%8C%EB%93%A4%EA%B8%B0)
  * [HTML(Hyper Text Markup Language)란?](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-07.-Create-Web-Page#htmlhyper-text-markup-language%EB%9E%80)
  * [html 파일 생성](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-07.-Create-Web-Page#html-%ED%8C%8C%EC%9D%BC-%EC%83%9D%EC%84%B1)
  * [CSS(Cascading Style Sheets)](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-07.-Create-Web-Page#csscascading-style-sheets)
* [Event 부여하기](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-07.-Create-Web-Page#event-%EB%B6%80%EC%97%AC%ED%95%98%EA%B8%B0)
  * [정적파일(index.html) 등록하기](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-07.-Create-Web-Page#%EC%A0%95%EC%A0%81%ED%8C%8C%EC%9D%BCindexhtml-%EB%93%B1%EB%A1%9D%ED%95%98%EA%B8%B0)
  * [버튼 제어 javascript 작성하기](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-07.-Create-Web-Page#%EB%B2%84%ED%8A%BC-%EC%A0%9C%EC%96%B4-javascript-%EC%9E%91%EC%84%B1%ED%95%98%EA%B8%B0)

# 웹 화면 만들기 

## HTML(Hyper Text Markup Language)란?

> HTML (Hypertext Markup Language,하이퍼텍스트 마크업 언어)는 프로그래밍 언어는 아니고, 우리가 보는 웹페이지가 어떻게 구조화되어 있는지 브라우저로 하여금 알 수 있도록 하는 마크업 언어입니다. 
> 이는 개발자로 하여금 복잡하게도 간단하게도 프로그래밍 할 수 있습니다. 
> HTML은 elements로 구성되어 있으며, 이들은 적절한 방법으로 나타내고 실행하기 위해 각 컨텐츠의 여러 부분들을 감싸고 마크업 합니다. 
> tags 는 웹 상의 다른 페이지로 이동하게 하는 하이퍼링크 내용들을 생성하거나, 단어를 강조하는 등의 역할을 합니다.

By [Mozilla document](https://developer.mozilla.org/ko/docs/Learn_web_development/Core/Structuring_content/Basic_HTML_syntax)

쉽게 말하면 우리가 만든 웹 페이지를 브라우저가 읽을 수 있도록 작성한 문서 입니다.

웹 브라우저에서 아무 사이트나 들어가 F12 버튼을 누르면 개발자 창이 나오는데,

Elements 탭에 보면 해당 사이트의 html 구조를 파악할 수 있습니다.

![image](https://github.com/user-attachments/assets/56f685c1-6c09-4300-ab71-6e498f01d703)

## html 파일 생성

웹 프로그래밍의 핵심은 바로 화면 입니다.

지금은 간단한 웹 페이지를 꾸며보겠지만 다양한 Frontend framework 를 사용하여 화려한 웹페이지를 꾸밀 수 있습니다.

1. vscode를 열어줍니다.

2. index.html 파일을 생성해줍니다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  
</body>
</html>
```

위 코드가 html 의 기본 구조 입니다.

<> 로 감싸져 있는 항목들이 tag 입니다. tag 별로 각자의 기능이 다릅니다.

시간이 되신다면 mdn 사이트를 보고 학습을 해보시는 것을 추천합니다.

튜토리얼도 있으니 초보자도 쉽게 따라할 수 있습니다.

Link => [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML)

여기에 우리가 추가를 했던 유저 정보를 관리하는 사이트를 만들어보겠습니다.

<body> 태그 안에 사용자 관리 기능 태그들을 추가해보겠습니다.

```html
<div class="container">
  <h1>User Management</h1>
  <form id="userForm">
    <input type="text" id="name" placeholder="Name" required>
    <input type="text" id="phone" placeholder="Phone..." required>
    <input type="number" id="age" placeholder="Age..." required>
    <button type="submit" class="add">Add User</button>
  </form>

  <div id="userList"></div>
</div>

<script src="app.js"></script>
```

### div

<div> 태그는 아무것도 표현하지 않습니다. 대신 태그들을 그룹화 하여 묶을 때 사용됩니다.

### h1

`<h1>`태그는 뉴스의 제목(Headline)과 같은 강조하는 텍스트를 표현합니다. 

h1, h2, h3 ... 으로 숫자를 조절하여 폰트의 크기를 조절할 수 있습니다. 

1이 폰트의 크기가 가장 크고 숫자가 커질수록 폰트의 크기는 작아집니다.

### form

<form> 태그는 사용자에게 데이터를 입력할 수 있는 등 상호작용을 할 수 있는 영역입니다.

보통 input, button, select 태그들이 웹 페이지에서 제어할 수 있는 요소들입니다.

### id

html 태그 네에 사용하는 id 는 해당 태그값이 고유한 id 속성을 지니게 합니다.

주 용도

* javascript 를 사용하여 특정 id 를 쉽게 찾을 수 있습니다.

* css 로 html 을 꾸밀 때 특정 id 에 스타일을 적용할 수 있습니다.

`<form id="userForm">` 에서 form tag 에 id "userForm" 을 부여해줍니다.

### class

class의 역할은 여러 요소에 공통적으로 적용할 수 있도록 합니다.

주 용도

* id 와 달리 중복으로 이름을 할당하여 일괄적으로 작업을 하기 위해 사용합니다.

이렇게 각 class 별로 css 스타일을 선언하고 원하는 element에 style을 부여할 수 있습니다.
```html
<button class="add">추가</button>
<button class="edit">수정</button>
<button class="delete">삭제</button>

```
```css
.add { background-color: green; color: white; }
.edit { background-color: blue; color: white; }
.delete { background-color: red; color: white; }

```

index.html 파일을 실행해보겠습니다.

html 파일은 웹 문서이기 때문에 서버의 도움 없이 단독으로 실행할 수 있습니다.

프로젝트 폴더로 이동하여 index.html 을 더블 클릭하면 브라우저에서 바로 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/593c9a81-3e08-47b3-9989-35e5b273e99f)

![image](https://github.com/user-attachments/assets/929a02dd-eeb8-4e2c-b8e9-bcb9eb5e27eb)

지금은 흰 화면에 글씨와 name, phone, age를 입력하는 칸만 있습니다.

물론 이대로 사용해도 상관은 없지만 멋진 웹페이지를 꾸미기 위해 반드시 필요한 것이 CSS 입니다.

## CSS(Cascading Style Sheets)

위에서 설명한 css 는 HTML 이나 XML로 작성된 문서의 표시 방법을 기술하기 위한 스타일 시트 언어입니다.

이 또한 MDN 튜토리얼이 있으니 참고해보면 좋을 것 같습니다.

Link => [CSS](https://developer.mozilla.org/docs/Web/CSS)

추가로 별도의 설치 없이 웹에서 바로 HTML, CSS, JS 코드를 작성하여 웹페이지가 어떻게 나타나는지 확인할 수 있는 사이트가 있습니다.

* [w3schools](https://www.w3schools.com/): 웹 및 프로그래밍, 데이터베이스 관련 기초 학습을 할 수 있습니다.

* [codepen](https://codepen.io/): 작업 결과를 웹에서 바로 확인할 수 있습니다.

* [jsfiddle](https://jsfiddle.net/): 작업 결과를 웹에서 바로 확인할 수 있습니다.

* [css selector](https://flukeout.github.io/): css selector 에 대해 연습하는 사이트 입니다.

* [flex example](https://flexboxfroggy.com/#ko): css flex 에 대해 연습하는 사이트 입니다.

css 예시는 다음과 같습니다.

```css
/* 특정 태그 요소들 모두 적용*/
div {
  background-color: green;
}

/* id */
#userForm {
  width: 300px;
}

/* class */
.container {
  width: 90%;
  background-color: gray;
}
```

CSS 는 <style> 태그 안에 작성을 해야 합니다.

`<head>` 태그 내부에 다음 코드를 입력해봅시다.

```css
<style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f9f9f9;
      margin: 0;
      padding: 20px;
    }
    .container {
      max-width: 600px;
      margin: auto;
      background: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    }
    h1 {
      text-align: center;
      color: #333;
    }
    form {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    input {
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    button {
      padding: 10px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    button.add {
      background-color: #4CAF50;
      color: white;
    }
    button.edit {
      background-color: #2196F3;
      color: white;
    }
    button.delete {
      background-color: #f44336;
      color: white;
    }
    .user-card {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 15px;
      border: 1px solid #ccc;
      border-radius: 4px;
      margin-top: 10px;
    }
    .user-details {
      flex: 1;
    }
    .user-actions {
      display: flex;
      gap: 10px;
    }
  </style>
```

index.html 을 닫고 다시 열면 아까와는 다르게 화면이 꾸며져 있는 것을 볼 수 있습니다.

![image](https://github.com/user-attachments/assets/fcb7b76b-3bda-47dd-85bf-68e19115118a)


# Event 부여하기

화면이 꾸며졌으니 DB와 연동작업을 하기 위해 javascript 로 제어를 할 수 있습니다.

node.js 서버를 실행해보겠습니다.

```text
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

## 정적파일(index.html) 등록하기

node.js 를 사용하여 index.html 파일을 열기 위해 서버 코드에 추가 작업이 필요합니다.

보통 정적인 파일들을 public 이란 폴더에서 관리 합니다.

public 폴더를 만들고 index.html 파일을 drag & drop 으로 이동시켜줍니다.

![image](https://github.com/user-attachments/assets/c6210209-5faf-4d2d-adc0-dd49228b2664)

users.js 파일을 열어줍시다.

서버에 정적 파일이 있는 경로를 추가하기 위해 다음 코드를 적용해봅니다.

```javascript
...
import { ObjectId } from 'mongodb';
import path from 'node:path';
import { fileURLToPath } from 'node:url';

...

const app = express();
const port = 3000;

// __dirname setting 
const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

app.use(express.json());

// set static file(public folder)
app.use(express.static(path.join(__dirname, 'public')));

// Provide index.html on root URL request
app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'index.html'));
});

```

path 와 url 패키지를 불러와 public 경로를 지정해줍니다.

그리고 express 에 / (root) 경로로 요청이 들어오면 index.html 문서를 반환하도록 설정했습니다.

이렇게 설정하면 index.html 파일을 직접 실행하지 않고 node.js를 사용하여 html 파일을 열 수 있습니다.

![image](https://github.com/user-attachments/assets/3802bed2-c448-4797-b6db-4463b732f8f1)

> 💡Tip
>
> url 끝에 / 문자는 보통 숨김처리가 됩니다. 
> 그래서 localhost:3000/ url 을 입력하면 브라우저에서는 localhost:3000 만 보여줍니다.

## 버튼 제어 javascript 작성하기

지금 상태에서 Add User 버튼을 클릭하면 아무 일도 벌어지지 않습니다. 

왜냐하면 Add User 버튼이 어떤 역할을 하는지 설정해주지 않았기 때문이죠.

public 폴더 안에 app.js 파일을 만들어보겠습니다.

index.html 에 있던 `<script src="app.js"></script>` 바로 이 sciprt 태그가 바로 html 에서 javascript 파일을 불러오기 위한 요소 입니다.

app.js 에서는 Mongodb와 연결을 할 필요가 없습니다. 이미 우리는 db.js 에서 Mongodb와 연결을 했고 users.js 에서 API로 지정을 했기 때문이죠.

css 에서 설명했듯이 id 나 class 이름을 사용하여 javascript 에서 html 요소를 제어할 수 있습니다.

```javascript
// public/app.js
const API_URL = 'http://localhost:3000/users';
const userForm = document.getElementById('userForm');
const nameInput = document.getElementById('name');
const phoneInput = document.getElementById('phone');
const ageInput = document.getElementById('age');
const userList = document.getElementById('userList');
let editingUserId = null;
```

document 라는 항목이 궁금하다면, 웹 브라우저에서 F12 를 누르면 개발자 모드가 나옵니다.

하단에 console 창이 있는데 여기에 document 를 입력하면 우리가 만들었던 index.html 요소가 나오는 것을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/6615de63-ded2-4df3-b3a3-61d3355ff141)

웹 페이지의 HTML 구조가 궁금하다면 HTML 태그별로 좌측에 있는 화살표를 클릭하면 자식 node 들이 확장됩니다.

### Read User List
```javascript
// Load User List
async function fetchUsers() {
  const response = await fetch(API_URL);
  const users = await response.json();
  displayUsers(users);
}

// Display User List
function displayUsers(users) {
  userList.innerHTML = '';
  for (const user of users) {
    const userCard = document.createElement('div');
    userCard.className = 'user-card';

    const userDetails = document.createElement('div');
    userDetails.className = 'user-details';
    userDetails.innerHTML = `<strong>${user.name}</strong><br>${user.phone} / ${user.age}`;

    const userActions = document.createElement('div');
    userActions.className = 'user-actions';

    const editButton = document.createElement('button');
    editButton.className = 'edit';
    editButton.textContent = 'Edit';
    editButton.onclick = () => editUser(user);

    const deleteButton = document.createElement('button');
    deleteButton.className = 'delete';
    deleteButton.textContent = 'Delete';
    deleteButton.onclick = () => deleteUser(user._id);

    userActions.appendChild(editButton);
    userActions.appendChild(deleteButton);

    userCard.appendChild(userDetails);
    userCard.appendChild(userActions);
    userList.appendChild(userCard);
  }
}
```

fetchUsers 메서드에서 fetch 는 REST API로 요청을 합니다.

특별한 설정을 해주지 않는다면 기본으로 GET 요청을 합니다.

네트워크 통신을 눈으로 확인하고 싶으면 개발자 도구에서 네트워크 탭을 눌러 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/9f4ba3d4-5a4b-4615-b8e2-b485c6ccd762)

통신이 성공하면 displayUsers 메서드에서 유저 리스트를 그려주는 역할을 합니다.

document.createElement 로 html 태그를 생성할 수 있습니다.

parentNode.appendChild 를 사용하여 부모 Node 에 자식 Node 로 추가할 수 있습니다.

### Add & Update User
Form tag 에 이벤트 추가해줍니다. addEventListener 를 사용하여 html tag 에 이벤트를 부여할 수 있습니다.

```javascript
// Add or Update User
userForm.addEventListener('submit', async (e) => {
  e.preventDefault();
  const user = { name: nameInput.value, phone: phoneInput.value };

  if (editingUserId) {
    await fetch(`${API_URL}/${editingUserId}`, {
      method: 'PUT',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(user),
    });
    editingUserId = null;
    userForm.querySelector('button').textContent = 'Add user';
  } else {
    await fetch(API_URL, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(user),
    });
  }

// reset input values
  nameInput.value = '';
  phoneInput.value = '';
  ageInput.value = '';
  fetchUsers();
});


// User Edit Mode
function editUser(user) {
  nameInput.value = user.name;
  phoneInput.value = user.phone;
  ageInput.value = user.age;
  editingUserId = user._id;
  userForm.querySelector('button').textContent = 'Edit User';
}
```

Jhon 의 정보를 다시 등록해보겠습니다.

이름, 번호, 나이를 적고 Add User 버튼을 누르면 등록이 됩니다.

![image](https://github.com/user-attachments/assets/da5a0f6d-fdad-4cea-9f1b-943b3d91eac6)

이어서 정보 수정도 해보겠습니다.

1. Edit 버튼을 누르면 input 안에 유저의 정보가 입력이 됩니다.

2. 수정할 정보를 입력합니다.

3. Edit User 버튼을 누르면 Jhon의 정보가 수정이 됩니다.

수정 전

![image](https://github.com/user-attachments/assets/b4b0ff85-f105-48e7-8f47-c8c3e70669be)

수정 후

![image](https://github.com/user-attachments/assets/048b726f-1885-43d3-bc0e-3fe081405d88)

### Delete User

마지막 관문 입니다.

사용자 삭제를 위한 메서드를 추가합니다.

```javascript
// 사용자 삭제
async function deleteUser(id) {
  await fetch(`${API_URL}/${id}`, { method: 'DELETE' });
  fetchUsers();
}
```

위에서 만들었던 displayUsers 메서드에서 이미 delete button 에 대한 이벤트를 부여했기 때문에
추가로 작업을 할 필요는 없습니다.

Jhon 의 정보를 Delete 하기 위해 Delete 버튼을 누르면 삭제됩니다.

![image](https://github.com/user-attachments/assets/6f866f14-236e-46ee-a1bc-f9d06d79a450)

