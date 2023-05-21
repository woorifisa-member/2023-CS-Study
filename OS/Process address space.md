# 프로세스 주소공간(Process address space)

## 목차

1. [주소공간](https://github.com/woorifisa-tech/2023-CS-Study/blob/main/OS/Process%20address%20space.md#1-%EC%A3%BC%EC%86%8C%EA%B3%B5%EA%B0%84)

   1.1 주소공간이란?

   1.2 프로세스와 주소공간

2. [프로세스 주소공간(메모리 공간) 종류](https://github.com/woorifisa-tech/2023-CS-Study/blob/main/OS/Process%20address%20space.md#2-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EC%A3%BC%EC%86%8C%EA%B3%B5%EA%B0%84%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B3%B5%EA%B0%84-%EC%A2%85%EB%A5%98)

   2.1 코드영역

   2.2 데이터영역

   2.3 BSS영역

   2.4 힙영역

   2.5 스택영역

3. [Java & Javascript 코드 예시](https://github.com/woorifisa-tech/2023-CS-Study/blob/main/OS/Process%20address%20space.md#3-java--javascript-%EC%BD%94%EB%93%9C-%EC%98%88%EC%8B%9C)

   3.1 Java 코드 예시

   3.2 Javascript 코드 예시

4. [예상 면접 질문](https://github.com/woorifisa-tech/2023-CS-Study/blob/main/OS/Process%20address%20space.md#4-%EC%98%88%EC%83%81-%EB%A9%B4%EC%A0%91-%EC%A7%88%EB%AC%B8)

## 1. 주소공간

### 1.1 주소공간이란?

컴퓨팅에서 `주소공간`은 물리 메모리나 가상 메모리, 레지스터 등 어떤 논리적 실체나 물리적 실체에 대응되는 주소의 범위를 정의한 공간을 의미한다. 메모리 주소는 컴퓨터 메모리의 물리적인 위치를 파악해서 데이터가 저장되는 위치를 가르키는데, 일상생활과 비교하면 집 주소와 같다고 할 수 있다.

### 1.2 프로세스와 주소공간

일반적으로 운영체제는 하나의 프로세스에 대하여 하나의 주소 공간을 제공한다. 이 주소공간은 다시말하면 메모리 공간이다. 이 메모리 공간은 메모리 관리자에 의해 제공되는데, 프로그램에 필요한 변수들, 메소드 등이 저장된다.

## 2. 프로세스 주소공간(메모리 공간) 종류

<center>
<img src="https://github.com/Jiyun-Parkk/woorifisa-fe-tech-seminar/assets/72537762/12f627fa-831a-4935-bc04-7d0203f9d8d7" />
</center>

### 2.1 코드영역(Code Space)

- 개발자가 작성한 소스코드가 저장된다
- 실행할 프로그램의 코드가 저장되는 영역으로 텍스트 영역이라고도 부른다
- 실행 파일을 구성하는 명령어들이 올라가는 메모리 영역으로, 함수, 제어문, 상수 등이 저장된다
- 컴파일 타임에 결정되고 중간에 코드를 바꿀 수 없게 `Read-Only`로 지정되어 있다

### 2.2 데이터영역(Data Space)

- 프로그램의 초기값이 있는 `전역변수`와 `정적(static)변수`가 저장되는 영역이다
- 프로그램이 구동되는 동안 항상 접근 가능한 변수가 저장되는 영역이다
- 전역변수, static값을 참조한 코드는 컴파일하고 나면 Data영역의 주소값을 가르키도록 바뀐다
- 데이터 영역은 프로그램의 시작과 함께 할당되며, 프로그램이 종료되면 소멸한다
- 실행 중도에 전역변수가 변경 될 수 도 있으니, 이 영역은 `Read-Write`로 지정되어 있다
- `main`함수가 실행되기 전에 저장된다. BSS영역에 있던 전역변수는 main이 실행되기 전 전부 0으로 초기화 되어 data영역에 저장된다.

### 2.3 BSS(Block Started By Symbol)

- `초기값이 없는 전역변수`와 정적(static) 변수가 저장되는 영역이다
- 초기화를 하지 않은 변수들을 위한 공간을 따로 만들어서 구분이 필요한 이유는, 전체 프로그램의 크기를 작게 만들 수 있기 때문이다
- 여러 프로그램을 다루는 경우 초기화가 안된 변수는 main 함수 실행전 메모리를 아끼는 역할을 할 수 있다.

### 2.4 힙영역(Heap Space)

- 런타임에 크기가 결정되는 메모리 영역이다
- `사용자에 의해 메모리 공간이 동적으로 할당`되고 해제된다
- `참조형의 데이터의 값`이 저장된다
- Heap은 메모리의 낮은 주소에서 높은 주소 방향으로 할당된다
- Heap과 Stack영역은 사실 같은 공간을 공유한다
- Heap이 메모리 위쪽 주소부터 할당되면, Stack은 아래쪽부터 할당된다.
- 각 영역이 상대 공간을 침범하는 일이 발생할 수 있는데, 이를 각각 Heap overflow, Stack overflow라고 한다.

### 2.5 스택영역(Stack Space)

- 함수의 호출과 관계되는 `지역변수`와 `매개변수`가 저장되는 영역이다
- Stack은 함수의 호출과 함께 할당되며, 함수의 호출이 완료되면 소멸한다
- `원시타입의 데이터가 값`과 함께 할당된다
- Heap 영역에 생성된 `Object타입의 데이터 참조값`이 할당된다
- 메모리의 높은 주소에서 낮은 주소의 방향으로 할당된다
- 컴파일 타임에 크기가 결정되기 때문에 `무한히 할당` 할 수 없다
- 재귀함수가 너무 깊게 호출되거나 함수가 지역변수를 너무 많이 가지고 있어 stack영역을 초과하면 stack overflow에러가 발생한다

## 3. Java & Javascript 코드 예시

### 3.1 Java 코드 예시

```java
public class Main {
  public static void main(String[] args) { // static main 함수는 Data 영역에 저장
    // new 연산자로 인스턴스가 생성되면 heap영역으로 들어간다
    // 개발자의 의도에 따라 만들어진 객체는 다양한 크기를 가질 수 있기 때문에 동적영역에 할당된다.
    Test test = new Test();
    String name = test.getName();
    System.out.println(name);

	System.out.println(Test.age);
	Test.printAge();

  }
}

class Test { // class는 정적 메모리 영역인 Data영역에 저장된다
	private String name = "jiyun";
	static int age = 0; // static 키워드가 붙은 변수나 함수도 Data 영역에 저장된다
	static void printAge() {
		System.out.println("바보");
	}
	String getName() {
		return this.name;
	}
}
```

<center>
<img src="https://github.com/Jiyun-Parkk/woorifisa-fe-tech-seminar/assets/72537762/301048b3-69de-4f4c-b4c0-4fc5df7c2d72" />
</center>

### 3.2 Javascript 코드 예시

```javascript
const a = "a";
const b = {
    apple:"red";
}
let c;
function test(name, age) {
    let myName = name;
    return console.log(myName, age);
}
test('jiyun', 0)
```

<center>
<img src="https://github.com/Jiyun-Parkk/woorifisa-fe-tech-seminar/assets/72537762/73ff4f1b-7ff3-4601-98e7-89ff4ae6cc80" />
</center>

## 4. 예상 면접 질문

### Q1. 프로세스의 구역을 나눈 이유가 무엇인가?

최대한 데이터를 공유하여 메모리 사용량을 줄이기 위함입니다. Code는 같은 프로그램 자체에서 모두 같은 내용이기 때문에 따로 관리하여 공유합니다. 예를들면 같은 프로그램을 여러개 띄울때 Code영역을 공유할 수 있습니다. Stack과 Data를 나눈 이유는, 스택 구조의 특성과 전역 변수의 활용성을 위함 입니다.

### Q2. Data영역과 BSS영역을 구분하는 이유는 무엇인가?

초기화되지 않은 변수는 프로그램이 실행될 때 영역만 잡아주면 되고, 그 값을 프로그램에 저장하고 있을 필요는 없으나 초기화가 되는 변수는 그 값도 프로그램에 저장하고 있어야 하기 때문입니다. 따라서 bss 영역 변수들이 많아져도 프로그램의 실행코드 사이즈를 늘리지 않습니다.

[참고-주소공간 위키백과](https://ko.wikipedia.org/wiki/%EC%A3%BC%EC%86%8C_%EA%B3%B5%EA%B0%84)

[참고-프로세스 주소공간](https://gona.tistory.com/4)

[참고-BSS 위키백과](<https://namu.wiki/w/BSS(%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B3%B5%ED%95%99)>)

[참고-메모리구조](https://june-17.tistory.com/211)
