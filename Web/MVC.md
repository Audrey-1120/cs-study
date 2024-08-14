## MVC 진행과정

1. 클라이언트가 url을 요청하면, 브라우저에서 스프링으로 request가 전송
2. Dispatcher Servlet이 request를 받으면, Handeler Mapping 을 통해 해당 url을 담당하는  Controller를 탐색 후 찾아냄
3. 찾아낸 Controller 로 request를 보내주고, 보내주기 위해 필요한 Model을 구성함
4. Model에서는 페이지 처리에 필요한 정보들을 DB에 접근하여 쿼리문을 통해 가져옴
5. 데이터를 통해 얻은 Model 정보를 Controller에게 response 해주면, Controller는 이를 받아 Model을 완성시켜 Dispatcher Servlet에게 전달
6. Dispatcher Servlet은 View Resolver를 통해 request에 해당하는 view 파일을 탐색 후 받아냄
7. 받아낸 View 페이지 파일에 Model을 보낸 후 클라이언트에게 보낼 페이지를 완성시켜 받아냄
8. 완성된 View 파일을 클라이언트에 response하여 화면에 출력

## 구성요소

```
 **Dispatcher Servlet**
 
 모든 request를 처리하는 중심 컨트롤러라고 볼 수 있다. Servlet Container에서 HTTP 프로토콜을 
 통해 들어오는 모든 request에 대해 제일 앞단에서 중앙집중식으로 처리해주는 핵심적인 역할.
 기존에는 web.xml에 모두 등록해야 했지만, Dispatcher Servlet이 모든 request를 핸들링하면서
 작업을 편리하게 할 수 있다.
```

```
**Handler Mapping**

클라이언트의 request url을 어떤 컨트롤러가 처리해야 할 지 찾아서 Dispatcher Servlet에게
전달해주는 역할을 담당
(@RequestMapping 이거를 이 핸들러가 찾아준다)
```

```
**Controller**

실질적인 요청을 처리한다. Dispatcher Servlet이 프론트 컨트롤러라면, 
Controller는 백엔드 컨트롤러라고 볼 수 있다.
모델의 처리결과를 담아 Dispatcher Servlet에게 반환해준다.
```

```
**View Resolver**

컨트롤러의 처리 결과를 만들 view를 결정해주는 역할을 담당한다.
```