# ThreadLocal

<br />

## <목차>
1. ThreadLocal 이란
2. ThreadLocal 사용하는 이유
3. TrheadLocal 사용법
4. ThreadLocal 장점
5. 주의할 점
6. 예상 면접 질문

<br />

## 1. ThreadLocal 이란

- ThreadLocal은 쓰레드마다 해당 쓰레드만 접근할 수 있는 저장 공간입니다.

- 아래처럼 여러 요청을 받아도 Java에서 제공하는 쓰레드 로컬을 사용해서 값을 저장하면 각 요청(쓰레드) 마다 쓰레드 자기 자신만 접근할 수 있는 공간에 값이 저장되고 해당 값을 안전하게 사용할 수 있습니다.

![](https://velog.velcdn.com/images/jiny798/post/32e66767-f6ca-4d41-a515-e746c7feccd2/image.png)

<br/> <br/>

## 2. ThreadLocal 사용하는 이유
- 먼저 쓰레드 로컬을 사용하지 않았을 때 발생할 수 있는 상황을 가정하겠습니다.
- SaveService를 빈으로 등록하고,
  이름을 받아서 StoredName에 저장하고 3초뒤 저장된 이름을 출력하는 메서드를 가집니다.

```java
@Service
@Slf4j
public class SaveService {

    private String StoredName;
    
    public String save(String name) {
        log.info("name을 StoredName 에 저장 name={} -> StoredName={}", name, StoredName);
        StoredName = name;

        sleep(3000);

        log.info("조회 StoredName={}",StoredName);
        return StoredName;
    }

```

<br/> <br/>

- 그리고 컨트롤러에서는 name을 요청받아
  위에서 만든 SaveService의 save() 를 호출하도록 하겠습니다.

```java
@Controller
@RequiredArgsConstructor
public class HomeController {

    private final SaveService saveService;

    @GetMapping("/{name}")
    @ResponseBody
    public String saveName(@PathVariable String name){

        //이름을 저장하고 저장된 이름을 출력하는 함수
        saveService.save(name);

        return "ok";
    }
}

```

<br/>

그럼 이제 아래와 같이 브라우저로 요청을 보내겠습니다
PONY 를 전달하는 요청을 보내고, 바로 JINY를 전달하는 요청을 보냅니다
![](https://velog.velcdn.com/images/jiny798/post/792dda36-553b-492d-ac6d-be9b5cf39065/image.png)



[결과]

![](https://velog.velcdn.com/images/jiny798/post/25169cd5-bd52-45d0-bff9-1c58e8b6b97b/image.png)

Service객체는 싱글톤 빈으로 등록되었고, 결국 StoredName 변수도 하나의 공간만 생깁니다.
그래서 StoredName에 PONY가 먼저 저장되었지만, 바로 뒤에 오는 JINY 요청이 덮어 쓰게 되는 것입니다. 흐름을 그림으로 본다면 다음과 같습니다

![](https://velog.velcdn.com/images/jiny798/post/d25e8da1-613a-436d-bfe9-333a1a5a4902/image.png)

여러 스레드가 동일한 변수를 사용하게 되면서 동시성 이슈가 발생하게 됩니다. <br/>
스레드 로컬을 사용하면 스레드마다 저장소가 생겨 이러한 동시성 이슈를 해결할 수 있습니다.

<br/> <br/>

## 3. ThreadLocal 사용법
- 선언
  **ThreadLocal<"저장할 데이터의 타입"> threadLocal = new ThreadLocal<>();**

- ThreadLocal에 값 저장하기
  **threadLocal.set(데이터);**

- ThreadLocal에 저장한 값 불러오기
  **threadLocal.get()**

```java
@Service
@Slf4j
public class SaveService {
    private ThreadLocal<String> StoredName = new ThreadLocal<>();

    public String save(String name) {
        log.info("name을 StoredName 에 저장 name={} -> StoredName={}", name, StoredName);
        StoredName.set(name);

        sleep(3000);

        log.info("조회 StoredName={}",StoredName.get());
        return StoredName.get();
    }

```

<br/>

그리고 다시 PONY 요청을 보내고 JINY 요청을 보냅니다

[결과]

![](https://velog.velcdn.com/images/jiny798/post/3884514e-b5d7-422f-94bc-76b478905a89/image.png)

요청(쓰레드) 마다 쓰레드로컬이 생겨 안전하게 값을 출력할 수 있게 되었습니다.
![](https://velog.velcdn.com/images/jiny798/post/8fde9665-4c26-456c-9c1c-462e9c3ced8e/image.png)

<br/> <br/>

## 4. ThreadLocal 장점

-  ThreadLocal을 통해 멀티쓰레드를 사용해도 Thread-safe 한 환경을 구성할 수 있다.

- 자바에서는 synchronized 예약어를 통해서도 Thread-safe 한 환경을 구성할 수는 있지만 둘은 해당 데이터를 같은 변수에 저장하냐, 다른 변수에 저장하냐에 차이가 있다.

- 쓰레드로컬은 쓰레드 별로 데이터를 다른 변수에 저장하지만,
  synchronized 방식은 쓰레드 별로 같은 변수를 사용하되, 동일한 변수에 접근할 때 나머지 쓰레드들이 접근 못하도록 블락킹하는 방식으로 동작합니다.
  그래서 멀티스레드 환경에서 오히려 성능 저하를 유발할 수 있습니다.

<br/> <br/>

## 5. 주의할 점

- 스프링부트 프로젝트를 하면 쓰레드는 보통 커넥션 풀을 사용해서 재사용하는 방식으로 작동한다.

- 그래서 쓰레드 로컬의 값을 사용 후 제거하지 않으면 커넥션 풀에서 스레드를 꺼냈을 때 스레드 로컬에 값이 남아 있을 수 있다. (아래 그림 참고)

- 반드시 ThreadLocal.remove() 을 통해 저장한 값을 제거해줘야 한다.

![](https://velog.velcdn.com/images/jiny798/post/fb3910fe-2f48-4a0c-9912-30e9eb15c53d/image.png)

<br/> <br/>

## 참고
- https://www.inflearn.com/questions/758827/%EA%B0%95%EC%9D%98%EB%A5%BC-%EB%93%A3%EB%8B%A4-%EB%AC%B8%EB%93%9D-threadlocal%EA%B3%BC-synchronized%EC%9D%98-%EC%84%B1%EB%8A%A5%EC%B0%A8%EC%9D%B4-%EA%B0%80-%EA%B6%81%EA%B8%88%ED%95%98%EC%97%AC%EC%84%9C-%EC%A7%88%EB%AC%B8%ED%96%88%EC%8A%B5%EB%8B%88%EB%8B%A4
- https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B3%A0%EA%B8%89%ED%8E%B8/dashboard
- https://velog.io/@gmtmoney2357/JAVA-%EC%93%B0%EB%A0%88%EB%93%9C-%EB%A1%9C%EC%BB%ACThreadLocal