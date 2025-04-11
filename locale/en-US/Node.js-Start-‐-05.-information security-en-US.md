# Critical information security

The most important thing when developing a server is information security.

For example, information such as secret API keys or database information can be dangerous when exposed.

## Use .env file

One of the methods Node.js uses for information security is using the .env file.

Please right-click on the explorer and create a .env file.

![image](https://private-user-images.githubusercontent.com/105468224/405109379-a011fbba-a9cb-4e81-90b1-37763ec08ba7.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Mzc0NDk0MTYsIm5iZiI6MTczNzQ0OTExNiwicGF0aCI6Ii8xMDU0NjgyMjQvNDA1MTA5Mzc5LWEwMTFmYmJhLWE5Y2ItNGU4MS05MGIxLTM3NzYzZWMwOGJhNy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMTIxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDEyMVQwODQ1MTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT05Y2NjMzBhMmVkMDMyNTEwNzgzYjg2ZTAzY2QyM2ZmOGEzZmRhYjhkZDRkOWIzNWU0Njg1M2JiMTNlMmU5YjMxJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.VuEfks8J-cyIDIhhHRm2gggVwdY6HS7zdUYfYHVmqYM)
![image](https://private-user-images.githubusercontent.com/105468224/405109577-fa9af941-b82a-4e41-b92c-e45f209f6fba.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Mzc0NDk0MTYsIm5iZiI6MTczNzQ0OTExNiwicGF0aCI6Ii8xMDU0NjgyMjQvNDA1MTA5NTc3LWZhOWFmOTQxLWI4MmEtNGU0MS1iOTJjLWU0NWYyMDlmNmZiYS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMTIxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDEyMVQwODQ1MTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lODkyOTQxMmM0ODI2MTU5OGZlNTQ1MWJmMGViNmFjMjJhMGMwNDAzODNmOWNjMmE0ZDlmZjBlMmYxNWZkZjIzJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.SCxF8bI61dAQ-NZJTzCt7uw3VakHIn3cwuF8YT9a8CY)

And enter important information.

The key combines the English capital letters with _.

For example, Enter the secret database information.

```text
DB_HOST=localhost
DB_PORT=5432
DB_USER=myuser
DB_PASSWORD=mypassword
```

## Install dotenv

To read the contents of the .env file, you must install dotenv in the npm package.

Link => https://www.npmjs.com/package/dotenv

Open the terminal and type npm i dotenv.

## Call Secret information

When dotenv package install finished, go to your code

And import dotenv package.

You can enter process.env.[KEY] to get the secret information.

```javascript
import express from 'express';
import dotenv from 'dotenv'; // import dotenv package

// Load environment variables in .env file
dotenv.config();

const app = express();
const port = 3000;

// Use .env variables
const dbHost = process.env.DB_HOST;
const dbPort = process.env.DB_PORT;
const dbUser = process.env.DB_USER;
const dbPassword = process.env.DB_PASSWORD;

console.log('Database Configuration:');
console.log(`Host: ${dbHost}`);
console.log(`Port: ${dbPort}`);
console.log(`User: ${dbUser}`);
console.log(`Password: ${dbPassword}`);

app.get('/', (req, res) => {
res.send('Hello World!')
})

app.listen(port, () => {
console.log(`Example app listening on port ${port}`)
})
```

Running the javascript file allows you to retrieve the information you entered in the .env file.

```text
D:\my-test\nodejs-guide> node .\serverExpress.js
Gmail Password:  mysecretpassword123!@
Database Configuration:
Host: localhost
Port: 5432
User: myuser
Password: mypassword
Example app listening on port 3000
```