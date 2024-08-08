# PCB & Context Switching

### Process Management

> CPU가 여러 개의 프로세스로 구성되어 있을 때, CPU 스케쥴링을 통해 관리하는 것

CPU가 각 프로세스에 대해 알아야 관리가 가능하다.

프로세스 특징을 가지고 있는 것이 **Process Metadata**이다.

#### Process Metadata

- Process ID
- Process State
- Process Priority
- CPU Registers
- Owner
- CPU Usage
- Memory Usage

Process Metadata는 프로세스가 생성되면 **PCB**에 저장된다.

<br>

### PCB (Process Control Block)

> 프로세스 메타데이터들을 저장해놓는 곳  
> 한 PCB 안에는 한 프로세스의 정보가 저장된다.

- 운영체제가 프로세스 스케쥴링을 위해 프로세스에 관한 모든 정보를 가지고 있는 데이터베이스

![](https://images.velog.io/images/klloo/post/5562a831-dc1e-4e95-b590-25cef88bd43e/image.png)

```
프로그램 실행 -> 프로세스 생성 -> 프로세스 주소 공간에 코드, 데이터, 스택 생성 -> 이 프로세스의 메타데이터들이 PCB에 저장
```

#### PCB가 필요한 이유

CPU에서는 interrupt가 발생해서 할당받은 프로세스가 대기 상태가 되고 다른 프로세스를 실행시킬 때 교체 작업이 이루어지는데, **앞으로 다시 수행할 대기 중인 프로세스에 관한 저장 값을 PCB에 저장**한다.

#### PCB 관리 방법

![](https://velog.velcdn.com/images/nnnyeong/post/55aa277d-f6b4-49af-acc2-3cc8494fd8ae/image.png)

운영체제는 빠르게 PCB에 접근하기 위해서 **프로세스 테이블**을 사용해 각 프로세스의 PCB를 관리하고, PCB는 **연결 리스트 방식**으로 관리된다.   프로세스가 생성되면 해당 PCB가 생성되고, 프로세스가 완료되면 제거된다.

여기서 수행 중인 프로세스를 변경할 때, CPU의 레지스터 정보가 변경되는 것을 **Context Switching**이라고 한다.

<br>

### Context Switching (문맥 교환)

> CPU가 이전의 프로세스 상태를 PCB에 보관하고 또 다른 프로세스의 정보를 PCB에 읽어 레지스터에 적재하는 과정

#### Context

- CPU가 프로세스를 실행시키기 위해 필요한 정보들 (프로세스의 데이터, CPU 레지스터 값)

- 프로세스가 메모리에 올라가서 실행될 때, CPU 내에 존재하는 레지스터들이 현재 실행 중인 프로세스 관련 데이터로 채워지게 되고 실행 중인 프로세스가 변경되면 CPU 내의 레지스터 값들이 변경된다.

#### 과정

![](https://velog.velcdn.com/images/nnnyeong/post/41a70967-180a-4394-a2c8-d8ebf342bb69/image.png)

- 1. 요청 발생

    - interrupt나 trap에 의해서 context를 바꿔야 한다는 요청이 발생한다.

- 2. PCB에 프로세스 정보 저장

    - 기존에 실행 중이던 프로세스 `P0`와 관련된 정보들을 PCB에 저장한다.

- 3. CPU 새롭게 할당

    - 운영체제는 새롭게 실행할 프로세스 `P1`에 대한 정보를 해당 PCB에서 가져와 CPU 레지스터에 적재한다.

#### Context Switching이 발생하는 경우

- 멀티태스킹

    - 실행 가능한 프로세스들이 운영체제의 스케쥴러에 의해 조금씩 번갈아가며 수행되는 것
    - 프로세스가 번갈아가며 CPU를 할당 받을 때 문맥교환이 이루어진다.

- 인터럽트 핸들링

    - 인터럽트가 발생하면 문맥 교환이 이루어진다.

- 사용자와 커널모드 전환

    - 필수는 아니지만 운영체제에 따라 발생할 수 있다.

#### overhead

> context switching에 소요되는 시간과 메모리

- context switching이 발생하면 시간과 메모리가 소요되기 때문에 **잦은 context switching은 성능 저하를 갖게 된다.**

- 프로세스 작업 중 오버 헤드를 감수해야 하는 상황

    - 프로세스를 수행하다가 입출력 이벤트가 발생해서 대기 상태로 전환시킨다. 이때, CPU를 그냥 놀게 두는 것보다 다른 프로세스를 수행시키는 것이 효율적이다.

- 그래서 CPU에 계속 프로세스를 수행시키도록 하기 위해 다른 프로세스를 실행시키고 context switching하는 것이다.

    - CPU가 놀지 않고, 사용자에게 빠른 일처리를 제공할 수 있다.

<br>

#### 문제
PCB가 필요한 이유는 CPU에서는 ⓐ가 발생해서 할당받은 프로세스가 대기 상태가 되고 다른 프로세스를 실행시킬 때 ⓑ 작업이 이루어지는데, **앞으로 다시 수행할 대기 중인 프로세스에 관한 저장 값**을 저장하기 위해서이다.

<br>

##### [참고]
[PCB와 Context Switching](<https://velog.io/@klloo/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-PCB%EC%99%80-Context-Switching>)

[Context Switching, PCB](<https://velog.io/@nnnyeong/OS-Context-Switching-PCB-Process-Control-Block>)
