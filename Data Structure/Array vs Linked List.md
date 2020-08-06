# Array vs Linked List

### Array (배열)

 ![img](https://api.ahribori.com/image/05xngyIM_-de5V9cvpKvQzqc.jpg) 

- 논리적 저장 순서와 물리적 저장 순서가 일치한다.

- 메모리의 할당할 사이즈 즉, 배열의 크기를 미리 정해놓고 사용한다.

  - 데이터의 최대 사이즈, 데이터가 계속 증가할 때는 부적합하다.

- Index로 해당 원소에 접근 할 수 있다.

  - 찾고자 하는 원소의 인덱스만 알면 빠르게 접근이 가능하다. ( **O(1)** )
  - Random access 가 가능하다.

- 데이터를 삭제 혹은 삽입할 때 비효율적이다.

  - 데이터 삭제 : 원소를 삭제 후 빈공간이 생기지 않도록 shift 작업을 추가적으로 해야한다. ( **O(n)** )
  - 데이터 삽입 : 삽입을 위해 모든 원소들의 인덱스를 shift해줘야한다.( **O(n)** )

  

### Linked List (연결 리스트)

 ![img](https://api.ahribori.com/image/wNNX1FcnCttbC_RnQSpoFnE_.jpg) 

- Array의 문제점을 해결하기 위한 자료구조
- 데이터와 다음 원소의 물리적인 주소를 저장한다. 
  - [저장할 데이터 + 다음 데이터의 물리적 주소]
- 데이터의 크기를 지정해 주지 않아도 된다. 
- 데이터의 삭제 혹은 삽입이 용이하다.
  - 다음 원소의 주소를 저장한 부분을 다른 값으로 수정하면 삭제와 삽입을 쉽게 할 수 있다. ( **O(1)** )
- 원하는 위치에 삭제 혹은 삽입을 하려면 검색(Search)하는 과정에서 첫번째 원소부터 확인해야한다.  ( **O(n)**  )
  - 논리적 저장 순서와 물리적 저장 순서가 일치하지 않기 때문
  - 삽입하고 정렬하는 것과 동일한 시간이 걸린다.



#### Memo

- ArrayList
- 단방향/ 양방향 연결 리스트
- Vector



### 추가 자료

- [자바 ArrayList, LinkedList 클래스 정리](https://gbsb.tistory.com/246)
-  [Java List collection](https://velog.io/@adam2/Array와-List그리고-Java-List) 

#### Reference

-  https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#array-vs-linked-list 
-  https://ahribori.com/article/591a5824c686bd0d48e95f47 