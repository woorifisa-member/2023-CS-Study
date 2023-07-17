# Symmetric_Key & Public_Key - 대칭키 & 공개키(+HTTPS)

## 목차
1. 대칭키 & 공개키 등장배경(+HTTPS)
2. 대칭키 & 공개키 개념 및 특징
3. 대칭키 & 공개키를 활용한 HTTPS 구현 과정 
4. 면접질문
5. 참고자료

<br />

## 1. 대칭키 & 공개키 등장배경(+HTTPS)

### HTTP의 한계점

**HTTP(Hyper Text Transfer Protocol)** : WWW(웹) 상에서 서버와 클라이언트(사용자) 간에 html 같은 웹 문서를 통해 정보를 주고받는 프로토콜(통신 규약)을 의미

<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_1.png" width="600px">
</div>

 HTTP 통신을 하기위해서는 OSI 계층에서 TCP 기반인 4계층에서 3-way-handshake로 연결과정을 거치고 7계층에서 HTTP 기반으로 데이터 전송을 하고 다시 4계층에서 4-way-handshake로 연결을 끊는 과정을 거쳐야 한다
[4. OSI7 계층별 설명 참고](https://github.com/woorifisa-member/2023-CS-Study/blob/main/Network/OSI%207%20Layer.md)
 
HTTP 통신은 별다른 암호화 작업 없이 텍스트를 그대로 교환<br>
-> 누군가 네트워크에 접근하여 신호를 가로채면 외부에 노출<br>
-> **개인정보를 취급하는 서비스라면 큰 보안적 허점**

<br />

### HTTPS의 등장

> **HTTP + SSL = HTTPS(HyperText Transfer Protocal Secure)**
인터넷 상에서 정보를 암호화하는 SSL 프로토콜을 이용하여 클라이언트(웹)과 서버가 데이터를 주고 받는 통신 규약

<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_2.png" width="600px">
</div>

`SSL(Secure Socket Layer)` : 데이터를 암호화하는 보안 기능을 갖고 있는 보안인증서

SSL 보안계층이 전송계층에 적용됨. HTTPS는 SSL위에 HTTP를 얹어서 보안이 보장된 통신을 하는 프로토콜

<br>

`HTTPS 장점`

<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_3.png" width="600px">
</div>

1. 기관으로부터 검증된 사이트만 사용을 허가하기에, 안정성과 관련해 사용자들에게 신뢰감 부여

2. SEO 평가에 https 적용 여부가 중요한 순위요소 중 하나


**SSL 암호화 통신은 `공개키`, `암호화` 방식이라는 알고리즘을 통해 구현**

<br />


## 2. 대칭키 & 공개키 개념 및 특징

### 대칭키(Symmetric Key)

<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_4.png" width="600px">
</div>

암호화와 복호화에 같은 암호키(대칭키)를 사용하는 알고리즘을 의미

`암호화` : 암호문으로 변환하는 과정

`복호화` : 암호문을 다시 평문으로 복원하는 과정

<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_5.jpg" width="600px">
</div>

`예시`
1. 유저의 컴퓨터와 네이버 서버에 동일한 키가 있다면 대칭 즉, 양쪽이 똑같다.
2. 유저가 로그인을 할때 실어 보내는 비밀번호를 동일한 키로 암호화한다.
3. 네이버에서는 마찬가지로 이를 복호화해서 인식한다.

`장점`

1. 동일한 키를 주고받기 때문에 매우 빠르다

`단점`

1. 대칭키 전달과정에서 해킹 위험에 노출될 수 있다.


<br />


### 공개키(Public Key)(비대칭키)

<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_6.png" width="600px">
</div>

한 쌍이지만 서로 다른 A,B키를 사용하는 알고리즘을 의미<br>

`개인키` : 비밀로 보관하는 키

`공개키` : 대중들에게 공개하는 키
<br>
A키로 암호화를 하면 오직 B키로만 복호화를 할 수 있고 반대로 B키로 암호화를 하면 A키로 만 풀 수 있다.


<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_7.jpg" width="600px">
</div>

`예시`
1. 네이버 서버는 A,B 키들 중 비밀키와 공개키를 정한다.
2. 사용자는 공개키로 비밀번호를 암호화 해서 네이버에 보낸다.
3. 이때 누군가 가로채도 같은 공개키로는 이 암호문을 풀어낼 수가 없으며 이것을 볼 수 있는 건 오직 개인키를 가진 네이버 뿐이다.
<br>
=> 따라서 이러한 원리로 개인 정보들을 안심하고 사이트에 보낼 수 있게된다.

<br>

`장점` 

- 사이트 신뢰 문제 해결 가능

`단점`

- 대용량의 데이터를 전송할 때 일일히 암호화/복호화를 진행하기에 무리

<br />

## 3. 대칭키 & 공개키를 활용한 HTTPS 구현 과정
<br>

`확인할 사항`
- 해당 사이트가 공유한 공개키가 정품이 맞는가?(모방사이트의 공개키는 아닌가?)
- CA(Certificate Authority) : 정품이 맞는지 인증해주는 공인 민간 기업

`브라우저->서버 접속 시 과정`

<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_8.png" width="600px">
</div>

1. 클라이언트(브라우저)는 서버를 신뢰하지 못한다. 따라서 handshake를 통해 탐색과정을 거침

<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_9.png" width="600px">
</div>

2. 서버는 답변으로 서버측에서 생성한 무작위 데이터와 인증서를 실어서 보냄

<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_10.png" width="600px">
</div>

3. 클라이언트는 인증서 진위여부를 브라우저에 내장된 CA의 정보를 통해 확인한다. 이때 **비대칭키 시스템**을 사용

<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_11.png" width="600px">
</div>

4. CA의 인증을 받은 인증서들은 해당 CA의 개인키로 암호화가 되어있음
-> 인증서 O : 브라우저에 저장된 **CA의 공개키로 데이터 복호화 가능**

<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_12.png" width="600px">
</div>

-> 인증서 X : 브라우저의 주소창에 위 이미지와 같은 표시가 발생


5. 인증서 복호화 O : 서버의 공개키가 포함되어있음<br>
-> 이때 주고 받은 데이터들은 **대칭키 방식과 비대칭 키 방식이 혼합되어 사용**


### 대칭키와 비대칭키의 혼합방식
<br>

`이유`

- 비대칭 키 방식으로 메시지를 암호화 및 복호화하는 건 대칭키로 할 때 보다 컴퓨터에 훨씬 큰 부담을 준다.<br>
-> 다량의 데이터를 비대칭 키로 일일히 암호화, 복호화 작업하는 것은 무리가 있다.


`구현`

<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_13.png" width="600px">
</div>

1. 데이터를 대칭키로 암호화

2. 그 대칭키를 공유할 때 비대칭키 사용

<div align='center'>   
    <img src="img/Symmetric_Key & Public_Key_14.png" width="600px">
</div>

3. handshake가 발생했을 때 사용하던 **무작위 데이터를 혼합**하여 **임시키 생성**<br>
-> 임시 키는 공개키로 암호화하여 서버로 전송

4. 서버와 클라이언트 양쪽에서 일련의 과정을 거쳐, **동일한 대칭키 생성**<br>
-> 대칭키를 공유할 일이 없으므로, 3자가 키를 가로챌 가능성이 낮아짐

> **대칭키를 주고받을 때만 공개키 암호화 방식을 사용하고 이후에는 계속 대칭키 암호화 방식으로 통신한다.**





## 4. 면접질문

Q1.  HTTP와 HTTPS는 무엇이고, 어떤 차이점이 있나요?

Q2.  SSL 인증서 암호화 기법인 대칭키 암호화 기법, 공개키 암호화 기법에 대해 설명해보세요.



## 5. 참고자료

- [HTTP vs. HTTPS 정리1](https://maivve.tistory.com/160?category=869411)
- [HTTP vs. HTTPS 정리2](https://devjem.tistory.com/3)
- [HTTP 통신 설명](https://sooolog.dev/HTTP-%ED%86%B5%EC%8B%A0%EA%B3%BC-TCP-%ED%86%B5%EC%8B%A0-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EC%9B%B9-%EC%86%8C%EC%BC%93%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC/)

- [대칭키와 비대칭키 정리](https://velog.io/@minj9_6/%EB%8C%80%EC%B9%AD%ED%82%A4%EC%99%80-%EB%B9%84%EB%8C%80%EC%B9%AD%ED%82%A4%EB%8A%94-%EB%AC%B4%EC%8A%A8-%EC%B0%A8%EC%9D%B4%EA%B0%80-%EC%9E%88%EC%9D%84%EA%B9%8C)

- [면접질문 정리](https://maivve.tistory.com/278)

- [총 정리](https://www.youtube.com/watch?v=H6lpFRpyl14)
