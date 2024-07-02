---
tags:
  - python
---
# sys 모듈

# 1. sys모듈을 이용한 표준 입출력

### 표준 입력 (`sys.stdin`)

`sys.stdin` : 표준 입력으로부터 데이터를 읽어올 수 있습니다. 
`sys.stdin.readline()` :  한 줄씩 읽을 수 있습니다.

```python
import sys

# 표준 입력으로부터 한 줄 읽기
input_data = sys.stdin.readline()

# 읽은 데이터 출력
print("입력된 데이터:", input_data)
```

### 표준 출력 (`sys.stdout`)

`sys.stdout`을 사용하여 표준 출력에 데이터를 쓸 수 있습니다. 
`sys.stdout.write()`를 호출하여 출력할 수 있습니다.

```python
import sys

# 표준 출력에 데이터 쓰기
sys.stdout.write("Hello, World!\n")
```

### 예제: 표준 입력과 표준 출력 조작

다음은 `sys` 모듈을 사용하여 표준 입력으로부터 여러 줄을 읽고, 표준 출력에 결과를 출력하는 예제입니다.

```python
import sys

# 표준 입력으로부터 여러 줄 읽기
lines = sys.stdin.readlines()

# 각 줄을 출력하기
for line in lines:
    sys.stdout.write("입력된 줄: " + line)
```

이 예제에서 `sys.stdin.readlines()`를 사용하여 여러 줄을 읽고, 그 후에 `sys.stdout.write()`를 사용하여 각 줄을 출력합니다. 이러한 방식을 통해 입출력을 조작할 수 있습니다.

# 2. input()과 print()가 느린 이유
<b>이 함수들은 표준 입력 및 출력을 수행하며, 여러 부가적인 작업들이 수행되기 때문</b>

<b>1. Buffering</b><br>
`print()` 함수는 출력을 버퍼링하여 일정량의 데이터가 쌓일 때 한 번에 출력됨. 
이는 작은 양의 데이터를 출력할 때도 버퍼링이 발생하므로 속도가 떨어질 수 있습니다. 
이러한 동작은 성능 향상을 위한 것이지만, 작은 프로그램에서는 불필요한 오버헤드로 느껴질 수 있습니다.
<br>
<b>2. String Formatting</b><br>
`print()` 함수는 문자열을 출력하기 위해 여러 형식화 작업을 수행
이는 출력할 내용을 문자열로 변환하고, 형식 지정 및 연결 등의 작업이 필요하기 때문에 속도에 영향을 줄 수 있습니다.
<br>
<b>3. Global Interpreter Lock(GIL)</b><br>
CPython (파이썬의 표준 구현체)에서는 GIL이라는 메커니즘이 존재합니다. GIL은 여러 스레드 간의 동시 실행을 제한하여 파이썬 코드를 안전하게 실행하도록 합니다. 이는 입출력 작업과 같이 I/O 바운드 작업에서는 크게 문제가 되지 않지만, CPU 집약적인 작업에서는 성능 저하를 일으킬 수 있습니다.
<br>
<b>4. I/O Overhead</b><br>
파일 또는 터미널과의 상호 작용은 운영체제와의 통신을 포함하므로 I/O 작업은 일반적으로 상당한 시간이 소요됩니다.


<i>이러한 이유들로 인해 `input()` 및 `print()` 함수는 대규모 데이터 처리나 높은 성능이 필요한 작업에서는 부적합할 수 있습니다. 특히, 대량의 입력을 처리해야 하는 경우에는 입출력 속도를 향상시키기 위해 다른 방법을 고려하는 것이 좋습니다.</i>
<br>
<br>

# 3. sys 모듈

- 시스템과 관련된 여러 기능을 제공하는 모듈
-  파이썬 인터프리터와 상호 작용하며, 시스템과 관련된 작업을 수행할 때 유용

1. **명령행 인수 (Command Line Arguments) 다루기**: `sys.argv`를 통해 명령행 인수를 리스트로 받을 수 있습니다. 이를 통해 스크립트에 전달된 인수들을 접근할 수 있습니다.
	- 명령행 인수는 현 문서 하단 참조.

    ```python
    import sys

    # 명령행 인수 출력
    print(sys.argv)
    ```

2. **모듈 검색 경로 (Module Search Path) 설정 및 확인**: `sys.path`를 통해 파이썬 모듈을 검색하는 경로들을 확인하고 조작할 수 있습니다.

    ```python
    import sys

    # 모듈 검색 경로 출력
    print(sys.path)
    ```

3. **표준 입출력 스트림 제어**: `sys.stdin`, `sys.stdout`, `sys.stderr`를 통해 각각 표준 입력, 표준 출력, 표준 오류 스트림에 접근할 수 있습니다.

    ```python
    import sys

    # 표준 출력 스트림에 메시지 출력
    sys.stdout.write("Hello, World!\n")
    ```

4. **프로그램 종료**: `sys.exit()`를 통해 프로그램을 강제로 종료할 수 있습니다.

    ```python
    import sys

    # 프로그램 종료
    sys.exit()
    ```

5. **메모리 관리 및 Garbage Collection**: `sys.getsizeof()`를 사용하여 객체의 메모리 크기를 확인하거나, `sys.setrecursionlimit()`로 재귀 제한을 설정할 수 있습니다.

    ```python
    import sys

    # 메모리 크기 확인
    size = sys.getsizeof([1, 2, 3])
    print(size)
    ```

6. **인터프리터 상태 및 정보**: `sys.version`, `sys.platform` 등을 통해 현재 파이썬 인터프리터의 버전 및 플랫폼 정보를 얻을 수 있습니다.

    ```python
    import sys

    # 파이썬 버전 및 플랫폼 정보 출력
    print(sys.version)
    print(sys.platform)
    ```

`sys` 모듈은 시스템 레벨에서 다양한 작업을 수행하기 위한 기능들을 제공하므로, 파이썬 스크립트를 다양한 환경에서 실행하거나 제어해야 할 때 유용합니다.


## 참고 : 명령행 인수

- 명령행 인수(command line arguments) : 프로그램을 실행할 때 명령행에서 전달되는 값
- 프로그램이 실행되는 동안에만 유효하며, 실행 중에 프로그램에게 정보나 옵션을 전달하는 데 사용

- 보통 명령행 인수는 프로그램 실행 명령어 뒤에 추가되어 전달됨

```bash
python my_program.py arg1 arg2 arg3
```

		- 명령행 인수 :  `arg1`, `arg2`, `arg3`


파이썬에서는 `sys.argv`를 사용하여 명령행 인수에 접근할 수 있습니다. 이는 스크립트를 실행할 때 전달된 모든 명령행 인수를 담고 있는 리스트입니다. 첫 번째 요소 (`sys.argv[0]`)는 스크립트의 이름이고, 그 뒤에 나오는 요소들이 명령행 인수입니다.

예를 들어, 다음과 같은 파이썬 스크립트를 실행한다고 가정해 봅시다:

```python
# my_program.py

import sys

print("스크립트 이름:", sys.argv[0])
print("전달된 명령행 인수:", sys.argv[1:])
```

그리고 명령행에서 다음과 같이 실행한다면:

```bash
python my_program.py arg1 arg2 arg3
```

결과는 다음과 같을 것입니다:

```
스크립트 이름: my_program.py
전달된 명령행 인수: ['arg1', 'arg2', 'arg3']
```

이렇게 명령행 인수를 활용하면 프로그램에게 외부에서 데이터를 전달하거나 프로그램의 동작을 제어하는 데 사용할 수 있습니다.