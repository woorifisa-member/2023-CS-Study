# Bubble Sort

### 목차
1. 버블 정렬의 개념
2. 예제
3. JS/Java Code
4. 장/단점
5. 시간 복잡도


## 1. 버블 정렬이란?
서로 **이웃**한 값과 비교하여, 더 **작은 값을 앞으로 이동**시키며 정렬한다.


## 2. 예제
<img src="https://user-images.githubusercontent.com/93786956/236809472-104d4d85-9e36-42bf-8847-6eb19dc7620d.png" idth=40%>
<br>

### 1회차
<img src="https://user-images.githubusercontent.com/93786956/236809589-917dc438-cc0e-4ad5-a3b7-a3f8687442d2.png" width=40%>
<br>

### 2회차
<img src="https://user-images.githubusercontent.com/93786956/236809624-ed9e9c59-07ec-47a6-b34e-5fa4929a4e2b.png" width=40%>
<br>


## 3. JS Code
### 소스코드
```
function bubbleSort(array) {
    let temp;
    for(let i = 0; i < array.length - 1; i++) {
        for(let j = 0; j < array.length - i - 1; j++) { 
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
<img src="https://user-images.githubusercontent.com/93786956/236810226-142d7733-6adc-42e6-8a19-6c8535c5e978.png" width=20%>
<br>

### 최적화
```
function OptimizedBubbleSort(array) {
    let temp;
    let swap;
    for(let i = 0; i < array.length - 1; i++) {
        swap = false;

        // 한바퀴를 돈 후에는 맨 뒤로 정렬된 가장 큰 값은 비교 제외
        for(let j = 0; j < array.length - i - 1; j++) { 
            if(array[j] > array[j+1]) {
                temp = array[j];
                array[j] = array[j+1];
                array[j+1] = temp;
                swap = true;
                console.log(array);
            }
        }
        if(!swap) break;
    }
}

OptimizedBubbleSort([14, 12, 1, 5, 10])
```
### 실행 결과
<img src="" width=40%>
<br>
