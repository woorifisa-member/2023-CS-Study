# 목차
1. 정규화의 등장 배경
    - 삽입 이상
    - 삭제 이상
    - 수정 이상
    - 해결안방안
2. 정규화란?
3. 정규형
    - 1차 정규형
    - 2차 정규형
    - 3차 정규형
    - 보이스-코드 정규형
<br>
<br>

# 정규화의 등장 배경

- Table name : student
- Field 
    - stu_id : 학번(기본키)
    - resident_id : 학생의 주민번호
    - name : 학생의 이름
    - year : 학생의 학년
    - address : 학생의 주소
    - dept_id : 학과 번호
    - dept_name : 학과명
    - office : 학과실

<br>

## 삽입 이상(insertion anomaly)
<div align='center'>   
    <img src="img/normalization_1.png" width="600px">
</div>

> 데이터를 삽입할 수 없거나 원치 않는 데이터를 삽입한다.
<br>
상황 : student 테이블에 새로운 학과 정보('930', '물리학과', '303호')를 입력한다면?
<br>
현상 : stu_id는 기본키 이므로 null 삽입이 불가능하다. 따라서 새로운 학과 정보를 삽입하고 싶다면, stu_id에 임의의 값을 생성해서 넣어야 한다.
<br>

## 삭제 이상(deletion anomaly)
<div align='center'>   
    <img src="img/normalization_2.png" width="600px">
</div>

> 삭제되지 말아야 할 정보까지 함께 삭제되는 현상이다.
<br>
상황 : 학번이 ‘1292501’인 레코드를 삭제한다면?
<br>
현상 : '전자공학과'의 office가 '308호'라는 사실도 함께 삭제된다. 만약 이 학생이 '전자공학과'의 유일한 학생이라면 문제가 발생하게 된다.
<br>

## 수정 이상(update anomaly)
<div align='center'>   
    <img src="img/normalization_3.png" width="600px">
</div>

> 중복된 정보의 일부만 수정하여 정보의 불일치(inconsistency)가 발생하는 현상이다.
<br>
상황 : '컴퓨터공학과'의 office가 '201호'에서 '211호'로 변경된다면?
<br>
현상 : dept_name이 '컴퓨터공학과'인 모든 레코드를 수정해야 한다. 만약 세 레코드 중 일부만 수정한다면 정보의 불일치가 발생하게 된다.
<br>

## 해결 방안
<div align='center'>   
    <img src="img/normalization_4.png" width="600px">
</div>

1. student 테이블에서 학과 정보를 `분리`하여 department 테이블을 생성한다.
2. dept_id(학과 번호) 필드를 이용하여 외래키로 학과 정보를 연결한다.

<br>
<br>

# 정규화란?
> 불필요한 데이터 중복을 피하기 위해 스키마를 분해하는 과정이다.


<br>
<br>

# 정규형




<br>
<br>



