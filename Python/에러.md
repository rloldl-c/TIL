# 에러와 예외

## 에러
- 프로그램이 실행되지 않음
- 줄에서 에러가 감지된 가장 앞의 위치를 가리키는 캐럿 기호(^) 표시
### 문법 에러(Syntax Error)
- EOL(End Of Line)
- EOF(End Of File)
- Invalid syntax
- assign to literal

## 예외(Exception)
- 실행 도중 예상치 못한 상황으로 프로그램이 멈추는 등 실행 중에 감지되는 에러를 예외라고 부름
  - 문법적으로 오류가 없음에도 발생하는 에러
- 예외는 여러 타입으로 나타나고, 메시지의 일부로 출력
- 사용자 정의 예외를 만들어서 관리할 수 있음

1. ZeroDivisionError: 0으로 나누고자 하는 경우
2. NameError: namespace 상에 이름이 없는 경우
3. TypeError
    - 타입 불일치<br>
      `1 + '1'`
    - arguments 부족 혹은 초과<br>
      `divmod()` <br>
      `divmod(1, 2, 3)`
4. ValueError: 타입은 올바르지만 값이 적절하지 않는 경우<br>
    `int('3.5')`
5. IndexError: index가 범위를 벗어난 경우
6. ModuleNotFoundError: 존재하지 않는 모듈을 improt한 경우<br>
    `import nonamed`
7. ImportError: 모듈은 있으나 존재하지 않는 클래스 / 함수를 가져오는 경우<br>
    `from random import samp`
8. IndentationError: 들여쓰기가 적절하지 않은 경우
9. KeyboardInterrupt: 프로그램을 임의로 종료한 경우