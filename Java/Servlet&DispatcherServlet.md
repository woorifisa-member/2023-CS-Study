# Servlet&DispatcherServlet

## 목차

1. CGI
2. Servlet
3. Dispatcher Servlet이란?

## 1. 💡CGI(Common Gateway Interface)

CGI는 서버와 어플리케이션 간에 데이터를 주고 받는 방식 또는 컨벤션이다.
아래와 같이 유저가 웹페이지를 요청했을때, 서버는 요청된 웹페이지를 보내준다. 만약 유저가 form에 어떤 값을 입력해서 서버에 보낸다면, 서버는 해당 정보를 처리해줄 어플리케이션 프로그램에 정보를 보내고 confirmation 메세지를 돌려준다.

클라이언트가 서버에 http 요청을 보내면 서버는 CGI 프로그램에게 요청을 전달해주고, 결과를 전달받기 위한 파이프라인을 연결한다. 따라서 CGI 프로그램은 입력에 대한 서비스를 수행하고, 결과를 클라이언트에게 전달하기 위해 결과 페이지에 해당하는 MIME 타입의 컨텐츠데이터를 웹 서버와 연결된 파이프라인에 출력하여 서버에 전달한다. 서버는 파이프라인을 통해 CGI프로그램에서 출력한 결과 페이지의 데이터를 읽어, HTTP 응답헤더를 생성하여 데이터를 함께 반환해준다.

<div align="center">

<img
  width="575"
  alt="image"
  src="https://github.com/Jiyun-Parkk/algorithm-test/assets/72537762/b81c55f7-3873-41f3-a432-b732710b8294"
/>

</div>

쉽게 말하면, 서버와 어플리케이션이 서로 소통할때, 클라이언트에서 요청한 것을 처리해줄 로직을 담고 있는 인터페이스이다. 따라서 어떤 언어든 이 인터페이스를 구현하기만 하면 웹서버와 소통할 수 있다.

### CGI 장점

- 언어, 플랫폼이 독립적이다.
- 매우 단순하고 다른 Server-side 프로그래밍 언어에 비해 훨씬 쉽게 수행할 수 있다
- 재사용할 수 있는 CGI 코드 라이브러리가 풍부하다
- CGI 코드를 수행하는데 특정 라이브러리가 필요하지 않기 때문에 매우 가볍다

### CGI 단점

- 느리다(요청이 올떄마다 DB connection)을 새로 열어야 한다.
- http 요청마다 새로운 프로세스를 만들기 때문에 서버 메모리를 많이 잡아먹는다.
- 페이지 로드 사이에 데이터가 메모리 캐시될 수 없다.

위와 같은 단점들을 보완하기 위해 등장한것이 바로 Servlet 이다.

## 2. Servlet

클라이언트의 요청을 처리하고, 그 결과를 반환한는 Servlet 클래스의 구현 규칙을 지킨 자바 기술을 의미한다. 클라이언트가 어떤 요청을 보내면 그에 대한 결과를 다시 전송해주기 위한 것이 Servlet의 역할이다.

Servlet은 자바로 만들어진 CGI이다. 그 특징을 보면 아래와 같다.

### Servlet 특징

- 클라이언트의 요청에 대해 동적으로 작동하는 웹 어플리케이션 컴포넌트
- Html을 사용하여 요청에 응답한다.
- java thread를 이용하여 동작한다.
- mvc 패턴에서 controller로 이용된다.
- http 프로토콜 서비스를 지원하는 `javax.servlet.http.httpservlet`클래스를 상속받는다.

일반적으로 웹서버는 정적인 페이지만 제공한다. 따라서 동적인 페이지를 제공하기 위해서는 다른 곳에 도움을 요청하여 동적인 페이지를 작성해야 한다. 이는 사용자가 요청한 시점에 페이지를 생성해서 전달해 주는 것을 의미한다. 이렇게 동적인 페이지를 생성해주는 것이 CGI이다.

### Servlet 동작 방식

<img
  width="615"
  alt="image"
  src="https://github.com/Jiyun-Parkk/algorithm-test/assets/72537762/2ec61f8e-0a05-4806-992c-6e9d60e31d49"
/>

1. 사용자가 URL을 입력하면 HTTP Request가 Servlet Container로 전송한다.
2. 요청을 전송받은 Servlet Container는 HttpServletRequest, HttpServletResponse객체를 생성한다.
3. web.xml을 기반으로 사용자가 요청한 URL이 어느 서블릿에 대한 요청인지 찾는다.
4. 해당 서블릿에서 service메소드를 호출한 후 클라이언트의 Get,Post 여부에 따라 doGet() 또는 doPost()를 호출한다.
5. doGet() or doPost() 메소드는 동적 페이지를 생성한 후 HttpServletResponse객체에 응답을 보낸다.
6. 응답이 끝나면 HttpServletRequest, HttpServletResponse 두 객체를 소멸시킨다.

### Servlet Container

서블릿은 관리자가 필요한데, 관리자 역할을 해주는 것이 Servlet Container다. 예를 들어서, 서블릿이 어떤 역할을 수행하는 정의서라고 하면, 서블릿 컨테이너는 그 정의서를 보고 수행한다고 볼 수 있다.

