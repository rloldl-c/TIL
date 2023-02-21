# 최단 경로
## 다익스트라
- 특정 노드에서 출발하여 다른 모든 노드로 가는 최단 경로를 계산
### 동작 과정
1. 출발 노드 설정
2. 최단 거리 테이블 초기화
    - 모든 노드까지 가는 비용은 무한, 자기 자신은 0으로 초기화
3. 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드 선택
4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신
5. 3번과 4번 과정 반복

### 간단한 구현 방법
- 총 $O(V)$ 번에 걸쳐서 가장 짧은 노드를 매번 선형탐색 ➡ 전체 시간 복잡도 $O(V^2)$
```python 
INF = int(1e9) # 무한을 의미하는 값으로 10억 설정

# 노드 개수, 간선 개수
n, m = map(int, input().split())
# 시작 노드 번호
start = int(input())
# 각 노드에 연결되어 있는 노드 정보
graph = [[] for _ in range(n+1)]
# 방문한 적이 있는지 체크하는 리스트
visited = [False] * (n+1)
# 최단 거리 테이블
distance = [INF] * (n+1)

# 모든 간선 정보 입력 받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a에서 b로 가는 비용이 c라는 의미
    graph[a].append((b, c))

# 방문하지 않은 노드 중에서 거리가 가장 짧은 노드 반환
def get_smallest_node():
    min_value = INF
    index = 0 # 거리가 가장 짧은 노드

    for i in range(1, n+1):
        if distance[i] < min_value and not visited[i]:
            min_value = distance[i]
            index = i
    
    return index

def dijkstra(start):
    # 시작 노드에 대해서 초기화
    distance[start] = 0
    visited[start] = True

    for i in graph[start]:
        distance = i[1]

    # 시작 노드를 제외한 전체 노드 n-1개 반복
    for i in range(n-1):
        # 현재 거리가 제일 짧은 노드를 꺼내서 방문처리
        now = get_smallest_node()
        visited[now] = True
        # 현재 노드와 연결된 노드 확인
        for j in graph[now]:
            cost = distance[now] + j[1]
            # 현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[j[0]]:
                distance[j[0]] = cost

dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n+1):
    # 도달할 수 없는 경우, 무한으로 출력
    if distance[i] == INF:
        print("INFINITY")
    # 도달할 수 있는 경우 거리를 출력
    else:
        print(distance[i])
```

### 힙(Heap)을 활용한 구현
- 노드를 하나씩 꺼내서 검사하는 while문은 최대 노드의 개수 $V$만큼 수행
- 현재 큐에서 꺼낸 노드와 연결된 다른 노드들을 확인하는 총횟수는 최대 간선의 개수($E$)만큼 수행
- 전체 과정은 E개의 원소를 큐에 넣었다가 모두 빼내는 연산과 유사하므로(중복 간선을 포함하지 않는 경우) <br>
$O(ElogE)$ ➡ $O(ElogV^2)$ ➡ $O(2ElogV)$ ➡ $O(ElogV)$
```python
import heapq
INF = int(1e9)

# 노드 개수, 간선 개수
n, m = map(int, input().split())
# 시작 노드 번호
start = int(input())
# 각 노드에 연결되어 있는 노드 정보
graph = [[] for _ in range(n+1)]
# 방문한 적이 있는지 체크하는 리스트
visited = [False] * (n+1)
# 최단 거리 테이블
distance = [INF] * (n+1)

# 모든 간선 정보 입력 받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a에서 b로 가는 비용이 c라는 의미
    graph[a].append((b, c))

def dijkstra(start):
    q = []
    # 시작 노드로 가기 위한 최단 경로는 0으로 설정하여 큐에 삽입
    heapq.heappush((q, (0, start)))
    distance[start] = 0

    while q:
        # 거리가 가장 짧은 노드 꺼내기
        dist, now = heapq.heappop(q)
        # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
        if distance[now] < dist:
            continue
        # 현재 노드와 연결된 다른 인접한 노드들을 확인
        for i in graph[now]:
            cost = dist + i[1]
            # 현재 노드를 거쳐서, 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n+1):
    # 도달할 수 없는 경우, 무한으로 출력
    if distance[i] == INF:
        print("INFINITY")
    # 도달할 수 있는 경우 거리를 출력
    else:
        print(distance[i])
```

<br>

## 플로이드 워셜
- 모든 노드에서 다른 모든 노드까지의 최단 경로를 모두 계산
- 다익스트라 알고리즘과는 달리 매 단계마다 방문하지 않은 노드 중에 최단 거리를 갖는 노드를 찾는 과정은 불필요
- 2차원 테이블에 최단 거리 정보를 저장하고 점화식에 따라 갱신   
- 각 단계마다 $a$에서 $b$로 가는 최단 거리보다 $a$에서 $k$를 거쳐 $b$로 가는 거리가 더 짧은지 확인   
- $D_{ab} = min(D_{ab}, D_{ak} + D_{kb})$
- 노드의 개수가 $N$개일 때 알고리즘상으로 $N$번의 단계 수행
    - 각 단계마다 $O(N^2)$의 연산을 통해 현재 노드를 거쳐가는 모든 경로를 고려
