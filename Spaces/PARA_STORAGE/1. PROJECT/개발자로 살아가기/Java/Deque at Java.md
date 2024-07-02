### package : java.util
# Interface Deque <E>

- parent class
	- Collections <E>, Iterable <E>, Queue <E>
- children classes
	- ArrayDeque, ConcurrentLinkedDeque, LinkedBlockingDeque, LinkedList

#### The Method about First Element(Head)
	- Insert : addFirst(e) , offerFirst(e)
	- Remove : removeFirst(), pollFirst()
	- Examine : getFirst(), peekFirst()

#### The Method about Last Element(Tail)
	- Insert : addLast(e) , offerLast(e)
	- Remove : removeLast(), pollLast()
	- Examine : getLast(), peekLast()

## METHOD DETAIL
##### addFirst
- void addFirst(E e)
**Inserts** the specified element at the **front** of this deque if it is possible to do so immediately without violating capacity restrictions, throwing an IllegalStateException if no space is currently available. When using a capacity-restricted deque, it is generally preferable to use method offerFirst(E).
- ###### Parameters:
e - the element to add
Throws:
IllegalStateException - if the element cannot be added at this time due to capacity restrictions
ClassCastException - if the class of the specified element prevents it from being added to this deque
NullPointerException - if the specified element is null and this deque does not permit null elements
IllegalArgumentException - if some property of the specified element prevents it from being added to this deque
##### addLast
void addLast(E e)
Inserts the specified element at the end of this deque if it is possible to do so immediately without violating capacity restrictions, throwing an IllegalStateException if no space is currently available. When using a capacity-restricted deque, it is generally preferable to use method offerLast(E).
This method is equivalent to add(E).

Parameters:
e - the element to add
Throws:
IllegalStateException - if the element cannot be added at this time due to capacity restrictions
ClassCastException - if the class of the specified element prevents it from being added to this deque
NullPointerException - if the specified element is null and this deque does not permit null elements
IllegalArgumentException - if some property of the specified element prevents it from being added to this deque

##### offerFirst
boolean offerFirst(E e)
Inserts the specified element at the front of this deque unless it would violate capacity restrictions. When using a capacity-restricted deque, this method is generally preferable to the addFirst(E) method, which can fail to insert an element only by throwing an exception.
Parameters:
e - the element to add
Returns:
true if the element was added to this deque, else false
Throws:
ClassCastException - if the class of the specified element prevents it from being added to this deque
NullPointerException - if the specified element is null and this deque does not permit null elements
IllegalArgumentException - if some property of the specified element prevents it from being added to this deque
##### offerLast
boolean offerLast(E e)
Inserts the specified element at the end of this deque unless it would violate capacity restrictions. When using a capacity-restricted deque, this method is generally preferable to the addLast(E) method, which can fail to insert an element only by throwing an exception.
Parameters:
e - the element to add
Returns:
true if the element was added to this deque, else false
Throws:
ClassCastException - if the class of the specified element prevents it from being added to this deque
NullPointerException - if the specified element is null and this deque does not permit null elements
IllegalArgumentException - if some property of the specified element prevents it from being added to this deque
##### removeFirst
E removeFirst()
Retrieves and removes the first element of this deque. This method differs from pollFirst only in that it throws an exception if this deque is empty.
Returns:
the head of this deque
Throws:
NoSuchElementException - if this deque is empty

##### removeLast
E removeLast()
Retrieves and removes the last element of this deque. This method differs from pollLast only in that it throws an exception if this deque is empty.
Returns:
the tail of this deque
Throws:
NoSuchElementException - if this deque is empty

##### pollFirst
E pollFirst()
Retrieves and removes the first element of this deque, or returns null if this deque is empty.
Returns:
the head of this deque, or null if this deque is empty

##### pollLast
E pollLast()
Retrieves and removes the last element of this deque, or returns null if this deque is empty.
Returns:
the tail of this deque, or null if this deque is empty

##### getFirst
E getFirst()
Retrieves, but does not remove, the first element of this deque. This method differs from peekFirst only in that it throws an exception if this deque is empty.
Returns:
the head of this deque
Throws:
NoSuchElementException - if this deque is empty

##### getLast
E getLast()
Retrieves, but does not remove, the last element of this deque. This method differs from peekLast only in that it throws an exception if this deque is empty.
Returns:
the tail of this deque
Throws:
NoSuchElementException - if this deque is empty

##### peekFirst
E peekFirst()
Retrieves, but does not remove, the first element of this deque, or returns null if this deque is empty.
Returns:
the head of this deque, or null if this deque is empty

##### peekLast
E peekLast()
Retrieves, but does not remove, the last element of this deque, or returns null if this deque is empty.
Returns:
the tail of this deque, or null if this deque is empty

##### removeFirstOccurrence
boolean removeFirstOccurrence(Object o)
Removes the first occurrence of the specified element from this deque. If the deque does not contain the element, it is unchanged. More formally, removes the first element e such that (o==null ? e==null : o.equals(e)) (if such an element exists). Returns true if this deque contained the specified element (or equivalently, if this deque changed as a result of the call).
Parameters:
o - element to be removed from this deque, if present
Returns:
true if an element was removed as a result of this call
Throws:
ClassCastException - if the class of the specified element is incompatible with this deque (optional)
NullPointerException - if the specified element is null and this deque does not permit null elements (optional)

##### removeLastOccurrence
boolean removeLastOccurrence(Object o)
Removes the last occurrence of the specified element from this deque. If the deque does not contain the element, it is unchanged. More formally, removes the last element e such that (o==null ? e==null : o.equals(e)) (if such an element exists). Returns true if this deque contained the specified element (or equivalently, if this deque changed as a result of the call).
Parameters:
o - element to be removed from this deque, if present
Returns:
true if an element was removed as a result of this call
Throws:
ClassCastException - if the class of the specified element is incompatible with this deque (optional)
NullPointerException - if the specified element is null and this deque does not permit null elements (optional)

