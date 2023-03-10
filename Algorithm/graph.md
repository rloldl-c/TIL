# 그래프

## 1. 그래프란
- 정점(vertex)과 이를 연결하는 간선(edge)들의 집합으로 이루어진 비선형 자료구조
- 정점(vertex): 간선으로 연결되는 객체, 노드(node)라고도 한다
- 간선(edge): 정점 간의 관계(연결)을 표현하는 선
- 경로(path): 시작 정점부터 도착 정점까지 거치는 정점을 나열한 것
- 인접(adjacency): 두 개의 정점이 하나의 간선으로 직접 연결된 상태

<br>

## 2. 그래프 종류
### 1. 무방향 그래프
- 간선의 방향이 없는 가장 일반적인 그래프
- 간선을 통해 양방향으로 이동 가능
- 차수(degree): 하나의 정점에 연결된 간선의 개수
- 모든 정점의 차수 총합 = 간선 수 x 2

### 2. 유방향 그래프
- 간선의 방향이 있는 그래프
- 간선의 방향이 가리키는 정점으로만 이동 가능
- 차수(degree): 진입 차수와 진출 차수로 나뉘어짐
  - 진입 차수: 외부 정점에서 들어오는 간선의 수
  - 진출 차수: 외부 정점으로 나가는 간선의 수

<br>

## 3. 그래프의 표현
- 문제에서 주어지는 간선이 연결하는 두 정점의 목록으로 그래프를 표현
### 1. 인접 행렬
- 두 정점을 연결하는 간선이 있는지 없는지를 행렬로 표현
```python
# 입력 = [0 1 / 0 2 / 1 3 / 1 4 / 2 4 / 2 5 / 4 6]

# 인접 행렬 만들기
n = 7 # 정점 개수
m = 7 # 간선 개수

graph = [[0] * n for _ in range(n)]

for _ in range(m):
    v1, v2 = map(int, input().split())
    # 양방향이니까 v1, v2 / v2, v1
    graph[v1][v2] = graph[v2][v1] = 1

# 인접 행렬 결과
graph = [
  [0, 1, 1, 0, 0, 0, 0],
  [1, 0, 0, 1, 1, 0, 0],
  [1, 0, 0, 0, 1, 1, 0],
  [0, 1, 0, 0, 0, 0, 0],
  [0, 0, 1, 0, 0, 0, 0],
  [0, 0, 0, 0, 1, 0, 0]
]
```

### 2. 인접 리스트
- 리스트를 통해 각 정점에 대한 인접 정점들을 표현
  - 리스트 인덱스가 각 정점이고 요소들이 인접 정점
```python
# 입력 = [0 1 / 0 2 / 1 3 / 1 4 / 2 4 / 2 5 / 4 6]

# 인접 리스트 만들기
n = 7 # 정점 개수
m = 7 # 간선 개수

graph = [[] for _ in range(n)]

for _ in range(m):
    v1, v2 = map(int, input().split())
    graph[v1].append(v2)
    graph[v2].append[v1]

# 인접 리스트 결과
graph = [
  [1, 2],
  [0, 3, 4],
  [0, 4, 5],
  [1],
  [1, 2, 6],
  [2],
  [4]
]
```
