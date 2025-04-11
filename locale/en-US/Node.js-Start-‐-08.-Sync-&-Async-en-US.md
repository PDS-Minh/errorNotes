# Index

* [Synchronous? & Asynchronous?](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async-en-US#synchronous--asynchronous)
  * [Synchronous Programing](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async-en-US#synchronous-programing)
  * [Asynchronous Programing](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async-en-US#asynchronous-programing)
* [Asynchronous of Javascript](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async-en-US#asynchronous-of-javascript)
  * [Callback](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async-en-US#callback-pattern)
  * [Promise](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async-en-US#promise)
  * [Async & Await](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async-en-US#async--await)
* [Tip - HTTP Status Code](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-08.-Sync-&-Async-en-US#tip---http-status-code)

# Synchronous? & Asynchronous? 

Earlier, we created a web page for simple user management.

Thank you so much for following me well.

I think I have a lot of questions, so I prepared additional supplementary materials.

It's about synchronization, asynchronous.

Imported some of the codes written by `app.js`.

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

If you look at the code above, you can see the keyword `async` or `await` before the function or variable.

If you already have a headache, it's normal.

First of all, I will forget the above and proceed slowly from the beginning.

## Synchronous Programing

Synchronous programming is a method in which you cannot perform one task before it is completed.

Let me give you an example.

```javascript
// Task1
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// Task2
console.log('Finish!');
```

Usually, javascript reads and executes a line from top to bottom of the code unless there is a specific command.

This is called an interpreter. Since this is knowledge related to computer science, it would be good to look for it if you have a chance later.

Interpreting the example codes in order is expected to output 0, 1, 2, 3, 4 and then Finish!.

'console.log('Finish!');' cannot be executed until the for loop is completely finished.

Simply put, synchronous programming can only do one thing at a time.

After Task 1 at the top, continue Task 2 at the bottom.

This is the most obvious method for programs where the order of action is important, but if the previous task is not finished, the later task will continue to wait.

![sync](https://github.com/user-attachments/assets/42d0bd67-d47a-49e5-b968-8fceba392deb)

## Asynchronous Programing

Asynchronous programming allows multiple tasks to be performed simultaneously without waiting in order.

Let's look at the example code.

```javascript
setTimeout(() => {
  console.log('Hi~!');
}, 1000);

console.log('bye~!');
```
setTimeout is a built-in function of javascript, which is often used to delay tasks.

The unit of seconds is expressed in ms, and 1000 is 1 second.

For synchronization programs, Hi~! should be output first and Bye~! should be output first.

However, when the above code is executed, Bye~! is output first and Hi~! is output one second later.

![async](https://github.com/user-attachments/assets/9302da11-4c49-41ed-99f3-8e98c8297437)

### Benefits of Asynchronous Programs

I'll explain it by comparing YouTube.

I searched chill guy, a meme that is popular in Korea these days.

![async example](https://github.com/user-attachments/assets/a8571e20-f73f-4dd9-9f64-62068d472a7f)

My prediction is the API that brings the list of chill guy related shorts and the API that brings the list of videos,

There will be a lot of request apps such as API to get chill guy update information from one channel of subscription.

You can check it by turning on the developer tool, so it would be good to check it.

Bringing all these requests in order will make YouTube viewers feel frustrated and angry or turn off the app.

Asynchronous programs are used to prevent such accidents.

You can run multiple requests at once and show them quickly from the completion of the request.

# Asynchronous of Javascript

Let me briefly explain the asynchronous history in Javascript.

## Callback Pattern

Before Promise appeared in the past, we used the Callback pattern to handle asynchronous events.

A callback pattern is a method of transferring functions that are called after an asynchronous operation is completed.

The more work you do, the more complicated the code and the less readable callback hell you get.

It is also difficult to handle errors when errors occur.

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

This is Promise.

Use .then(), .catch(), to clean up asynchronous tasks to avoid callback hell as objects that indicate completion or failure of asynchronous tasks.

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

With Callback, it is clearly readable and can manage asynchronous tasks in its own way.

## Async & Await

I don't like this because it's complicated! I like something more concise!

It's just something I made up and it's the grammar of ES2017 that appeared to make it easier to use promis.

Asynchronous code can be written as easily as synchronous code.

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

Readability has been improved and error handling can be made cleaner using the `try-catch` block.

You can add a number of asynchronous tasks inside the try block and control the error in the catch block when an error occurs.

This is a must-do in web programming.

API that queries user information that was worked on by db.js.

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

If you look inside the logic, the inside of the try block looks up the user's id in MongoDB, and if there is a user, the status code 200 and user information are displayed,

If you don't have a user, send the stat code 404 and the message 'Not Found User.'

In addition, if an unexpected error occurs, a stat code 500, a 'Failed Found User', and a detail error message are sent to the user.


# Tip - HTTP Status Code

Sometimes when you use a web page or some service, if the page doesn't work properly, you'll see a screen called 404 Not Found or 500 something.

This is the HTTP status code to identify the server's response status to the request.

It consists of three digits, the first number represents the type, and the second number defines the posture content.


## HTTP status code type

### 1xx: Informational

Provides guidance that your request has been received successfully.

Used to inform whether to continue with the next task.

**Example**:

* 100Continue—Means that you can continue sending requests immediately.

* 101 Switching Protocols—Means that the server has received and executed a protocol change.

### 2xx: Successful

Used when a request is successfully processed.

**Example**:

* 200 OK: Successfully processed your request.

* 201 Created: A new asset was successfully created by request.

* 204 No Content: Processed successfully, but nothing is sent.

### 3xx: Redirection

Directs you to a different location to complete your request.

**Example**:

* 301 Moved Permanently: The requested asset has been moved permanently.

* 302 Found: Inheritance temporarily in another location.

* 304 Not Modified: If the requested asset is already up to date, use the casting file automatically.

### 4xx: Client Error

Used when there is a problem with the user's request.

**Example**:

* 400 Bad Request: The request document is incorrect and the server cannot understand.

* 401 Unauthorized: Authentication required. User is not already authenticated.

* 403 Forbidden: Authenticated but unable to perform the operation because you do not have lookup rights.

* 404 Not Found: The requested asset could not be found.

### 5xx: Server Error

Used when an error occurred while the server was processing the request.

**Example**:

* 500 Internal Server Error: Server internal error.

* 502 Bad Gateway: The server receives an incorrect response.

* 503 Service Unavailable: The server is unable to process the request due to insufficient performance.