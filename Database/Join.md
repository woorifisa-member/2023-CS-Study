# Join

정의 : 두 개의 테이블을 서로 묶어서 하나의 결과를 만들어 내는 것을 말한다.<br/>
사용 목적 : 검색하고 싶은 데이터가 한개의 테이블이 아닌 여러개의 테이블에 나누어져 있을 때 데이터를 한번에 검색하기 위함.<br/>
JOIN을 사용하기 위해선 두 테이블에 모두 존재하는 `공통 칼럼`이 있어야 한다.<br/>

## 목차
- INNER JOIN
 - INNER JOIN 종류
- OUTER JOIN
 - LEFT(RIGHT) OUTER JOIN, FULL OUTER JOIN <bt/>

### INNER JOIN

![image](https://github.com/woorifisa/2023-CS-Study/assets/61819350/71c5f48e-5753-40ff-ac4b-8c16854ba3f5)

특정 컬럼을 기준으로 정확히 매칭된 행들만 추출한다. (-> 두 테이블의 특정 칼럼(join시 연결에 사용한 칼럼)이 동일한 행만 추출한다.)
즉, 두 테이블의 교집합을 추출하는 것

SQL 코드 예시
```SQL
SELECT *
FROM FOOD_A AS A
INNER JOIN FOOD_B AS B
ON A.FOODNM = B.FOODNM;
```
결과 테이블 예시
|A.ID|A.FOODNM|B.ID|B.FOODNM|
|----|--------|----|--------|
|1   |돈까스   |2   |돈까스    |
|2   |초밥     |1   |초밥     |

#### OUTER JION

##### LEFT OUTER JOIN

  ![image](https://github.com/woorifisa/2023-CS-Study/assets/61819350/7a9534d0-d23f-4b45-92e4-b3bb05c6c2ae)
  테이블 A는 모두 B에는 A에 존재하는(매핑되는) 행들만 추출한다.
  A에 있는데 B에는 없는 경우 NULL 처리
  
SQL 코드 예시
```SQL
SELECT *
FROM FOOD_A AS A
LEFT OUTER JOIN FOOD_B AS B
ON A.FOODNM = B.FOODNM;
```
 결과 테이블 예시
|A.ID|A.FOODNM|B.ID|B.FOODNM|
|----|--------|----|--------|
|1   |돈까스   |2   |돈까스    |
|2   |삼겹살   |NULL|NULL    |
|3   |초밥     |1   |초밥     |
|4   |곱창전골  |NULL |NULL   |
  
 RIGHT OUTER JOIN의 경우 LEFT와 반대
  
  - FULL JOIN
  ![image](https://github.com/woorifisa/2023-CS-Study/assets/61819350/65c76536-7457-48f1-a26e-75db765bf003)

SQL 코드 예시
```SQL
SELECT *
FROM FOOD_A AS A
FULL OUTER JOIN FOOD_B AS B
ON A.FOODNM = B.FOODNM;
```
양쪽 모두에 조건이 일치하지 않는 것들까지 모두 결합한다.
즉, LEFT OUTER JOIN과 RIGHT OUTER JOIN을 합친 것에서 중복 행을 제거한 것과 같음



#### 정리 (면접 질문 예시)
##### Q. inner join과 outer join의 차이를 설명해주세요

A. inner join은 서로 연관된 내용만 검색하는 조인 방법입니다. 결합할 때 사용하는 칼럼이 동일한 행만 추출하게 됩니다. (두 테이블의 교집합)

A. outer join은 한 쪽에는 데이터가 있고 한 쪽에는 데이터가 없는 경우, 데이터가 있는 쪽의 내용을 전부 출력하는 방법입니다. (두 테이블의 합집합)


##### Q. JOIN에서 ON이 WHERE의 차이를 설명해주세요.

A. ON이 WHERE보다 먼저 실행되어 JOIN을 하기 전에 필터링을 하고 WHERE는 JOINDMF 한 후에 필터링을 합니다.
   즉, ON 조건으로 필터링이 된 레코들간 JOIN이 이루어지고 JOIN을 한 결과에서 WHERE 조건절로 필터링이 이뤄집니다.
   
   

  
