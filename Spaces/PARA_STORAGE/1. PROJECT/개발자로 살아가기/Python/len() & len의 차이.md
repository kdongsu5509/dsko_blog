---
tags:
  - python
---
<h4>len()</h4> 
- 파이썬의 내장 함수
- 인자로 전달된 객체의 길이(요소의 개수)를 반환 
- `len()` 함수는 문자열, 리스트, 튜플, 딕셔너리 등 다양한 시퀀스 객체에 사용 가능. 

```python
len(object)
```

	- `object`는 길이를 확인하려는 객체입니다.

```python
#예시
my_list = [1, 2, 3, 4, 5]
length = len(my_list)
print(length)  # 출력: 5
```


<h4>len</h4>
- `len`은 내장 함수가 아니라 "객체의 속성(attribute) 중 하나"
- 문자열 객체의 길이를 나타내는 속성 => `len`
- 직접 접근할 수도 있음.

```python
my_string = "Hello, World!"
length_with_len = len(my_string)
length_direct_access = my_string.__len__()  # 이 방법도 가능하지만 권장되지 않습니다.

print(length_with_len)          # 출력: 13
print(length_direct_access)     # 출력: 13
```
