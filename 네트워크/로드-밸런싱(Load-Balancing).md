# 로드 밸런싱

서버가 처리해야 할 업무 혹은 요청(Load)을 여러 대의 서버로 나누어(Balancing) 처리하는 것.  
한 대의 서버로 부하가 집중되지 않도록 트래픽을 관리해 각각의 서버가 최적의 퍼포먼스를 보일 수 있도록 하는 것이 목적이다.

서비스의 규모가 커지고, 이용자 수가 늘어나서 기존의 서버로는 원활한 서비스 동작이 불가능 할 때, 대처할 수 있는 방법은 크게 두 가지 방법이 있다.

- Scale-up : 기존의 서버 성능을 확장하는 방식.
- Scale-out : 기존의 서버와 동일하거나 낮은 성능의 서버를 증설하는 방식.

로드 밸런싱은 Scale-out방식을 선택했을 때, 여러 대의 서버로 트래픽을 균등하게 분산해주기 위해 필요하다.

</br>

## 로드 밸런싱 기법

- **라운드로빈**  
   서버에 들어온 요청을 순서대로 돌아가며 배정하는 방식.  
   클라이언트의 요청을 순서대로 분배하기 때문에 여러 대의 서버가 동일한 스펙을 갖고 있고, 서버와의 연결(세션)이 오래 지속되지 않는 경우에 활용하기 적합하다

- **가중 라운드로빈**  
  각각의 서버마다 가중치를 매기고 가중치가 높은 서버에 클라이언트 요청을 우선적으로 배정하는 방식.  
   주로 서버의 트래픽 처리 능력이 상이한 경우 사용된다.

- **IP해싱**  
   클라이언트의 IP 주소를 해싱하여 특정 서버로 매핑해서 요청을 처리하는 방식.

- **최소 연결**  
   요청이 들어온 시점에 가장 적은 연결상태를 보이는 서버에 우선적으로 트래픽을 배정하는 방식.  
   자주 세션이 길어지거나, 서버에 분배된 트래픽들이 일정하지 않은 경우에 적합한 방식이다.

- **최소 응답 시간**  
   서버의 현재 연결 상태와 응답 시간을 고려하여 트래픽을 배정하는 방식.

</br>

## L4 로드 밸런싱과 L7 로드 밸런싱

### L 4 & L 7

L4, L7은 각각 Layer 4(전송 계층) 프로토콜과 Layer 7(응용 계층) 프로토콜의 헤더를 부하 분산에 이용하기 때문에 붙은 접두사이다. 모든 요청을 L4 혹은 L7 로드 밸런서가 받아 서버들에게 적절히 나누어 준다.

### L4 로드 밸런서

네트워크 계층(IP, IPX)이나 전송 계층(TCP, UDP)의 정보(IP주소, 포트번호, MAC주소, 전송 프로토콜)를 바탕으로 트래픽을 분배한다.
![image](https://nesoy.github.io/assets/posts/20180602/5.png)

### L7 로드 밸런서

애플리케이션 계층(HTTP, FTP, SMTP)에서 HTTP 헤더, 쿠키 등과 같은 사용자의 요청을 기준으로 특정 서버에 트래픽을 분산하는 것이 가능하다.  
패킷의 내용을 확인하고 그 내용에 따라 로드를 특정 서버에 분배하는 것이 가능하기 때문에 URL에 따라 부하를 분산시키는 등 클라이언트의 요청을 보다 세분화 해서 서버에 전달할 수 있다.

또한, L7 로드 밸런서의 경우 특정한 패턴을 지닌 바이러스를 감지해 네트워크를 보호할 수 있으며, DoS/DDoS와 같은 비정상적인 트래픽을 필터링할 수 있어 네트워크 보안 분야에서도 활용되고 있다.
![image](https://nesoy.github.io/assets/posts/20180602/6.png)
