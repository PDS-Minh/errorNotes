# REST API 란?

우리가 웹 페이지를 사용할 때 주소창을 보면 / 로 구분 된 url 주소를 볼 수 있습니다.

google 사이트에서 `node.js` 를 검색했습니다.

`node.js` 검색 결과를 확인할 수 있고 화면 최 상단에 url 주소가 바뀐 것을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/7332c449-6cff-4c4b-9be2-ccc96581eca9)

기존
```
https://www.google.com
```

검색
```
https://www.google.com/search?q=node.js&newwindow=1&sca_esv=e993029fa676fbb3&sxsrf=ADLYWIK2OxMce_N5zoEuJgUmDXymFN_t6A%3A1736842647552&source=hp&ei=lx2GZ_ujH-60vr0PxOjHyAo&iflsig=AL9hbdgAAAAAZ4Yrpy5wOwYuOQYOsMGpkqJyShQaVjIR&ved=0ahUKEwi7y6SI4_SKAxVumq8BHUT0EakQ4dUDCBk&uact=5&oq=node.js&gs_lp=Egdnd3Mtd2l6Igdub2RlLmpzMgoQIxiABBgnGIoFMgoQABiABBgUGIcCMgUQABiABDIFEAAYgAQyBRAAGIAEMgUQABiABDIFEAAYgAQyBRAAGIAEMgUQABiABDIFEAAYgARIuiVQpRRYsiNwAngAkAEAmAGEAaABngaqAQMwLje4AQPIAQD4AQGYAgmgArcGqAIKwgIHECMYJxjqAsICDRAuGNEDGMcBGCcY6gLCAgQQIxgnwgIREC4YgAQYsQMY0QMYgwEYxwHCAgsQABiABBixAxiDAcICChAAGIAEGEMYigXCAgsQLhiABBixAxiDAcICCBAAGIAEGLEDwgIEEAAYA5gDB_EFc0wCkxLbBk6SBwMyLjegB7g7&sclient=gws-wiz
```

위 내용을 개발자도구를 사용하여 확인할 수 있습니다.

```
q: node.js
newwindow: 1
sca_esv: e993029fa676fbb3
sxsrf: ADLYWIKqyVzzD8u6Dy3lvCOu9PIpPRq8Ww:1736842654007
ei: nh2GZ4QU8qS-vQ-nsMPoBQ
ved: 0ahUKEwiE27CL4_SKAxVykq8BHSfYEF0Q4dUDCBA
oq: node.js
gs_lp: Egxnd3Mtd2l6LXNlcnAiB25vZGUuanNIAFAAWABwAHgBkAEAmAEAoAEAqgEAuAEMyAEAmAIAoAIAmAMAkgcAoAcA
sclient: gws-wiz-serp
```

서버에 요청을 하기 위해 정해진 경로와 데이터를 전달해야 합니다.

## 1. API란?

API 는 Application Programming Interface 의 약자로, 프로그램 간의 소통을 도와주는 인터페이스 입니다.

API는 식당의 메뉴판과 같습니다.

예를 들어, 음식점에 가면 메뉴판을 보고 음식을 주문하죠. 하지만 어떻게 요리가 만들어지는지는 알 필요가 없습니다.

마찬가지로, API를 통해 우리는 원하는 데이터를 요청(Request)하고, 결과(Response)를 받을 수 있습니다.

## 2. REST란?

REST는 "Representational State Transfer"의 약자입니다. 웹 상에서 데이터를 주고받기 위한 원칙과 규칙입니다.

### REST의 기본 원칙

1. 자원(Resource) 기반 설계
  * 모든 데이터는 자원(resource)으로 표현됩니다.
  * 예를 들어, 사용자가 하나의 자원이고, 게시물도 하나의 자원입니다.

2. HTTP 메서드 사용
  * REST API는 자원을 다룰 때 HTTP 메서드를 사용합니다.
  * 주요 메서드는 다음과 같습니다:
    * GET: 데이터를 조회
      * 예: 사용자 목록을 가져오기
    * POST: 데이터를 생성
      * 예: 새로운 사용자 추가하기
    * PUT: 데이터를 수정
      * 예: 사용자의 정보를 업데이트
    * DELETE: 데이터를 삭제
      * 예: 사용자를 삭제하기

3. URI로 자원을 표현
  * 각 자원은 고유한 URL로 식별됩니다.
  * 예:
    * 사용자 목록: https://example.com/users
    * 특정 사용자: https://example.com/users/123

4. Stateless(상태가 없음)
  * 서버는 클라이언트의 상태를 기억하지 않습니다.
  * 클라이언트가 필요한 모든 정보를 요청에 포함해야 합니다.

## 3. REST API란?
REST의 원칙을 따르는 API를 REST API라고 부릅니다.
REST API는 클라이언트와 서버가 데이터를 주고받을 때 사용됩니다.

예시:
  * 우리가 사용하는 웹사이트나 앱(예: 쇼핑몰, 소셜 미디어)은 대부분 REST API로 동작합니다.
  * 클라이언트: 브라우저나 앱
  * 서버: 데이터베이스와 비즈니스 로직이 있는 곳

