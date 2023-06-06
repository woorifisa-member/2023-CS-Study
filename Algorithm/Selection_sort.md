# Selection sort

## 목차

1. 선택정렬이란?
2. 선택정렬의 장단점
3. Javascript / Java / Python으로 선택정렬하기
4. Java에서는 어떤 정렬 알고리즘을 사용할까(참고)
5. 면접예상질문

## 1. 선택정렬이란?

선택 정렬이란 제자리 정렬 알고리즘의 하나로, 다음과 같은 순서로 이루어진다.

- 주어진 리스트 중에 최소값을 찾는다
- 그 값을 맨 앞에 위치한 값과 교체한다
- 맨 처음 위치를 뺀 나머지 리스트를 같은 방법으로 교체한다

### ✅ 선택정렬 예제

<center>
<img width="446" alt="image" src="https://github.com/woorifisa-member/2023-CS-Study/assets/72537762/fd45d44e-a711-4674-9e0b-1ecdbe838f20" />
</center>

### ✅ 의사코드

```
for i = 0 to n:
    a[i]부터 a[n - 1]까지 차례로 비교하여 가장 작은 값이 a[j]에 있다고 하자.
    a[i]와 a[j]의 값을 서로 맞바꾼다.
```

### ✅ 시간 복잡도와 효율성

선택정렬의 시간복잡도는 `O(n^2)` 이다. 선택정렬과 유사한 정렬로는 `삽입정렬`이 있는데, 둘의 차이점은 아래와 같다.

< 선택정렬 >

은 k+1 번째 요소를 찾기 위해 나머지 모든 요소들을 탐색

< 삽입정렬 >

k+1 번째 요소를 배치하는 데 필요한 만큼의 요소만 탐색하기 때문에 선택정렬에 비해 효율적

하지만 삽입정렬 또한 `최악의` 시간복잡도가 `O(n^2)`으로 선택정렬과 같다. 왜냐하면 배열의 길이가 길거나 정렬이 안되어 있을 수록 삽입정렬이나 선택정렬이나 비효율적이라는 단점이 있기 때문이다.

## 2. 선택정렬의 장단점

### 💡 장점

- 알고리즘이 단순하다
- 정렬을 위한 비교 횟수는 많지만, 거품정렬(Bubble Sort)에 비해 실제로 교환하는 횟수는 적기 때문에 많은 교환이 일어나야 하는 자료상태에서 비교적 효율적이다
- 거품정렬(Bubble Sort)와 마찬가지로 정렬하고자 하는 배열 안에서 교환하는 방식이므로 다른 메모리 공간을 필요로 하지 않는다.

### 💡 단점

- 시간복잡도가 O(n^2)으로 비효율적이다
- `불안정 정렬`이다.

> 안정정렬: 중복된 값을 입력된 순서와 동일하게 정렬하는 알고리즘. 대표적으로 삽입정렬, 합병정렬, 버블정렬이 있다.

> 불안정정렬: 중복된 값이 입력된 순서와 동일하지 않게 정렬되는 알고리즘. 대표적으로 퀵정렬, 선택정렬, 계수정렬이 있다.

## 3. Javascript / Java / Python으로 선택정렬하기

### ✅ Javascript

```javascript
function selectionSort() {
  let list = [2, 4, 3, 0, 8, 5];
  let indexMin;
  let temp;
  // n - 1개 만큼 pass가 돌기 때문에 length - 1만큼 반복문을 돌립니다
  for (let i = 0; i < list.length - 1; i++) {
    // 2, 4, 3, 0, 8 까지
    indexMin = i;
    for (let j = i + 1; j < list.length; j++) {
      // 4, 3, 0, 8, 5 까지
      // 원소 하나하나와 비교하면서 최소값을 구합니다.
      if (list[j] < list[indexMin]) {
        // 첫번째 최소값:
        // list[3] = 0
        // list[0] = 2
        // j = 3
        indexMin = j;
      }
      temp = list[indexMin]; // 0을 임시변수에 저장
      // 값 swap
      list[indexMin] = list[i];
      list[i] = temp;
    }
  }
}
```

### ✅ Java

