---
tags:
  - python
---
<h3 style="color : blue;">내장 함수들 설명</h3>

# bisect.bisect_right(a, x, lo=0, hi=len(a))

- 정렬된 리스트 `a`에 새로운 원소 `x`를 삽입할 위치를 찾아줌
	- 기본적으로 전체 리스트를 대상으로 하며, 찾은 위치는 이미 있는 `x`의 기존 항목 뒤(오른쪽)에 올 것입니다. 반환 값은 a를 이분하여, 왼쪽은 모든 `val < x`이고, 오른쪽은 모든 `val >= x`이 되도록 하는 인덱스 `i`입니다.

### bisect.bisect_left(a, x, lo=0, hi=len(a))
- `bisect_right`와 비슷하지만, 반환 값은 a를 이분하여, 왼쪽은 모든 `val <= x`이고, 오른쪽은 모든 `val > x`이 되도록 하는 인덱스 `i`입니다.

### bisect.insort_left(a, x, lo=0, hi=len(a))
- 정렬된 리스트 `a`에 `x`를 정렬된 순서로 삽입. 
	- `a`가 이미 정렬되었다고 가정할 때, `a.insert(bisect.bisect_left(a, x, lo, hi), x)`와 동등합니다. 이 삽입은 이진 탐색을 통해 이루어지며, 검색에 소요되는 O(log n)과 삽입에 소요되는 O(n)의 시간 복잡도를 고려해야 합니다.

### bisect.insort_right(a, x, lo=0, hi=len(a))
- `insort_right` 함수는 `insort_left`와 비슷하지만, a에 `x`를 x의 기존 항목 다음에 삽입합니다.


<h3 style="color : blue;">이진 탐색 모듈 Bisect 원형 코드</h3>

```Python
"""Bisection algorithms."""

  

def insort_right(a, x, lo=0, hi=None):

    """Insert item x in list a, and keep it sorted assuming a is sorted.

  

    If x is already in a, insert it to the right of the rightmost x.

  

    Optional args lo (default 0) and hi (default len(a)) bound the

    slice of a to be searched.

    """

  

    if lo < 0:

        raise ValueError('lo must be non-negative')

    if hi is None:

        hi = len(a)

    while lo < hi:

        mid = (lo+hi)//2

        if x < a[mid]: hi = mid

        else: lo = mid+1

    a.insert(lo, x)

  

def bisect_right(a, x, lo=0, hi=None):

    """Return the index where to insert item x in list a, assuming a is sorted.

  

    The return value i is such that all e in a[:i] have e <= x, and all e in

    a[i:] have e > x.  So if x already appears in the list, a.insert(x) will

    insert just after the rightmost x already there.

  

    Optional args lo (default 0) and hi (default len(a)) bound the

    slice of a to be searched.

    """

  

    if lo < 0:

        raise ValueError('lo must be non-negative')

    if hi is None:

        hi = len(a)

    while lo < hi:

        mid = (lo+hi)//2

        if x < a[mid]: hi = mid

        else: lo = mid+1

    return lo

  

def insort_left(a, x, lo=0, hi=None):

    """Insert item x in list a, and keep it sorted assuming a is sorted.

  

    If x is already in a, insert it to the left of the leftmost x.

  

    Optional args lo (default 0) and hi (default len(a)) bound the

    slice of a to be searched.

    """

  

    if lo < 0:

        raise ValueError('lo must be non-negative')

    if hi is None:

        hi = len(a)

    while lo < hi:

        mid = (lo+hi)//2

        if a[mid] < x: lo = mid+1

        else: hi = mid

    a.insert(lo, x)

  
  

def bisect_left(a, x, lo=0, hi=None):

    """Return the index where to insert item x in list a, assuming a is sorted.

  

    The return value i is such that all e in a[:i] have e < x, and all e in

    a[i:] have e >= x.  So if x already appears in the list, a.insert(x) will

    insert just before the leftmost x already there.

  

    Optional args lo (default 0) and hi (default len(a)) bound the

    slice of a to be searched.

    """

  

    if lo < 0:

        raise ValueError('lo must be non-negative')

    if hi is None:

        hi = len(a)

    while lo < hi:

        mid = (lo+hi)//2

        if a[mid] < x: lo = mid+1

        else: hi = mid

    return lo

  

# Overwrite above definitions with a fast C implementation

try:

    from _bisect import *

except ImportError:

    pass

  

# Create aliases

bisect = bisect_right

insort = insort_right
```


