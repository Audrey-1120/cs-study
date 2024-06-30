## 0) 공부하기 전에..

- 3 way handshake와  4 way handshake는 TCP에서 논리적인 접속을 성립하기 위한 과정이다.
- OSI 7 계층의 전송 계층에서는 사용자들 간의 신뢰성 있는 데이터 전달을 책임진다고 했다.
- 여기서 사용하는것이 바로 **TCP**와 **UDP**이다.
    - 전송계층에서는 인터넷의 기반인 TCP/IP와 일반적인 네트워크 모델을 모두 포함한다고 한다.
    - 전송계층에서 사용하는 데이터 단위는 세그먼트이다.
- TCP는 연결형 서비스로 신뢰적인 전송을 보장한다. 그러나 UDP는 비 연결형 서비스로 신뢰성이 떨어진다.
    - 여기서 TCP는 3-way handshaking 과정을 통해 연결을 설정하고 4-way handshaking을 통해 해제한다. UDP는 이러한 과정이 없기 때문에 속도는 빠르겠지만 전송의 신뢰성이 떨어지는 것이다.

## 1) 3-way hand**shake, 4-way handshake란?**

**3-way handshake : TCP의 접속 과정**

**4-way handshake : TCP의 접속 해제 과정**

## 2) TCP 제어 플래그

TCP 헤더에서는 특수한 목적의 패킷을 위한 6개의 제어 플래그를 가짐.

**2-1) 순서**

URG, ACK, PSH, RST, SYN, FIN

활성화되는 비트만 1로 표현함. ex) SYN/ACK의 경우 010010

**2-2) 플래그**

 **SYN(Synchronize Sequence Number) / 000010**

- 연결 설정. Suquence Number를 랜덤으로 설정하여 세션 연결하는데 사용
- 초기에 Sequence Number 전송

 **ACK(Acknowledgement) / 010000**

- 응답 확인. 패킷을 받았음을 의미
- Acknowledgement Number 필드가 유효한지 나타냄.
- SYN 세그먼트 전송 이후(TCP 연결 시작후) 모든 세그먼트에는 항상 이 비트가 1로 셋팅됨

FIN(Finish) / 000001

- 연결 해제
- 세션 연결 종료시킬때 사용
- 더이상 전송할 데이터가 없음을 의미.
- **시퀀스 번호(Sequence Number), ACK번호(Acknowledgement Number)**
    
    **시퀀스 번호**
    
    - 데이터 스트림의 각 바이트를 고유하게 식별하기 위해 사용됨. TCP 연결에서 각 바이트마다 시퀀스 번호가 할당됨.
        - 초기값: 연결을 설정할 때, 클라이언트와 서버는 각각 임의의 초기 시퀀스 번호(ISN)를 선택함.
    
    **ACK 번호**
    
    - 수신자가 마지막으로 성공적으로 수신한 데이터의 다음 바이트의 시퀀스 번호를 나타냄. 즉, 수신자가 다음에 기대하는 바이트의 시퀀스 번호.
        - 확인: 송신자가 데이터를 보냈을 때, 수신자는 해당 데이터를 받았음을 ACK 번호로 확인

## 3) 3-way handshake

- TCP 통신을 이용하여 데이터를 전송하기 위해 **네트워크 연결을 설정**하는 과정
- 총 세단계로 이루어져 있음.

![Untitled](https://github.com/Audrey-1120/cs-study/assets/100057254/e3147263-7ca0-4322-9736-afca2f167ec3)

1. **SYN(Synchronize)**
    - 클라이언트가 서버에 연결 요청을 보냄. 이 패킷에는 SYN 플래그가 설정되어 있음.
        - 해당 패킷에는 시퀀스 번호 x 포함.
        - `클라이언트 → 서버: “SYN, Sequence Number = x”`
2. **SYN-ACK (synchronize-Acknowledge)**
    - 서버가 클라이언트의 요청을 수락하고 SYN 플래그와 ACK 플래그가 설정된 패킷을 클라이언트에게 보냄.
        - 해당 패킷에는 서버의 시퀀스 번호 y와 클라이언트의 시퀀스 번호 x에 대한 ACK 번호 x+1이 포함됨.  (ACK 번호는 수신자가 마지막으로 성공적으로 수신한 데이터의 다음 바이트의 시퀀스 번호이므로 x+1)
        - `서버 → 클라이언트: “SYN, ACK, Sequence Number = y, Acknowledgement Number = x+1”`
        - 여기서 sequence Number = y는 서버의 초기 시퀀스 번호이고, Acknowledgement Number = x + 1은 클라이언트의 시퀀스 번호 x에 대한 확인 응답.
3. **ACK(Acknowledge)**
    - 클라이언트가 서버의 응답을 확인하고 ACK 플래그가 설정된 패킷을 서버로 보냄.
        - 해당 패킷에는 클라이언트의 시퀀스 번호 x+1과 서버의 시퀀스 번호 y에 대한 ACK 번호 y+1이 포함됨.
        - `클라이언트 → 서버: “ACK, Sequence Number = x + 1, Acknowledgement Number = y+1”`
        - 여기서 sequence Number = x+1는 클라이언트의 다음 시퀀스 번호이고, Acknowledgement Number = y+1은 서버의 시퀀스 번호 y에 대한 확인 응답

위와 같이 3번의 통신이 완료되면 연결이 성립된다. (3번이라서 3-way handshake!)

## 4) 4-way handshake

- **TCP 연결을 종료**하는 과정이며 4단계로 이루어져 있음. FIN 플래그를 이용함.
- FIN(finish) : 세션을 종료시키는데 사용되며, 더 이상 보낸 데이터가 없음을 의미.

![22323434](https://github.com/Audrey-1120/cs-study/assets/100057254/6cc87751-54dd-482a-bea2-0fc20e30fe0b)

1. **FIN**
- 클라이언트는 서버에게 연결을 종료한다는 FIN 플래그가 설정된 패킷을 보냄.
1. **ACK(Acknowledge)**
- 서버는 FIN 패킷을 수신하고 ACK 플래그가 설정된 패킷을 보냄.
    - 이때 모든 데이터를 보내기 위해 CLOSE_WAIT 상태가 됨.
    - 서버에서 클라이언트로 보낼 남은 데이터가 있을 경우 이때 나머지를 모두 전송시킴.
1. **FIN**
- 데이터가 모두 전송되었다면 서버도 연결을 종료하기 위해 FIN 플래그가 설정된 패킷을 클라이언트에게 보냄.
1. **ACK(Acknowledge)**
- 클라이언트가 FIN 패킷을 수신하고 ACK 플래그가 설정된 패킷을 서버로 보냄.
    - 이때 아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME_WAIT을 통해 기다림

서버는 ACK를 받은 이후 소켓을 닫음

TIME_WAIT시간이 끝나면 클라이언트도 닫음

위와 같이 4번의 통신이 완료되면 연결이 해제됨.