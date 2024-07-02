## Java에서 해시를 사용하는 것을 알아보자
참고 :  [프로그래머스-완주하지 못한 선수](https://school.programmers.co.kr/learn/courses/30/lessons/42576?language=java)


```Java
import java.util.*;

class Solution {
    public String solution(String[] participant, String[] completion) {
        Map<String, Integer> map = new HashMap<>();
        
        for(String p : participant){
            map.put(p, map.getOrDefault(p, 0) + 1);
        }
        for(String c : completion){
            map.put(c, map.get(c) - 1);
        }
        for(Map.Entry<String, Integer> entry : map.entrySet()){
            if(entry.getValue() > 0){
                return entry.getKey();
            }
        }
        String answer = "";
        return answer;
    }
}
```

`map.getOrDefault(K,V)` 
- 해당 key가 존재하지 않는 경우 : `k`를 기본 key로 설정하고 , `V`를 기본 value로 설정후 삽입
- 해당 key가 존재하는 경우 : 이미 존재하는 값을 가져온 다음, value에 +1.

`map.get(K)`
- K라는 key를 가진 녀석의 value 호출

`map.entrySet()`
- Original Form : Set<Map.Entry<K,V>>	entrySet()
- Returns a [`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html "interface in java.util") view of the mappings contained in this map.



