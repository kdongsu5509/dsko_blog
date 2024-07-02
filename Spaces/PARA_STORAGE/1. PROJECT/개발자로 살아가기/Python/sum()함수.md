---
tags:
  - python
---
기본 구조 내용 -> 공식 문서 발췌.
<h4>sum() 함수의 기본 구조</h4>
- sum(_iterable_, _/_, _start=0_)
	- _start_ 및 _iterable_ 의 항목들을 왼쪽에서 오른쪽으로 합하고 합계를 반환
	- _iterable_ 의 항목은 일반적으로 숫자며 시작 값은 문자열이 될 수 없음.

		- 문자열의 시퀀스를 연결하는 가장 선호되고 빠른 방법은 `''.join(sequence)` 를 호출하는 것임
		- 확장된 정밀도로 부동 소수점 값을 더하려면 [`math.fsum()`](https://docs.python.org/ko/3/library/math.html#math.fsum "math.fsum") 
		- 일련의 이터러블들을 연결하려면 [`itertools.chain()`](https://docs.python.org/ko/3/library/itertools.html#itertools.chain "itertools.chain") 를 고려해보세요.


<h4>sum() 함수의 시간 복잡도</h4>
- sum()함수는 내부적으로 반복문을 통해 모든 원소를 하나 하나 순회하며 더한다.
	- 그렇기에 시간 복잡도는 O(N).

->나중에 참고할 만한 것들
	- 가우스 공식(공차수열일 때)
	- 분할 정복
	- 포인터 활용-> 이건 진짜 모르겠음. 꼭 공부해놓을 예정임.