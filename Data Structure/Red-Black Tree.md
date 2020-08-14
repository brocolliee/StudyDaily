





# Red-Black Tree

### 정의 

이진 탐색 트리의 불균형한 트리 구조는 검색 효율이 나빠진다. 레드-블랙 트리(Red-Black Tree)는 이를 해결하기 위해 사용하는 자가 균형 이진 탐색 트리(Self-Balancing Binary Search Tree)이다.



### 속성

 <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Red-black_tree_example.svg/2880px-Red-black_tree_example.svg.png" alt="img" style="zoom: 50%;" /> 



1. **노드는 Red or Black 중 하나다.**
2. **Root 노드는 Black이다.**
3. **모든 리프(leaf) 노드들은 Black이다.**
4.  **Red 노드의 자식들은 모두 Black이다.**
   - Red 노드들은 연속으로 나타날 수 없다.
   - Black 노드 만이 Red 노드의 부모가 된다.
   - Black 노드 자식들은 Red일 필요는 없다.
5. **Root 노드와 모든 리프(leaf) 노드사이에 있는 Black 노드 수는 모두 동일하다.** 
   - **Black-Height** : 어떤 노드(A 노드)로부터 리프(leaf) 노드 사이에 있는 Black 노드의 수 (단, 맨 앞의 노드인 A 노드 제외) 

### 특징

- 레드- 블랙 트리는 이진탐색 트리에서 나온 것으로 **이진 탐색 트리 특징**을 가진다.
- Root 노드부터 리프(leaf) 노드까지의 경로 중  최대 경로(가장 먼 경로)는 최소 경로(가장 가까운 경로)의 2배보다 작다. (**Balanced** 상태)
- NIL은 리프(leaf) 노드라고 간주한다.



### 삽입

- 노드를 insertion 하는 시간 : **O(logn)**으로 현재 노드가 들어갈 위치를 찾는다.

- Black-Height의 변경을 최소화 하기 위해 삽입된 노드는 Red로 지정한다. (속성 #5)

  - Red를 넣게되면 Double Red가 될 수 있다. (속성 #4)

-  레드-블랙 트리의 속성을 유지하기 위해 Rotation을 수행하고 노드의 색을 조절한다. 

  -  **Restructing** : 삽입한 노드와 부모, 부모의 부모를 가지고 Restructing을한다.
- 삽입한 노드 부모의 형제가 Black일 때 사용한다.
    - 다른 서브트리에 영향을 끼치지 않으므로 한번의 Restructuring이면 끝난다.
- Time complexity : 자체 시간 복잡도는 O(1) 이지만 insertion으로 인해 **O(logn)**
    - <img src="https://t1.daumcdn.net/cfile/tistory/998F903359CF658617" alt="img" style="zoom: 33%;" /> 

  - **Recoloring** : 삽입한 노드의 부모와 부모의 형제를 Black으로 하고 내 부모의 부모를 Red로 한다. 
- 삽입한 노드의 부모의 형제가 Red일 때 사용한다. 
    - Restructing과 다르게 여러 번 작업이 될 수 있다.
- Time complexity : 자체 시간 복잡도는 O(1)이지만 또한 Recoloring은 최악의 경우 Root까지 거슬러 올라갈 수 있으므로 **O(logn)**이 걸리게 된다. 
    - <img src="https://t1.daumcdn.net/cfile/tistory/9956CA3359CF658708" alt="img" style="zoom: 33%;" /> 

  - 이미지 및 설명 출처 : https://zeddios.tistory.com/237  <=  자세한 설명 참고 사이트

### 삭제

- 레드-블랙 트리의 속성을 유지해야한다.
- Time complexity : **O(logn)**
- 삭제될 노드의 child의 개수, 삭제할 노드의 수 등에 따라서 삭제 방법(rotation)이 달라진다.
  1. 삭제 노드가 Red 일 경우 : 어떠한 추가 작업이 필요하지 않는다. 
  2. 삭제 노드가 Black일 경우 : Black-Height가 1 감소하기때문에 black 노드가 1개 추가 될 수 있도록 rotation을 한 후 노드의 색깔을 조정한다. 

- **삭제 예시**
  
  - **처음**
    
    - <img src="..\_Images\[RBT]example_1.png" alt="example_1" style="zoom:67%;"/>
  - **노드 0002 삭제**
    - 0001이 0002 자리로 올라온다.
      
      - <img src="..\_Images\[RBT]example_2.png" alt="example_2" style="zoom:67%;"/>
      
        
    - Black -Height로 인해 노드 색 조정
      
      - <img src="..\_Images\[RBT]example_3.png" alt="example_3" style="zoom:67%;"/>
  - **노드 005 삭제**
    - 0005 삭제 후 0005 자식이 없기 때문에 Leaf 노드가 올라온다.
      - <img src="..\_Images\[RBT]example_4.png" alt="example_4" style="zoom:67%;"/>
    - Black-Height로 인해 Rotation후 노드 색 조정
      - <img src="..\_Images\[RBT]example_5.png" alt="example_5" style="zoom:67%;"/>
    - <img src="..\_Images\[RBT]example_6.png" alt="example_6" style="zoom:67%;"/>

### 사용

- Java Collection의 ArrayList, HashMap (Seperate Chaining)

  

### 추가 자료

- [Red-Black Tree vs AVL]( [https://velog.io/@agugu95/%EC%9D%B4%EC%A7%84-%ED%8A%B8%EB%A6%AC%EC%9D%98-%EA%B7%A0%ED%98%95-RED-BALCKAVL](https://velog.io/@agugu95/이진-트리의-균형-RED-BALCKAVL) ) 
- [Red-Black Tree Visualization](https://www.cs.usfca.edu/~galles/visualization/RedBlack.html)

#### Reference

-   https://zeddios.tistory.com/237 

-  https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#red-black-tree 

-  [https://ko.wikipedia.org/wiki/%EB%A0%88%EB%93%9C-%EB%B8%94%EB%9E%99_%ED%8A%B8%EB%A6%AC](https://ko.wikipedia.org/wiki/레드-블랙_트리) 