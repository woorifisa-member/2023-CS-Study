## 목차
1. SQL
2. NoSQL
3. 수직적(Vertical) & 수평적(Horizontal) 확장(Scaling)
4. SQL과 NoSQL의 차이점
5. SQL과 NoSQL을 사용하는 케이스
<br>
<br>

# SQL
<div align='center'>   
    <img src="img/SQL vs NoSQL_1.png" width="600px">
</div>

- `구조화`된 쿼리 언어(Structured Query Language)의 약자로, 특정 유형의 데이터베이스와 상호 작용하는 데 사용하는 쿼리 언어이다.
- RDBMS(관계형 데이터베이스 관리 시스템)에서 데이터 저장, 수정, 삭제, 검색이 가능하다.
<br>

## SQL 특징
### 엄격한 스키마
- 데이터는 사전에 정의된 `엄격한` 데이터 스키마(structure)를 따라 데이터베이스 테이블에 저장된다.
  - column : 하나의 속성에 대한 정보를 저장한다. column마다 이름과 데이터 타입이 정의된다.
  - row(record) : 데이터 `형식에 맞는` 데이터가 저장된다.
  - 스키마를 준수하지 않는 row는 추가할 수 없다.
<br>

### 관계
- 데이터들을 여러 개의 데이블에 나누어 저장하여 데이터의 중복을 피할 수 있다.
- 각 테이블에는 중복된 속성과 이 속성에 따른 데이터가 저장되어있지 않고, 다른 테이블에 저장되지 않은 데이터만을 가지고 있다.
<br>
<br>

# NoSQL
<div align='center'>   
    <img src="img/SQL vs NoSQL_2.png" width="600px">
</div>

- SQL(관계형 데이터베이스)과 반대되는 접근 방식을 갖는다.
- `스키마(구조)와 관계 없이` 다른 구조의 데이터를 같은 `Collection`(=SQL table)에 추가할 수 있다.
- 레코드를 문서(`documents`)라고 부르며, JSON 데이터와 비슷한 형태를 가지고 있다. 
- 관계형 데이터베이스처럼 데이터를 여러 테이블에 나누어 저장되지 않고, 관련 데이터를 **동일한 Collection에 담는다.**
    - ➡️ Collection에는 필요한 모든 정보를 가진 Documents가 있으므로, 데이터 탐색 시, Join할 필요가 없어, **Join 개념이 존재하지 않는다.**
    - Join 하고 싶을 때에는 Collection을 통해 데이터를 복제하여 각 컬렉션 일부분에 속하는 데이터를 산출하도록 한다.
- 여러 컬렉션과 문서가 변경된 경우, 
<br>

## NoSQL 특징
- 유연성 : 스키마 선언이 없어 엄격한 테이블 구조의 제약을 받지 않는다. 따라서 필드의 추가 및 삭제가 자유롭다.
- 확장성 : 수직적 확장성을 제공하여 서버 확장이 용이하다.
- 고성능 : 대용량 데이터를 처리하는 성능이 뛰어나다.
- 가용성 : 여러 대의 백업 서버 구성이 가능하여 장애 발생 시에도 무중단 서비스가 가능하다.
<br>

# 수직적(Vertical) & 수평적(Horizontal) 확장(Scaling)
<div align='center'>   
    <img src="img/SQL vs NoSQL_4.png" width="600px">
</div>

## 수직적(Vertical) 확장
- 단순히 데이터베이스의 서버 성능을 향상시키는 것이다.
- 예) CPU 업그레이드
- 일반적으로 관계형 데이터베이스의 확장 방식이다.
    - 같은 테이블 스키마를 가진 데이터를 다수의 데이터베이스에 분산하여 저장하는 방식인 샤딩(Sharding)을 활용해서 데이터를 저장하여 수평적 확장을 할 수는 있으나, 구현하기 어렵다.
<br>

## 수평적(Horizontal) 확장
- 더 많은 서버가 추가되고 데이터베이스가 전체적으로 분산된다. 따라서 하나의 데이터베이스에서 작동하지만 여러 호스트에서 작동한다.
- NoSQL 데이터베이스에서 기본적으로 수평적 확장을 지원하여, 여러 서버에서 데이터베이스를 쉽게 분산할 수 있다.
<br>
<br>


# SQL과 NoSQL의 차이점
<div align='center'>   
    <img src="img/SQL vs NoSQL_5.png" width="600px">
</div>





<div align='center'>   
    <img src="img/SQL vs NoSQL_3.png" width="600px">
</div>