##### add
boolean add(E e)
Inserts the specified element into the queue represented by this deque (in other words, at the tail of this deque) if it is possible to do so immediately without violating capacity restrictions, returning true upon success and throwing an IllegalStateException if no space is currently available. When using a capacity-restricted deque, it is generally preferable to use offer.
This method is equivalent to addLast(E).

Specified by:
add in interface Collection%3CE%3E
Specified by:
add in interface Queue<E>
Parameters:
e - the element to add
Returns:
true (as specified by Collection.add(E))
Throws:
IllegalStateException - if the element cannot be added at this time due to capacity restrictions
ClassCastException - if the class of the specified element prevents it from being added to this deque
NullPointerException - if the specified element is null and this deque does not permit null elements
IllegalArgumentException - if some property of the specified element prevents it from being added to this deque

##### offer
boolean offer(E e)
Inserts the specified element into the queue represented by this deque (in other words, at the tail of this deque) if it is possible to do so immediately without violating capacity restrictions, returning true upon success and false if no space is currently available. When using a capacity-restricted deque, this method is generally preferable to the add(E) method, which can fail to insert an element only by throwing an exception.
This method is equivalent to offerLast(E).

Specified by:
offer in interface Queue<E>
Parameters:
e - the element to add
Returns:
true if the element was added to this deque, else false
Throws:
ClassCastException - if the class of the specified element prevents it from being added to this deque
NullPointerException - if the specified element is null and this deque does not permit null elements
IllegalArgumentException - if some property of the specified element prevents it from being added to this deque

##### remove
E remove()
Retrieves and removes the head of the queue represented by this deque (in other words, the first element of this deque). This method differs from poll only in that it throws an exception if this deque is empty.
This method is equivalent to removeFirst().

Specified by:
remove in interface Queue<E>
Returns:
the head of the queue represented by this deque
Throws:
NoSuchElementException - if this deque is empty

##### poll
E poll()
Retrieves and removes the head of the queue represented by this deque (in other words, the first element of this deque), or returns null if this deque is empty.
This method is equivalent to pollFirst().

Specified by:
poll in interface Queue<E>
Returns:
the first element of this deque, or null if this deque is empty

##### element
E element()
Retrieves, but does not remove, the head of the queue represented by this deque (in other words, the first element of this deque). This method differs from peek only in that it throws an exception if this deque is empty.
This method is equivalent to getFirst().

Specified by:
element in interface Queue<E>
Returns:
the head of the queue represented by this deque
Throws:
NoSuchElementException - if this deque is empty

##### peek
E peek()
Retrieves, but does not remove, the head of the queue represented by this deque (in other words, the first element of this deque), or returns null if this deque is empty.
This method is equivalent to peekFirst().

Specified by:
peek in interface Queue<E>
Returns:
the head of the queue represented by this deque, or null if this deque is empty

##### push
void push(E e)
Pushes an element onto the stack represented by this deque (in other words, at the head of this deque) if it is possible to do so immediately without violating capacity restrictions, throwing an IllegalStateException if no space is currently available.
This method is equivalent to addFirst(E).

Parameters:
e - the element to push
Throws:
IllegalStateException - if the element cannot be added at this time due to capacity restrictions
ClassCastException - if the class of the specified element prevents it from being added to this deque
NullPointerException - if the specified element is null and this deque does not permit null elements
IllegalArgumentException - if some property of the specified element prevents it from being added to this deque

##### pop
E pop()
Pops an element from the stack represented by this deque. In other words, removes and returns the first element of this deque.
This method is equivalent to removeFirst().

Returns:
the element at the front of this deque (which is the top of the stack represented by this deque)
Throws:
NoSuchElementException - if this deque is empty

##### remove
boolean remove(Object o)
Removes the first occurrence of the specified element from this deque. If the deque does not contain the element, it is unchanged. More formally, removes the first element e such that (o==null ? e==null : o.equals(e)) (if such an element exists). Returns true if this deque contained the specified element (or equivalently, if this deque changed as a result of the call).
This method is equivalent to removeFirstOccurrence(Object).

Specified by:
remove in interface Collection<E>
Parameters:
o - element to be removed from this deque, if present
Returns:
true if an element was removed as a result of this call
Throws:
ClassCastException - if the class of the specified element is incompatible with this deque (optional)
NullPointerException - if the specified element is null and this deque does not permit null elements (optional)

##### contains
boolean contains(Object o)
Returns true if this deque contains the specified element. More formally, returns true if and only if this deque contains at least one element e such that (o==null ? e==null : o.equals(e)).
Specified by:
contains in interface Collection<E>
Parameters:
o - element whose presence in this deque is to be tested
Returns:
true if this deque contains the specified element
Throws:
ClassCastException - if the type of the specified element is incompatible with this deque (optional)
NullPointerException - if the specified element is null and this deque does not permit null elements (optional)

##### size
int size()
Returns the number of elements in this deque.
Specified by:
size in interface Collection<E>
Returns:
the number of elements in this deque
iterator
Iterator<E> iterator()
Returns an iterator over the elements in this deque in proper sequence. The elements will be returned in order from first (head) to last (tail).
Specified by:
iterator in interface Collection<E>
Specified by:
iterator in interface Iterable<E>
Returns:
an iterator over the elements in this deque in proper sequence
descendingIterator
Iterator<E> descendingIterator()
Returns an iterator over the elements in this deque in reverse sequential order. The elements will be returned in order from last (tail) to first (head).
Returns:
an iterator over the elements in this deque in reverse sequence>)