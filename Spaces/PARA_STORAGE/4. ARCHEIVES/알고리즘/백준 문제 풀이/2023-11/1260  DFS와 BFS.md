---
tags:
  - Baekjoon
---
1. 문제
![[1260번_ DFS와 BFS.png]]

2. 문제 파악
- 이 문제는 DFS와 BFS를 사용해보는 기초적인 문제임.
	- 이 문제 해결 Key는 Edge에 연결된 2개의 Vertex정보를 받으면 이것을 어떻게 인접 행렬로 표현할 것인가를 해결하는 것이었음.
		- vertex1, vertex2를 입력받고, 그것을 리스트에 맞게 -1 감소시켜 각각 넣는다.
		- 이후 정렬을 통해 작은 숫자부터 큰 숫자로 가도록 만든다.
		- 이후 기존에 알던 것 처럼 DFS, BFS을 이용해서 문제를 해결하도록 한다.
		- 참고 : [[5-0.DFS & BFS]] 





4. 정답 코드 
```
from collections import deque

  

def dfs(graph, start, visited):

    visited[start] = True

    print(start+1, end=" ")

    for i in graph[start]:

        if not visited[i]:

            dfs(graph, i, visited)

  

def bfs(graph, start, visited):

    heap = deque([start])

    visited[start] = True

    while heap:

        pop = heap.popleft()

        print(pop+1, end=" ")

        for i in graph[pop]:

            if not visited[i]:

                heap.append(i)

                visited[i] = True

  

vertex, edge, start = map(int, input().split())

  

#입력을 받는 부분

#2차원 배열을 만들어서 인접 행렬 방식 사용

  

graph = []

for a in range(vertex):

    t = []

    graph.append(t)

#2차원 배열 완성 2 * vertex

  

for a in range(edge):

    x, y = map(int, input().split())

    #x,y 로 입력을 받을 거에요. -> x에도 y가 들어가야하고, ,y에도 x가 들어가야한다.

    #x에 y를 넣을거야.

    something1 = graph[x-1]

    something1.append(y-1)

    something2 = graph[y-1]

    something2.append(x-1)

  

visited1 = [False] * (vertex)

visited2 = [False] * (vertex)

  

for z in range(vertex):

    s = graph[z]

    s.sort()

  

dfs(graph, start-1, visited1)

print()

bfs(graph, start-1, visited2)
```

내가 지금까지 알고 있는 DFS, BFS 알고리즘 해결 방법은, 그래프가 2차원 인접행렬로 주어질 때 사용가능한 방법이다.

이번에도 그것을 사용했다.

입력은 어떤 edge가 어떤 vertex 2개를 연결하는 지에 관해서만 제공했다.
-> 아 그러면 두 vertex가 2차원 인접행렬을 표로 나타낼 때, x,y축을 이루는 값이므로, 2차원 그래프를 생성한 후에, 이 값들을 하나씩 줄여서 각각 넣자.
-> 그 후에 sort해서 순서대로 정렬하자
-> 그 후에 dfs, bfs라는 함수를 실행하되, 출력시에는, 입력할 때 하나 줄인 것을 고려하여, +1를 하여 출력이 되도록 하자.