### 1) 리액트를 왜 사용하는가?

**모바일 앱 처럼 동작하는 웹들.**

- 메이저 SNS 들도 마찬가지로 새로고침 없이 웹 탐색이 가능함.
- 이런 사이트들을 Web-app이라고 부름.
- 실제로 앱은 아니지만 앱과 사용성이 동일함.

**Web-app을 쉽게 만들 수 있는 언어 → React, Angular, Vue**

**웹앱의 장점**

- 모바일 앱으로 발행이 쉬움.
- 앱처럼 뛰어난 UX
- 기존 웹사이트 보다 비즈니스적으로 강점이 많음.
- 모든 웹사이트는 React나 웹을 많이 도입하는 추세임.

---

### 2) 리액트란?

**자바스크립트의 라이브러리**

- 자바스크립트를 그대로 사용하지만 문법적으로 다름
- 웹사이트의 내용이 바뀔 경우 자동으로 업데이트를 해줌.
- 코드 재활용을 많이 함.
- 리액트는 HTML, JS가 합쳐진 파일임. 이를 JSX 문법이라고 부름.

**App.jsx**

- 이 파일의 내용이 웹사이트에 보임.

```jsx
function App() {
  return (
    <main>
      안녕하세요
    </main>
  );
};
```

**index.html**

- 리액트는 SPA(Single Page Application) 라고 해서 페이지가 하나밖에 없음. (.html 파일 1개)
    - 페이지를 로드할때마다 이 html 파일의 내용을 변경해준다고 생각하면 됨.
    - 마치 유저의 눈에는 웹페이지가 여러개인것처럼 보임.

```jsx
...
<body>
  <div id="root"></div> // 이 부분!
  <script type="module" src="/src/main.jsx"></script>
...
```

**main.jsx**

- index.html 파일과 App.jsx를 연결해주는 브릿지역할

```jsx
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
  document.getElementById('root') // 여기서의 root가 index.html의 root
)
```

- root에 </App>을 그려준다고 이해하면 됨.
- 참고로 우린 이 파일 수정할 일 없음.

---

**참고사이트**

[React 기초 0강 : 리액트왜 쓰는지 알려줌 (+ 수강시 필요 사전지식)](https://www.youtube.com/watch?v=LclObYwGj90)

[이거 모르면 프론트엔드 개발자 못됨 | 리액트 진짜 쉽게 설명해줌 | 리액트 초보자 입문 강의 1탄](https://www.youtube.com/watch?v=MeZ3FCTub3I)