```java
void selectionSort(int[] list) {
    int indexMin, temp;

    for (int i = 0; i < list.length - 1; i++) {
        indexMin = i;
        for (int j = i + 1; j < list.length; j++) {
            if (list[j] < list[indexMin]) {
                indexMin = j;
            }
        }
        temp = list[indexMin];
        list[indexMin] = list[i];
        list[i] = temp;
    }
}
```

### ✅ Python

```python
def selectionSort(x):
	length = len(x)
	for i in range(length-1):
	    indexMin = i
		for j in range(i+1, length):
			if x[indexMin] > x[j]:
				indexMin = j
		x[i], x[indexMin] = x[indexMin], x[i]
	return x
```

## 4. Java에서는 어떤 정렬 알고리즘을 사용할까

### ✅ Arrays.sort()

일반 배열을 정렬하는 Arrays 클래스의 `sort()` 메서드는 `듀열 피봇 퀵정렬`을 사용한다.

```java
    public static void sort(int[] a) {
        DualPivotQuicksort.sort(a, 0, a.length - 1, null, 0, 0);
    }
```

듀얼 피봇 퀵정렬을 일반 퀵정렬과 다르게 피봇을 2개를 두고 3개의 구간을 만들어 퀵정렬을 한다고 한다. 이렇게 하면 랜덤 데이터에 대해서 평균적으로 더 좋은 성능을 낸다고 한다.

### ✅ Collections.sort

Collection의 sort는 Arrays와 다른 알고리즘을 사용하고 있다. 아래 캡처 화면은 ArrayList Collection의 정렬 메서드의 구현부다. 코드 설명을 보면 `Tim정렬`을 사용한다고 되어 있는데, Tim정렬은 삽입정렬과 합병정렬을 결한하여 만든 정렬이다.

<center>
<img width="614" alt="image" src="https://github.com/woorifisa-member/2023-CS-Study/assets/72537762/61e8bf9b-dc7b-4080-8ed8-1317006d711b" />
</center>

### ❓ Arrays.sort() VS Collections.sort()

Arrays와 Collections를 정렬했을때 사용하는 알고리즘이 다른 이유는, `참조 지역성 원리`에 있다고 한다.

> 참조 지역성 원리: 동일한 값 또는 해당 값의 근처에 있는 스토리지 위치가 자주 액세스 되는 특성

이는 CPU의 캐싱 전략에 영향을 미치는데, CPU가 데이터를 액세스하며 해당 데이터만이 아니라 인접한 메모리에 있는 데이터 또한 캐시 메모리에 함께 올려둔다.

정렬의 실제 동작 시간은 `C*시간복잡도+a`이다. 여기서 C의 값은 참조 지역성 원리가 영향을 미친다.

Array는 메모리적으로 각 값들이 연속적인 주소값을 가지고 있기 때문에, `C의 값이 낮다.` 따라서 지역성이 좋은 퀵 정렬을 이용하면, 좋은 성능을 제공할 수 있다.

하지만 Collection의 List는 메모리가 인접한 ArrayList 뿐만 아니라, LinkedList도 함께 있기 때문에 참조 인접성이 좋지 않다. 따라서 Arrays에 비해 `C의 값이 상대적으로 높다.` 따라서 합병정렬과 삽입정렬을 병합한 Tim정렬을 이용하는게 더 좋은 성능을 제공할 수 있다고 한다.

## 5. 면접예상질문

<details>
<summary>선택정렬에 대해 설명해주세요</summary>
선택 정렬은 첫 번째 값을 두번째 부터 마지막 값까지 차례대로 비교하여 최솟값을 찾아 첫 번째에 놓고,
두 번째 값을 세 번째 부터 마지막 값까지 비교하여 최솟값을 찾아 두 번째 위치에 놓는 과정을 반복하며 정렬하는 알고리즘입니다. 시간복잡도는 O(n^2)입니다.
</div>
</details>

[참고 - Java의 sort 알고리즘](https://sabarada.tistory.com/138)

[참고 - Naver d2 Tim sort](https://sabarada.tistory.com/138)

[참고 - 선택정렬 알고리즘](https://prodo-developer.tistory.com/110)

[참고 - 위키백과 선택정렬](https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC)

👍 [실습할수 있는 곳 - 정렬 면접질문 및 연습문제](https://www.techiedelight.com/ko/sorting-interview-questions/)
