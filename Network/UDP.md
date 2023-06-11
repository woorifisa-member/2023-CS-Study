# UDP

## 목차

1. UDP란?
2. UDP와 TCP
   - TCP 특징
   - 실시간 서비스에서 TCP의 단점
   - 실시간 서비스에서의 단점을 해결하고자 등장한 UDP
   - UDP 작동방식
   - UDP와 TCP 비교해보기
3. UDP에 의존하는 서비스 종류
4. UDP가 DDos 공격에 사용되는 방법
5. 면접질문

## 💡 먼저 보면 좋은 글

🔗 [TCP 3 way handshake & 4 way handshake](https://github.com/woorifisa-member/2023-CS-Study/blob/main/Network/TCP%203%20way%20handshake%20%26%204%20way%20handshake.md)

written by.[Suhyun](https://github.com/ooutta)

## 1. UDP란? (User Datagram Protocol)

전송 계층 통신 프로토콜인 UDP는 음성 및 비디오 트래픽을 위한 일반적인 프로토콜이다. UDP는 `User Datagram Protocol`의 약자로 `비디오 재생` 또는 `DNS조회`과 같이 시간에 민감한 전송을 위해 사용 되는 통신 프로토콜을 의미한다.

> 💡 프로토콜: 기기 간 통신은 교환되는 데이터 형식에 대해 상호 합의를 요구하는데, 이러한 형식을 정의하는 규칙의 집합을 프로토콜이라고 한다.

## 2. UDP와 TCP

### TCP 특징

- 네트워크 통신에 있어서 신뢰성을 얻기 위해 프로그램들은 주로 `TCP` 통신을 함
- TCP는 데이터의 신뢰성을 보장하기 때문에, 누락된 데이터를 모두 받기 위한 메커니즘으로 설계됨

👉 이메일이나 파일전송에서는 필수적이었지만, `실시간 스트리밍 서비스` 같은 경우 단점이 발생

### 실시간 서비스에서 TCP의 단점

- 실시간 스트리밍 영상을 사용한다고 했을때, 아주 사소한 부분을 다운받지 못했을 경우에 실시간 스트리밍이 중지되기 일쑤였다.

- TCP는 혼잡제어를 위해 전송하는 양도 조절하기 떄문에, 영상의 퀄리티가 안정적이지 못했다.

### 실시간 서비스에서의 단점을 해결하고자 등장한 UDP

UDP는 TCP의 모든 실뢰성 기능이 없다고 보면 된다. 상대가 접속했다는 것, 그리고 전송속도를 설정했다는 조건만 있으면 데이터를 전송할 수 있다. 따라서 받는 쪽에서 데이터를 제대로 받고 있는지 조차도 신경 쓰지 않는다.

✅ UDP로 자료를 제공할 경우, 32 kbps, 48 kbps, 64 kbps와 같이 다양한 전송률 옵션을 선택하는 형태로 제공된다.

### UDP 작동 방식

일반적으로 다른 전송 프로트콜은 `먼저 연결을 설정`, `해당 패킷의 순서를 표시`, `의도한 대로 도착했는지 여부 확인` 등을 수행한다.

> 💡 패킷: 패킷은 네트워크가 전달하는 데이터의 형식화된 블록. pack과 bucket의 합친 말로, 우체국에서 화물을 적당한 덩어리로 나눠 행선지를 표시하는 꼬리표를 붙일 때 사용하는 말이다. 즉, 정보를 보낼 때 특정 형태에 맞추어 보낸다는 것이다. 네트워크를 통해서 전송되는 데이터 조각.

UDP는 위에서 언급한 과정들을 모두 무시하고, `패킷`을 대상 컴퓨터로 직접 보내는 간단한 방식으로 프로세스를 수행한다. 여기서 이 UDP 패킷을 `데이터그램`이라고 한다.

또한 UDP 통신은 TCP와 다르게 `핸드셰이크` 과정이 없이, 다른 컴퓨터로 데이터 전송을 시작할 수 있다.

🔗 [TCP 3-way handshake](https://github.com/woorifisa-member/2023-CS-Study/blob/main/Network/TCP%203%20way%20handshake%20%26%204%20way%20handshake.md#tcp-3-way-handshake)

<center>
<img width="672" alt="image" src="https://github.com/woorifisa-member/2023-CS-Study/assets/72537762/b2dd9a92-b9e8-42b0-9337-e3046e5f048a"/>
<figcaption>출처: cloudflare</figcaption>
</center>

### UDP와 TCP 비교해보기

| 특징                      | TCP                 | UDP                                      |
| ------------------------- | ------------------- | ---------------------------------------- |
| 연결설정                  | TCP 3-way-handshake | 안함                                     |
| 패킷의 순서               | 표시 ⭕️            | 표시 ❌                                  |
| 데이터 신뢰성 확인        | 확인 ⭕️            | 확인 ❌                                  |
| 속도                      | 상대적으로 느림     | 상대적으로 빠름                          |
| 안정성                    | 높음                | 낮음                                     |
| 패킷 수신 순서            | 순서 ⭕️            | 확인안함                                 |
| 패킷이 도착하지 않은 경우 | 다시 TCP 전송       | 다시 전송하지 않음. (애초에 확인을 안함) |

- 신뢰성이 보장되지 않아서 손실되는 데이터가 발생할 수 있다
- 하지만 동영상의 경우, 데이터가 몇개 소실되어봤자 전체 화면에서 일부 구역만 제대로 안나오는 수준에 불과하다.
- UDP 헤더에는 목적지주소, 데이터순서, checksum과 실데이터만 포함되고, 확인응답 같은 것이 없기 때문에 TCP보다 용량이 가볍고 송신속도가 빠르다.
- 하지만 확인응답을 하지 못하기때문에 신뢰도가 TCP보다 떨어지게 된다. 따라서 `UDP는 비연결형`이라 부르며 `TCP는 연결형`이라 구분한다.

✅ 사용자가 크게 불만이 없다면 굳이 느린 TCP로 전송 받을 이유가 없다.

✅ UDP는 데이터가 손실되어도 재전송을 하지 않기 때문에, 오류, 손실, 중복을 허용할 수 있어야 한다.

```text
기술적으로 보면, 이러한 패킷 손실은 UDP의 결함이라기보다는 인터넷 구축 방식의 결과입니다. 대부분의 네트워크 라우터는 패킷 순서 지정 및 도착 확인을 의도적으로 수행하지 않습니다. 그렇게 할 경우 수행할 수 없는 양의 추가 메모리가 필요하기 때문입니다. TCP는 애플리케이션에서 이를 필요로 할 때 이 격차를 메우는 방법입니다.

//출처: cloudflare.com
```

## 3. UDP에 의존하는 서비스 종류

- 시간에 민감한 통신에 주로 사용됨
- 음성 및 비디오 트래픽
- 인터넷 기반 전화 서비스에서 사용되는 `Voice over IP(VoIP)`
- 보이스톡, 화상통화, 디스코드 등

## 4. UDP가 DDos 공격에 사용되는 방법

패킷 손실과 같은 것은 심각한 문제가 아니지만, UDP는 별도의 핸드셰이크가 필요하지 않기 때문에 공격자는 먼저 해당 서버의 통신 시작 권한을 얻지 않고도 대상 서버에 트래픽 폭주를 시킬 수있다.

<center>
<img width="562" alt="image" src="https://github.com/woorifisa-member/2023-CS-Study/assets/72537762/5e41dcd4-440e-430e-beef-be790eca9843" />
<figcaption>출처: cloudflare</figcaption>
</center>

UDP 폭주 공격은 많은 개수의 UDP 데이터그램을 대상 컴퓨터의 임의 포트로 보낸다. 그에 따라 대상이 똑같이 많은 개수의 ICMP 패킷으로 응답하게 되며, 이는 해당 포트에 연결할 수 없음을 나타낸다.

## 5. 면접질문

<details>
<summary>TCP UDP 방식을 비교해주세요</summary>
TCP와 UDP 모두 네트워크 계층 중 전송계층에서 사용하는 프로토콜 입니다.
TCP는 3-way handshaking과정을 통해 연결을 설정해서 신뢰도를 확보해서 순서를 보장하는 대신 속도가 느리고,
UDP는 순서를 보장하지 않고 신뢰도가 낮은 데이터 전송을 하는 대신, 단방향 데이터 전송으로 속도가 빠르다는 차이가 있습니다. 따라서 TCP는 신뢰도가 필요한 HTTP 통신, 이메일 등에 사용되고, UDP는 빠른 속도가 중요한 스트리밍 서비스에 사용됩니다.
</details>
<br />

[나무위키 - Voice over IP](https://namu.wiki/w/VoIP)

[위키백과 - UDP](https://namu.wiki/w/UDP)

[Cloudflare - UDP란 무엇입니까?](https://www.cloudflare.com/ko-kr/learning/ddos/glossary/user-datagram-protocol-udp/)

[Cloudflare - UDP 플러드 공격](https://www.cloudflare.com/ko-kr/learning/ddos/udp-flood-ddos-attack/)

[UDP 홀펀치](https://en.wikipedia.org/wiki/UDP_hole_punching)

[Discord 음성 연결](https://discord.com/developers/docs/topics/voice-connections)
