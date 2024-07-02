### 원형
_class_ collections.Counter([_iterable-or-mapping_])

#### 설명
A [`Counter`](https://docs.python.org/ko/3/library/collections.html#collections.Counter "collections.Counter") is a [`dict`](https://docs.python.org/ko/3/library/stdtypes.html#dict "dict") subclass for counting [hashable](https://docs.python.org/ko/3/glossary.html#term-hashable) objects. It is a collection where elements are stored as dictionary keys and their counts are stored as dictionary values. Counts are allowed to be any integer value including zero or negative counts. The [`Counter`](https://docs.python.org/ko/3/library/collections.html#collections.Counter "collections.Counter") class is similar to bags or multisets in other languages.

- A `counter` is a `dict` subclass for counting `hashable` object.
- It is a collections where elements are stored as dictionary kest and their counts are stored as dictionary values.
- *Counts are allowed to be any integer value including zero or negative counts.*
```Python
c = Counter(['eggs', 'ham'])

# count of a missing element is zero
c['bacon']
```

- 삭제
```Python
c['sausage'] = 0                # counter entry with a zero count
del c['sausage']                # del actually removes the entry
```

### Constructor
```Python
c = Counter()                           # a new, empty counter
c = Counter('gallahad')                 # a new counter from an iterable
c = Counter({'red': 4, 'blue': 2})      # a new counter from a mapping
c = Counter(cats=4, dogs=8)             # a new counter from keyword args
```



### Method
##### 기본 Dict Method + 아래 Method
###### 예외.
 - 예외 1
	 - update([iterable-or-mapping]) :
		 - 요소는 이터러블에서 세거나 다른 매핑(또는 계수기)에서 더해집니다. 
		 - dict.update()와 비슷하지만, 교체하는 대신 더합니다. 
		 - 또한, 이터러블은 (key, value) 쌍의 시퀀스가 아닌, 요소의 시퀀스일 것으로 기대합니다.
	 - fromkeys(_iterable_) : 
		 - 이 클래스 메서드는 [`Counter`](https://docs.python.org/ko/3/library/collections.html#collections.Counter "collections.Counter") 객체에 구현되지 않았습니다.

###### 추가 Method
1. elements()
	- 개수만큼 반복되는 요소에 대한 이터레이터를 반환합니다.
	- 0요소는 처음 발견되는 순서대로 반환됩니다. 
	- 요소의 개수가 1보다 작으면 elements()는 이를 무시합니다.
```Python
c = Counter(a=4, b=2, c=0, d=-2)
sorted(c.elements())
['a', 'a', 'a', 'a', 'b', 'b']
```

1. most_common([n])
	- n 개의 가장 흔한 요소와 그 개수를 가장 흔한 것부터 가장 적은 것 순으로 나열한 리스트를 반환합니다.
	-  n이 생략되거나 None이면, most_common()은 계수기의 모든 요소를 반환합니다. 
	- 개수가 같은 요소는 처음 발견된 순서를 유지합니다:
```Python
Counter('abracadabra').most_common(3)
[('a', 5), ('b', 2), ('r', 2)]
```
>>>

1. subtract([iterable-or-mapping])
	- 이터러블이나 다른 매핑 (또는 계수기)으로부터 온 요소들을 뺍니다. 
	- dict.update()와 비슷하지만 교체하는 대신 개수를 뺍니다. 
	- 입력과 출력 모두 0이나 음수일 수 있습니다.
```python
c = Counter(a=4, b=2, c=0, d=-2)
d = Counter(a=1, b=2, c=3, d=4)
c.subtract(d)
c
Counter({'a': 3, 'b': 0, 'c': -3, 'd': -6})
```

1. total() : Compute the sum of the counts.
```python
c = Counter(a=10, b=5, c=0)
c.total()
15
```



##### Benutzen1
```Python
c.total()                       # total of all counts
c.clear()                       # reset all counts
list(c)                         # list unique elements
set(c)                          # convert to a set
dict(c)                         # convert to a regular dictionary
c.items()                       # convert to a list of (elem, cnt) pairs
Counter(dict(list_of_pairs))    # convert from a list of (elem, cnt) pairs
c.most_common()[:-n-1:-1]       # n least common elements
+c                              # remove zero and negative counts>)
```

##### Benutzen2
```Python
c = Counter(a=3, b=1)
d = Counter(a=1, b=2)
c + d                       # add two counters together:  c[x] + d[x]

c - d                       # subtract (keeping only positive counts)

c & d                       # intersection:  min(c[x], d[x])

c | d                       # union:  max(c[x], d[x])

c == d                      # equality:  c[x] == d[x]

c <= d                      # inclusion:  c[x] <= d[x]
```