## React란?

Meta에서 제공하는 node.js 기반의 javascript 라이브러리이다.

가상 DOM이라는 개념을 사용하여, SPA 구현에 강력한 기능을 제공한다.

이 가상 DOM(virtual dom)을 통해 변경 전 상태와 변경 후 상태를 비교한 뒤 바뀐 부분이 있다면 그 구분만 다시 렌더링한다. 또한, 컴포넌트 단위로 개발이 이루어지기 때문에 재사용성이 높다.

(렌더링이란? HTML을 우리가 아는 웹사이트의 모습으로 만들어 화면(브라우저)에 뿌려주는 것.

작성된 HTML이 문법에 따라 화면에 적용시켜 주는 것이 렌더링이다. 

보통 브라우저 엔진에는 2개의 엔진이 도는데, 바로 이 렌더링 엔진과 자바스크립트 엔진이다.)

개념은 일단 위와 같음. 실제로는 언제, 어떻게 쓰이는 것인지?

→ 강의시간에 비동기통신을 통해 SPA를 구현할때 보다 편리하게 화면을 구성하기 위해 REACT를 사용한다고 했음. 그렇다면 비동기통신을 사용할때 쓰이는 기술인데, 어떻게 쓰이는 것인가? 응답을 받와야 화면을 구성할때 사용한다!

## React의 주요 특징 3가지

1. 선언적 (↔ 명령적)
2. 컴포넌트 기반
3. 범용적

그렇다면 데이터 값은 어떻게 전달하는가? props을 통해 컴포넌트에 전달한다.

```jsx
function Video({ video }) {
  return (
    <div>
      <Thumbnail video={video} />
      <a href={video.url}>
        <h3>{video.title}</h3>
        <p>{video.description}</p>
      </a>
      <LikeButton video={video} />
    </div>
  );
}
```

React 공식 홈페이지에 가면 첫화면에 나오는 예시 코드이다.

props는 부모 컴포넌트로부터 자식 컴포넌트로 데이터를 전달해주는 역할을 한다.

## 구조분해할당(비구조화할당)

props 에 대해 찾아보면 비구조화할당/구조분해할당에 대해 계속 언급된다.

그렇다면 구조분해할당(비구조화할당)이란?

→ES6부터 사용되는 새로운 자바스크립트 표현식. 좌항에는 변수 우항에는 할당값을 넣어 이전보다 간편하게 객체나 데이터를 정의할 수 있게 되었다.

```jsx
const picture = {
  color: 'greybrown',
  price: 10
};

const { color, price } = picture;
```

이런식으로 정의해서 console.log(color)로 데이터를 뽑아볼 수 있다.

(원래 했던 방식은 concole.log(picture.color))






+이 분의 글이 많은 참고가 되었음!

[https://velog.io/@winterlood/React가-처음인-당신-Ep1.-탄생편](https://velog.io/@winterlood/React%EA%B0%80-%EC%B2%98%EC%9D%8C%EC%9D%B8-%EB%8B%B9%EC%8B%A0-Ep1.-%ED%83%84%EC%83%9D%ED%8E%B8)
