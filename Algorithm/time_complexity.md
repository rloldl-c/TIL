# 시간 복잡도(Time Complexity)
- 알고리즘의 수행 시간
- 최악의 입력 n개가 들어온다고 가정하고 측정
- 시간 복잡도가 높다? 느린 알고리즘
- 시간 복잡도가 낮다? 빠른 알고리즘

### 1. 단순 코드 구문
ex) 사칙연산, 읽고 쓰기 등<br>
총 시간 = n * k
```python
statement 1
statement 2
statement 3
...
statement k
```

### 2. 조건문
총 시간 = max(시간(code block 1), 시간(code block 2))
```python
if <expression>:
    code block 1
else:
    code block 2
```

### 3. 반복문
1. 단순 반복문<br>
총 시간 = N
```python
for i in range(N):
    code block 1
```

2. 중첩 반복문(1)<br>
총 시간 = N * M
```python
for i in range(N):
    for j in range(M):
        code block 1
```

3. 중첩 반복문(2)<br>
총 시간 = N + (N-1) + (N-2) + ... + 1
```python
for i in range(N):
    for j in range(i, N):
        code block 1
```

## 빅오(Big-O) 표기법
- 입력 n이 무한대로 커진다고 가정하고 시간 복잡도를 간단하게 표시하는 것
- 최고차항만 남기고 계수와 상수는 제거

### 1. O(1): 단순 산술 계산
- a + b, 100 * 200, ...

### 2. O(logN): 크기가 N인 리스트를 반절씩 순회 / 탐색
- 이진탐색(Binary Search), ...

### 3. O(N): 크기가 N인 리스트를 순회
- 1중 for문, ...

### 4. O(NlongN): 크기가 N인 리스트를 반절씩 순회*탐색
- 높은 성능의 정렬(Merge, Quick, Heap Sort)

### 5. O(N^2): 2중 리스트 순회
### 6. O(N^3): 3중 리스트 순회
### 7. O(2^N): 크기가 N인 집합의 부분 집합
### 8. O(N!): 크기가 N인 순열
<br>

## 알고리즘 문제에 적용
- 문제: 입력된 수 N까지 연속된 숫자들의 합 구하기
- 제한시간: 1초
- 입력: 1 <= N <= 1,000,000,000
```python
n = int(input())
total = 0

# (1) N = 1,000,000,000인 경우 제한시간을 초과
for i in range(1, n+1):
    total += i

# (2) N = 1,000,000,000인 경우에도 제한시간을 초과하지 않음
total = n * (n + 1) / 2

print(total)
```