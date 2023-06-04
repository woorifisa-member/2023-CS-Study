# Heap

## 목차
1. 힙(Heap) 개념
    1.1. 종류<br>
    1.2. 특징
2. 활용예시<br>
3. 구현<br>
    3.1. 힙의 삽입<br>
    3.2. 힙의 삭제
4. 장단점
5. 면접질문 & 코테 예시
6. 참고자료

<br />

## 1. 힙(Heap) 개념

`힙(Heap)` : 완전 이진 트리의 일종으로 <strong>우선순위 큐</strong>를 위하여 만들어진 자료구조. 데이터에서 최대값과 최소값을 빠르게 찾기 위해 고안되었다.

우선순위 큐 : 우선순위의 개념을 <span>큐</span>에 도입한 자료구조

<div align='center'>   
    <img src="img/Heap_1" width="600px">
</div>

<br />

### 1.1 종류
<div align='center'>   
    <img src="img/Heap_2" width="600px">
</div>

- `최대 힙(max heap)` : 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진트리
    - key(부모 노드) >= key(자식 노드) 

- `최소 힙(min heap)` : 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진트리
    - key(부모 노드) <= key(자식 노드)

<br />

### 1.1 특징

여러 개의 값들 중에 최댓값이나 최솟값을 빠르게 찾아내도록 만들어진 자료구조이다.

- `heap order property` : 부모 자식 노드간에 대소 비교가 가능하다
    - 각 노드의 값은 자신의 자식노드가 가진 값보다 크거나 같다(최대 힙, Max heap)
    - 각 노드의 값은 자신의 자식노드가 가진 값보다 작거나 같다(최소 힙, Min heap).

- `heap shape property` : 완전이진트리 모양이다. (완전이진트리 속성을 만족)

> 루트 노드는 항상 최대값 or 최솟값만을 갖는다.(중복허용)

> 키값의 대소관계는 오로지 부모노드와 자식노드 간에만 성립
-> <strong>특히 형제 사이에는 대소관계가 정해지지 않는다.</strong>



<br />


### 2. 활용예시

여러개의 값들 중에서 가장 큰 값이나 가장 작은 값을 찾을 때 사용된다.

- 시뮬레이션 시스템

- 네트워크 트래픽 제어

- 운영 체제에서의 작업 스케쥴링(우선 순위 기반 일들)

- 수치 해석적인 계산



<br />


## 3. 구현

- 힙을 저장하는 표준적인 자료구조는 `배열`

- 구현을 쉽게 하기 위하여 배열의 첫번째 인덱스인 '0'은 사용 X

- 특정 위치의 노드 번호는 새로운 노드가 추가되어도 변하지 않는다.
    - ex. 루트노드의 오른쪽 노드 번호는 항상 3

<div align='center'>   
    <img src="img/Heap_3" width="600px">
</div> 

- 힙에서 부모 노드와 자식 노드의 관계
    - 왼쪽 자식의 인덱스 = (부모의 인덱스)*2
    - 오른쪽 자식의 인덱스 = (부모의 인덱스)*2+1
    - 부모의 인덱스 = (자식의 인덱스)/2

<br>

### 3.1. 힙의 삽입

<div align='center'>   
    <img src="img/Heap_4" width="600px">
</div> 

1. 힙에 새로운 요소가 들어오면, 일단 새로운 노드를 힙의 마지막 노드에 이어서 삽입

2. 새로운 노드를 부모 노드들과 교환해서 힙의 성질을 만족시킴

``` java

/* 최대힙 삽입 */
void insert_max_heap(int x){
maxHeap[++heapSize] = x; // 힙 크기를 하나 증가하고 마지막 노드에 x를 넣는다.

for (int i=heapSize; i>1; i/=2) {
  // 마지막 노드가 자신의 부모 노드보다 크면 swap
  if (maxHeap[i/2] < maxHeap[i]) {
    swap(i/2, i);
  } else {
    break;
  }
}
}

```

#### 3.2. 힙의 삭제

<div align='center'>   
    <img src="img/Heap_5" width="600px">
</div> 

1. 최대 힙에서 최댓값은 루트 노드이므로 루트 노드가 삭제
-> 최대 힙(max heap)에서 삭제 연산은 최댓값을 가진 요소를 삭제하는 것이다.

2. 삭제된 루트 노드에는 힙의 마지막 노드를 가져온다.
 
3. 힙을 재구성한다.

``` java

/* 최대힙 삭제 */
int delete_max_heap(){
if (heapSize == 0) // 배열이 빈 경우
  return 0;

int item = maxHeap[1]; // 루트 노드의 값을 저장한다.
maxHeap[1] = maxHeap[heapSize]; // 마지막 노드의 값을 루트 노드에 둔다.
maxHeap[heapSize--] = 0; // 힙 크기를 하나 줄이고 마지막 노드를 0으로 초기화한다.

for (int i=1; i*2<=heapSize;) {
  // 마지막 노드가 왼쪽 노드와 오른쪽 노드보다 크면 반복문을 나간다.
  if (maxHeap[i] > maxHeap[i*2] && maxHeap[i] > maxHeap[i*2+1]) {
    break;
  }
  // 왼쪽 노드가 더 큰 경우, 왼쪽 노드와 마지막 노드를 swap
  else if (maxHeap[i*2] > maxHeap[i*2+1]) {
    swap(i, i*2);
    i = i*2;
  }
  // 오른쪽 노드가 더 큰 경우, 오른쪽 노드와 마지막 노드를 swap
  else {
    swap(i, i*2+1);
    i = i*2+1;
  }
}
return item;
}

```

