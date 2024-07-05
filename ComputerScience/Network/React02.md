# React 기초 02

## createRoot()

- createRoot() 함수는 HTML 요소라는 하나의 인수를 사용함.
- 이 함수의 목적은 React 구성 요소가 표시될 HTML 요소를 정의하는 것.

## render()

- 렌더링 해야하는 리액트 컴포넌트를 정의하기 위해 호출하는 함수.
    - 어디서? index.html에서

```jsx
const container = document.getElementById('root');
const root = ReactDOM.createRoot(container);
root.render(<p>Hello</p>);
```

```jsx
<body>
  <div id="root"></div>
</body>
```

- 결과는 <div id=”root”> 요소에 표시됨.

### HTML 코드

JSX 문법을 사용해서 HTML 코드를 포함하는 변수를 만들어 root 노드에 표시함.

```jsx
const myelement = (
  <table>
    <tr>
      <th>Name</th>
    </tr>
    <tr>
      <td>John</td>
    </tr>
    <tr>
      <td>Elsa</td>
    </tr>
  </table>
);

const container = document.getElementById('root');
const root = ReactDOM.createRoot(container);
root.render(myelement);
```

### root node

- 결과를 표시하려는 HTML 요소

---

## JSX란 무엇인가?

- JavaScript XML
- 리액트에서 HTML을 작성할 수 있고, 이 과정이 더 쉬워짐.

**1) createElement나 appendChild()없이도 JavaScript안에 HTML코드를 추가할 수 있음.**

```jsx
const myElement = <h1>I Love JSX!</h1>;

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
```


**2) 표현식을 중괄호{}안에 작성할 수 있음.**

```jsx
const myElement = <h1>React is {5 + 5} times better with JSX</h1>;
```

**3) 여러줄로 HTML을 작성할 때는 괄호안에 넣음.**

```jsx
const myElement = (
  <ul>
    <li>Apples</li>
    <li>Bananas</li>
    <li>Cherries</li>
  </ul>
);
```

**4) HTML은 하나의 최상위 요소로 묶여야 함.**

예를 들어 두개의 문단을 작성하려면 두 문단을 부모 요소안에 넣어야 함.

```jsx
const myElement = (
  <div>
    <p>I am a paragraph.</p>
    <p>I am a paragraph too.</p>
  </div>
);
```

- 이때 fragment를 사용해서 여러 줄을 묶을 수 있음.
    - 이는 <></>같이 생김.
    
    ```jsx
    const myElement = (
      <>
        <p>I am a paragraph.</p>
        <p>I am a paragraph too.</p>
      </>
    );
    ```
    

**5) 요소는 닫혀야 한다.**

JSX는 XML 규칙을 따르기 때문에 HTML 요소는 적절하게 닫혀야 함.

**6) 속성 class = className을 사용함.**

JSX에서는 렌더링될때 className 속성을 class 속성으로 변환함.

```jsx
const myElement = <h1 className="myclass">Hello World</h1>;
```

참고사이트

[W3Schools.com](https://www.w3schools.com/react/react_jsx.asp)