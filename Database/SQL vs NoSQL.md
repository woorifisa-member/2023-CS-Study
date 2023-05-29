## 목차
1. SQL
2. NoSQL
3. SQL과 NoSQL의 차이점
4. SQL과 NoSQL을 사용하는 케이스
<br>
<br>

# SQL
<div align='center'>   
    <img src="img/SQL vs NoSQL_1.png" width="600px">
</div>
- 구조화된 쿼리 언어(Structured Query Language)의 약자로, 특정 유형의 데이터베이스와 상호 작용하는 데 사용하는 쿼리 언어이다.
- RDBMS(관계형 데이터베이스 관리 시스템)에서 데이터 저장, 수정, 삭제, 검색이 가능하다.
<br>

## SQL 특징
### 엄격한 스키마
- 데이터는 사전에 정의된 `엄격한` 데이터 스키마(structure)를 따라 데이터베이스 테이블에 저장된다.
  - column : 하나의 속성에 대한 정보를 저장한다. column마다 이름과 데이터 타입이 정의된다.
  - row(record) : 데이터 형식에 맞는 데이터가 저장된다.
  - 스키마를 준수하지 않는 row는 추가할 수 없다.
<br>

### 관계
- 데이터들을 여러 개의 데이블에 나누어 저장하여 데이터의 중복을 피할 수 있다.
- 각 테이블에는 중복된 속성과 그에 따른 데이터가 저장되어있지 않다.
<br>
<br>

# NoSQL
<div align='center'>   
    <img src="img/SQL vs NoSQL_2.png" width="600px">
</div>
- SQL(관계형 데이터베이스)과 반대되는 접근 방식을 갖는다.
- SQL은 정해진 스키마를 따라야만 데이터 삽입이 가능하지만, NoSQL은 **구조와 관계 없이** 다른 구조의 데이터를 같은 `Collection`(=SQL table)에 추가할 수 있다.
- 스키마와 관계가 없다 => 레코드를 문서(`documents`)라고 부른다.
    - Documents는 JSON 데이터와 비슷한 형태를 가지고 있다. 
- 관계형 데이터베이스처럼 데이터를 여러 테이블에 나누어 저장되지 않고, 관련 데이터를 **동일한 Collection에 담는다.**
    - ➡️ Collection에는 필요한 모든 정보를 가진 Documents가 있으므로, 데이터 탐색 시, Join할 필요가 없어, **Join 개념이 존재하지 않는다.**
    - Join 하고 싶을 때에는 Collection을 통해 데이터를 복제하여 각 컬렉션 일부분에 속하는 데이터를 산출하도록 한다.
    - 
