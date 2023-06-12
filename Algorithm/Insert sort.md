# Insert sort

## 목차
1. 삽입 정렬이란?
<br> 1.1 개념
<br> 1.2 예제
2. 특징
<br> 2.1 장점
<br> 2.2 단점
3. 시간 복잡도
<br>4.1  정렬 알고리즘 시간 복잡도 비교
4. 삽입 정렬  의사 코드(Pseudo code)
5. 구현
6. 면접 예상 질문
---
<br>

## 1. 삽입 정렬(InsertionSort)이란?
 선택 정렬, 거품 정렬과 더불어 대표적인 O(N^2)정렬 알고리즘

<br>

### 1.1 개념

- 자료 배열의 모든 요소를 `2번째 부터` 차례대로 `이미 정렬된 배열 앞 (왼쪽) 부분과 비교`
- 자신의 위치를 찾아 삽입할 위치를 지정
- 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입하여 정렬을 완성`하는 알고리즘

<br>

- 매 순서마다 해당 원소를 삽입할 수 있는 위치를 찾아 해당 위치에 삽입

- `key값은 2번째 인덱스부터 시작`, key값이 자료의 길이만틈 이동되었을 때 정렬이 완성된다.

<div align='center'>   
    <img src="img/Insert sort_1.gif" width="750px">
</div>
<br>

### 1.2 예제
<b>예제 1</b>
<div align='center'>   
    <img src="img/Insert%20sort_2.png" width="750px">
</div>

<br>
<b>예제 2</b><br>
배열에 8, 5, 6, 2, 4가 저장되어 있다고 가정하고 자료를 오름차순으로 정렬해 보자

<div align='center'>   
    <img src="img/Insert%20sort_3.png" width="750px">
</div>

<br>

## 특징
패스가 거듭될 수록 탐색 범위가 점점 넓어진다.
<br>(선택/ 거품 정렬은 거듭될 수록 범위가 좁아진다)

### 2.1  장점
- 안정한 정렬 방법 (바로 옆의 데이터와 비교하기 때문)
- 자료의 수가 적을 경우 알고리즘 구현이 매우 간단
- 이미 정렬되어 있는 경우나 자료의 수가 적은 정렬에 매우 효율적

### 2.2  단점
- 비교적 많은 레코드들의 이동을 포함
- 자료의 수가 많고 자료의 크기가 클 경우 적합하지 않음

<br>

## 3. 시간 복잡도
- <b>최선의 경우</b>
    - 비교 횟수
        - 이동 없이 1번의 비교만 이루어진다.
        - 외부 루프: (n-1)번
    - Best T(n) = O(n)

<br>

- <b>최악의 경우(입력 자료가 역순일 경우)</b>
    - 비교 횟수
        - 외부 루프 안의 각 반복마다 i번의 비교 수행
        - 외부 루프: (n-1)+(n-2)+...+2+1=n(n-1)/2=O(n^2)
    - 교환 횟수
        - 외부 루프의 각 단계마다 (i+2)번의 이동 발생
        - n(n-1)/2 + 2(n-1) = (n^2+3n-4)/2 = O(n^2)
    - Worst T(n) = O(n^2)

<br> 

### 4.1 알고리즘 시간 복잡도 비교
<div align='center'>   
    <img src="img/Insert sort_5.png" width="750px">
</div>  
<br>

<div align='center'>   
    <img src="img/Insert sort_4.png" width="750px">
</div>  

- 단순(구현 간단)하지만 비효율적인 방법
    -  삽입 정렬, 선택 정렬, 버블 정렬
- 복잡하지만 효율적인 방법
    - 퀵 정렬, 힙 정렬, 합병 정렬, 기수 정렬
<br>


## 4. 삽입 정렬  의사 코드(Pseudo code)

```
1. i=1
2. j=i
3. a[j-1] > a[i] 이고 j > 0인 동안
  3.1. a[j] = a[j-1]
  3.2. j--
4. a[j] = a[i]
```
- 배열에서 i번째 미만은 이미 정렬된 상태이며 i번째 항을 적절한 위치에 삽입하는 과정을 반복한다.

## 5.구현
- 두개의 반복문이 필요
- 내부 반복문에서는 정렬 범위에 새롭게 추가된 값과 기존 값들을 뒤에서 부터 계속해서 비교해나가면서 앞의 값이 뒤의 값보다 클 경우 자리 교대(swap)
- 외부 반복문에서는 정렬 범위를 2에서 N으로 확대

### ⭐ java
```
void insertionSort(int[] arr)
{
   for(int index = 1 ; index < arr.length ; index++){ // 1.
      int temp = arr[index];
      int prev = index - 1;
      while( (prev >= 0) && (arr[prev] > temp) ) {    // 2.
         arr[prev+1] = arr[prev];
         prev--;
      }
      arr[prev + 1] = temp;                           // 3.
   }
   System.out.println(Arrays.toString(arr));
}
```
- 첫 번째 원소 앞(왼쪽)에는 어떤 원소도 갖고 있지 않기 때문에, 두 번째 위치(index)부터 탐색을 시작한다. 
    1) temp에 임시로 해당 위치(index) 값을 저장하고, prev에는 해당 위치(index)의 이전 위치(index)를 저장한다.
    2) 이전 위치(index)를 가리키는 prev가 음수가 되지 않고, 이전 위치(index)의 값이 '1'번에서 선택한 값보다 크다면, 서로 값을 교환해 주고 prev를 더 이전 위치(index)를 가리키도록 한다.
    3) '2'번에서 반복문이 끝나고 난 뒤, prev에는 현재 temp 값보다 작은 값들 중 제일 큰 값의 위치(index)를 가리키게 된다. 따라서, (prev+1)에 temp 값을 삽입해 준다.

### ⭐ python
```
array = [7,5,9,0,3,1,6,2,4,8]

