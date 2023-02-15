# 오늘 한 일
## SQL - JOIN
- 두 개 이상 테이블 간의 관계를 만들어주는 키워드
- INNER JOIN / OUTER JOIN(LEFT JOIN, RIGHT JOIN)으로 나뉨
- LEFT JOIN은 왼쪽 테이블의 모든 레코드를 조회, RIGHT JOIN은 오른쪽 테이블의 모든 레코드를 조회
- LEFT JOIN, RIGHT JOIN 상관 없이 FROM절 뒤에 오는 테이블이 왼쪽 테이블에 해당

<br>

## Algorithm - 백트래킹
- 모든 경우의 수를 확인해야하는데 깊이가 정해지지 않아 for문을 사용하지 못하는 경우 재귀를 이용하여 접근
    - ex) [BOJ 15649번](https://www.acmicpc.net/problem/15649): 1부터 N까지 자연수 중에서 중복 없이 M개를 고른 수열
1. 몇 개인지 카운트 하는 변수를 인자로 함수 정의
2. 카운트 변수가 M과 같아지면 프린트하고 return
3. 그렇지 않으면 1부터 N까지 중에 이미 선택한 값이 아닌 수를 하나 선택하고
4. 방문 체크 + 결과값 추가 + 재귀 호출
- 시간복잡도
    - 중복 가능: $N^N$
    - 중복 불가: $N!$

- 예시코드
```python
n, m = map(int, input().split())
res = [] # 결과값 저장할 리스트
visited = [False] * (n+1)

def recur(num):
    if num == m:
        print(*res)
        return

    for i in range(1, n+1):
        if not visited[i]:
            visited[i] = True
            res.append(i)
            recur(num+1)
            visited[i] = False
            res.pop()

recur(0)
```