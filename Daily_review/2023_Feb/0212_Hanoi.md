# 오늘 한 일
## 재귀 - 하노이의 탑
### 원반의 개수 n / 막대 1번에서 3으로 옮기는 것이 목표
<br>

### 1. n = 1일 때
1.  1번 원반을 3번 막대로 옮기기

### 2. n = 2일 때
1. 1번 원반을 2번 막대로 옮기기
2. 2번 원반을 3번 막대로 옮기기
3. 1번 원반을 3번 막대로 옮기기

### 3. n = 3일 때
1. 1번 원반을 3번 막대로 옮기기
2. 2번 원반을 2번 막대로 옮기기
3. 1번 원반을 2번 막대로 옮기기
4. 3번 원반을 3번 막대로 옮기기
5. 1번 원반을 1번 막대로 옮기기
6. 2번 원반을 3번 막대로 옮기기
7. 1번 원반을 3번 막대로 옮기기

### 재귀적으로 보자면
1. 1번부터 n-1번 원반을 목표 막대가 아닌 다른 막대로 옮기기(재귀)
2. n번 원반을 목표 막대로 옮기기
3. 1번부터 n-1번 원반을 목표 막대로 옮기기(재귀)
- 총 $2^n - 1$번의 이동으로 옮길 수 있음

```python
def hanoi(num, start, via, end):
    if num == 1:
        print(start, end)
        return
    
    hanoi(num-1, start, end, via)
    print(start, end)
    hanoi(num-1, via, start, end)
```