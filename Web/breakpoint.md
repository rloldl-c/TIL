# Breakpoints
- 웹 페이지를 다양한 화면 크기에서 적절하게 배치하기 위한 분기점
- 화면 너비에 따라 6개의 분기점 제공
- 각 breakpoints마다 설정된 최대 너비 값 **이상으로** 화면이 커지면 grid system 동작이 변경
- 화면이 작을 때 코드를 먼저 작성한 후 breakpoints를 작성하는 것이 더 편함

||xs<br>$\lt$ 576px|sm<br>$\geq$ 576px|md<br>$\geq$ 768px|lg<br>$\geq$ 992px|xl<br>$\geq$ 1200px|xxl<br>$\geq$ 1400px|
|---|---|---|---|---|---|---|
|Container<br>`max-width`|None(auto)|540px|720px|960px|1140px|1320px|
|Class prefix|`.col-`|`.col-sm-`|`.col-md-`|`.col-lg-`|`.col-xl-`|`.col-xxl-`|