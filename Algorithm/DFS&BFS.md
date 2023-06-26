# DFS & BFS

## 목차

1. 그래프 순회
2. 백트래킹
3. DFS란? - 깊이우선탐색
4. DFS 구현
5. BFS란?
6. BFS 구현

## 1. 그래프 순회

그래프 순회는 하나의 정점으로부터 시작해서 모든 정점들을 한번씩 방문하는 것을 말한다. 예를 들어서 특정 도시에서 다른 도시로 이동할 수 있는 지 여부, 전자 회로에서 특정 단자와 단자가 서로 연결되어 있는지 여부 등이 있다.

## 2. 백트래킹

백트래킹은 모든 경우의 수를 전부 고려하는 알고리즘이다. 방식에 따라서 DFS(Depth First)-깊이우선, BFS(Breadth First)-너비우선, BFS(Best First)-최선우선이 있다.

모든 경우의 수를 고려해야 하는 상황이라면, BFS보다는 DFS로 구현하는 것이 편리하고 좋다.

## 3. DFS란? - 깊이우선탐색

DFS(Depth First Search)는 다른 말로 깊이우선탐색이라고도 하는데, 트리나 그래프에서 한 루트로 탐색하다가 특정 상황에서 최대한 깊숙이 들어가서 확인한 뒤 다시 돌아가 다른 루트로 탐색하는 방식이다.

DFS의 예로는 미로찾기가 있다. 한 방향으로 들어갔다가 막다른 길이면 왔던 길을 돌아가서 다른 방향으로 간다. 이것을 목표지점이 나올 때까지 반복하는 것이다.

따라서 일반적으로 검색이 아닌 순회를 하는 경우에 많이 사용 된다. 특히 단말노드에만 데이터를 저장하는 정렬 트리 구조에서 항상 순서대로 데이터를 방문한다는 장점이 있다.

### DFS 트리

한 정점을 두번 이상 방문하지 않는 연결그래프에서 DFS트리라는 구조가 만들어진다.

<div align="center">
<img width="328" alt="image" src="https://github.com/woorifisa-member/2023-CS-Study/assets/72537762/6454aaec-c6bb-407e-aaae-e4d7e7fd49f9" />
</div>

### DFS 구현방법

DFS는 재귀를 이용하면 쉽게 구현할 수 있다. `탐색 공간이 제한`되어 있고, `탐색 공간 내 탐색 목표가 있는지 검사`할 때 유용하게 사용된다.

재귀는 콜스택이 쌓이는 형식이기 때문에 직접 스택으로 구현할 수 있다.

### 재귀함수 호출 예

```java

public static void main(String args[]){
    returns(3);
}

public static void returns(int n) {
    if(n == 0) {
        return
    } else {
        returns(n - 1);
        System.out.println(n);
    }
}

// 1
// 2
// 3
```

<img width="614" alt="image" src="https://github.com/Jiyun-Parkk/algorithm-test/assets/72537762/68981f12-4454-4478-85b7-e95276678768" />

### DFS 장점

- 현 경로상의 노드들만 기억하면 되므로 저장 공간의 수요가 비교적 적다
- 목표 노드가 싶은 단계에 있을 경우 해를 빨리 구할 수 있다.

### DFS 단점

- 해가 없는 경로에 깊이 빠질 가능성이 있다.
- 미리 지정한 임의 깊이까지만 탐색하고 목표 노드를 발견하지 못하면 다음 경로를 따라 탐색하는 바법이 유용하다
- 얻어진 해가 최단 경로가 된다는 보장이 없다.

## 4. DFS 구현

위에서 언급한 재귀함수로 함수가 콜스택에 쌓이고 호출되는 것이 반복되면 아래의 순서로 DFS 구현이 가능하다.

1. 탐색 시작 노드를 스택에 삽입하고 방문처리를 한다
2. 스택의 최상단 노드에 방문하지 않은 인접 노드가 있으면 그 인접 노드를 스택에 넣고 방문 처리를 한다. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다.
3. 2번 과정을 더이상 수행할 수 없을 때까지 반복한다.

### DFS 템플릿코드

