# Join

정의 : 한 데이터베이스 내에서 두개 이상의 테이블을 결합한 것
사용 목적 : 검색하고 싶은 데이터가 한개의 테이블이 아닌 여러개의 테이블에 나누어져 있을 때 데이터를 한번에 검색하기 위함
JOIN을 사용하기 위해선 두 테이블에 모두 존재하는 `공통 칼럼`이 있어야 한다.

## 목차 (대분류)
 - INNER JOIN
 - OUTER JOIN (LEFT, RIGHT, FULL OUTER JOIN)

### 소분류
 - INNER JOIN 종류
 - OUTER JOIN 종류
 - 기타 JOIN (Natural JOIN, Self JOIN, CROSS JOIN)

#### 내용
- INNER JOIN
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

- OUTER JION
  - LEFT OUTER JOIN
  
  
  
