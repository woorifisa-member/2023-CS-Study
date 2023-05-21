# Factory Method Pattern

## 목차
1. 개념
2. 예제
3. 사용 시기
4. 장점
5. 단점
6. 예상 면접 질문
<br>
<br>

## 1. 개념
변경이 자주 일어나는 객체 생성 코드를 별도의 공장(Factory) 클래스로 분리 및 캡슐화하여 대신 생성하게 하는 생성 디자인패턴이다.
객체를 생성할 때 어떤 클래스의 인스턴스를 만들지 자식 클래스가 결정하도록 한다.

<div align='center'>   
    <img src="img/Factory_method_1.png" width="600px">
</div>

- Product : 팩토리 메서드로 생성될 객체의 공통 인터페이스
- ConcreteProduct : 구체적으로 객체가 생성되는 클래스
- Creator : 팩토리 메서드를 갖는 클래스
- ConcreteCreator : 팩토리 메서드를 구현하는 클래스로, ConcreteProduct 객체를 생성
<br>
<br>

## 2. 예제
식당의 지점별로 다른 품종의 사과를 제공하는 예제입니다.
<br>

### Product
```
// 사과마다 수행할 공통 작업 추상 메서드 선언
public abstract class Apple {
    public abstract void wash();
    public abstract void peel();
    public abstract void slice();
}
```
<br>

### ConcreteProduct
```
// 사과 품종 중 부사 클래스를 생성하여 추상 메서드 구현
public class Busa extends Apple {
    @Override
    public void wash() {
        System.out.println("Busa: wash");
    }

    @Override
    public void peel() {
        System.out.println("Busa: peel");
    }

    @Override
    public void slice() {
        System.out.println("Busa: slice");
    }
}
```
<br>

### Creator
```
// 자식 클래스에서 getApple 메서드를 무조건 구현하는 추상 메서드인 팩토리 메서드 선언
public abstract class Restaurant {
    public Apple servingApple(String kind) {
        Apple apple = getApple(kind);
        apple.wash();
        apple.peel();
        apple.slice();
        return apple;
    }
    public abstract Apple getApple(String kind);
}
```
외부에서 Apple 객체를 생성할 때는 servingApple() 메서드를 호출하면 되고, 실제로 어던 객체를 생성할 지는 추상 메서드  getApple()를 구현한 자식 클래스에서 결정한다. 
<br>

### ConcreteCreator
```
// Seoul, NewYork 지점별로 다른 품종의 사과를 제공하는 getApple 메서드 오버라이딩
public class SeoulRestaurant extends Restaurant {
    // Factory method
    @Override
    public Apple getApple(String kind) {
        Apple apple = null;
        if(kind.equals("busa")) apple = new Busa();
        else if(kind.equals("hongok")) apple = new Hongok();
        else if (kind.equals("hongro")) apple = new Hongro();
        return apple;
    }
}

public class NewYorkRestaurant extends Restaurant {
    @Override
    public Apple getApple(String kind) {
        Apple apple = null;
        if(kind.equals(“koru")) apple = new Koru();
        else if(kind.equals(“crispy")) apple = new Evercrispy();
        else if (kind.equals(“pl")) apple = new Pinklady();
        return apple;
    }
}
```
새로운 사과 종류가 추가되어도 Factory method만 변경할 필요가 있고 실제 사과를 사용하는 클래스는 영향 받지 않는다. 
매개변수 kind에 따라 사과 객체를 생성하고, 이를 리턴한다.
<br>

#### Main
```
public class Main {
    public static void main(String[] args) {
        Restaurant namgajwa = new SeoulRestaurant();
        namgajwa.servingApple("busa");
        Restaurant manha = new NYRestaurant();
        manha.servingApple("pl");

    }
}
```
<br>
<br>

## 3. 사용 시기
- 생성할 객체의 타입을 예측할 수 없을 때
- 클래스 생성과 사용의 처리 로직을 분리해서 결합도를 낮추고자 할 때
- 코드가 동작해야 하는 객체의 유형과 종속성을 캡슐화를 통해 정보를 은닉하고자 할 때
<br>
<br>

## 4. 장점
- 생성자(Creator)와 구현 객체(concrete product)의 강한 결합을 피할 수 있다.
- 팩토리 메서드를 통해 객체의 생성 후 공통으로 할 일을 수행하도록 지정해줄 수 있다. (`servingApple`)
- 캡슐화, 추상화를 통해 생성되는 객체의 구체적인 타입을 감출 수 있다.
- 단일 책임 원칙 준수 : 객체 생성 코드를 한 곳 (패키지, 클래스 등)으로 이동하여 코드를 유지보수하기 쉽게 할수 있으므로 원칙을 만족한다.
- 개방/폐쇄 원칙 준수 : 기존 코드를 수정하지 않고 새로운 유형의 제품 인스턴스를 프로그램에 도입할 수 있어 원칙을 만족한다.

<br>
<br>

## 5. 단점
- 각 제품 구현체마다 팩토리 객체들을 모두 구현해주어야 하기 때문에, 구현체가 늘어날때 마다 팩토리 클래스가 증가하여 서브 클래스 수가 많아진다.
- 코드의 복잡성이 증가한다.
<br>
<br>


## 6. 예상 면접 질문
Q. 팩토리 패턴이란? <br>
A. 객체를 직접 생성하지 않고, 자식 클래스에서 어떤 객체를 생성할 지 결정하도록 위임하는 생성 디자인 패턴입니다. 객체 생성 코드를 별도의 공장(Factory) 클래스로 분리하여 캡슐화하기때문에 SOLID 원칙 중, 단일 책임 원칙과 개방-폐쇄 원칙을 준수합니다. 그러나 각 Product 구현체가 늘어날 때마다 팩토리 클래스가 증가하여 서브 클래스 수가 많아집니다.
<br>
<br>

Q. 
A.