정리하면 서블릿 컨테이너는 클라이언트의 요청을 받아주고 응답할 수 있게 웹서버와 소켓으로 통신하는데, 대표적인 예로 톰캣이 있다. 톰캣은 실제로 웹 서버와 통신하며 JSP와 Servlet이 작동하는 환경을 제공해준다.

### Servlet Container의 역할

1. 웹서버와 통신 지원
   서블릿 컨테이너는 서블릿과 서버가 손쉽게 통신할 수 있게 해준다.
2. 서블릿 생명주기 관리
   서블릿 컨테이너는 서블릿의 탄생과 죽음을 관리한다.
3. 멀티스레드 지원 및 관리
   서블릿 컨테이너는 요청이 들어올 때 마다 Java Thread를 하나 생성하는데 HTTP 서비스 메소드를 실행하고 나면 스레드는 자동으로 죽게 된다. 원래는 스레드를 관리해야 하지만, 서버가 다중 스레드를 생성 및 운영해주니, 스레드의 안정성에 대해 걱정하지 않아도 된다.
4. 선언적인 보안 관리
   서블릿 컨테이너를 사용하면 개발자는 보안에 관련된 내용을 서블릿 또는 자바 클래스에 구현해 높지 않아도 된다.

### 사용자 요청에 따른 서버 응답 흐름

1. 요청전송
   서버가 사용자로부터 특정 URL 경로로 요청을 받음
2. Instantiate a servlet
   서블릿 컨테이너는 web.xml 파일이나 @WebServlet으로 맵핑된 정보를 토대로 요청받은 URL에 맵핑된 서블릿 클래스를 인스턴스화 함.
3. Processing the business logic
   생성된 클래스 내 메서드에 작성된 소스 코드를 실행
4. Response to the Client
   결과 데이터나 페이지를 사용자에게 응답

사용자 요청에 의해 생성된 서블릿 객체는 서블릿 컨테이너 내부에 보관한다. 그리고 동일한 경로로 요청이 올 경우 보관하고 있던 서블릿을 재사용한다. 매 요청시마다 새롭게 서블릿 객체를 생성하지 않는다.

정리하면 서블릿 컨테이너는 작성된 서블릿 클래스들을 인스턴스화 하고, 서블릿 컨테이너 내부에 보관하고 있다가 요청에 따라 해당 서블릿 객체를 실행시켜주는 역할을 한다.

### Servlet 생명주기

1. init() called
   생성된 서블릿에 별도의 초기화 작업이 필요할 때 사용.
   서블릿이 사용할 리소스 로드. 설정값 초기화 등의 작업이 이루어진다.

2. service() called
   클라이언트로부터 요청이 있을 때마다 계속 호출됨.
   요청 내용에 대한 응답처리와 같은 실제 서블릿이 처리해야 할 작업을 수행함.
3. destroy() called
   서블릿 인스턴스의 종료 작업을 처리할 때 사용된.
   서블릿 컨테이너에 의해 생성되었던 서블릿 인스턴스가 메모리에서 제거될 때 호출됨.

## 3. Dispatcher Servlet이란?

dispatch는 보내다라는 뜻을 가지고 있다. 따라서 Dispatcher Servlet은 HTTP 프로토콜로 들어오는 모든 요청을 가장 먼저 받아 적합한 컨트롤러에 위임해주는 Front Controller라고 할 수 있다.

Front Controller는 여러 컨트롤러 제일 앞에서 서버로 들어오는 클라이언트의 모든 요청을 받아서 처리해주는 역할을 해준다. 기본적인 사용자 요청은 이 서블릿이 담당하고, 사용자가 요청한 세부 경로에 맞게 적합한 Controller나 Handler를 찾아 전달하여 요청을 처리한 후 결과를 응답해준다.

디스패처 서블릿은 공통적인 작업을 먼저 처리한 후에 해당 요청을 처리해야 하는 컨트롤러를 찾아서 작업을 위임한다.

## 디스패처 서블릿의 장점

DispatcherServlet이 등장하면서 web.xml의 역할이 많이 축소되었다. 예전에는 모든 서블릿을 URL 매핑을 위해 web.xml에 모두 등록해 주어야 했지만, dispatcher-servlet이 해당 어플리케이션으로 들어오는 모든 요청을 핸들링해주고 공통 작업을 처리하면서 상당히 편리해졌다.

- 정적 리소스에 대한 요청과 어플리케이션에 대한 요청 분리
- 어플리케이션에 대한 요청을 탐색하고, 없을 경우 정적 리소스에 대한 요청으로 처리

## 면접질문

1. Servlet과 Dispatcher Servlet의 차이를 말씀해주세요.
2. Dispatcher Servlet의 장점을 말씀해주세요.

[참고 - 디스패처 서블릿](https://velog.io/@betterfuture4/Spring-Dispatcher-Servlet-%EC%A0%95%EB%A6%AC)

[참고 - 서블릿](https://tecoble.techcourse.co.kr/post/2021-05-23-servlet-servletcontainer/)

[참고 - 디스패처 서블릿1](https://tecoble.techcourse.co.kr/post/2021-06-25-dispatcherservlet-part-1/)

[참고 - 디스패처 서블릿2](https://tecoble.techcourse.co.kr/post/2021-07-15-dispatcherservlet-part-2/)

[참고 - spring argumentResolve interceptor](https://tecoble.techcourse.co.kr/post/2021-05-24-spring-interceptor/)
