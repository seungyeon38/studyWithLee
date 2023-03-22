# TCP (Transmission Control Protocol)
- TCP는 연결형 프로토콜로, 전송된 패킷의 순서와 누락 여부를 검사하며, 필요에 따라 패킷 재전송을 수행하는 신뢰성 있는 전송을 보장합니다(OSI 4계층 전송계층).

## ACK, SYN, FIN
- ACK(Acknowledgement) 승인의 약자로 요청을 확인했다는 응답.
- SYN (Synchronize + Sequence Number) 연결이 이루어지도록 요청하는 의미.
- FIN(Finish) 세선 연결을 종료시킬 때 사용되며 더 이상 전송할 데이터가 없음을 나타내는 것.

## 3-way Handshake
![image](https://user-images.githubusercontent.com/32945436/226533429-c17b4f89-9673-4762-a0c5-dbd2b0a109eb.png)
- 연결이 성립하는 과정을 이야기하는 것이다.
1. 클라이언트가 서버에게 SYN 패킷을 보냄(SYN M)
2. 서버가 SYN(M)을 받고, 클라이언트로 받았다는 신호인 ACK와 SYN을 보낸다(SYN: N, ACK: M+1)
3. 클라이언트는 서버의 응답은 (SYN: N, ACK: M+1)을 받고, ACK(N+1)을 서버로 보낸다.

- 이와 같이 3번의 통신이 완료되면 연결이 성립(3번의 통신이므로 3 way handshake)

## 4-way Handshake
![image](https://user-images.githubusercontent.com/32945436/226533892-9bd8d9d6-de58-4762-a042-42475b7053fc.png)
- 3-way는 TCP의 연결의 초기화 및 성립하는 과정을 보여주는 것이라면, 4-way는 연결을 해제하는 과정이다.
1. 클라이언트가 연결을 종료하겠다는 FIN 플래그를 전송하며, 이 때 클라이언트는 FIN_WAIT상태에 돌입한다.
2. 서버는 클라이언트의 요청을 받고, 확인메시지로 ACK를 보낸다. 그리고 데이터를 모두 보낼 때까지 잠깐 TIME_OUT이 되는데 서버는 CLOSE_WAIT 상태가 된다.
3. 데이터를 모두 보내고 통신이 끝나면, 다시 연결이 종료되었다는 FIN 플래그를 서버가 보낸다. 이 때 서버는 LAST_ACK 상태가 된다.
4. 클라이언트는 종료메시지를 확인한 ACK를 보낸다. 서버는 ACK메시지를 받고 연결을 CLOSE한다. 클라이언트는 데이터를 아직 덜 받았을 경우를 생각해 일정시간 세션을 남겨놓고 잉여패킷을 기다린다(TIME_WAIT)

### TIME_WAIT
- 서버에서 FIN을 마지막에 전송하기 전에 그전에 보냈던 패킷들이 유실되거나 Routing 지연(경로 선택 지연)으로 인해 재전송 등이 생겨 FIN 패킷보다 늦게 도착하면 클라이언트가 바로 종료했을 때 데이터가 유실된다. 이를 방지하기 위해 클라이언트는 FIN을 받아도 일정시간(기본:240초)를 기다리며 잉여 패킷을 기다린다. 그래서 일정시간이 지난뒤 CLOSE상태로 변화하는 것이다.
