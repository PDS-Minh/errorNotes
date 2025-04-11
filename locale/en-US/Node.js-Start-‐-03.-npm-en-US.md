# Use npm

npm is open-source package share repository.

Whole world developers are sharing package and using.

## Package managing

You can set it up in the package.json file to manage projects and packages at npm.

You can easily generate project with npm commands.

Open the termianl and input `npm init`;

Then, items for project management are automatically created. 

If this process is annoying, you can skip it by adding the option 'npm init -y'.

```
PS D:\my-test\nodejs-guide> npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (nodejs-guide)
version: (1.0.0)
description:
entry point: (server.js)
test command:
git repository:
keywords:
author:
license: (ISC)
About to write to D:\my-test\nodejs-guide\package.json:

{
  "name": "nodejs-guide",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server.js"
  },
  "author": "",
  "license": "ISC",
  "description": ""
}


Is this OK? (yes)
```

You can verify that the package.json file has been created in the Explorer.

The default generated package.json internal structure is as follows.

```
{
  "name": "nodejs-guide",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server.js"
  },
  "author": "",
  "license": "ISC",
  "description": ""
}
```

The scripts area is the area where you run the javascript file

You can run the javascript file using commands set by the user, such as 'npm run test' and 'npm run start'.

If you enter the `npm run test` in the terminal as a test, you can see the following results.

```
D:\my-test\nodejs-guide> npm run test

> nodejs-guide@1.0.0 test
> echo "Error: no test specified" && exit 1
```

If you enter the `npm run start` in the terminal, you can run the server.


```
D:\my-test\nodejs-guide> npm run start

> nodejs-guide@1.0.0 start
> node server.js

listening on 8080
```

## Add Package

You can search the package in the npm homepage and then installed package in your project.

Link => https://www.npmjs.com/

Let's installed about date package.

Find the `dayjs` and then click to result list.

![image](https://github.com/user-attachments/assets/0a83a909-bcea-4854-99cb-afabd0efd381)

Copy 'npm i dayjs' in the install area to the right, where i stands for install.

Next, paste and run the copy to the terminal of the vs code.

```
D:\my-test\nodejs-guide> npm i dayjs

added 1 package, and audited 2 packages in 3s

found 0 vulnerabilities
```

When installed finish, you can find the dayjs package in the node_modules folder. 

You can see that dayjs have been added to the dependencies entry in the package.json file.

![image](https://github.com/user-attachments/assets/8227b681-7046-4aa0-9191-bebdf4599fbc)

## Using Package

### Call module

There are two main ways to import modules from javascript.

1. require:

  * Use the CommonJS system.
  * Default support in the Node.js.
  * Files can be dynamically loaded at runtime.
  * Use module.exports to export modules.

```
const dayjs = require("dayjs");
```

2. import:

   * Used by ES Modules (ESM).
   * Module system defined in JavaScript standards, supported by browsers and the latest Node.js.
   * Static loading, which analyzes files in the compilation phase.
   * Export the module using export or export default.

```
import dayjs from "dayjs";
```

The module setting method can also be set in package.json.

```
{
  "type": "module" // "commonjs" or "module"
}
```

More detailed description is in the Node.js official document. 

Node.js Type => https://nodejs.org/api/packages.html#type

This is the main difference between CommonJS and Es Module

| Feature              | CommonJS                                             | ES Modules                                     |
|----------------------|------------------------------------------------------|------------------------------------------------|
| Import               | Use `require` Function                               | Use `import` keyword                           |
| Export               | module.exports                                       | `export` or `export default`                   |
| Load Point           | Dynamic Load in runtime                              | Static analysis during compile                 |
| Support Tree Shaking | ❌                                                    | ⭕                                              |
| Environment          | Use default with Node.js                             | Use as standard in browser and Node.js         |
| Use it               | Extensions can be omitted in file path (.js default) | Need to .js or .mjs Extensions                 |
| Compatibility        | Compatible with older Node.js projects               | Available in the latest JavaScript environment |

That was a long explanation. Let's get started.

Here is an example of how to use Dayjs.

```
dayjs('2018-08-08') // parse

dayjs().format('{YYYY} MM-DDTHH:mm:ss SSS [Z] A') // display

dayjs().set('month', 3).month() // get & set

dayjs().add(1, 'year') // manipulate

dayjs().isBefore(dayjs()) // query
```

Let's write the code as below.

The method of using the date as an embedded object in javascript is available through `new Date()`.

```
[test01.js]
import dayjs from "dayjs";

const todayNewDate = new Date();
const todayDayjs = dayjs().format('YYYY-MM-DD');

console.log('Today: ' + todayNewDate);
console.log('Today: ' + todayDayjs);

[terminal]
D:\my-test\nodejs-guide> node .\test01.js
Today: Wed Jan 08 2025 10:11:23 GMT+0900 (대한민국 표준시)
Today: 2025-01-08
```

You can import the current date from javascript using newDate(), 

but It comes in a different format than the YYYY-MM-DD format we want.

You must create a custom method `dateFormat` to create a code date format.

```
[test01.js]
import dayjs from "dayjs";

// Date Embedded Objects
const todayNewDate = new Date();
const year = todayNewDate.getFullYear();
const month = todayNewDate.getMonth() + 1;
const day = todayNewDate.getDate();
const dateFormat = (year, month, day) => {
  const tempMonth = month < 10 ? `0${month}` : month;
  const tempDay = day < 10 ? `0${day}` : day;
  return `${year}-${tempMonth}-${tempDay}`;
}

console.log('Today: ' + dateFormat(year, month, day));

// dayjs package
const todayDayjs = dayjs().format('YYYY-MM-DD');
console.log('Today: ' + todayDayjs);

[terminal]
D:\my-test\nodejs-guide> node .\test01.js
Today: 2025-01-08
Today: 2025-01-08
```

Show the date with 

It took **9** lines of code to express the date, while `dayjs` were solved with **1** line.

This can be easily solved by using a library that has already been created to make it easier for users to use.

But you shouldn't rely too much on the package.

## Node.js Start
- [Node.js start - 04. REST API](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-04.-REST-API-en-US)
- [Node.js start - 05. Information security](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-05.-information-security-en-US)