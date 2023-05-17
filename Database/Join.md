# Join

정의 : 두 개의 테이블을 서로 묶어서 하나의 결과를 만들어 내는 것을 말한다. <br />
사용 목적 : 검색하고 싶은 데이터가 한개의 테이블이 아닌 여러개의 테이블에 나누어져 있을 때 데이터를 한번에 검색하기 위함. <br />
JOIN을 사용하기 위해선 두 테이블에 모두 존재하는 `공통 칼럼`이 있어야 한다. <br /><br />

## <목차>
1. INNER JOIN
    1.1 INNER JOIN 종류
2. OUTER JOIN
    2.1 LEFT(RIGHT) OUTER JOIN, FULL OUTER JOIN  

<br />

## 1. INNER JOIN

<br />

### INNER JOIN
* 특정 컬럼을 기준으로 정확히 매칭된 행들만 추출하는 것
* 두 테이블의 특정 칼럼(join시 연결에 사용한 칼럼)이 동일한 행만 추출한다.
* 즉, 두 테이블의 교집합을 추출하는 것

<br />

<div align='center'>   
    <img src="img/database_join_1.jpg" width="750px">
</div>

<br />

### INNER JOIN 예시

#### 테이블 A
|TABLE : FOOD_A|
|ID|FOODNM|
|1|돈까스|
|2|삼겹살|
|3|초밥|
|4|곱창전골|

#### 테이블 B
|TABLE : FOOD_B|
|ID|FOODNM|
|1|초밥|
|2|돈까스|
|3|칼국수|
|4|햄버거|

<br />

```SQL
SELECT *
FROM FOOD_A AS A
INNER JOIN FOOD_B AS B
ON A.FOODNM = B.FOODNM;
```
<br />

#### 결과 테이블
|A.ID|A.FOODNM|B.ID|B.FOODNM|
|----|--------|----|--------|
|1|돈까스|2|돈까스|
|2|초밥|1|초밥|

<br />

### OUTER JION
*   조인하는 테이블에서 한 쪽에는 데이터가 있고, 한 쪽에는 데이터가 없는 경우, 데이터가 있는 쪽 테이블의 내용을 모두 출력하는 것
*   조건에 맞지 않아도 해당하는 챙을 출력하고 싶을 때 사용할 수 있다.
  
<br />

<div align='center'>   
    <img src="img/database_join_2.jpg" width="750px">
</div>

<br />

#### LEFT OUTER JOIN 예시

<br />

#### 테이블 A
|TABLE : FOOD_A|
|ID|FOODNM|
|1|돈까스|
|2|삼겹살|
|3|초밥|
|4|곱창전골|

#### 테이블 B
|TABLE : FOOD_B|
|ID|FOODNM|
|1|초밥|
|2|돈까스|
|3|칼국수|
|4|햄버거|

<br />

```SQL
SELECT *
FROM FOOD_A AS A
LEFT OUTER JOIN FOOD_B AS B
ON A.FOODNM = B.FOODNM;
```
<br />

#### 결과 테이블
|A.ID|A.FOODNM|B.ID|B.FOODNM|
|----|--------|----|--------|
|1|돈까스|2|돈까스|
|2|삼겹살|NULL|NULL|
|3|초밥|1|초밥|
|4|곱창전골|NULL|NULL|
  
* RIGHT OUTER JOIN의 경우 LEFT와 반대
  
### FULL JOIN

* 양쪽 모두에 조건이 일치하지 않는 것들까지 모두 결합한다.
* 즉, LEFT OUTER JOIN과 RIGHT OUTER JOIN을 합친 것에서 중복 행을 제거한 것과 같다.

<br />

<div align='center'>   
    <img src="img/database_join_3.jpg" width="750px">
</div>

<br />

```SQL
SELECT *
FROM FOOD_A AS A
FULL OUTER JOIN FOOD_B AS B
ON A.FOODNM = B.FOODNM;
```

<br />


### 면접 질문 예시 ✏️

<br />

#### Q1 inner join과 outer join의 차이를 설명해주세요

*  inner join은 서로 연관된 내용만 검색하는 조인 방법입니다. 결합할 때 사용하는 칼럼이 동일한 행만 추출하게 됩니다. (두 테이블의 교집합)
*  outer join은 한 쪽에는 데이터가 있고 한 쪽에는 데이터가 없는 경우, 데이터가 있는 쪽의 내용을 전부 출력하는 방법입니다. (두 테이블의 합집합)


<br />

#### Q2 JOIN에서 ON이 WHERE의 차이를 설명해주세요.

* ON이 WHERE보다 먼저 실행되어 JOIN을 하기 전에 필터링을 하고 WHERE는 JOINDMF 한 후에 필터링을 합니다.
* 즉, ON 조건으로 필터링이 된 레코들간 JOIN이 이루어지고 JOIN을 한 결과에서 WHERE 조건절로 필터링이 이뤄집니다.
   

<br /><br />
 
#### Reference
https://cceeun.tistory.com/189
https://admm.tistory.com/40
  
