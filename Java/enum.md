# enum

## 목차

1. 상수를 정의하는 다양한 방법
2. enum(enumeration - 열거)이란?
3. enum에 멤버 추가하기
4. enum의 조상 java.langh.enum
5. EnumSet과 EnumMap
6. 면접질문

## 1. 상수를 정의하는 다양한 방법

enum은 여러개의 상수를 선언할 때 편리하게 선언할 수 있는 방법이다. 자바 1.5버전 이후에는 상수를 정의할 때 enum을 많이 사용하고 있지만, enum이 나오기 이전에는 어떻게 상수를 표현했을까?

### ✅ 값에 따라 결과 고정시키기

먼저 첫번째 방법은 값에 따라서 각각에 맞는 결과값이 출력되도록 하는 방법이다.

```java
/**
 * 월요일 == 1
 * 화요일 == 2
 * 수요일 == 3
 *  */

int day = 1;

switch(day) {
    case 1:
        System.out.println("월요일");
        break;
    case 2:
        System.out.println("화요일");
        break;
    case 3:
        System.out.println("수요일");
        break;
    // ...
}
```

위 코드에서는 어떤 값이 어떤 결과를 내야하는지 주석으로 의미를 전달하고 있는데, 만약 주석이 업데이트 되지 않거나 삭제되면 해당 코드가 어떤 의미인지 이해하기가 어려워진다.

### ✅ final 키워드 사용하기

두번째 방법은 아래와 같이 final 키워드를 사용해서 하나씩 정의하는 방법이다.

```java

class Sample {
    private static final int ONE = 1;
    private static final int TWO = 2;
    private static final int THREEE = 3;
}

```

이 경우에는 첫번째 예시와 다르게 상수의 이름이 명확하게 있어서 이해하기 쉬우나, 추가로 상수를 추가하기 위해서는 코드를 한줄 더 추가해야 한다. 결국에는 하나의 값을 정의하기 위해 너무 많은 코드가 작성될 수 있게 된다. 그리고 만약 중복된 이름의 상수가 있다면, 컴파일 단계에서 오류가 발생하게 된다.

이와 같은 중복에 대한 오류를 방지하기 위해 interface나 class로 각각의 상수 집합끼리 중복되지 않도록 정의할 수 있다.

### ✅ interface나 class 활용하기

아래와 같이 interface를 활용하면 필요한 곳에서 interface를 가져다 사용하기만 하면 된다. 또한 명확하게 `DAY`라는 집합으로 묶여져 있기 때문에, 다른데서 동일하게 `MONDAY` 상수를 정의하더라도 중복될 위험도 없다. 그리고 `public static final` 속성도 생략할 수 있어서 코드를 더 간결하게 쓸 수도 있다.

```java
interface DAY {
    int MONDAY = 1;
    int TUESDAY = 2;
    int WEDNESDAY = 3;
    int THURSDAY = 4;
}
```

하지만 이 방법도 문제가 있다. 서로 다른 집합에 정의된 상수들이 서로 비교가 되면 안되는데, 위와 같이 정의하면 서로 다른 집합의 상수들이 비교가 가능해진다.

```java

interface DAY {
    int MONDAY = 1;
    int TUESDAY = 2;
    int WEDNESDAY = 3;
    int THURSDAY = 4;
}

interface DAY2 {
    int MONDAY = 1;
    int TUESDAY = 2;
    int WEDNESDAY = 3;
    int THURSDAY = 4;
}
class Sample {
    public static void main(String[] args) {
        if(DAY.MONDAY == DAY2.MONDAY) {
            // true
        }
    }
}
```

위와 같이 비교하게 되면 값만 비교하기 때문에 true가 나온다. 이러한 문제점들을 해결하는 방법이 바로 enum이다.

## 2. enum(enumeration - 열거)이란?

enum은 `열거형`이라고 하는데, 열거형은 서로 연관된 상수들의 집합이다. 문자열이나 숫자들을 나타내는 기본 자료형의 값을 고정할 수 있다. 만약 어떤 클래스가 상수로만 이루어져 있다면 class로 선언할 필요 없이, enum으로 선언해주면 된다.

enum을 정의할때는 아래와 같이 사용한다.

