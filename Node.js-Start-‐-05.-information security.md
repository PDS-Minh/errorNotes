# Critical information security

우리가 서버 개발을 할 때 가장 중요한 것은 정보보안 입니다.

예를 들어 비밀 API 키나 데이터베이스의 정보 같은 노출되면 큰일나는 정보들 입니다.

## .env 파일 사용하기

Node.js 에서 정보보안을 위해 사용하는 방법 중 하나는 .env 파일을 사용하는 것 입니다.

탐색기에서 마우스 우클릭을 누르고 .env 파일을 생성합니다.

![image](https://private-user-images.githubusercontent.com/105468224/405109379-a011fbba-a9cb-4e81-90b1-37763ec08ba7.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Mzc0NDk0MTYsIm5iZiI6MTczNzQ0OTExNiwicGF0aCI6Ii8xMDU0NjgyMjQvNDA1MTA5Mzc5LWEwMTFmYmJhLWE5Y2ItNGU4MS05MGIxLTM3NzYzZWMwOGJhNy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMTIxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDEyMVQwODQ1MTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT05Y2NjMzBhMmVkMDMyNTEwNzgzYjg2ZTAzY2QyM2ZmOGEzZmRhYjhkZDRkOWIzNWU0Njg1M2JiMTNlMmU5YjMxJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.VuEfks8J-cyIDIhhHRm2gggVwdY6HS7zdUYfYHVmqYM)
![image](https://private-user-images.githubusercontent.com/105468224/405109577-fa9af941-b82a-4e41-b92c-e45f209f6fba.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Mzc0NDk0MTYsIm5iZiI6MTczNzQ0OTExNiwicGF0aCI6Ii8xMDU0NjgyMjQvNDA1MTA5NTc3LWZhOWFmOTQxLWI4MmEtNGU0MS1iOTJjLWU0NWYyMDlmNmZiYS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMTIxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDEyMVQwODQ1MTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lODkyOTQxMmM0ODI2MTU5OGZlNTQ1MWJmMGViNmFjMjJhMGMwNDAzODNmOWNjMmE0ZDlmZjBlMmYxNWZkZjIzJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.SCxF8bI61dAQ-NZJTzCt7uw3VakHIn3cwuF8YT9a8CY)

그리고 중요한 정보들을 입력해줍니다.

예시로 데이터베이스 정보를 입력하겠습니다.

```text
GMAIL_PASSWORD=mysecretpassword123!@#
DB_HOST=localhost
DB_PORT=5432
DB_USER=myuser
DB_PASSWORD=mypassword
```

## dotenv 설치

.env 파일의 내용을 읽어오려면 npm package 에 있는 dotenv 를 설치해야합니다.

Link => https://www.npmjs.com/package/dotenv

터미널을 열고 `npm i dotenv` 를 입력합니다.

## 비밀 정보 호출

설치가 끝나면 코드로 돌아가 dotenv package 를 가져옵니다.

process.env.[KEY] 를 입력하여 비밀 정보를 가져올 수 있습니다.

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

javascript 파일을 실행하면 .env 파일에 입력한 정보들을 불러올 수 있습니다.

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