# Bubble Sort

### 목차
1. 버블 정렬이란?
2. 예제
3. JS Code
4. 최적화 (+ 최적화된 JAVA Code)
5. 장/단점
6. 시간 복잡도

<br>

## 1. 버블 정렬이란?
서로 **이웃**한 값과 비교하여, 더 **작은 값을 앞으로 이동**시키며 정렬한다. 
<br>

(정렬을 하는 방식이 물속에서 물 위로 올라오는 물방울 모양 같다고 해서 버블 정렬이라고 한다.)

<br>
<br>

## 2. 예제
<img src="https://user-images.githubusercontent.com/93786956/236809472-104d4d85-9e36-42bf-8847-6eb19dc7620d.png" width=40%>
<br>

### 1회차
<img src="https://user-images.githubusercontent.com/93786956/236809589-917dc438-cc0e-4ad5-a3b7-a3f8687442d2.png" width=30%>
<br>

### 2회차
<img src="https://user-images.githubusercontent.com/93786956/236809624-ed9e9c59-07ec-47a6-b34e-5fa4929a4e2b.png" width=30%>
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
<img src="https://github.com/woorifisa/2023-CS-Study/assets/93786956/41a9d809-2d79-4f46-a813-817e4281c414" width=25%>
<br>

### 문제점
이전 회차에서 자리 비교가 한 번도 일어나지 않았다.
-> 정렬이 완료되었다.

기존 코드는 이미 정렬이 완료되었어도, n * n번의 for문을 게속 실행한다.
-> 정렬이 완료된 경우, 루프를 취소하고 빠져 나오도록 한다.

<br>
<br>

## 4. 최적화
#### JS
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

#### JAVA
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
<img src="https://github.com/woorifisa/2023-CS-Study/assets/93786956/cbecd2e9-b578-4837-b834-8d0e99874cfb" width=25%>
<br>

### 실행 결과
<img src="https://github.com/woorifisa/2023-CS-Study/assets/93786956/4c5c1e4d-ffa7-4655-90dd-c9995527862c" width=25%>
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
#### 최적화 전
|Average|Best|Worst|
|:---:|:---:|:---:|
|O(n*2)|O(n*2)|O(n*2)|

<br>

#### 최적화 후
|Average|Best|Worst|
|:---:|:---:|:---:|
|O(n*2)|O(n)|O(n*2)|
