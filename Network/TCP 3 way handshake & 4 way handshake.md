# TCP 3 way handshake & 4 way handshake

## 목차
1. 사전 지식
    - TCP란?
    - TPC Segment 구조
    - Port
    - Flag
2. TCP 3-way handshake
3. TCP 4-way handshake 
<br>
<br>

## 1. 사전 지식
### TCP란?
네트워크 계층 중 전송 계층에서 사용하는 프로토콜 중 하나로, 신뢰성을 보장하는 연결형 서비스이다.
<br>

### TPC Segment 구조
(이미지 첨부)
- Source port : 출발지 포트 번호
- Destination port : 목적지 포트 번호
- sequence numbers : 세그먼트 내 데이터의 첫 바이트 번호
- acknowledgements : 상대로부터 전송 받길 기대하는 다음 바이트 번호. 누적 확인 응답.
<br>

### Port 
- CLOSED : 포트가 닫힌 상태
- LISTEN : 포트가 열린 상태로 연결 요청 대기 중.
- SYN_SENT : 클라이언트가 포트를 열어 SYN를 서버에 전달한 상태.
- SYN_RCVD : SYNC 요청을 받은 서버의 상태. 클라이언트에 SYN, ACK 송신 후 상대방의 응답을 기다리는 중.
- ESTABLISHED : 포트 연결 상태. 통신이 가능한 상태.
<br>

### Flag(Control bit, 6bit)
- TCP Header에는 Control bit(플래그 비트, 6bit)가 존재하며, 각각의 bit는 아래와 같다. 6bit 중 각 위치의 bit가 1이면 해당 패킷이 어떤 내용을 담고 있는 패킷인지를 나타낸다.
- URG(urgent) : 긴급 비트. 해당 세그먼트의 데이터가 우선순위가 높다. urgent data pointer 필더의 값이 유효함을 나타낸다.
- `ACK` : 승인 비트 (010000). 패킷 수신 승인을 의미한다. ackowledgements 필드의 값이 유효함을 나타낸다. 
- PSH(push) : 밀어넣기 비트. 송수신 버퍼에 있는 데이터는 일정한 크기가 쌓인 후 처리되어야 하는데, 이것과 관계 없이 즉시 처리해야할 때 사용한다.
- RST(reset) : 초기화 비트. 강제 종료하여 연결을 중단한다.
- `SYN` : 동기화 비트 (000010). 상대와의 연결을 설정한다.
- `FIN` : 종료 비트 (000001). 남은 송신측 데이터가 없어 연결을 종료한다.

<br>
<br>


## TCP 3-way handshake
- TCP 통신을 이용하여 데이터를 전송하기 위해 네트워크 연결을 `수립`하는 과정이다.
(이미지 첨부)
- 연결 수립 과정
  1. 클라이언트 -> 서버 : 클라이언트는 초기번호 `x`를 고르고 서버에게 접속을 요청하는 `SYN` 패킷을 송신한다. 
     - 클라이언트 상태 : LISTEN -> `SYN_SENT`
  2. 서버 -> 클라이언트 : 서버는 SYN 요청을 수신하고, 세그먼트의 초기 번호 `y`를 골라 클라이언트에게 요청을 받아들이겠다는 의미의 `ACK`와, `SYN`를 송신한다.
     - 서버 상태 : LISTEN -> `SYN_RCVD`
  3. 클라이언트 -> 서버 : 클라이언트는 이를 최종적으로 수락하는 패킷 `ACK`를 보낸다.
      - 클라이언트 상태 : SYN_SENT -> `ESTABLISHED`
      - 서버 상태 : SYN_RCVD -> `ESTABLISHED`
- 이 과정을 통해 서버, 클라이언트 모두 데이터를 전송할 준비가 되었다는 것을 보장한다.

<br>
<br>

## TCP 4-way handshake
- TCP의 연결을 `해제`하는 과정이다.
(이미지 첨부)
- 해제 과정
  1. 클라이언트 -> 서버 : 클라이언트가 서버에게 연결 종료 요청 `FIN`을 송신한다.
      - 클라이언트 상태 : ESTABLISHED -> `FIN_WAIT_1`
  2. 서버 -> 클라이언트 : 서버는 FIN을 수신하고, 연결 종료 응답 `ACK`를 송신한다. 아직 데이터를 보낼 수 있는 상태이며, 자신의 통신이 끝날때까지 대기한다. 
      - 서버 상태 : ESTABLISHED -> `CLOSE_WAIT`
      - 클라이언트 상태 : FIN_WAIT_1 -> `FIN_WAIT_2`
  3. 서버 -> 클라이언트 : 서버는 데이터를 모두 보낸 후, 클라이언트의 연결 종료 요청에 합의한다는 의미로 연결 종료 요청 `FIN`을 송신한다. 승인 번호를 보내줄 때까지 기다리는 상태로 들어간다.
      - 서버 상태 : CLOSE_WAIT -> LAST_ACK
  4. 클라이언트 -> 서버 : 클라이언트는 FIN을 수신받고,  서버에게 확인했다는 응답으로 `ACK`를 반환한다. 아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME_WAIT를 통해 대기 후 종료한다.
      - 클라이언트 상태 : FIN_WAIT_2 -> `TIMED_WAIT` -> `CLOSED`
