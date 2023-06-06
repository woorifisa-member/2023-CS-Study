# TDD
<br/>

## 목차

1. TDD란?
2. TDD 방법
3. TDD의 장단점
4. 면접질문
<br/>

## TDD란?

- TDD(Test Driven Development)
    
    : 테스트 주도 개발
    

<p align="center"><img src="https://github.com/woorifisa-member/2023-CS-Study/blob/main/Software%20Engineering/image/tdd.png?raw=true"
width="600px" height="500px"/></p>

- 기존 단위 테스트는 설계(디자인) 이후 코드를 짜고 그에 대한 테스트 코드를 작성함.
- TDD는 테스트 코드를 먼저 개발하고 작성하고 그에 맞춰 실제 코드를 작성함.
- 책을 쓰는 과정에 많이 비유한다. 작가가 목차를 먼저 작성하고 그에 맞게 본문을 작성하는 것 처럼 목차에 해당하는 것이 TDD 에서의 테스트 코드라는 것.
<br/>

## TDD 방법

### TDD의 과정

- 크게 질문, 응답, 정제로 나뉘어짐

(1). 질문

- 작성하고자 하는 메소드나 기능이 무엇인지 선별하고 작성 완료 조건을 정해서 실패 하는 테스트 케이스를 작성하는 행위.
- tdd에서 가장 중요한 부분이자 가장 어려운 부분

(2). 응답

- 테스트 케이스를 통과하는 코드를 작성하는 과정
- 리턴타입은 null, 0 등으로 설정해놓고 시작함. (스켈레톤 구현)
- todo list를 작성하며 진행해 나감.
- 실패한 테스트가 모두 성공하도록 작성해야 함.

(3). 정제

- todo목록을 지우면서 리팩토링이 필요한지 확인함.
- 소스의 가독성이 적절한지, 중복된 코드가 없는지, 이름이 잘못 부여된 메서드나 변수명은 없는지
    
    구조의 개선이 필요하지는 않은지를 확인함.

<br/>

### 예시코드

- 요구사항
    
    중간고사, 기말고사, 과제 점수를 통한 성적을 내는 간단한 프로그램을 만들어보자
    
    점수 총합 90점 이상은 A, 80점 이상은 B, 70점 이상은 C, 60점 이상은 D, 나머지는 F다.
    
    TDD 테스트케이스를 먼저 작성한다.
    
    35 + 25 + 25 = 85점이므로 등급이 B가 나와야 한다.
 <br/>

- 테스트 코드를 먼저 작성

```java
public class GradeTest {
    
    @Test
    public void scoreResult() {
        
        Score score = new Score(35, 25, 25); // Score 클래스 생성
        SimpleScoreStrategy scores = new SimpleScoreStrategy();
        
        String resultGrade = scores.computeGrade(score); // 점수 계산
        
        assertEquals("B", resultGrade); // 확인
    }
    
}
```
<br/>

- 테스트 코드에 맞추어서 필요 클래스들을 작성한다.
- Score 클래스

```java
public class Score {
    
    private int middleScore = 0;
    private int finalScore = 0;
    private int homeworkScore = 0;
    
    public Score(int middleScore, int finalScore, int homeworkScore) {
        this.middleScore = middleScore;
        this.finalScore = finalScore;
        this.homeworkScore = homeworkScore;
    }
    
    public int getMiddleScore(){
        return middleScore;
    }
    
    public int getFinalScore(){
        return finalScore;
    }
    
    public int getHomeworkScore(){
        return homeworkScore;
    }
    
}
```

- SimpleScoreStrategy 클래스

```java
public class SimpleScoreStrategy {
    
    public String computeGrade(Score score) {
        
        int totalScore = score.getMiddleScore() + score.getFinalScore() + score.getHomeworkScore(); // 점수 총합
        
        String gradeResult = null; // 학점 저장할 String 변수
        
        if(totalScore >= 90) {
            gradeResult = "A";
        } else if(totalScore >= 80) {
            gradeResult = "B";
        } else if(totalScore >= 70) {
            gradeResult = "C";
        } else if(totalScore >= 60) {
            gradeResult = "D";
        } else {
            gradeResult = "F";
        }
        
        return gradeResult;
    }
    
}
```
<br/>

## TDD의 장단점
<br/>

### 장점

- **보다 튼튼한 객체 지향적인 코드 생산**<br/>
TDD는 코드의 재사용 보장을 명시하므로 TDD를 통한 소프트웨어 개발 시 기능 별 철저한 모듈화가 이뤄진다. 이는 종속성과 의존성이 낮은 모듈로 조합된 소프트웨어 개발을 가능하게 하며 필요에 따라 모듈을 추가하거나 제거해도 소프트웨어 전체 구조에 영향을 미치지 않게 된다.
- **재설계 시간의 단축**<br/>
테스트 코드를 먼저 작성하기 때문에 개발자가 지금 무엇을 해야하는지 분명히 정의하고 개발을 시작하게 된다. 또한 테스트 시나리오를 작성하면서 다양한 예외사항에 대해 생각해볼 수 있다. 이는 개발 진행 중 소프트웨어의 전반적인 설계가 변경되는 일을 방지할 수 있다.
- **디버깅 시간의 단축**<br/>
이는 유닛 테스팅을 하는 이점이기도 하다. 예를 들면 사용자의 데이터가 잘못 나온다면 DB의 문제인지, 비즈니스 레이어의 문제인지 UI의 문제인지 실제 모든 레이러들을 전부 디버깅 해야하지만, TDD의 경우 자동화 된 유닛테스팅을 전재하므로 특정 버그를 손 쉽게 찾아낼 수 있다.
- **디버깅 시간의 단축**<br/>
이는 유닛 테스팅을 하는 이점이기도 하다. 예를 들면 사용자의 데이터가 잘못 나온다면 DB의 문제인지, 비즈니스 레이어의 문제인지 UI의 문제인지 실제 모든 레이러들을 전부 디버깅 해야하지만, TDD의 경우 자동화 된 유닛테스팅을 전재하므로 특정 버그를 손 쉽게 찾아낼 수 있다.
- **추가 구현의 용이함**<br/>
개발이 완료된 소프트웨어에 어떤 기능을 추가할 때 가장 우려되는 점은 해당 기능이 기존 코드에 어떤 영향을 미칠지 알지 못한다는 것이다. 하지만 TDD의 경우 자동화된 유닛 테스팅을 전제하므로 테스트 기간을 획기적으로 단축시킬 수 있다.
<br/>

### 단점

- **가장 큰 단점은 바로 생산성의 저하이다.**<br/>
개발 속도가 느려진다고 생각하는 사람이 많기 때문에 TDD에 대해 반신반의 한다. 왜냐하면 처음부터 2개의 코드를 짜야하고, 중간중간 테스트를 하면서 고쳐나가야 하기 때문이다. TDD 방식의 개발 시간은 일반적인 개발 방식에 비해 대략 10~30% 정도로 늘어난다.
- SI 프로젝트에서는 소프트웨어의 품질보다 납기일 준수가 훨씬 중요하기 때문에 TDD 방식을 잘 사용하지 않는다.
<br/>

## 면접 질문

- TDD를 적용한 프로젝트를 경험해 봤는지?
- 경험 했다면 어떠한 장단점을 느꼈는지?
