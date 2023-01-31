# 이차원 리스트
- 리스트를 원소로 가지는 리스트
```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(matrix[0])
# [1, 2, 3]
print(matrix[1])
# [4, 5, 6]
print(matrix[2])
# [7, 8, 9]
print(matrix[0][0])
# 1
print(matrix[1][2])
# 5
print(matrix[2][0])
# 7
```

<br>

## 1. 이차원 리스트 만들기
1. 반복문
```python
matrix = []

# n x m 행렬
n = 100
m = 100
for _ in range(n):
    matrix.append([0] * m)
```

2. 리스트 컴프리헨션
```python
matrix = []

# n x m 행렬
matrix = [[0] * m for _ in range(n)]
```

<br>

## 2. 이차원 리스트 입력 받기
1. 행렬의 크기가 미리 주어지는 경우
```python
matrix = []

n = 3
m = 3

for _ in range(3):
    line = list(map(int, input().split()))
    matrix.append(line)

matrix = [list(map(int, input().split())) for _ in range(3)]
```

2. 행렬의 크기를 입력 받는 경우
```python
n, m = map(int, input().split())
matrix = []

for _ in range(n):
    line = list(map(int, input().split()))
    matrix.append(line)

matrix = [list(map(int, input().split())) for _ in range(n)]
```

<br>

## 3. 순회
1. 행 우선 순회
```python
matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8].
    [9, 0, 1, 2]
]

for i in range(3):
    for j in range(4):
        print(matrix[i][j], end=" ")
    print()

# 1 2 3 4
# 5 6 7 8
# 9 0 1 2
```

2. 열 우선 순회
```python
matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8].
    [9, 0, 1, 2]
]

for i in range(4):
    for j in range(3):
        print(matrix[j][i], end=" ")
    print()

# 1 5 9
# 2 6 0
# 3 7 1
# 4 8 2
```

### 3. map() 활용
1. 총합 구하기
```python
matrix = [
  [1, 1, 1, 1],
  [1, 1, 1, 1],
  [1, 1, 1, 1]
]

total = sum(map(sum, matrix))
print(total)
# 12
```

2. 최대, 최소값 구하기
```python
matrix = [
  [0, 5, 3, 1],
  [4, 6, 10, 8],
  [9, -1, 1, 5]
]

max_ = max(map(max, matrix))
min_ = min(map(min, matrix))
print(max_, min_)
# 10 -1
```

<br>

## 4. 전치
- 전치(transpose): 행과 열을 바꾸는 것
```python
matrix = [
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9, 0, 1, 2]
]

# 행과 열 크기가 반대인 새로운 리스트 생성
new_matrix = [[0] * 3 for _ in range(4)]

# 행과 열 바꾸기
for i in range(4):
    for j in range(3):
        new_matrix[i][j] = matrix[j][i]

"""
new_matrix = [
  [1, 5, 9],
  [2, 6, 0],
  [3, 7, 1],
  [4, 8, 2]
]
"""
```

<br>

## 5. 회전
1. 왼쪽으로 90도 회전
```python
matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]

n = 3
new_matrix = [[0] * n for _ in range(n)]

for i in range(n):
    for j in range(n):
        new_matrix[i][j] = matrix[j][n-i-1]

"""
new_matrix = [
  [3, 6, 9],
  [2, 5, 8],
  [1, 4, 7]
]
"""
```

1. 오른쪽으로 90도 회전
```python
matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]

n = 3
new_matrix = [[0] * n for _ in range(n)]

for i in range(n):
    for j in range(n):
        new_matrix[i][j] = matrix[n-j-1][i]

"""
new_matrix = [
  [7, 4, 1],
  [8, 5, 2],
  [9, 6, 3]
]
"""
```