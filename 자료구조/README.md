# 📔 자료구조


### ✔️ 연결 리스트 (Linked List)

- 포인터를 이용해서 자료를 연속적으로 저장하는 방식
- 시간 복잡도 (Time Complexity)
    - 검색: `O(n)`
    - 삽입/삭제: `O(1)`



### ✔️ 큐 (Queue) & 스택 (Stack) & 데크 (Deque)

- 큐(Queue)
    - FIFO (First-in First-out); 삽입 시 리스트의 가장 마지막에 추가되며, 삭제 시 가장 앞의 요소가 나온다
- 스택(Stack)
    - LIFO(Last-in First-out); 삽입 시 리스트의 가장 앞에 추가되며, 삭제 시에도 가장 앞의 요소가 나온다
    - 함수 호출의 순서 제어 및 postfix notation으로 표현된 식 연산 시 사용이 가능하다
- 데크(Deque; Double Ended Queue)
    - 삽입과 삭제가 리스트의 양 끝에서 모두 발생 가능한 자료구조



### ✔️ **트리 (Tree)**

- **Cycle이 없는 그래프** ⭐️
- 용어
    - Degree(차수): 노드 별 자식의 수, 혹은 트리의 경우 차수 중 가장 큰 수
    - Terminal Node(단말 노드; Leaf Node): 차수가 0인 노드
    - None-Terminal Node(비단말 노드): 차수가 0이 아닌 노드
    - Sibling(형제 노드): 동일한 부모를 갖는 노드들



### ✔️ 이진 트리 (Binary Tree)

- 노드의 차수가 2인 트리
    - 한 레벨의 최대 노드 개수는 2<sup>i-1</sup>
- 완전 이진트리 (complete binary tree): 마지막 level을 제외하고 모든 level의 노드가 2<sup>i-1</sup> 인 것; 모두 채워진 것
- **트리 순회 (Traversal)**
    - **In-order:** 왼쪽 노드 - 자신 - 오른쪽 노드 순으로 탐색
    - **Pre-order:** 자신 - 왼쪽 노드 - 오른쪽 노드 순으로 탐색
    - **Post-order:** 왼쪽 노드 - 오른쪽 노드 - 자신 순으로 탐색



### ✔️ 이진 탐색 트리 (Binary Search Tree; BST)

- **조건**
    - 노드 왼쪽에 있는 모든 서브트리의 값은 노드 값보다 작음
    - 노드 오른쪽에 있는 모든 서브트리의 값은 노드 값보다 큼
- **시간 복잡도 (Time Complexity)**
    - 검색: `O(log n)`
    - 삽입/삭제: `O(log n)`
    - 단, balance가 맞지 않으면 최악의 경우에 `O(n)`의 시간복잡도를 가짐
- **삽입**
    - 위치를 찾아가며 빈 위치에 넣으면 됨
- **삭제**
    - 자식이 하나 있으면 노드를 삭제하고 그 자식을 위로 올리면 됨
    - 자식이 둘 있으면 오른쪽 자식의 서브트리 중 가장 작은 값으로 교체하고, 해당 노드 다시 삭제
        - 가장 작은 값은 가장 왼쪽에 있는 값이며, 이 노드는 자식이 하나 이하 있음이 보장됨

    <img src="images/bst-delete.png" alt="BST deletion" width="600">



### ✔️ 힙 (Heap)

- 완전이진트리(Complete binary tree)
- 부모의 값이 자식의 값보다 항상 크거나 작음 (큰 경우: max-heap, 작은 경우: min-heap)
- 배열로 표현 가능
    - 부모가 `n[i]`일 때 왼쪽 자식은 `n[i*2]`, 오른쪽 자식은 `n[i*2+1]`
- **삽입**
    - 가장 마지막에 (`n[n.len]`)에 노드 삽입 후, 위 방향으로 percolating 수행

    ![Heap insertion](images/heap-insert.png)

- **삭제 (pop; delete min)**
    - 가장 마지막의 노드를 첫 번째로 옮긴 후 아래 방향으로 percolating 수행

```c
void percolateDown(int[] A, int i, int N) {
    int child = 2 * i;
    int rightChild = 2 * i + 1;
    if (child >= N)
        return;
    if (rightChild < N && A[rightChild] < A[child])
        child = rightChild;

    if (A[i] > A[child]) { // Min-heap
        swap(A[i], A[child]);
        percolateDown(A, child, N);
    }
}
```

- **시간 복잡도 (Time Complexity)**
    - 검색 / 삽입 / 삭제: `O(log n)`
    - Build heap: `O(n)`
    - Heap sort: `O(nlog n)`



### ✔️ 다른 트리들

- **AVL**(Adelson-Velskii and Landis)
    - 왼쪽 서브트리와 오른쪽 서브트리의 높이 차이가 1보다 크면 안됨
    - 삽입 및 삭제시 조건을 검사하고 불만족시 회전 (rotate)
- **B-Tree**
    - 노든 leaf 노드의 level이 같음
    - 한 노드의 키는 최대 b-1개
    - 모든 non-leaf 노드는 b-1이상 b미만의 자식 수를 가짐
- **RB(Red Black) Tree**
    - 노드의 색깔을 red나 black으로 둠
    - 제약조건들을 바탕으로 트리가 한쪽으로 쏠리지 않게 해줌



### ✔️ 해싱 (Hashing)

- 같은 값을 넣으면 항상 같은 값이 나오는 함수(Hash Function)를 이용하여 키를 찾아내고, 이를 테이블의 인덱스로 사용하여 조회 및 삽입을 하는 방식
- 해시 테이블 (Hash Table): 고정된 크기를 가진 key-value 형식의 자료구조 (주로 배열 사용)
- 해시 테이블의 크기가 충분하면 검색, 삽입, 삭제 모두 `O(1)`의 시간 복잡도를 가짐
- **해시 함수 (Hash Function)**
    - 나머지 연산(mod)를 이용하는 방법
    - ASCCI 코드를 이용하는 방법
    - 기타 등등
- **충돌 (Collision)**
    - 2개 이상의 레코드가 같은 키를 가질 수 있는 문제
    - 방법 1: Separate chaining
        - 해시 테이블의 각 레코드를 linked list로 구성하고, 검색 시 순회하는 방식
    - 방법 2: Open addressing
        - 이미 레코드가 사용 중이면 다른 빈 공간을 사용하는 방식
        - Linear probing: 순차적으로 다음 빈 레코드에 삽입
        - Quadratic probing: 키를 i<sup>2</sup> 순으로 증가시켜 빈 공간 검색
    - 방법 3: Extendible hashing
        - Directory 구조로 해시 테이블을 구성하는 방식

---

### 참고 자료

- 한양대학교 자료구조론 수업 강의자료, 노미나 교수 (CSE2010)
  - 교재 - Fundamentals of Data Structures in C 2/e, Horowitz 외
- https://gmlwjd9405.github.io
