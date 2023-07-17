# 목차
- Annotation이란?
- Java의 기본 Annotation
- 
- 예상 면접 질문
<br>

# Anotation이란?
## 의미
- 사전적 의미로는 주석
- 자바에서의 어노테이션은 코드 사이에 주석처럼 쓰여서 특별한 의미, 기능을 수행하도록 하는 기술
- 프로그램에게 추가적인 정보를 제공해주는 메타데이터
- Meta Data : 데이터를 위한 데이터. 예를 들어 사진 데이터에서의 날짜, 시간, 위치 등의 데이터.
<br>

## 용도
- 컴파일러에게 코드 문법 에러를 체크하도록 정보를 제공
- 빌드나 배치시 코드를 자동으로 생성할 수 있도록 정보 제공
- 실행 시(Runtime) 특정 기능을 실행하도록 정보 제공
<br>

# Java의 기본 Annotation
> ### @Override <br>
> : 해당 메서드가 부모의 메서드를 오버라이드한 메서드라는 것을 명시. <br>
> 부모 클래스 혹인 인터페이스에서 해당 메서드를 찾을 수 없다면 컴파일 에러 발생.
```
public class Parent {
  public void method() { ... }
}

public class Child extends Parent {
  @Override
  public void method() { ... }
}
```
<br>

> ### @FunctionalInterface <br>
> : 해당 인터페이스가 함수형 인터페이스라는 것을 명시. 이 어노테이션이 없어도 함수형 인터페이스로 동작하고 사용하는 데에는 문제가 없. 그러나 인터페이스 검증과 유지보수를 위해서 붙여주는 게 좋음. <br>
> 메서드가 존재하지 않거나, default method, static method를 제외한 2개 이상의 메서드가 존재할 경우 컴파일 요류 발생
> 함수형 인터페이스 : 추상 메서드가 오직 하나인 인터페이스. default method 또는 static method는 여러 개 존재해도 상관 X
```
@FunctionalInterface
interface CustomInterface<T> {
    // abstract method 오직 하나
    T myCall();

    // default method 는 존재해도 상관없음
    default void printDefault() {
        System.out.println("Hello Default");
    }

    // static method 는 존재해도 상관없음
    static void printStatic() {
        System.out.println("Hello Static");
    }
}
```
<br>

> ### @Deprecated <br>