- 따라서 총 시간 복잡도는 $O(N^3)$
```python
INF = int(1e9)

# 노드의 개수 및 간선의 개수 입력
n = int(input())
m = int(input())
# 2차원 리스트를 만들고 무한으로 초기화
graph = [[INF] * (n+1) for _ in range(n+1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0으로 초기화
for a in range(1, n+1):
    for b in range(1, n+1):
        if a == b:
            graph[a][b] = 0

# 각 간선에 대한 정보를 입력 받아, 그 값으로 초기화
for _ in range(m):
    # a에서 b로 가는 비용은 c
    a, b, c = map(int, input().split())
    graph[a][b] = c

# 점화식에 따라 플로이드 워셜 알고리즘 수행
for k in range(1, n+1):
    for a in range(1, n+1):
        for b in range(1, n+1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 수행 결과 출력
for a in range(1, n+1):
    for b in range(1, n+1):
        if graph[a][b] = INF:
            print("INFINITY", end=" ")
        else:
            print(graph[a][b], end=" ")
    print()
```

<br>

## 문제 풀이 1
- 어떤 나라에는 N개의 도시가 있다. 그리고 각 도시는 보내고자 하는 메시지가 있는 경우, 다른 도시로 전보를 보내서 다른 도시로 해당 메시지를 전송할 수 있다.
- 하지만 X라는 도시에서 Y라는 도시로 전보를 보내고자 한다면, 도시 X에서 Y로 향하는 통로가 설치되어 있어야 한다. 예를 들어 X에서 Y로 향하는 통로는 있지만 Y에서 X로 향하는 통로가 없다면 Y는 X로 메시지를 보낼 수 없다. 또한 통로를 거쳐 메시지를 보낼 때는 일정 시간이 소요된다.
- 어느 날 C라는 도시에서 위급 상황이 발생했다. 그래서 최대한 많은 도시로 메시지를 보내고자 한다. 메시지는 도시 C에서 출발하여 각 도시 사이에 설치된 통로를 거쳐, 최대한 많이 퍼져나갈 것이다.
- 각 도시의 번호와 통로가 설치되어 있는 정보가 주어졌을 때, 도시 C에서 보낸 메시지를 받게 되는 도시의 개수는 총 몇개이며 도시들이 모두 메시지를 받는 데까지 걸리는 시간은 얼마인지 계산하시오.
```python
import heapq
INF = int(1e9)

def dijkstra(start):
    q = []
    # 시작 노드로 가기 위한 최단 거리는 0으로 설정하여 큐에 삽입
    heapq.heappush(q, (0, start))
    distance[start] = 0

    while q:
        # 가장 거리가 짧은 노드에 대한 정보 꺼내기
        dist, now = heapq.heappop(q)
        if distance[now] < dist:
            continue
        # 현재 노드와 연결된 다른 인접한 노드 확인
        for i in graph[now]:
            cost = dist + i[1]
            # 현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

n, m, start = map(int, input().split())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트
graph = [[] for _ in range(n+1)]
# 최단 거리 테이블을 무한으로 초기화
distance = [INF] * (n+1)

# 간선 정보 입력 받기
for _ in range(m):
    x, y, z = map(int, input().split())
    graph[x].append((y, z))

dijkstra(start)

count = 0 # 도달할 수 있는 노드의 개수
max_distance = 0 # 도달할 수 있는 노드 중에서 가장 멀리 있는 노드와의 거리

for d in distance:
    if d != 1e9:
        count += 1
        max_distance = max(max_distance, d)

# 시작 노드는 제외해야 하므로 count - 1을 출력
print(count - 1, max_distance)
```

<br>

## 문제풀이 2
- 미래 도시에는 1번부터 N번까지의 회사가 있는데 특정 회사끼리는 서로 도로를 통해 연결되어 있다. 방문 판매원 A는 현재 1번 회사에 위치해 있으며, X번 회사에 방문해 물건을 판매하고자 한다.
- 미래 도시에서 특정 회사에 도착하기 위한 방법은 회사끼리 연결되어 있는 도로를 이용하는 방법이 유일하다. 또한 연결된 2개의 회사는 양방향으로 이동할 수 있다. 공중 미래 도시에서 특정 회사와 다른 회사가 도로로 연결되어 있다면, 정확히 1만큼의 시간으로 이동할 수 있다.
- 또한 오늘 방문 판매원 A는 기대하던 소개팅에도 참석하고자 한다. 소개팅의 상대는 K번 회사에 존재한다. 방문 판매원 A는 X번 회사에 가서 물건을 판매하기 전에 먼저 소개팅 상대의 회사에 찾아가서 함께 커피를 마실 예정이다. 따라서 방문 판매원 A는 1번 회사에서 출발하여 K번 회사를 방문한 뒤에 X번 회사로 가는 것이 목표다.
- 방문 판매원이 회사 사이를 이동하게 되는 최소 시간을 계산하시오.
```python
INF = int(1e9)

n, m = map(int, input().split())
graph = [[INF] * (n+1) for _ in range(n+1)]

for a in range(1, n+1):
    for b in range(1, n+1):
        if a == b:
            graph[a][b] = 0

for _ in range(m):
    a, b = map(int, input().split())
    graph[a][b] = 1
    graph[b][a] = 1

x, k = map(int, input().split())

for i in range(1, n+1):
    for a in range(1, n+1):
        for b in range(1, n+1):
            graph[a][b] = min(graph[a][b], graph[a][i] + graph[i][b])

distance = graph[1][k] + graph[k][x]

if distance >= INF:
    print(-1)
else:
    print(distance)
```