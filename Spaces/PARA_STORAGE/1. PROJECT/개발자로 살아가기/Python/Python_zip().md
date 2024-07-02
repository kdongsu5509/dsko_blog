---
sticker: emoji//1f910
---

## 파이썬의 zip() 함수 이해하기

파이썬의 `zip()` 함수는 여러 개의 이터러블(iterable) 객체를 인자로 받아, 각 객체가 담고 있는 원소들을 튜플의 형태로 차례대로 짝지어 새로운 이터레이터(iterator)를 생성하는 역할을 합니다. 이 과정은 마치 지퍼(zipper)를 올리는 것처럼 두 그룹의 데이터를 서로 엮어줍니다. 🤝

---

### zip() 함수의 기본 사용법
- **예제 1**: 두 리스트의 원소를 짝지어 출력하기
  ```python
  numbers = [1, 2, 3]
  letters = ["A", "B", "C"]
  for pair in zip(numbers, letters):
      print(pair)
  ```
  출력 결과는 `(1, 'A')`, `(2, 'B')`, `(3, 'C')`가 됩니다. [[1]](https://www.daleseo.com/python-zip/)

- **예제 2**: zip() 함수를 사용하여 두 변수의 원소를 짝지어 처리하기
  ```python
  list1 = [1, 2, 3, 4]
  list2 = ['one', 'two', 'three', 'four']
  for x, y in zip(list1, list2):
    print(x, y)
  ```
  이 코드는 `1 one`, `2 two`, `3 three`, `4 four`를 출력합니다. [[2]](https://wjunsea.tistory.com/106)

### zip() 함수의 고급 사용법
- **zip()과 * 연산자를 사용한 언패킹**: `zip(*iterable)` 형태로 사용하면, zip으로 묶인 데이터를 다시 원래의 시퀀스 데이터로 분리할 수 있습니다.
  ```python
  x = [1, 2, 3]
  y = [4, 5, 6]
  zipped = zip(x, y)
  x2, y2 = zip(*zipped)
  ```
  이 경우, `x2`와 `y2`는 원래의 `x`, `y` 리스트와 동일한 내용을 담게 됨. [[3]](https://www.programiz.com/python-programming/methods/built-in/zip)

---

zip() 함수는 데이터를 짝지어 처리해야 할 때 매우 유용하게 사용