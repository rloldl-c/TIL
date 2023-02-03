# 리스트
## 1. 배열(Array)
- 여러 데이터들이 연속된 메모리 공간에 저장되어 있는 자료구조
- 인덱스를 통해 데이터에 빠르게 접근
- 데이터 타입 고정, 배열의 길이 변경 불가

## 2. 연결 리스트(Linked List)
- 데이터가 담긴 여러 노드들이 순차적으로 연결된 형태의 자료구조
- 현재 노드가 다음 순서의 노드 데이터 주소를 가르키는 형태로 연결
- 길이 변경 가능, 삽입과 삭제가 편리

## 리스트 컴프리헨션
- 리스트를 간단하게 생성하는 방법
```python
numbers = []
for i in range(5):
  numbers.append(i)

# ==================================

numbers = [i for i in range(5)]
```
- if문으로 필터링도 가능
```python
odd_num = [i for i in range(10) if i % 2 == 1]
```

<br>

# 스택(Stack)
- 데이터를 한 쪽에서만 넣고 빼는 자료구조
- 가장 마지막에 들어온 데이터가 가장 먼저 나가는 LIFO(후입선출) 방식
- `push`: 스택에 새로운 데이터를 삽입
- `pop`: 스택의 가장 마지막 데이터를 추출
- 파이썬에서는  `append()`와 `pop()`으로 스택을 구현
### 언제 사용할까?
- 이전의 작업을 기억할 때(뒤집기, 되돌아가기)
- 괄호 매칭, 함수 호출(재귀), 백트래킹, DFS
### 문제
- [BOJ 10773번 제로](https://www.acmicpc.net/problem/10773)

```python
test = int(input())
numbers = []

for i in range(test):
    n = int(input())
    if n == 0:
        numbers.pop()
    else:
        numbers.append(n)

print(sum(numbers))
```

# 큐(Queue)
- 한 쪽 끝에서 데이터를 넣고, 다른 쪽 끝에서만 데이터를 뺄 수 있는 자료구조
- 가장 먼저 들어온 데이터가 가장 먼저 나가는 FIFO(선입선출) 방식
- dequeue: 큐의 맨 앞 데이터를 추출
- enqueue: 큐의 맨 뒤에 데이터를 삽입
- 파이썬에서는 `append()`와 `pop(0)`으로 큐를 구현
### 언제 사용할까?
- 순서와 대기
- BFS, 다익스트라(우선순위 큐)
### 문제
- [BOJ 2161번 카드1](https://www.acmicpc.net/problem/2161)
```python
num = int(input())
card = [i for i in range(1, num+1)]

while len(card) != 1:
    print(card.pop(0), end=" ")
    card.append(card.pop(0))

print(card[0])
```

## 덱(Deque)
- 큐에 저장된 데이터가 많아지면 pop(0)을 할 경우 인덱스가 바뀌면서 비효율적이라 덱을 사용하는 편이 좋음
- 양 방향으로 삽입과 삭제가 자유로운 큐
- `appendleft()`,` popleft()`로 양 방향에서 삽입과 추출이 가능
```python
from collections import deque

num = int(input())
card = deque(range(1, num+1))

while len(card) != 1:
    print(card.popleft(), end=" ")
    card.append(card.popleft())

print(card[0])
```

# 힙(Heap)
- 이진 트리 형태의 자료구조
- 튜플을 요소로 사용 가능
### 언제 사용할까?
- 데이터가 지속적으로 정렬되어야 할 때
- 데이터에 삽입/삭제가 빈번한 경우 사용
## heap 모듈
- Minheap으로 구현(최소값이 먼저)
1. `heapq.heapify()`: 힙이 아닌 리스트를 힙으로 변환
2. `heapq.heappop(heap)`: 힙에서 가장 작은 요소를 반환
3. `heapq.heappush(heap, item)`: 힙 구조를 유지하면서 item을 heap에 삽입

### 문제
- [BOJ 11286번](https://www.acmicpc.net/problem/11286)
```python
import sys
import heapq

input = sys.stdin.readline

test = int(input())
numbers = []

for _ in range(test):
    n = int(input())

    if n != 0:
        heapq.heappush(numbers, (abs(n), n))
    else:
        if numbers:
            print(heapq.heappop(numbers)[1])
        else:
            print(0)
```

<br>

# 셋(Set)
- 수학에서의 집합을 나타내는 자료구조
- 연산
    1. `.add()`
    2. `.remove()`
    3. `|` (합집합)
    4. `-` (차집합)
    5. `&` (교집합)
    6. `^` (대칭차집합)

### 언제 사용할까?
- 데이터의 중복이 없어야 할 때
- 정수가 아닌 데이터의 삽입/삭제/탐색이 자주 일어날 때

### 문제
- [BOJ 1269번](https://www.acmicpc.net/problem/1269)
```python
import sys
input = sys.stdin.readline

a, b = map(int, input().split())
a_set = list(map(int, input().split()))
b_set = list(map(int, input().split()))
a_set = set(a_set)
b_set = set(b_set)

print(len(a_set ^ b_set))
```