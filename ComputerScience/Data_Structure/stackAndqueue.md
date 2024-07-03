# 스택 & 큐

## 스택(Stack)

한 방향에서만 입력과 출력이 가능하다.

(즉 들어간 쪽으로만 나올 수 있다 → LIFO(Last In First Out, 후입선출)

-함수의 콜스택, 문자열 역순 출력, 연산자 후위표기법 등에서 사용

push() : 데이터 넣음

pop() : 데이터 최상위 값 뻄

isEmpty() : 비어있는지 확인

isFull : 꽉차있는지 확인

+이제 깃허브에서 stash pop 이 무슨 뜻이었는지 알 수 있다

sp : push 와 pop의 경우 해당 위치를 알고있어야하므로 sp(스택포인터)가 필요함. sp는 다음 값이 들어갈 위치를 가리키고 있다(기본값 -1)

```c
//pop와 push의 sp사용

public void push(Object o) {
    if(isFull(o)) {
        return;
    }
    
    stack[++sp] = o;
}

public Object pop() {
    
    if(isEmpty(sp)) {
        return null;
    }
    
    Object o = stack[sp--];
    return o;
    
}
```

```c
//isEmpty 와 isFull
private boolean isEmpty(int cnt) {
    return sp == -1 ? true : false;
}

// isFull의 경우 MAX_SIZE 사용
private boolean isFull(int cnt) {
    return sp + 1 == MAX_SIZE ? true : false;
}
```

## 동적배열스택

위와 같은 경우 MAX_SIZE 라는 최대크기가 존재하게 된다.(isFull의 사용)

최대 크기가 없는 스택은 어떻게 만들 수 있는가?

1. arraycopy를 활용한 동적배열 사용(임시배열을 만들어 확장시 복사)
2. 연결리스트를 사용

## 큐(Queue)

입력과 출력을 한 쪽 끝(front, rear)으로 제한

(한쪽으로만 들어가고 다른 한쪽으로만 나간다 → FIFO(First In First out, 선입선출))

-버퍼, BFS

큐의 가장 첫 원소를 front, 

큐의 가장 끝 원소를 rear 이라고 함.

들어올 떄는 rear로 들어오고, 나갈 때는 front 부터 빠지는 특성.

접근은 front와 rear로만 가능하다.

enQueue() : 데이터 넣음

deQueue() : 데이터 뺌

isEmpty() : 비어있는지 확인

isFull() : 꽉차있는지 확인

stack 과 마찬가지로 sp역할(데이터 입출력시 해당 값의 위치 기억)을 하는게 필요한 데,

front(deQueue 할 위치 기억) 와 rear(enQueue 할 위치 기억) 이 그 역할을 한다.

```c
public void enQueue(Object o) {
    
    if(isFull()) {
        return;
    }
    
    queue[++rear] = o;
}
```

```c
public Object deQueue(Object o) {
    
    if(isEmpty()) { 
        return null;
    }
    
    Object o = queue[front];
    queue[front++] = null;
    return o;
}
```

**원형 큐**

:  큐 빈 메모리가 남았더라고, rear 가 끝에 도달한다면 꽉 차있는 것으로 판단할 수 있음. 이를 개선한 것이 ‘원형 큐’. 논리적으로 배열의 처음과 끝이 연결되어 있는 것으로 간주 함

→ 원형 큐는 초기 공백 상태일 때 front와 rear가 0 이며, 공백/포화 상태를 쉽게 구분하기 위해 자리 하나를 항상 비워놓는다. 메모리 공간은 잘 활용한다는 장점이 있지만, 배열로 구현되어 있어 큐의 크기가 제한된다는 단점이 있다. 이를 개선한 것이 ‘연결리스트 큐’이다.

**연결리스트 큐**

: 크기가 제한이 없고 삽입, 삭제가 편리하다.

→ 데이터 입력은 끝 부분인 tail에 한다. 기존의 tail은 보관하고 새로운 tail을 생성해나가는 방식. 큐가 비었으면 head = tail을 통헤 둘이 같은 노드를 가리키도록 한다. 큐가 비어있지 않다면, 기존 tail의 next에 새로만든 tail을 설정한다.

데이터 출력은 head로부터 꺼낸다.(FIFO니까!) head의 데이터를 미리 저장해두고, 기존의 head를 그 다음 노드의 head로 설정한다. 저장해둔 데이터를 return 해서 값을 빼온다. 

이처럼 삽입은 tail, 제거는 head로 하면서 삽입/삭제를 스택처럼 O(1)에 가능하도록 구현이 가능하다.


Q. 스택은 oo선출이고 큐는 xx선출이다. oo와 xx에 들어갈 알맞은 단어는?