```java
// 1) 방문 검사 배열 - 옵션(중복검사가 필요할경우)
// N은 방문 횟수
boolean[] isVisited = new boolea[N];

Stack<Integer> stack = new Stack<>();
// 2) 초기상태
stack.add(0);
// 3) 탐색 진행
// stack이 빌때까지 진행
while(!stack.isEmpty()){
    int state = stack.pop(); // stack의 가장 위에 있는 요소
    // 4) 중복 검사 - 옵션
    if(isVisited[state]) {
         continue; // 만약 방문한 노드면 다시 탐색
    } else {
        isVisited[state] = true; // 방문하지 않았다면 방문처리
    }
     // 5) 현재의 상태 처리
    /* 현재상태를 처리하는 코드*/

    // 6) 전이상태
    for(int next: getNextStates(state)) {
        // 7) 범위검사 - 별도의 범위가 있을 경우
        if(!범위검사조건){
            continue;
        }
        // 8) 유효성 검사 - 필요한 경우
        if(!유효성검사){
            continue;
        }
        // 9) 상태전이
        stack.push(next);
    }
}
```

1. 방문 검사 배열 - 중복검사가 필요할경우
2. 중복 검사
3. 범위검사 - 별도의 범위가 있을 경우
4. 유효성 검사 - 필요한 경우

### 프로그래머스 타겟넘버

[프로그래머스-타겟넘버](https://github.com/Jiyun-Parkk/algorithm-test/tree/master/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4/lv2/43165.%E2%80%85%ED%83%80%EA%B2%9F%E2%80%85%EB%84%98%EB%B2%84)

## 5. BFS란? - 너비우선탐색

BFS(Breadth First Search)는 DFS와 같이 완전 탐색 기법 중 하나로, 주로 최단 거리나 최단 시간 등 목표상태에 도달할 수 있는 가장 빠른 경로를 탐색하는데 활용된다.

### BFS 탐색 순서

BFS는 탐색 상태와 초기 상태 사이의 거리에 따라 주어진 탐색 공간을 탐색한다. `초기상태에서 가까운 상태부터 탐색`한다. 목표 상태를 발견했다면, 해당 상태가 타색 공간에 있는 여러 목표 상태 중 최단 경로에 있는 상태라는 것을 알 수 있다.

<div align="center">
<img width="315" alt="image" src="https://github.com/woorifisa-member/2023-CS-Study/assets/72537762/115b3901-531d-4b12-9762-eace97b4482d" />
</div>

### BFS의 특징

1. 탐색 공간의 깊이 제한 없음

- BFS는 항상 최단 경로의 목표 상태를 찾아낼 수 있기 때문에 탐색 공간이 아무리 깊더라도 목표 상태가 존재하기만 하면 찾아갈 수 있다. 하지만 목표 상태까지의 시간 복잡도를 잘 따져 보아야 한다.

2. 높은 공간 복잡도

- BFS는 초기 상태의 거리에 따라 탐색을 진행한다. 이떄 같은 거리에 있는 모든 상태를 큐 자료 구조에 넣는다. 일반적으로 트리 높이보다 훨씬 큰 값으로 높은 공간 복잡도를 차지 한다.

## 6. BFS 구현

BFS는 큐 자료구조를 이용하는데, DFS와 마찬가지로 큐가 탐색 공간을 나타내고 상태를 전이시키며 탐색 공간에 추가하는 방식으로 탐색을 진행한다.

```java
boolea[] isVisited = new boolean[N];
Queue<Integer> queue = new LinkedList<>();
queue.add(0);
isVisited[0] = true;
while(!quere.isEmpty()) {
    int state = queue.poll();
    /*현재 상태 state 처리*/
    for(int next: getNextStates(state)) {
        if(!범위 검사 조건) {
            continue;
        }
        if(!유효성 검사) {
            continue;
        }
        // 중복검사
        if(isVisited[state]){
            continue;
        }
        // 방문처리
        isVisited[state] = true;
        queue.add(next);
    }
}
```

대부분 DFS 코드와 동일하지만 두가지 차이점이 있다

- 탐색 공간의 자료구조로 큐를 사용한다는 점
- 중복검사시점. BFS에서는 큐에 넣는 순서대로 상태를 방문한다. 따라서 큐에 넣으면서 방문처리를 하기 때문에 큐에 불필요한 상태가 들어가는 것을 방지할 수 있다.

### 프로그래머스 단어변환

[프로그래머스 단어변환](https://github.com/Jiyun-Parkk/algorithm-test/tree/master/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4/lv3/43163.%E2%80%85%EB%8B%A8%EC%96%B4%E2%80%85%EB%B3%80%ED%99%98)

## 차이점

| 구분         | DFS                         | BFS                    |
| ------------ | --------------------------- | ---------------------- |
| 깊이         | 깊이가 정해져 있을 때       | 깊이에 제한이 없음     |
| 상황         | 모든 경우의 수를 구해야할때 | 최단 경로를 구해야할때 |
| 사용자료구조 | 스택                        | 큐                     |