for i in range(1, len(array)): # 두 번째 원소부터 시작.
	for j in range(i,0,-1): #인덱스 i부터 0까지 1씩 감소하며 반복하는 것. 여기서 j는 삽입하고자 하는 원소를 의미.
    	if array[j]<array[j-1]: #왼 쪽에 있는 데이터와 비교해서, 더 작다면 위치를 바꿔준다.
        	array[j], array[j-1] = array[j-1], array[j]
        else : #자기보다 작은 데이터를 만나면 그 위치에서 멈춘다.
        	break
print(array)
```

### ⭐ JS
```
function insertionSort(array) {
  for (let i = 1; i < array.length; i++) {
    let cur = array[i];

    let left = i - 1;

    while (left >= 0 && array[left] > cur) {
      array[left + 1] = array[left];
      left--;
    }
    array[left + 1] = cur;
    console.log(`${i}회전: ${array}`);
  }

  return array;
}

console.log(insertionSort([5, 4, 3, 2, 1]));
```

### 6. 면접 예상 질문

Q. 삽입 정렬에 대해 설명해주세요<br>
A. 삽입 정렬은 두 번째 값부터 시작해 그 앞에 존재하는 원소들과 비교하여 삽입할 위치를 찾아 삽입하는 정렬 알고리즘입니다.
평균 시간복잡도는 O(n^2)이며, Best Case 의 경우 O(n)까지 높아질 수 있습니다.

<br>

### 참고 자료들
[ 삽입 정렬 Java 구현](https://lealea.tistory.com/252)

[ 삽입 정렬 JS 구현 ](https://velog.io/@rkio/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-JS-%EC%82%BD%EC%9E%85-%EC%A0%95%EB%A0%ACInsertion-Sort#:~:text=function%20insertionSort%28array%29%20%7B%20for%20%28let%20i%20%3D%201%3B,left%EB%B2%88%20%EC%9D%B8%EB%8D%B1%EC%8A%A4%20%EA%B0%92%EC%9D%84%20left%20%2B%201%EB%B2%88%20%EC%9D%B8%EB%8D%B1%EC%8A%A4%EC%97%90%20%EB%84%A3%EB%8A%94%EB%8B%A4.)

[ 예제, 시간 복잡도 ](https://gmlwjd9405.github.io/2018/05/06/algorithm-insertion-sort.html)

[ 의사 코드 예시 ](https://hellmath.tistory.com/19#:~:text=%EC%9A%B0%EC%84%A0%20%EC%82%BD%EC%9E%85%20%EC%A0%95%EB%A0%AC%EC%9D%98%20%EC%9D%98%EC%82%AC%EC%BD%94%EB%93%9C%20%28Pseudo%20code%29%EB%A5%BC%20%EB%B3%B4%EB%A9%B4%20%EB%8B%A4%EC%9D%8C%EA%B3%BC,%EC%83%81%ED%83%9C%EC%9D%B4%EB%A9%B0%20i%EB%B2%88%EC%A7%B8%20%ED%95%AD%EC%9D%84%20%EC%A0%81%EC%A0%88%ED%95%9C%20%EC%9C%84%EC%B9%98%EC%97%90%20%EC%82%BD%EC%9E%85%ED%95%98%EB%8A%94%20%EA%B3%BC%EC%A0%95%EC%9D%84%20%EB%B0%98%EB%B3%B5%ED%95%A9%EB%8B%88%EB%8B%A4.)

[  신입 개발자 기술 면접 질문 정리(삽입 정렬 외의 다양한 자료들 수록) ](https://dev-coco.tistory.com/160#:~:text=%F0%9F%92%A1%20%EC%82%BD%EC%9E%85%20%EC%A0%95%EB%A0%AC%20%28Injection%20Sort%29%EC%97%90%20%EB%8C%80%ED%95%B4%20%EC%84%A4%EB%AA%85%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94.%20%EC%82%BD%EC%9E%85,Case%20%EC%9D%98%20%EA%B2%BD%EC%9A%B0%20O%20%28n%29%EA%B9%8C%EC%A7%80%20%EB%86%92%EC%95%84%EC%A7%88%20%EC%88%98%20%EC%9E%88%EC%8A%B5%EB%8B%88%EB%8B%A4.)