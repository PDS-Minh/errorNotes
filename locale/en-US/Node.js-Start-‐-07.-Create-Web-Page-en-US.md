# Index

* [Create Web Page](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-07.-Create-Web-Page-en-US#create-web-page)
  * [About HTML(Hyper Text Markup Language)?]()
  * [Create html file](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-07.-Create-Web-Page-en-US#create-html-file)
  * [CSS(Cascading Style Sheets)](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-07.-Create-Web-Page-en-US#csscascading-style-sheets)
* [Granting an Event](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-07.-Create-Web-Page-en-US#granting-an-event)
  * [Register a static file(index.html)](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-07.-Create-Web-Page-en-US#register-a-static-file-indexhtml)
  * [Creating a button control javascript](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-07.-Create-Web-Page-en-US#creating-a-button-control-javascript)

# Create Web Page 

## About HTML(Hyper Text Markup Language)?

> HTML (HyperText Markup Language) is a markup language that tells web browsers how to structure the web pages you visit. 
> It can be as complicated or as simple as the web developer wants it to be. HTML consists of a series of elements, 
> which you use to enclose, wrap, or mark up different parts of content to make it appear or act in a certain way. 
> The enclosing tags can make content into a hyperlink to connect to another page, italicize words, and so on

By [Mozilla document](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content/Basic_HTML_syntax)

Simply put, it is a document written so that the web page we created can be read by the browser.

If you go to any site in a web browser and press the F12 button, the developer window appears,

You can view the Elements tab to understand the html structure of the site.

![image](https://github.com/user-attachments/assets/56f685c1-6c09-4300-ab71-6e498f01d703)

## Create html file

The core of web programming is the screen.

For now, we're going to decorate a simple web page, but you can decorate it with a variety of frontend frameworks.

1. Open vscode.

2. Create index.html file.

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

The code above is the basic structure of html.

The items wrapped in `<>` are tags. Each tag has different functions.

If you have time, I recommend you to look at the mdn site and learn.

There is also a tutorial, so even beginners can easily follow it.

Link => [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML)

Let's create a site that manages the user information that we added here.

Let's add user management function tags to the `<body>` tag.

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

The `<div>` tag does not express anything; instead, it is used to group and group tags.
### h1

The `<h1>` tag represents highlighted text, such as the headline of the news.

You can adjust the font size by adjusting the numbers with h1, h2, h3, and so on. 

1The font size is the largest and the larger the number, the smaller the font size.

### form

The `<form>` tag is an area where you can interact, such as entering data to the user.

Usually, the input, button, and select tags are the elements that can be controlled from the web page.

### id

The id used in the html tagnet causes the tag value to have a unique id attribute.

main use

* You can easily find a specific id using javascript.

* When decorating html with css, you can apply a style to a specific id.

In '<formid="userForm">', give the form tag id "userForm".

### class

The role of class allows for common application across multiple elements.

main use

* Unlike id, duplicate names are assigned and used to work in batches.

In this way, you can declare the css style for each class and assign style to the desired element.

```html
<button class="add">Add</button>
<button class="edit">Edit</button>
<button class="delete">Delete</button>

```
```css
.add { background-color: green; color: white; }
.edit { background-color: blue; color: white; }
.delete { background-color: red; color: white; }

```

Let's run the index.html file.

Because the html file is a web document, it can run independently without the help of a server.

You can go to the Project folder and double-click index.html to see it right away in your browser.

![image](https://github.com/user-attachments/assets/593c9a81-3e08-47b3-9989-35e5b273e99f)

![image](https://github.com/user-attachments/assets/929a02dd-eeb8-4e2c-b8e9-bcb9eb5e27eb)

Right now, there is only a space on the white screen where you enter the letters and name, phone, and age.

Of course, it doesn't matter if you use it as it is, but CSS is a must to decorate a nice web page.

## CSS(Cascading Style Sheets)

The css described above is a style sheet language that describes how documents are displayed in HTML or XML.

There is also an MDN tutorial, so it would be nice to refer to it.

Link => [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)

Additionally, there is a site where you can write HTML, CSS, and JS codes directly from the web without installing them separately to see how the web page appears.

* [w3schools] (https://www.w3schools.com/) : You can learn basic things about the web, programming, and databases.

* [codepen] (https://codepen.io/) : You can see the results of the action directly on the web.

* [jsfiddle] (https://jsfiddle.net/) : Work results are available right on the web.

* [css selector] (https://flukeout.github.io/) : This is a site where you practice about css selector.

* [flex example] (https://flexboxfroggy.com/ #ko): This is a site where you practice about css flex.

An example of css is as follows.

```css
/* Apply all specific tag elements */
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

CSS must be written in the `<style>` tag.

Enter the following code inside the `<head>` tag.

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

If you close and reopen index.html, you will see that the screen is decorated differently than before.

![image](https://github.com/user-attachments/assets/fcb7b76b-3bda-47dd-85bf-68e19115118a)


# Granting an Event

Since the screen is decorated, you can control it with javascript to work with the DB.

Let's run the node.js server.

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

## Register a static file (index.html)

Additional action is required in the server code to open the index.html file using node.js.

Usually, static files are managed in a folder called public.

Create a public folder and move the index.html file to drag & drop.

![image](https://github.com/user-attachments/assets/c6210209-5faf-4d2d-adc0-dd49228b2664)

Let's open the user.js file.

To add a path with a static file on the server, apply the following code.

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

Gets the path and url packages and specifies the public path.

And I set the express to return the index.html document when a request is received via the / (root) path.

This setting allows you to open the html file using node.js without running the index.html file directly.

![image](https://github.com/user-attachments/assets/3802bed2-c448-4797-b6db-4463b732f8f1)

> 💡Tip
>
> At the end of url / the text is usually hidden.
> So if you type localhost:3000/url, the browser only shows localhost:3000.

## Creating a button control javascript

If you click the Add User button in this state, nothing will happen.

Because I didn't set up what the Add User button does.

Let's create an app.js file in the public folder.

The `<script src="app.js"></script>` in index.html is this scrap tag, which is the element for retrieving javascript files from html.

You don't need to connect with Mongodb in app.js because we already connected with Mongodb in db.js and designated it as API in user.js.

As described in css, you can control the html element in javascript by using the id or class name.

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

If you're curious about the item document, press `F12` in your web browser to get developer mode.

There is a console window at the bottom, and if you type document here, you can see that the index.html element that we created appears.

![image](https://github.com/user-attachments/assets/6615de63-ded2-4df3-b3a3-61d3355ff141)

If you're curious about the HTML structure of a web page, click the arrow to the left of each HTML tag to expand the child nodes.

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

In the fetchUsers method, fetch makes a request to the REST API.

If you don't make any special settings, I will make a GET request by default.

If you want to see network communication visually, you can check it by clicking the Network tab in the developer tool.

![image](https://github.com/user-attachments/assets/9f4ba3d4-5a4b-4615-b8e2-b485c6ccd762)

When communication is successful, the displayUsers method draws a user list.

You can create html tags with document.createElement.

You can use parentNode.appendChild to add a child Node to the parent Node.

### Add & Update User
Add an event to the format tag. You can assign an event to the html tag using the addEventListener.

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

Let me re-register Jhon's information.

Write down your name, number, age, and press the Add User button to register.

![image](https://github.com/user-attachments/assets/da5a0f6d-fdad-4cea-9f1b-943b3d91eac6)

Next, I'll also revise the information.

1. When you press the Edit button, the user's information is entered into the input.

2. Enter the information you want to modify.

3. Press the Edit User button to modify Jhon's information.

Before the modification

![image](https://github.com/user-attachments/assets/b4b0ff85-f105-48e7-8f47-c8c3e70669be)

After the modification

![image](https://github.com/user-attachments/assets/048b726f-1885-43d3-bc0e-3fe081405d88)

### Delete User

This is the last gateway.

Add a method for deleting users.

```javascript
// 사용자 삭제
async function deleteUser(id) {
  await fetch(`${API_URL}/${id}`, { method: 'DELETE' });
  fetchUsers();
}
```

The displayUsers method I created above has already assigned an event for delete button
You don't need to do any additional work.

If you press the Delete button to delete Jhon's information, it will be deleted.

![image](https://github.com/user-attachments/assets/6f866f14-236e-46ee-a1bc-f9d06d79a450)

