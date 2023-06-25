# 트리(Tree)
<br/>

## 목차

1. 트리의 개념
2. 트리의 특징
3. 트리 순회
4. 이진 트리(Binary Tree)
5. 예상 면접 질문
<br/>

## 트리의 개념

### 트리란?

- 그래프의 일종으로 노드와 간선을 이용하여 데이터의 배치형태를 계층구조로 나타낸 자료구조이다.

### 트리의 구조

<p align="center"><img src="https://velog.velcdn.com/images%2Fkimdukbae%2Fpost%2F4680ea5f-ce25-492c-9358-c780bb98611d%2Fimage.png"
width="440px" height="350px"/></p>
<br/>

- 서로 다른 두 노드를 연결하는 길이 하나뿐인 그래프를 트리라고 부른다.
- 일반적으로 대상 정보의 각 항목들을 계층적으로 구조화할 때 사용하는 비선형 자료구조이다.
- 리스트와 다르게 데이터가 단순히 나열되는 구조가 아닌 트리는 부모(parent)와 자식(child)의 계층적인 관계로 표현된다.

## 트리의 특징

- 트리는 하나의 루트 노드를 갖는다.
- 루트 노드는 0개 이상의 자식 노드를 갖고 있다. 그 자식 노드 또한 0개 이상의 자식 노드를 갖고 있고, 이는 반복적으로 정의된다.
- 트리에서 루트노드를 제외한 모든 노드는 단 하나의 부모노드를 가진다.
- 트리는 사이클이 없다.
- 노드(node)들과 노드들을 연결하는 간선(edge)들로 구성되어 있다.
- 노드가 N개인 트리는 항상 N-1개의 간선(edge)을 가진다.
    - 즉, 간선은 항상 (정점의 개수 - 1) 만큼을 가진다.
- 루트에서 어떤 노드로 가는 경로는 유일하다.
    - 임의의 두 노드 간의 경로도 유일하다. 즉, 두 개의 정점 사이에 반드시 1개의 경로만을 가진다.
<br/>
<br/>

## 트리 순회

`트리`의 순회란 `트리`의 각 노드를 체계적인 방법으로 탐색하는 과정을 의미한다. 노드를 탐색하는 순서에 따라 **`전위 순회`, `중위 순회`, `후위 순회`** 3가지로 분류된다.

### 전위 순회(Preorder)

<p align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/a/ac/Preorder-traversal.gif"
width="500px" height="400px"/></p>
<br/>

**루트노드 --> 왼쪽 서브트리 --> 오른쪽 서브트리** 의 순서로 순회하는 방식이다. **`깊이 우선 순회`**라고도 불린다.
<br/>


### 중위 순회(Inorder)

<p align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/4/48/Inorder-traversal.gif"
width="500px" height="400px"/></p>
<br/>

**왼쪽 서브트리 --> 노드 --> 오른쪽 서브트리** 의 순서로 순회하는 방식이다. **`대칭 순회`**라고도 불린다.
<br/>

### 후위 순회(Postorder)

<p align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/2/28/Postorder-traversal.gif"width="500px" height="400px"/></p>
<br/>

**왼쪽 서브트리 --> 오른쪽 서브트리 --> 노드** 의 순서로 순회하는 방식이다.
<br/>
<br/>

## 이진 트리(Binary Tree)

### 이진 트리?

- 트리(Tree) 자료구조는 여러 가지 유형이 있는데, 그중 가장 기본이 되는 트리는 `이진 트리(Binary Tree)` 구조이다.
- `이진 트리`는 2개 이하의 자식노드를 가진다. (자식노드가 없거나 1개의 자식노드만 가지는 것도 가능하다.
- 2개의 자식노드 중에서 왼쪽의 노드를 `Left Node`라고 하고, 오른쪽의 노드를 `Right Node`라고 한다.

### 이진 트리의 종류

- 편향 이진 트리
    
    <p align="center"><img src="https://velog.velcdn.com/images%2Fkimdukbae%2Fpost%2F349a3344-f85e-4a66-ab4e-5d16027f249c%2Fimage.png"width="440px" height="300px"/></p>
    <br/>
    
    편향 이진 트리는 하나의 차수로만 이루어져 있는 경우를 의미한다. 이러한 구조는 배열(리스트)와 같은 선형 구조이므로 'Leaf Node'(가장 아래쪽에 위치한 노드) 탐색 시 모두 데이터를 전부 탐색해야 한다는 단점이 있어 효율적이지 못하다. 
    
    <br/>
    
- 완전 이진 트리
    
    <p align="center"><img src="https://velog.velcdn.com/images%2Fkimdukbae%2Fpost%2F6a9d01ed-de21-41cd-971f-14faaee17946%2Fimage.png"width="440px" height="350px"/></p>
    <br/>
    
    모든 노드가 왼쪽부터 차근차근 생성되는 이진 트리를 의미한다.
    
    힙(Heap)은 완전 이진 트리의 일종이다.
    
    <br/>
    
- 포화 이진 트리
    
    <p align="center"><img src="https://velog.velcdn.com/images%2Fkimdukbae%2Fpost%2F5ca863d7-202e-4fe2-9d71-5fab60dee42e%2Fimage.png"width="440px" height="350px"/></p>
    <br/>
    
    포화 이진 트리는 'Leaf Node'를 제외한 모든 노드의 차수가 2개로 이루어져 있는 경우를 의미한다. 이 경우 해당 차수에 몇 개의 노드가 존재하는지 바로 알 수 있으므로 노드의 개수를 파악할 때 용이한 장점이 있다.
    
    > 리프 노드(leaf node/leaf): 루트 노드를 제외한 차수가 1인 정점을 뜻한다.
    > 
    
    <br/>
    

## 예상 면접 질문

- 트리에 대해서 설명해 주세요
- 이진 트리의 종류에 대해서 설명해 주세요
- 트리의 순회에 설명해 주세요 (필기 시험 같은 것 에서 트리가 주어지고 각 순회에 대해 탐색 노드 순서를 적는 문제가 나오기도 함)