```java
enum 열거형이름 {상수명1, 상수명2...}
```

그리고 enum을 활용하면 아래와 같이 작성할 수 있다.

```java
class Sample {
    static final int ONE = 1;
    static final int TWO = 2;
    static final int THREEE = 3;
}
```

```java
 enum Numbers {ONE, TWO, THREE};
 enum Foods {CARROT, MEAT, RICE};
class Sample {
    final Numbers numbers;
    final Foods foods;
}
```

- 코드가 단순해지고 가독성이 좋아진다.
- 인스턴스 생성과 상속을 방지한다.
- 키워드 enum을 사용하기 때문에 구현의 의도가 열거임을 분명하게 나타낼 수 있다.
- 자동완성, 오타검증 등등 IDE의 적극적인 지원을 받을 수 있다

## 3. enum에 멤버 추가하기

enum 상수에는 추가 속성을 부여할 수 있다. 예를 들어서 enum 타입의 상수들이 방향을 의미할때, 방향의 속성들까지 함께 표현될 수 있다.
멤버를 추가하기 위해서는 아래와 같은 조건들이 있어야 한다.

1. 멤버 값을 할당하기 위해 생성자를 만들어줘야 한다.
2. 해당 값을 가져오기 위한 getter를 만든다.

결국 일반 클래스의 생성자와 getter를 만드는 것과 동일하다.

```java

enum Direction {
    EAST("동"),
    WEST("서"),
    SOUTH("남"),
    NORTH("북"),

    private final String value;
    // 꼭 final이어야 할 필요는 없지만 상수값을 저장하기 위함이므로 final로 지정
    Dirction(String value) {
        this.value = value;
    }
    public String getValue() {
        return value;
    }
    }
```

주의해야 할 점은 일반 클래스와 같이 생성자를 만들고 getter를 만들었지만 `new` 키워드로 객체를 생성하는 것은 불가능하다. 왜냐하면 기본적으로 enum의 생성자는 묵시적으로 `private`이기 때문이다.

```java
    /**
     * Sole constructor.  Programmers cannot invoke this constructor.
     * It is for use by code emitted by the compiler in response to
     * enum type declarations.
     *
     * @param name - The name of this enum constant, which is the identifier
     *               used to declare it.
     * @param ordinal - The ordinal of this enumeration constant (its position
     *         in the enum declaration, where the initial constant is assigned
     *         an ordinal of zero).
     */
    protected Enum(String name, int ordinal) {
        this.name = name;
        this.ordinal = ordinal;
    }
```

- 단독 생성자. 프로그래머는 이 생성자를 호출할 수 없습니다.
- 컴파일러가 생성한 코드에 대한 응답으로 사용하기 위한 것입니다.

### ✅ enum의 비교

enum은 클래스와 마찬가지로 그 자체로 타입이 된다. 이러한 특성과 함께 enum을 사용해서 상수를 정의했을 때, 값을 비교하면 값 비교 이전에 타입을 먼저 비교한다. 따라서 아래와 같이 비교하게 되면 컴파일 에러가 발생하게 된다.

```java
if(Sample.Numbers.One == Sample.Foods.CARROT) {}
// 둘다 값 자체는 0이지만 타입이 다르기 때문에 complie에러가 발생한다.
```

따라서 enum은 같은 enum 내에서만 `==`으로 비교가 가능한데(같은 객체내에서 값만 비교), `equals()` 메서드가 아닌 `==`으로 비교한다는 것은 그만큼 빠른 성능을 제공한다는 것이다. 하지만 `<` 나 `>`는 사용할 수 없고 `compareTo`메서드로 비교해야 한다.

> `==` 비교 : 주소값을 비교. 컴파일 시 타입 체크가 들어감.

> `equals()` 비교 : 객체의 값을 비교. 내부적으로 값을 비교할 때 `==`을 사용한다. 컴파일 단계에서 타입 체크를 하지 않는다.

아래는 enum 객체의 `compareTo()` 메서드의 구현부인데, 같은 enum 타입이 아니면 예외가 발생하도록 처리되어 있다. 그리고 기존 `compareTo()`메서드와 동일하게, 오른쪽이 크면 음수, 같으면 0, 왼쪽이 크면 양수를 리턴해준다. 아래 코드에서 보면 ordinal 값으로 비교하는 것을 볼 수 있다.

