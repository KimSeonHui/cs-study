# 브라우저 렌더링 과정

브라우저가 화면에 나타나는 요소를 렌더링 할 때, 웹킷(Webkit)이나 게코(Gecko) 등과 같은 렌더링 엔진을 사용한다.

> **렌더링 엔진이란?**  
> 요청 받은 내용을 브라우저 화면에 표시하는 일을 함

<br />

렌더링 엔진이 HTML, CSS, JavaScript로 렌더링할 때, **CRP(Critical Rendering Path)** 라는 프로세스를 사용해 다음 단계들로 이루어진다.

1. **HTML 파싱 후, DOM 트리 구축**
2. **CSS 파싱 후, CSSOM 트리 구축**
3. **JavaScript 실행**
   > 주의! HTML 중간에 script가 있으면 HTML 파싱이 중단됨!
4. **DOM과 CSSOM을 조합해 렌더 트리 구축**
   > 주의! `display : none` 속성과 같이 화면에 보이지도 않고 영역을 차지하지도 않는 것은 렌더 트리로 구축되지 않는다!
5. **레이아웃 생성**
6. **페인팅**

![image](https://github.com/baeharam/Must-Know-About-Frontend/assets/44824456/0c9f60ae-9922-4e9e-bbcd-b572904c47dc)

---

### 1. DOM 트리 구축

HTML 파서를 통해 HTML 마크업을 파싱해 DOM 트리로 변환한다.
DOM은 마크업과 1:1 관계를 맺으며 루트 요소 `<html>`로 시작해 각 페이지의 element/text에 대한 노드가 만들어진다.

```html
<html>
  <head>
    <title>Understanding the Critical Rendering Path</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <header>
      <h1>Understanding the Critical Rendering Path</h1>
    </header>
    <main>
      <h2>Introduction</h2>
      <p>Lorem ipsum dolor sit amet</p>
    </main>
    <footer>
      <small>Copyright 2017</small>
    </footer>
  </body>
</html>
```

![image](https://github.com/baeharam/Must-Know-About-Frontend/assets/44824456/7ad3d07c-326a-46d8-976d-c498303b2fc8)

> **주의**  
> 부분적으로 실행할 수 있어 페이지에 내용을 표시하기 위해 전체 문서를 로드할 필요가 없음!
> 하지만 다른 리소스인 `CSS`, `JavaScript`로 페이지 렌더링이 중단될 수 있음!

---

### 2. CSSOM 트리 구축

CSS 파서를 통해 CSS를 파싱해 CSSOM(CSS Object Model) 트리를 구축한다. CSSOM은 DOM과 연관된 스타일의 Object 표현이다.

```css
body {
  font-size: 18px;
}

header {
  color: plum;
}
h1 {
  font-size: 28px;
}

main {
  color: firebrick;
}
h2 {
  font-size: 20px;
}

footer {
  display: none;
}
```

![image](https://github.com/baeharam/Must-Know-About-Frontend/assets/44824456/43c36838-d80b-4a72-8933-ba009be22a7e)

---

### 3. JavaScript 실행

JavaScript는 **파서 차단 리소스(parser blocking resource)** 로 간주되기 때문에 HTML 파싱이 JavaScript에 의해 차단된다.

HTML 파서가 `<script>` 태그를 만나면 fetch를 중단하고 실행한다. 따라서 JavaScript 파일 내에 HTML DOM 요소를 참조하는 로직이 있는 경우 해당 HTML이 표시된 후에 `<script>` 를 배치해야 한다.

> **JavaScript로 파서 차단되는 걸 피하는 방법 - `async` 속성 사용하기**  
> `<script async src="script.js"></script>`

---

### 4. 렌더링 트리 구축

렌더링 트리는 DOM과 CSSOM의 조합으로 페이지에서 최종적으로 렌더링 될 내용을 나타내는 트리이다.

즉, 페이지에 실제로 표시되는 내용만 포함되기 때문에 `display : none` 과 같이 보이지도 않고 영역을 차지하지 않는 요소는 렌더링 트리에 포함되지 않는다. (`visibility :hidden`은 트리에 나타남 )

위 예제의 DOM과 CSSOM을 사용해 렌더링 트리가 생성된다.

![image](https://github.com/baeharam/Must-Know-About-Frontend/assets/44824456/c4b8be50-6757-45a3-a97a-d3f0efd925e0)

---

### 5. 레이아웃 생성(Layout / Reflow 단계)

뷰포트를 기반으로 렌더 트리의 각 노드가 가지는 정확한 위치와 크기를 계산한다.

---

### 6. 페인팅

계산한 위치와 크기를 기반으로 실제로 화면에 그리는 단계이다.
페인트 단계에서 처리되는 시간은 DOM 크기와 적용되는 스타일에 따라 다르다.

---

### 단계 확인

CRP 과정을 개발자도구로 확인할 수 있다.
![image](https://github.com/baeharam/Must-Know-About-Frontend/assets/44824456/5079505d-90ba-4b72-bb93-4a6baeedba3b)

1. Parse HTML을 통해 HTML 파싱 후 , DOM 트리 구축
2. Parse Stylesheet를 통해 CSS 파싱 후, CSSOM 트리 구축
3. Evaluate Script를 통해 JavaScript 실행
4. 렌더 트리 구축
5. Layout을 통해 뷰포트 기준으로 렌더트리 노드들의 각 크기 / 위치 계산
6. Paint를 통해 Layout에서 계산한 값들로 각 요소를 화면에 그림

---

### 참고 자료

- [브라우저의 랜더링 원리](https://github.com/baeharam/Must-Know-About-Frontend/blob/main/Notes/frontend/browser-rendering.md)
- [Naver, 브라우저는 어떻게 동작하는가?](https://d2.naver.com/helloworld/59361)
- [HTML Critical rendering path의 이해](https://blog.asamaru.net/2017/05/04/understanding-the-critical-rendering-path/)
