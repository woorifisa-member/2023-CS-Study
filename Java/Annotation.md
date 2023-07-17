# 목차
- Annotation이란?
  - 의미
  - 용도
  - 종류
- Built-in Annotation
- Meta Annotation
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

## 종류
- Built-in Annotation : 자바에서 기본적으로 제공하는 표준 어노테이션
- Meta Annotation : 커스텀 어노테이션을 만들 수 있게 제공된 어노테이션
<br>
<br>


# Built-in Annotation
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
<br>

> ### @FunctionalInterface <br>
> : 해당 인터페이스가 함수형 인터페이스라는 것을 명시(Java 8 이상). 이 어노테이션이 없어도 함수형 인터페이스로 동작하고 사용하는 데에는 문제가 없음. 그러나 인터페이스 검증과 유지보수를 위해서 붙여주는 것이 좋음. <br>
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
<br>

> ### @Deprecated <br>
> : 해당 메서드가 더 이상 사용되지 않음을 표시. 사용할 경우 컴파일 경고 발생. <br>
<br>
<br>

> ### @SuppressWarnings
> : 이클립스의 컴파일러에서 사용을 권장하지 않는 경고 문구를 노란색 밑줄로 표기하는 경우가 있다. 이 때 선언한 곳의 컴파일 경고를 무시하기 위한 어노테이션
```
@SuppressWarnings("all") // 하나만 적용
@SuppressWarnings({"rawtypes", "unchecked"}) // 두 개 이상 적용
```

<details>
<summary>SuppressWarnings Options</summary>
<div markdown="1">
- all : 모든 경고 <br>
- cast : 캐스트 연산자 관련 경고 <br>
- dep-ann : 사용하지 말아야 할 주석 관련 경고 <br>
- deprecation : 사용하지 말아야 할 메서드 관련 경고 <br>
- fallthrough : switch문에서 break 누락 관련 경고 <br>
- finally : 반환하지 않는 finally 블럭 관련 경고 <br>
- null : null 분석 관련 경고 <br>
- rawtypes : 제너릭을 사용하는 클래스 매개 변수가 불특정일 때의 경고 <br>
- unchecked : 검증되지 않은 연산자 관련 경고 <br>
- unused : 사용하지 않는 코드 관련 경고 <br>
</div>
</details>

<br>
<br>

> ### @SafeVarargs <br>
> : 제너릭같은 가변인자의 매개변수를 사용할 때의 경고를 무시(Java 7 이상)
<br>
<br>

# Meta Annotation
> ### @Retention
> : 컴파일 시 어노테이션을 어느 시점까지 유지할 것인지 결정

<details>
<summary>Retention Options</summary>
<div markdown="1">
- RetentionPolicy.SOURCE : 소스 코드(.java)까지 유지 <br>
- RetentionPolicy.CLASS : 클래스 파일(.class)까지 유지(=바이트 코드) <br>
- RetentionPolicy.RUNTIME : 런타임까지 유지(=사실상 안 사라진다.) <br>
</div>
</details>

<br>
<br>

> ### @Target
> : 어노테이션을 어디에 적용할 것인지 지정
<br>
<br>

> ### @Inherited
> : 어노테이션의 상속을 가능하게 함
```
@Inherited
@interface Anno {}

@Anno
class A {}

// @Inherited가 붙은 애너테이션을 사용했으므로 자식 클래스는 따로 선언할 필요 X
// @Anno
class B extends A {}
```
<br>
<br>

> ### @Documented
> : 해당 어노테이션을 Javadoc에 포함시킴
```
@Documented
public @interface DocInterface {}
```
<br>
<br>

> ### @Native
> : 해당 어노테이션을 네이티브 코드로 선언
> 네이티브 코드 : CPU와 운영체제가 직접적으로 실행할 수 있는 코드들(*.exe, *.dll)
<br>
<br>

# 예상 면접 질문
Q. 어노테이션의 용도에 대해 설명해주세요. <br>
A. 어노테이션은 컴파일러를 위한 정보를 제공하기 위해 사용됩니다. 컴파일 과정에서 어노테이션 정보로부터 해당하는 코드를 생성하는 용도입니다. <br>
<br>

Q. 오버라이딩 어노테이션을 생략해도 어노테이션이 있는 것처럼 동일하게 작동하는데, 왜 오버라이딩 어노테이션을 사용할까요? <br>
A. 컴파일 타임에 오버라이딩에 대한 안전성을 부여해주기 때문입니다. 또한 가독성면에서 이 메서드가 오버리이딩되었음을 쉽게 파악할 수 있습니다. 추가적으로, 오버라이드 시에 메서드명의 오타를 방지할 수 있습니다.