<br />


## 3. 장단점

<strong>장점</strong>

- 최대값,최솟값을 찾는데 최적화 되어있다.
(배열이나 연결 리스트 같은 자료구조는 최소/최대 값을 얻어내려면 O(n)이 걸린다.)

- 삽입 및 삭제 연산이 빠르다
    - 힙의 시간 복잡도
    peek() : O(1)
    insert : O(logn)
    remove: O(logn)

<div align='center'>   
    <img src="img/Heap_6" width="600px">
</div> 


<strong>단점</strong>

- 힙은 느슨한 정렬상태(반정렬상태)이므로, 완벽히 정렬되지 않은 상태이다.


<br />


## 5. 면접 질문 및 코테 예시


Q1: 💡 Stack과 Queue, Tree와 Heap의 <strong>구조</strong>에 대해 설명해주세요.

A1 : Stack과 Queue는 선형 자료구조의 일종이며, Array와 LinkedList로 구현할 수 있습니다.
Stack은 후입선출(LIFO)방식 즉, 나중에 들어간 원소가 먼저 나오는 구조이고
Queue는 선입선출(FIFO)방식 즉, 먼저 들어간 원소가 먼저 나오는 구조를 갖습니다.

Tree는 스택과 큐와 같은 선형 구조가 아닌 비선형 자료구조이며, 계층적 관계를 표현하기에 적합합니다.
Heap은 최댓값 또는 최솟값을 찾아내는 연산을 쉽게 하기 위해 고안된 구조로,
각 노드의 키값이 자식의 키값보다 작지 않거나(최대힙) 그 자식의 키값보다 크지 않은(최소힙) 완전이진트리 입니다.


Q2 : 💡 Priority Queue(우선순위 큐)에 대해 설명해주세요.

A2 : 우선순위 큐는 들어간 순서에 상관없이 우선순위가 높은 데이터를 먼저 꺼내기 위해 고안된 자료구조입니다.
우선순위 큐 구현 방식에는 배열, 연결 리스트, 힙이 있고, 그중 힙 방식이 worst case라도 시간 복잡도 O(logN)을 보장하기 때문에 일반적으로 완전 이진트리 형태의 힙을 이용해 구현합니다.


Q3 : 💡 최대 힙, 최소 힙에 대한 상황(트리 그려져있음)이 주어지고, 삽입과 삭제 시 어떻게 진행되는지 설명해주세요. 
+ 수도 코드로 구현 해주세요

A3 : 우선순위를 정하고, 이에 부합하는 것부터 빼야하기 때문에 트리의 부모-자식에 대한 swap이 일어나는 과정을 잘 설명할 줄 알면 될 것 같습니다.

(우선순위 큐 구현하라고 하면 Heap 짜면 됩니다)

<br>

### 코테문제

Q 프로그래머스 level 2. - 더맵게

🔍 문제 설명
매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다.
모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을
아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.

섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)
Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.

Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때,
모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

배열중 스코빌 지수가 가장 낮은 두개의 음식을 조건(x + y*2)을 통해서 계산해
모든 배열의 값이 k 이상이 되게 만들어 섞은 횟수를 return 하는 문제

📢 제한 사항
scoville의 길이는 2 이상 1,000,000 이하입니다.
K는 0 이상 1,000,000,000 이하입니다.
scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.



A : 힙(우선순위 큐)은 자동으로 정렬이 된다는 것을 이용해 제일 작은 값과 그 다음 작은 값을 꺼내 연산 후 비교

``` java

import java.util.*;

class Solution {
    public int solution(int[] scoville, int K) {
        int answer = 0;
        
        
        //우선순위 큐 선언
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        
        //우선순위 큐에 스코빌 배열 요소 삽입
        for(int i : scoville){
            pq.offer(i);
        }
        
        //최솟값이 조건 K보다 작을 때 반복
        while(pq.peek() < K){
            pq.offer(pq.poll() + pq.poll()*2); // 최솟값 반환, 다음 최솟값 반환 * 2
            answer++;
            
            //마지막 남은 음식도 K보다 작으면 -1 반환
            if (pq.peek() < K && pq.size() == 1) {
                answer = -1;
                break;
            }
        }
        
        return answer;

```





## 6. 참고 자료

- 힙의 특징 및 종류 : https://gamedevlog.tistory.com/37

- 힙(Heap)의 활용예시 : https://velog.io/@yanghl98/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Heap%ED%9E%99-%EA%B0%9C%EB%85%90-%EC%A2%85%EB%A5%98-%ED%99%9C%EC%9A%A9-%EC%98%88%EC%8B%9C-%EA%B5%AC%ED%98%84

- 힙(Heap)의 구현 : https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html
- 좀 더 자세한 참고자료 : https://sleepybird.tistory.com/139

- 힙(Heap)의 장단점 : https://velog.io/@tonic523/%ED%9E%99-%EC%98%81%EC%97%AD-vs-%EC%8A%A4%ED%83%9D-%EC%98%81%EC%97%AD

- 면접 1,2번 질문 : https://dev-coco.tistory.com/159

- 면접 3번 질문 : https://okky.kr/articles/673648

- 코테 질문 : 프로그래머스 https://school.programmers.co.kr/learn/courses/30/lessons/42626
- 코테 풀이 : https://velog.io/@mongu_93/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%ED%9E%99Heap-%EB%8D%94-%EB%A7%B5%EA%B2%8C-JAVA
