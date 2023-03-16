## WebSocket
- 서버와 클라이언트 간의 메시지 교환을 위한 통신 규약(프로토콜)
- HTML5 표준의 일부로 WebSocket이 만들어졌으며, HTTP와 다르게 양방향 통신이 가능함.

### TCP Socket과 차이
- ip주소 포트번호로 연결하는 것과 달리 최초엔 HTTP Request를 하고 접속이 된다면 웹소켓 프로토콜(WS)로 변경

### 특징
- HTTP에서 Request보내고 Response보내는 것보다 쉽게 데이터 교환가능.
- 웹서버에 연결하는 포트는 HTTP처럼 80으로 동일함.
- 브라우저와 웹서버 모두 WebSocket기능을 지원해야함 (서버는 Jetty, GlassFish, Node.js, Netty, Grizzly 등)이 있음
- 구버전 브라우저는 지원하지 않음
- HTTP 규격을 따라가서 CORS나 인증 등을 기존처럼 사용가능하다. 

## Socket.io
- 표준 기술이 아니고 웹소켓 기술을 사용하는 라이브러리이다.
- 웹소켓뿐만 아니고 실시간 웹 기술을 사용할 수 있게 해준 것이다.
- JavaScript를 이용해서 브라우저 종류에 상관없이 구현할 수 있도록 해준 것.
### 특징
- 바로 사용할 수 있는 기술이며, 서버는 Node.js로 밖에 사용할 수 없다.
- 개발자는 Socket.io로 개발을 하고 클라이언트로 푸쉬 메시지를 보내기만 하면, WebSocket을 지원하지 않는 브라우저의 경우는 브라우저 모델과 버전에 따라서 AJAX Long Polling, MultiPart Streaming, Iframe을 이용한 푸쉬, JSONP Polling, Flash Socket 등 다양한 방법으로 내부적으로 푸쉬 메시지를 보내준다.
- 따라서, 브라우저 종류에 국한되지 않고 사용할 수 있다.
- 연결 실패시 fallback을 통해 다른 방식으로 연결 시도한다.
- 방 개념이 있어서, 일부 클라이언트에게만 데이터 전송이 가능(broadcasting)


## 어떤 걸 써야하냐?
- Broadcasting기능이 있는 socket.io는 채팅같이 사용자들을 관리해야하는 서비스일 때 사용하면 유용함.
- 하지만 거래소와 같은 것은 단순 데이터 전송이며 많은 양이라서 비용이 적은 WebSocket을 쓰는 것이 좋음.

## Webrtc
- Web Real Time Communication의 약자이며 소켓 기술들은 브라우저와 서버가 통신하는 것이다.
- 브라우저와 브라우저 간의 통신을 위한 것.
- 브라우저 간 직접 통신이라서 지연시간이 짧고, 훨씬 빠르다. 즉 고성능이다.

### 시그널링
- 각 브라우저(디바이스)간의 위치(IP)를 발견하고 미디어 포맷협의가 필요한데, 이 프로세스가 시그널링.
- 이는 웹소켓, socket.io를 통해 연결한다.


[참고자료] 
- https://www.peterkimzz.com/websocket-vs-socket-io/ </br>
- https://velog.io/@kkj53051000/WebRTC%EC%99%80-%EC%8B%9C%EA%B7%B8%EB%84%90%EB%A7%81%EC%9D%B4%EB%9E%80-%EC%8B%9C%EA%B7%B8%EB%84%90%EB%A7%81-Mozilla-%EB%B6%84%EC%84%9D



