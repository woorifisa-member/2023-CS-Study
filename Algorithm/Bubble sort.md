# Bubble Sort

## 목차
1. 버블 정렬이란?
2. 예제
3. JS Code
4. 최적화 (+ 최적화된 JAVA Code)
5. 장/단점
6. 시간 복잡도

<br>
<br>

## 1. 버블 정렬이란?
서로 `이웃`한 값과 비교하여, 더 `작은 값을 앞으로 이동`시키며 정렬한다. 
<br>

(정렬을 하는 방식이 물속에서 물 위로 올라오는 물방울 모양 같다고 해서 버블 정렬이라고 한다.)

<br>
<br>

## 2. 예제
<div align='center'> 
<img src="img/Bubble sort_1.png" width=40%>
<br>

### 1회차
<img src="img/Bubble sort_2.png" width=30%>
<br>

### 2회차
<img src="img/Bubble sort_3.png" width=30%>
</div>

<br>
<br>

## 3. JS Code
### 소스코드
```
function bubbleSort(array) {
    let temp;
    for(let i = 0; i < array.length - 1; i++) {
        for(let j = 0; j < array.length - 1; j++) { 
            if(array[j] > array[j+1]) {
                temp = array[j];
                array[j] = array[j+1];
                array[j+1] = temp;
            }
            console.log(array);
        }
    }
}

bubbleSort([14, 12, 1, 5, 10])
```
### 실행 결과
<div align='center'>  
<img src="img/Bubble sort_4.png" width=25%>
</div>
<br>

### 문제점
이전 회차에서 자리 비교가 한 번도 일어나지 않았다.
-> 정렬이 완료되었다.

기존 코드는 이미 정렬이 완료되었어도, n * n번의 for문을 게속 실행한다.
-> 정렬이 완료된 경우, 루프를 취소하고 빠져 나오도록 한다.

<br>
<br>

## 4. 최적화
### JS
```
function OptimizedBubbleSort(array) {
    let temp;
    let swap;
    for(let i = 0; i < array.length - 1; i++) {
        swap = false;

        for(let j = 0; j < array.length - i - 1; j++) { 
            if(array[j] > array[j+1]) {
                temp = array[j];
                array[j] = array[j+1];
                array[j+1] = temp;
                swap = true;
            }
	    console.log(array);
        }
        if(!swap) break;
    }
}

OptimizedBubbleSort([14, 12, 1, 5, 10])
```

<br>

### JAVA
```
import java.util.Arrays;

public class main {
    public static void main(String[] args) {
        int[] array = { 14, 12, 1, 5, 10 };
	int temp;
        boolean swap;
        
	for(int i = 0; i < array.length - 1; i++) {
         	swap = false;
		for(int j = 0; j < array.length - i - 1; j++) {
			if(array[j] > array[j + 1]) {
				temp = array[j];
				array[j] = array[j + 1];
				array[j + 1] = temp;
                    		swap = true;
			}
                	System.out.println(Arrays.toString(array));
		}
            	if(!swap) break;
	  }
    }
}
```
### 실행 결과
<div align='center'>  
<img src="img/Bubble sort_5.png" width=25%>
</div>
<br>

### 실행 결과
<div align='center'>   
<img src="img/Bubble sort_6.png" width=25%>
</div>
<br>
<br>

## 5. 장단점
### 장점
- 구현이 간단하다.

### 단점
- 시간 복잡도가 평균 모두 O(n*2)로, 비효율적이다.

<br>
<br>

## 6. 시간 복잡도
### 최적화 전
|Average|Best|Worst|
|:---:|:---:|:---:|
|O(n*2)|O(n*2)|O(n*2)|

<br>

### 최적화 후
|Average|Best|Worst|
|:---:|:---:|:---:|
|O(n*2)|O(n)|O(n*2)|
