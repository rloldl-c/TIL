# 오늘 한 일
## JavaScript
### `window.scrollTo`
```javascript
window.scrollTo(x-coord, y-coord)
window.scrollTo({top: value, left: value, behavior: value})
```
- 지정된 위치로 스크롤을 이동
- `top`: 수직으로 이동할 위치
- `left`: 수평으로 이동할 위치
- `behavior`: 스크롤 효과
    - `auto`: 기본값, 설정한 위치로 바로 이동
    - `smooth`: 부드럽게 스크롤 되는 애니메이션을 보여줌

<br>

### `in`
```javascript
prop in objects
```
- 속성이 객체에 존재하면 `true`를 반환
- 배열에서 사용할 경우 value가 아닌 **index**를 확인
``` javascript
const trees = ["redwood", "bay", "cedar", "oak", "maple"];
0 in trees         // true
3 in trees         // true
6 in trees         // false
"bay" in trees     // false(배열의 값이 아닌 인덱스를 작성해야 함)
```

<br>

### `includes()`
```javascript
arr.includes(valueToFind[, fromIndex])
```
- 배열이 특정 요소를 포함하고 있으면 `true`, 아니면 `false`를 반환
- `fromIndex`로 검색을 시작할 위치를 명시 가능
    - `fromIndex` 값이 배열의 길이와 같거나 크다면 `false`를 반환
    - `fromIndex` 값이 음수라면 배열 길이에서 `fromIndex` 값을 뺀 결과로 판별
        ```javascript
        // arr.length = 3
        // fromIndex = -100
        // computed index = 3 + (-100) = -97

        const arr = ['a', 'b', 'c'];

        arr.includes('a', -100); // true
        arr.includes('b', -100); // true
        arr.includes('c', -100); // true
        arr.includes('a', -2); // fromIndex = 3 + (-2) = 1, false
        ```