## 4. REST API의 실제 동작 예시
  ### 예: 블로그 게시물을 다루는 REST API
    * GET 요청: https://example.com/posts
      → 모든 게시물을 가져옵니다.

    * GET 요청: https://example.com/posts/1
      → ID가 1인 게시물을 가져옵니다.

    * POST 요청: https://example.com/posts
      → 새로운 게시물을 추가합니다. (요청 본문에 게시물 내용 포함)

    * PUT 요청: https://example.com/posts/1
      → ID가 1인 게시물을 수정합니다.

    * DELETE 요청: https://example.com/posts/1
      → ID가 1인 게시물을 삭제합니다.

## 5. REST API를 왜 사용할까요?

1. 표준화
  * 모든 시스템이 같은 방식으로 데이터를 주고받기 때문에 쉽게 통합 가능.
2. 확장성
  * 서버와 클라이언트를 독립적으로 개발할 수 있음.
3. 유연성
  * 다양한 클라이언트(브라우저, 모바일 앱)에서 사용 가능.

# REST API 사용해보기

## 1. express 설치

express는 Node.js 를 위한 빠르고 간결한 웹 프레임워크 중 하나로 쉽게 서버를 구성할 수 있는 패키지를 제공하는 프레임워크입니다.

vscode 에서 새 터미널을 열어줍니다.

`npm i express` 를 입력하여 express 패키지를 설치합니다.

package.json파일의 dependencies 에 express 가 설치된 것을 확인할 수 있습니다.

```json
{
  "dependencies": {
    "express": "^4.21.2"
  }
}
```

## 2. 서버 실행하기

express 를 사용하여 웹 서버를 만들어보겠습니다.

express 공식문서의 예제는 다음과 같습니다.

[serverExpress.js]
``` javascript
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```

저는 새로운 파일 serverExpress.js 를 만들고 여기에 예제의 내용을 입력하겠습니다.

터미널에서 node serverExpress.js 를 입력하여 서버를 실행 할 수도 있고 package.json 의 scripts에 실행 명령어를 추가할 수도 있습니다.

저는 scripts에 express 실행 파일을 추가했습니다.

[package.json]
```json

{
  "scripts": {
    "start:express": "node serverExpress.js"
  }  
}

```

`start:express` 를 실행해보겠습니다.

```
Executing task: npm run start:express 


> nodejs-guide@1.0.0 start:express
> node serverExpress.js

file:///D:/my-test/nodejs-guide/serverExpress.js:1
const express = require('express')
                ^

ReferenceError: require is not defined in ES module scope, you can use import instead
This file is being treated as an ES module because it has a '.js' file extension and 'D:\my-test\nodejs-guide\package.json' contains "type": "module". To treat it as a CommonJS script, rename it to use the '.cjs' file extension.
    at file:///D:/my-test/nodejs-guide/serverExpress.js:1:17
    at ModuleJob.run (node:internal/modules/esm/module_job:222:25)
    at async ModuleLoader.import (node:internal/modules/esm/loader:316:24)        
    at async asyncRunEntryPointWithESMLoader (node:internal/modules/run_main:123:5)
```

오류가 발생했습니다.

당황하지 않고 메세지를 처음부터 읽어봅시다.

node serverExpress.js 여기 까지는 실행이 됐는데 문제는 그 다음 줄 입니다.

친절하게 어느 위치에서 오류가 발생하는지 알려줍니다.

``` javascript
const express = require('express')
                ^
```

그 다음, 오류 메세지를 읽어봅시다. 영어를 읽을 수 없다면 번역기를 돌려봅시다.

```
ReferenceError: require is not defined in ES module scope, you can use import instead
```

require 는 ES module 에서 정의되지 않아 require 대신 import 를 사용해야 합니다.

serverExpress.js 의 코드 내용을 수정하러 갑시다.

[serverExpress.js]
``` javascript
// const express = require('express')
import express from 'express';

...
```

require 부분을 주석 처리하거나 삭제하고 import 를 사용하여 패키지를 호출합니다.

그 다음, 다시 실행하면 서버가 정상적으로 실행 된 것을 확인할 수 있습니다.

```
Executing task: npm run start:express 


> nodejs-guide@1.0.0 start:express
> node serverExpress.js

Example app listening on port 3000
```

## 3. API 요청하기

API 요청을 하기 위해 Postman 프로그램을 사용 할 수도 있지만 기본적으로 브라우저에서도 가능 하므로 빈 브라우저를 하나 띄워봅시다.

기본 url 주소는 localhost 이고 port는 원하는대로 설정할 수 있습니다.

개발서버에서 주로 사용하는 포트번호는 3000 입니다.

브라우저에 localhost:3000/ 을 입력합니다.

브라우저에 Hello World! 텍스트가 출력되는것을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/4de2dda4-1220-4b3d-b686-9a49ef141426)

지금은 간단한 텍스트 정도만 출력할 수 있지만 데이터베이스를 연결하고 CSS를 꾸미면 Facebook 같은 멋진 SNS를 만들 수도 있습니다.

## Node.js Start
- [Node.js Start - 05 정보보안](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-05.-information-security)