```java
    public final int compareTo(E o) {
        Enum<?> other = (Enum<?>)o;
        Enum<E> self = this;
        if (self.getClass() != other.getClass() && // optimization
            self.getDeclaringClass() != other.getDeclaringClass())
            throw new ClassCastException();
        return self.ordinal - other.ordinal;
    }
```

## 4. enum의 조상 java.lang.enum

enum의 조상은 `java.langh.Enum`이고, 이 클래스는 아래와 같은 메서드를 제공한다.

| 메서드                                    | 설명                                                      |
| ----------------------------------------- | --------------------------------------------------------- |
| CLASS<E> getDeclaringClass()              | 열거형 class 객체를 반환한다.                             |
| String name()                             | 열거형 상수의 이름을 문자열로 반환한다.                   |
| int ordinal()                             | 열거형 상수가 정의된 순서를 반환한다.(0부터 시작)         |
| T valueOf(Class<T> enumType, String name) | 지정된 열거형에서 name과 일치하는 열거형 상수를 반환한다. |

```java
package bronz;
public enum Day{
    MONDAY("월요일"),
    TUESDAY("화요일"),
    WEDNESDAY("수요일"),
    THURSDAY("목요일"),
    FRIDAY("금요일");

    private final String name;
    Day(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

```java

public class Main {
    public static void main(String[] args) throws IOException {
        System.out.println(Day.FRIDAY.getDeclaringClass());
        System.out.println(Day.FRIDAY.name());
        System.out.println(Day.FRIDAY.ordinal());
        System.out.println(Day.valueOf("FRIDAY"));
    }
}
```

```bash
class bronz.Day // getDeclaringClass()
FRIDAY // name()
4 // ordinal()
FRIDAY // valueOf()
```

💡 ordinal()은 열거형 상수가 정의된 순서를 반환하지만, 이 값을 상수의 값으로 사용하지 않는 것이 좋다. 이 값은 enum 클래스 내부적으로만 사용하기 위해 정의된 값이기 때문이다.

## 5. EnumSet과 EnumMap

### EnumSet

EnumSet은 열거형 유형 에 대한 Set 인터페이스 의 특수 구현입니다 . Set 인터페이스를 구현하고 Java에서 AbstractSet을 확장합니다.

- EnumSet 클래스는 Java Collections Framework 의 멤버 이며 동기화되지 않습니다.
- EnumSet의 모든 요소는 집합이 명시적으로 또는 암시적으로 생성될 때 지정되는 단일 열거형 형식 에서 가져와야 합니다.
- EnumSet은 HashSet보다 훨씬 빠릅니다.
- EnumSet은 null 개체를 삽입하려고 하면 null 개체 삽입을 허용하지 않으며 NullPointerException을 발생시킵니다

### EnumMap

EnumMap은 열거 유형 에 대한 Map 인터페이스 의 특수 구현입니다. Map 인터페이스를 구현하고 Java에서 AbstractMap을 확장합니다.

- EnumMap은 HashMap 보다 훨씬 빠릅니다.
- EnumMap 클래스는 Java Collections Framework 의 멤버입니다 .
- EnumMap은 키의 자연스러운 순서로 유지되는 정렬된 컬렉션입니다.
- 각 EnumMap 인스턴스의 모든 키는 동일한 enum 유형 의 키여야 합니다.
- EnumMap은 null 키를 삽입하려고 하면 null 키 삽입을 허용하지 않으며 NullPointerException을 발생시킵니다.
- 성능 향상을 위해 EnumMap은 내부적으로 배열로 표시됩니다.

⭐️ [참고 - EnumSet과 EnumMap](https://www.geeksforgeeks.org/difference-between-enummap-and-enumset-in-java/)

## 6. 면접질문

1. class와 enum의 차이점은 무엇인가?
2. enum을 어떤 상황에서 사용했고, 사용한 이유가 무엇인가?

[참고 - enum의 뿌리를 찾아서](https://www.nextree.co.kr/p11686/)

[참고 - 우아한 형제들 Java enum 활용기](https://techblog.woowahan.com/2527/)
