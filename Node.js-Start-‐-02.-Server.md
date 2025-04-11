# Node.js Web Server 만들기

앞서 [Node.js Guide](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Guide) 페이지에서 서버에 대해 간략히 설명 했습니다.

Node.js Web Server를 만드는 방법은 직접 http 모듈을 사용하는 것과 npm init 을 통해 더욱 확장 가능한 프로젝트를 만들 수 있습니다.

## HTTP란?

서버를 사용하기 앞서 웹의 기초인 HTTP에 대해 알아봅시다.

HTTP(Hypertext Transfer Protocol)란 네트워크 장치 간에 정보를 전송하도록 설계 된 **규칙** 입니다.

요청/응답(Request/Response)으로 구성되어 있고 HTML 같은 문서를 전송합니다.

다음은 서버와 클라이언트가 동작하는 방식 입니다.

사용자가 웹 브라우저에서 클릭 혹은 키보드 이벤트를 통해 규칙에 알맞는 요청을 합니다.

서버는 해당 요청을 수신하고 html, css, image 등 가공된 문서를 사용자에게 전달 합니다.

![](https://mdn.github.io/shared-assets/images/diagrams/http/overview/fetching-a-page.svg)

HTTP 에 대한 내용은 방대하므로 모두 설명하는 것은 힘들고 시간이 될 때 문서를 읽어보는것이 도움이 될 것 입니다.

Link => https://developer.mozilla.org/ko/docs/Web/HTTP

## 본격적인 서버 만들기 - http 모듈 사용하기

탐색기 창에서 server.js 파일을 생성 후 다음 코드를 입력합니다.

```
const http = require('http');

http.createServer(function(req, res) {
  res.write('<h1>Hello world</h1>');
  res.end('<p>Hello Node.js Server!</p>');
}).listen(8080, function () {
  console.log('listening on 8080');
});
```

터미널에 `node server.js` 를 입력합니다.

터미널에 서버가 실행 되면 `listening on 8080` 이라는 메세지가 출력됩니다.

![image](https://github.com/user-attachments/assets/e3bd49c7-e083-430e-b895-a0e958041d9b)

위 메세지의 뜻은 server가 8080 port 에서 대기 중 임을 나타냅니다.

port는 서버에서 특정 service 나 application으로 들어오는 데이터의 출입구 번호 입니다.

쉽게 비유를 해보겠습니다.

URL 은 여러분의 집 주소이고 port 번호는 여러분의 집 도어락 비밀번호 입니다.

**Address: 서울특별시 서초구 강남대로 00길 00**

  <img src="https://github.com/user-attachments/assets/d7ab5f78-194d-469b-a52f-8e1b350254f2" alt="network" width="50%" />

**Port: 8080**

  <img src="https://github.com/user-attachments/assets/a5dbaacc-992b-4bdf-a093-b37c6228a8d7" alt="network" width="50%" />

이제 웹 서버로 요청을 해보겠습니다.

브라우저에서 새 탭을 열고 주소창에 url:port 주소를 입력합니다.

```
http://localhost:8080
```

server.js 에서 입력했던 html 태그가 화면에 나타난 것을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/d41b5980-3792-4b73-9e39-f579def0b133)

## npm 사용하기

npm 도 앞서 설명했듯이 Node Package Manager 의 약어로, 다양한 node.js 개발 관련 패키지를 사용할 수 있습니다.

다음 페이지에서 이어서 설명하겠습니다.

## Node.js Start
- [Node.js Start - 03 npm](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-03.-npm)
- [Node.js start - 04. REST API](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-04.-REST-API)
- [Node.js Start - 05 정보보안](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-05.-information-security)
- [Node.js Start - 06 Connect Database](https://github.com/pmirnc-dev/pds-welcome/wiki/Node.js-Start-%E2%80%90-06.-Connect-Database)

