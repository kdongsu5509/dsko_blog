### 파이썬에서 객체를 복사하는 2가지 방법
1. **얕은 복사 (Shallow Copy):**
   - 얕은 복사는 객체의 최상위 레벨만을 복사하고, 내부의 객체는 원본과 공유합니다.
   - `copy()` 메서드를 사용하여 얕은 복사를 수행할 수 있습니다.
   - `copy` 모듈의 `copy()` 함수도 얕은 복사를 수행합니다.
   - 리스트의 경우 `[:]` 슬라이싱을 사용하여 얕은 복사를 수행할 수도 있습니다.

    예시:
    ```python
    import copy

    original_list = [[1, 2], [3, 4]]
    shallow_copied_list = copy.copy(original_list)

    shallow_copied_list[0][0] = 0

    print(original_list)  # 출력: [[0, 2], [3, 4]]
    ```

2. **깊은 복사 (Deep Copy):**
   - 깊은 복사는 객체의 모든 내부 객체까지 새로운 객체로 복사합니다. 따라서 원본과 완전히 독립적인 객체가 생성됩니다.
   - `copy` 모듈의 `deepcopy()` 함수를 사용하여 깊은 복사를 수행할 수 있습니다.

    예시:
    ```python
    import copy

    original_list = [[1, 2], [3, 4]]
    deep_copied_list = copy.deepcopy(original_list)

    deep_copied_list[0][0] = 0

    print(original_list)  # 출력: [[1, 2], [3, 4]]
    ```

파이썬의 `copy` 모듈은 얕은 복사와 깊은 복사를 수행하는 함수를 제공합니다. 따라서 복사 방법을 선택할 때는 객체의 구조와 참조 관계를 고려하여 적절한 방법을 사용해야 합니다.

함께 보면 좋을 자료  : [[Java에서의 얇은 복사]]