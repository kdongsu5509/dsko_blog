---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/java/java/"}
---

[LV2_할인행사_프로그래머스](https://school.programmers.co.kr/learn/courses/30/lessons/131127?language=java)
를 보면서 맛보자.

```java
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

public class Solution {
    public int solution(String[] want, int[] number, String[] discount) {
        Map%3CString, Integer%3E di = new HashMap<>();
        for (int x = 0; x < number.length; x++) {
            di.put(want[x], x);
        }

        int[] li = new int[number.length];
        for (int y = 0; y < number.length; y++) {
            li[y] = number[y];
        }

        int answer = 0;

        for (int idx = 0; idx < discount.length - 9; idx++) {
            int[] tempLi = new int[li.length]; // 새로운 배열 생성
            System.arraycopy(li, 0, tempLi, 0, li.length); // 배열 복사
            for (int i = idx; i < idx + 10; i++) {
                try {
                    String tk = discount[i];
                    int tempLiIdx = di.get(tk);
                    if (tempLi[tempLiIdx] > 0) {
                        tempLi[tempLiIdx] -= 1;
                    }
                } catch (NullPointerException e) {
                    continue;
                }
            }
            int tempSum = Arrays.stream(tempLi).sum(); // 배열의 합을 계산하여 tempSum에 할당
            if (tempSum == 0) {
                answer++;
            }
        }
        return answer;
    }
}
```
- 위의 Logic에서는 매번 복사를 하기 전에 DeepCopy를 진행했습니다. -> 당연히 변화되는 값이 원본 정수 배열에 영향을 미치지 않습니다.

- 그럼 해당 문제에 ShallowCopy를 한 경우의 코드를 보겠습니다.
```java
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

public class Solution {
    public int solution(String[] want, int[] number, String[] discount) {
        Map%3CString, Integer%3E di = new HashMap<>();
        for (int x = 0; x < number.length; x++) {
            di.put(want[x], x);
        }

        int[] li = new int[number.length];
        for (int y = 0; y < number.length; y++) {
            li[y] = number[y];
        }

        int answer = 0;

        for (int idx = 0; idx < discount.length - 9; idx++) {
            int[] tempLi = li.clone(); // 배열 복사
            for (int i = idx; i < idx + 10; i++) {
                try {
                    String tk = discount[i];
                    int tempLiIdx = di.get(tk);
                    if (tempLi[tempLiIdx] > 0) {
                        tempLi[tempLiIdx] -= 1;
                    }
                } catch (NullPointerException e) {
                    continue;
                }
            }
            int tempSum = Arrays.stream(tempLi).sum(); // 배열의 합을 계산하여 tempSum에 할당
            if (tempSum == 0) {
                answer++;
            }
        }
        return answer;
    }
}
```
- 여기서는 Object.clone()을 이용해 shallowCopy를 진행했습니다. 그러나 프로그래머스에서 이 코드를 진행시켜보면 정답으로 처리됩니다! -> Why?
- [Object.clone() 관련 java docs](<https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Object.html#clone()>)
- Summarize
	- 관례적으로 Object.clone()은 원본과 독립적이기 때문이다!!
	- But, Python과 같은 것에서는 다름.
		- Python3에서는 shallowCopy시 같이 변하니, deepCopy를 구현하자.

###### 함께 보면 좋을 자료
[[Spaces/PARA_STORAGE/1. PROJECT/개발자로 살아가기/Python/Copy at python\|Copy at python]]
