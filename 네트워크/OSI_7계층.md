## OSI 7계층
- OSI(Open Systems Interconnection) 모델은 네트워크 통신을 7개의 계층으로 나누어 설명하는 개념이다. 각 계층들은 특정 기능을 수행하며, 기능은 서로 독립적으로 설계가 될 수 있다.

![image](https://user-images.githubusercontent.com/32945436/227431153-06db0d53-d819-4c61-98e0-ff898e51f598.png)

#### 1. 물리계층(Physical Layer)
- 데이터를 전송하기 위한 물리적 매체와 관련된 기능을 수행합니다. 
- 대표적인 장비는 케이블, 허브, 리피터 등이 있다.

#### 2. 데이터 링크 계층(DataLink Layer)
- 물리 계층에서 발생할 수 있는 오류를 검출하고 수정하는 것 처럼 데이터를 안정적으로 전송하기 위한 기능을 수행.
- MAC 주소(물리적 주소) 등의 정보를 이용해서 데이터를 전송.
- 대표적인 장비는 스위치이다.

#### 3. 네트워크 계층(Network Layer)
- 데이터를 목적지로 전송하기 위한 경로를 설정하는 기능 수행, 즉 라우팅 기능 수행.
- IP주소를 이용해서 패킷을 전달.
- 라우터가 대표적인 장비.

#### 4. 전송 계층(Transport Layer)
- 통신을 활성화 하기 위한 계층이다.
- 포트를 열어서 프로그램들이 전송을 할 수 있게 한다.
- 데이터가 오면 4계층에서 합쳐서 5계층으로 보냄
- 여기까지 물리적인 계층.
- TCP, UDP 등의 프로토콜을 이용해서 데이터 전송을 관리.

#### 5. 세션 계층(Session Layer)
- 데이터가 통신하기 위한 논리적인 연결이다.
- 통신을 하기 위한 대문.
- 여기서부터는 응용프로그램(어플리케이션) 관점에서 보는 것.
- 세션 설정, 유지, 종료, 중단시 복구 등의 기능이 있음.
- 양 끝단의 응용프로세스가 통신을 관리하기 위한 방법 제공.
- TCP/IP 세션을 만들고 없애는 책임을 짐.
- 사용자들을 동기화하고 오류 복구 등을 다룸.

#### 6. 표현 계층(Presentation Layer)
- 이 계층은 데이터를 응용 프로그램이 이해할 수 있는 형식으로 변환하는 기능을 수행. 
- 예를 들어, ASCII 코드를 유니코드로 변환하거나, 데이터를 인코딩하는 등의 기능을 수행.
- 데이터 인코딩 하는 것은 TEXT인지 GIF인지 구분하는 것.

#### 7. 응용 계층(Application Layer)
- 가장 상위에 속한 계층이며, 사용자나 응용프로그램과 직접 상호작용한다.
- 네트워크에서 데이터 전송과 관련된 응용프로그램을 실행한다.
- 다양한 프로토콜과 서비스를 사용한다.
- HTTP, FTP, SMTP, DNS 등이 있다.
- 브라우저나 메일같은 것들은 프로토콜 등을 쉽게 사용하게 해주는 것이다.
- 모든 통신의 끝단은 프로토콜이지 브라우저가 아닌 것.
  * HTTP 웹상에서 웹서버 및 웹브라우저 상호간의 데이터 전송을 위한 프로토콜.
  * 요청과 응답, 메시지 교환 형태(응답 요청), 비연결성 프로토콜이며 이전의 상태 유지x
  * SMTP = 이메일을 보내고 받기 위해 이용되는 프로토콜.

HTTP의 경우 다음 링크 참조
[HTTP](네트워크/HTTP&HTTPS.md)

[참고자료] https://shlee0882.tistory.com/110
