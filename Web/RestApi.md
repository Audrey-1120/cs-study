# REST Api

> HTTP 의 장점을 활용한 아키텍쳐.  
→ HTTP URL을 통해 자원(Resource)을 명시하고 HTTP Method(GET, POST, PUT, DELETE)를 통해서 해당 자원(URL)에 대한 CRUD(Create, Read, Update, Delete)를 적용함.
> 

### REST의 요소

---

- method

| Method | 의미 | Idempotent |
| --- | --- | --- |
| POST | Create | No |
| GET | Select | Yes |
| PUT | Update | Yes |
| DELETE | Delete | Yes |

+idempotent : 한 번 수행하냐, 여러 번 수행했을 때 동일한 결과가 나오나?

- Resource
    - http://momo.com/meetings 와 같은 URI
    - 모든 것을 Resource(명사)로 표현하고, 세부 Resource에는 id를 붙임

- Message
    - 메시지 포맷 : JSON, XML과 같은 형태가 있음
    
    (+메시지포맷이란?  ‘응답메세지’, ‘요청메세지’로 나뉘는 클라이언트-서버간 통신에 필요한 메시지 구조. 이 포맷내에서 REST Api의 여러 요소 등이 사용되는 것)
    

### REST 특징

---

- **Uniform Interface**
    - HTTP 표준만 맞는다면, 다른 요소들에 종속되지 않는 Interface
    
       → 플랫폼 등 특정 언어나 기술에 종속되지 않고 사용가능 한 Loosely Coupling
    
    - Self-Descirptive Messages
    
          : API 메세지만 보고, API를 이해할 수 있는 구조
    
        → Method, Resource를 이용해 무슨 행위를 하는지 직관적으로 이해할 수                       있음
    
- **Statelessness(상태 비유지)**
    - HTTP Session 과 같은 컨텍스트 저장소에 상태정보 저장 안함
    - Requset만 Message로 처리하면 되고, 컨텍스트 정보를 신경쓰지 않아도 되므로, 구현이 단순해짐
    
    → 즉 각 요청이 독립적으로 처리되게 하는 원칙이다. 서버는 클라이언트의 상태를 추적하지 않으며, 따라서 클라이언트의 요청에는 필요로하는 모든 정보가 담겨 있어야 한다(←서버가 추적을 안해서 모르니까!).  서버가 각 요청을 개별적으로 처리할 수 있게되어 구현이 단순해진다. 반면, **stateful(상태 유지)** 같은 경우는 주로 세션등을 통해 클라이언트를 추적해 정보를 얻는다. 로그인 유지 등이 대표적인 에! statelessness 와 stateful 둘 중 하나가 단독으로 쓰이는 게 아니라 이 둘이 조화되어 쓰인다.
    
- Resourece 지향 아키텍쳐(Roa)

+Roa란? 시스템의 데이터를 자원(Resource)으로 간주하고, 각 자원에 고유한 URI를 부여하여 접근하는 방식. PUT :  Momo.com/meetings/akg45 ← 아마도 식별번호 45번 모임(=데이터)을 수정하는 것이리라고 예측할 수 있다. 

Q. 다음 주 REST Api 의 메소드가 아닌것은? 

1. Connect
2. Get
3. Post
4. Put
5. Delete

+추가문제! 그렇다면 그건 어디의 무엇하는 Method 였을까요?