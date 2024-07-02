---
tags:
  - python
---
### 일반 입력 : input()
- 일반적인 경우에는 문제 없음. 
- 그러나, 입력하는 데이터가 많은 경우에 시간 초과의 주범이 되기도 함.

### 해결책 : sys.readline()
- 한 줄씩 입력받는 함수.

```Python
import sys
input_data = sys.stdin.readline().rstrip()
```
<b>- rstrip() 은 필수!!</b><br>
"realine()으로 입력 시 Enter(공백문자)까지 입력됨."<br>
공백 문자를 제거하기 위해서 rstrip()를 사용함.



```Dataview
table
	field file.name as 파일명
from "프로그래밍/Python"
sort file.size desc
```


