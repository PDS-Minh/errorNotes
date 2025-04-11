# npm 사용하기

npm은 오픈소스 패키지 공유 저장소 입니다.

전 세계의 개발자들이 패키지를 공유하고 사용할 수 있습니다.

## Package 관리하기

npm 으로 프로젝트 및 package 를 관리하기 위해 package.json 파일에서 설정할 수 있습니다.

npm 명령어로 쉽게 생성할 수 있습니다.

터미널을 열고 `npm init` 을 입력합니다.

프로젝트 관리를 위한 항목들이 자동으로 생성 됩니다.

이 과정이 귀찮다면 `npm init -y` 옵션을 추가하여 건너뛸 수 있습니다.

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

탐색기에 package.json 파일이 생성된 것을 확인할 수 있습니다.

기본 생성된 package.json 내부 구조는 다음과 같습니다.

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

scripts 영역은 javascript 파일을 실행하는 영역으로 

`npm run test`, `npm run start` 등 사용자가 설정 한 명령어를 통해 javascript 파일을 실행할 수 있습니다.

테스트로 터미널에 npm run test 를 입력하면 다음과 같은 결과를 확인할 수 있습니다.

```
D:\my-test\nodejs-guide> npm run test

> nodejs-guide@1.0.0 test
> echo "Error: no test specified" && exit 1
```

터미널에 npm run start 를 입력하여 서버를 실행할 수 있습니다.

```
D:\my-test\nodejs-guide> npm run start

> nodejs-guide@1.0.0 start
> node server.js

listening on 8080
```

## Package 추가하기

npm 홈페이지에서 원하는 package를 검색 후 내 프로젝트로 다운로드 할 수 있습니다.

Link => https://www.npmjs.com/

날짜에 관련된 패키지를 추가해보겠습니다.

npm 사이트에서 dayjs 를 검색 후 제일 다운로드 수가 많은 패키지를 선택하겠습니다.

![image](https://github.com/user-attachments/assets/0a83a909-bcea-4854-99cb-afabd0efd381)

우측에 install 영역에 있는 `npm i dayjs` 를 복사합니다. 여기서 i 는 install의 약자 입니다.

그 다음, vs code 의 터미널에 복사 한 내용을 붙여넣기 후 실행 합니다.

```
D:\my-test\nodejs-guide> npm i dayjs

added 1 package, and audited 2 packages in 3s

found 0 vulnerabilities
```

설치가 완료되면 node_modules 폴더에 dayjs 패키지가 설치 된 것을 확인할 수 있습니다.

package.json 파일의 dependencies 항목에 dayjs 가 추가된 것을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/8227b681-7046-4aa0-9191-bebdf4599fbc)

## Package 사용하기

### 모듈 불러오기

javascript에서 모듈을 가져오는 방식은 크게 2가지 입니다.

1. require:

  * CommonJS 모듈 시스템에서 사용됩니다.
  * Node.js에서 기본적으로 지원합니다.
  * 파일을 런타임에 동적으로 로드할 수 있습니다.
  * module.exports를 사용하여 모듈을 내보냅니다.

```
const dayjs = require("dayjs");
```

2. import:

  * ES Modules(ESM)에서 사용됩니다.
  * JavaScript 표준에 정의된 모듈 시스템으로, 브라우저와 최신 Node.js에서 지원됩니다.
  * 정적 로딩 방식이며, 파일을 컴파일 단계에서 분석합니다.
  * export 또는 export default를 사용하여 모듈을 내보냅니다.

```
import dayjs from "dayjs";
```

모듈 설정 방식 또한 package.json 에서 설정을 할 수 있습니다.

```
{
  "type": "module" // "commonjs" or "module"
}
```

더 자세한 설명은 Node.js 공식 문서에 있습니다.

Node.js Type => https://nodejs.org/api/packages.html#type

CommonJS 와 ES Modules 방식의 주요 차이점 입니다.

| 특징        | CommonJS                  | ES Modules               |
|-----------|---------------------------|--------------------------|
| 가져오기      | require 함수 사용             | import 키워드 사용            |
| 내보내기      | module.exports            | export 또는 export default |
| 로드 시점     | 런타임에 동기적으로 로드             | 컴파일 단계에서 정적으로 분석         |
| 트리 셰이킹 지원 | ❌                         | ⭕                        |
| 환경        | Node.js에서 기본적으로 사용        | 브라우저와 Node.js에서 표준으로 사용  |
| 사용 방식     | 파일 경로에 확장자 생략 가능 (.js 기본) | .js 또는 .mjs 확장자 필요       |
| 호환성       | 오래된 Node.js 프로젝트와 호환      | 최신 JavaScript 환경에서 사용 가능 |

설명이 길었습니다. 이제 본격적으로 시작해보겠습니다.

Dayjs 사용 방법 예제는 다음과 같습니다.

```
dayjs('2018-08-08') // parse

dayjs().format('{YYYY} MM-DDTHH:mm:ss SSS [Z] A') // display

dayjs().set('month', 3).month() // get & set

dayjs().add(1, 'year') // manipulate

dayjs().isBefore(dayjs()) // query
```

이렇게 코드를 작성 해봅시다.

javascript 의 내장 객체로 날짜를 사용하는 방법은 new Date() 를 통해 사용할 수 있습니다.

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

javascript에서 현재 날짜를 가져오는 방법은 new Date()를 사용하여 가져올 수 있지만 

우리가 원하는 YYYY-MM-DD 형식이 아닌 다른 형태로 나옵니다.

코드 날짜 포멧을 만드는 커스텀 메서드 `dateFormat` 를 생성해줘야 합니다.

```
[test01.js]
import dayjs from "dayjs";

// Date 내장 객체
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

날짜를 표현하기 위해 9 줄의 코드가 소요된 반면, dayjs는 1 줄로 해결 됐습니다.

이처럼 사용자가 사용하기 쉽게 이미 만들어진 라이브러리를 사용하면 간단하게 해결할 수 있습니다.

그렇다고 패키지에만 너무 의존해서는 안됩니다.

## Node.js Start
- [Node.js start - 04. REST API](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-04.-REST-API)
- [Node.js Start - 05 정보보안](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-05.-information-security)
- [Node.js Start - 06 Connect Database](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-06.-Connect-Database)