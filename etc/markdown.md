# 마크다운 문법 정리

## Heading
- 문서의 제목이나 소제목
- #의 개수에 따라 heading level이 정해짐(h1~h6까지)

## List
- 순서가 있는 리스트(ol)와 순서가 없는 리스트(ul)로 구성
- tab으로 하위 항목 구성 가능
- ol: 1. text
- ul: - text / * text

## Fenced Code block
- backtick(`) 기호 3개를 사용하여 작성
```python
printf("hello")
```

## Inline Code block
- backtick 기호 1개를 사용하여 작성

## Link
```bash
[문자열](url)
```
- [naver](https://naver.com)
- 파일이나 폴더도 삽입 가능

## Image
```bash
![문자열](url)
```
- ![text](image.jpg)
- 다른 폴더에 있는 이미지를 불러오기 위해서는 파일 경로 필요

## Blockquote
```bash
>text
```
>이런 식으로 보여짐

## 텍스트 효과
```bash
**text** / __text__
```
- **bold**
```bash
*text* / _text_
```
- *italic*
