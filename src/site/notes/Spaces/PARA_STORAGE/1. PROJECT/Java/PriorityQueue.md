---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/java/priority-queue/"}
---

>[!abstract]
> package java.util
>Class PriorityQueue<E>

- #### Appendix
	- 비경계 우선순위 큐는 우선순위 힙을 기반으로 하며, 요소들은 자연 순서에 따라 정렬되거나 큐 생성 시 제공된 Comparator에 따라 정렬됩니다. 우선순위 큐는 null 요소를 허용하지 않으며, 자연 순서에 의존하는 경우 비교할 수 없는 객체의 삽입을 허용하지 않습니다. 이 큐의 헤드는 지정된 순서에 따라 가장 작은 요소이며, 가장 작은 값에 여러 요소가 연결되어 있으면 임의로 하나를 선택합니다. 우선순위 큐의 검색 작업인 poll, remove, peek, 및 element는 큐의 헤드에 있는 요소에 액세스합니다.
	- 우선순위 큐는 비경계이지만, 큐에 저장된 요소들을 저장하는 배열의 크기를 조절하는 내부 용량이 있습니다. 이는 항상 큐 크기보다 적어도 큽니다. 요소들이 우선순위 큐에 추가됨에 따라 용량은 자동으로 증가하며, 성장 정책의 세부 사항은 명시되어 있지 않습니다.
	- 이 클래스와 그 반복자는 Collection 및 Iterator 인터페이스의 모든 선택적 메서드를 구현합니다. 메서드 iterator()에서 제공되는 Iterator는 우선순위 큐의 요소를 특정한 순서로 반복하는 것을 보장하지 않습니다. 정렬된 반복이 필요한 경우 Arrays.sort(pq.toArray())를 사용하는 것을 고려하십시오.
	- 이 구현은 동기화되지 않음에 유의하십시오. 여러 스레드가 큐를 수정하는 경우 PriorityQueue 인스턴스에 여러 스레드가 동시에 액세스하지 않아야 합니다. 대신, 스레드 안전한 PriorityBlockingQueue 클래스를 사용하십시오.
	- 구현 참고: 이 구현은 enqueuing 및 dequeuing 메서드(offer, poll, remove() 및 add)에 대해 O(log(n)) 시간을 제공합니다. remove(Object) 및 contains(Object) 메서드에 대해서는 선형 시간을 제공합니다. 검색 메서드(peek, element 및 size)에 대해서는 상수 시간을 제공합니다.
	- 이 클래스는 Java Collections Framework의 구성원입니다.



### 생성자 세부 정보
#### PriorityQueue()
- 기본 초기 용량(11)을 가지며, 요소들을 자연 순서에 따라 정렬합니다.

#### PriorityQueue(int initialCapacity)
- 지정된 초기 용량을 가지며, 요소들을 자연 순서에 따라 정렬합니다.
  - initialCapacity: 이 우선순위 큐의 초기 용량

#### PriorityQueue(Comparator%3C? super E%3E comparator)
- 기본 초기 용량을 가지며, 요소들을 지정된 Comparator에 따라 정렬합니다.
  - comparator: 이 우선순위 큐를 정렬하는 데 사용되는 Comparator. null인 경우 요소의 자연 순서가 사용됩니다.

#### PriorityQueue(int initialCapacity, Comparator<? super E> comparator)
- 지정된 초기 용량을 가지며, 요소들을 지정된 Comparator에 따라 정렬합니다.
  - initialCapacity: 이 우선순위 큐의 초기 용량
  - comparator: 이 우선순위 큐를 정렬하는 데 사용되는 Comparator. null인 경우 요소의 자연 순서가 사용됩니다.

#### PriorityQueue(Collection<? extends E> c)
- 지정된 컬렉션의 요소를 포함하는 우선순위 큐를 생성합니다.
  - c: 이 우선순위 큐에 넣을 요소가 있는 컬렉션

#### PriorityQueue(PriorityQueue<? extends E> c)
- 지정된 우선순위 큐의 요소를 포함하는 우선순위 큐를 생성합니다.
  - c: 이 우선순위 큐에 넣을 요소가 있는 우선순위 큐

#### PriorityQueue(SortedSet<? extends E> c)
- 지정된 정렬된 집합의 요소를 포함하는 우선순위 큐를 생성합니다.
  - c: 이 우선순위 큐에 넣을 요소가 있는 정렬된 집합

### 메서드 세부 정보
#### add(E e)
- 지정된 요소를 이 우선순위 큐에 삽입합니다.
  - e: 추가할 요소
  - 반환값: Collection.add(E)에 따라 true

#### offer(E e)
- 지정된 요소를 이 우선순위 큐에 삽입합니다.
  - e: 추가할 요소
  - 반환값: Queue.offer(E)에 따라 true

#### peek()
- 이 큐의 헤드를 반환하되, 제거하지 않습니다. 큐가 비어있으면 null을 반환합니다.
  - 반환값: 이 큐의 헤드 또는 큐가 비어있으면 null

#### remove(Object o)
- 지정된 요소의 단일 인스턴스를 큐에서 제거합니다.
  - o: 제거할 요소
  - 반환값: 큐가 지정된 요소를 포함하고 있는 경우 true

#### contains(Object o)
- 이 큐가 지정된 요소를 포함하면 true를 반환합니다.
  - o: 포함 여부를 확인할 객체
  - 반환값: 이 큐가 지정된 요소를 포함하면 true

#### toArray()
- 이 큐의 모든 요소를 포함하는 배열을 반환합니다. 요소들은 특정한 순서 없이 반환됩니다.
  - 반환값: 이 큐의 모든 요소를 포함하는 배열

#### toArray(T[] a)
- 이 큐의 모든 요소를 포함하는 배열을 반환합니다. 반환되는 배열의 런타임 유형은 지정된 배열의 유형과 동일합니다.
  - a: 요소를 저장할 배열
  - 반환값: 이 큐의 모든 요소를 포함하는 배열

#### iterator()
- 이 큐의 요소를 순회하는 반복자를 반환합니다. 요소는 특정한 순서로 반환되지 않습니다.
  - 반환값: 이 큐의 요소를 순회하는 반복자

#### size()
- 이 컬렉션의 요소 수를 반환합니다. 요소 수가 Integer.MAX_VALUE보다 크면 Integer.MAX_VALUE를 반환합니다.
  - 반환값: 이 컬렉션의 요소 수

#### clear()
- 이 우선순위 큐에서 모든 요소를 제거합니다.

#### poll()
- 이 큐의 헤드를 가져와 제거합니다. 큐가 비어있으면 null을 반환합니다.
  - 반환값: 이 큐의 헤드 또는 큐가 비어있으면 null

#### comparator()
- 이 큐의 요소를 정렬하는 데 사용되는 Comparator를 반환합니다. 이 큐가 요소의 자연 순서에 따라 정렬되는 경우 null을 반환합니다.
  - 반환값: 이 큐를 정렬하는 데 사용되는 Comparator

#### spliterator()
- 이 큐의 요소 위에 늦은 바인딩 및 fail-fast Spliterator를 생성합니다. Spliterator는 Spliterator.SIZED, Spliterator.SUBSIZED 및 Spliterator.NONNULL을 보고합니다.
  - 반환값: 이 큐의 요소 위에 있는 Spliterator