# System call

> 운영체제는 **커널**과 **인터페이스**로 구성되어 있다.

### 커널

- 운영체제의 핵심적인 기능을 모아놓은 것

- 자동차가 운영체제라면 **엔진**이 커널에 해당된다.

    - 세단, 스포츠카, SUV 등 자동차 종류가 다양하듯이 운영체제 종류도 다양하지만 성능을 결정하는 것은 커널이다.

- 컴퓨터 전원을 켜면 운영체제는 동시에 수행된다.

- 운영체제 중 항상 필요한 부분만 전원이 켜짐과 동시에 메모리에 올려놓고, 나머지 부분은 필요할 때 메모리에 올려서 사용하게 되는데,  
이때 **메모리에 상주하는 운영체제 부분**을 커널이라고 한다.

- 프로세스 관리 / 메모리 관리 / 파일 시스템 관리 / 입출력 관리 / 프로세스 간 통신 관리

<br>

### 인터페이스

- 커널에 사용자의 명령을 전달하고 실행 결과를 사용자에게 알려주는 역할

- 자동차의 핸들, 브레이크, 계기판 등이 인터페이스에 해당된다.

- 운영체제는 커널과 인터페이스로 분리되어, 같은 커널이어도 다른 인터페이스 형태로 제작 가능하다.

    - 이렇게 다른 인터페이스로 장착되면 사용자에게 다른 운영체제로 보인다.

<br>

### 시스템 콜

- 운영체제는 다양한 서비스들을 수행하기 위해 하드웨어를 직접적으로 관리한다.

- 반면에 응용 프로그램은 운영체제가 제공하는 인터페이스를 통해서만 자원을 사용할 수 있다.

- 여기서 **운영체제가 제공하는 이러한 인터페이스**를 **시스템 콜**이라고 한다.

- 커널 영역의 기능을 사용자 모드가 가용 가능하도록, 프로세스가 하드웨어에 직접 접근해서 필요한 기능을 할 수 있도록 해준다.

    - 즉, 응용 프로그램이 시스템 콜을 사용해서 원하는 기능을 수행할 수 있다.

### 시스템 콜 종류

<details>
<summary>1. 프로세스 제어 (Process Control)</summary>
<div markdown="1">
- 끝내기 (exit), 중지 (abort)
</div>
<div markdown="1">
- 적재 (load), 실행 (execute)
</div>
<div markdown="1">
- 프로세스 생성 (create process) - fork
</div>
<div markdown="1">
- 프로세스 생성 획득과 속성 설정
</div>
<div markdown="1">
- 시간 대기 (wait time)
</div>
<div markdown="1">
- 사건 대기 (wait event)
</div>
<div markdown="1">
- 사건을 알림 (signal event)
</div>
<div markdown="1">
- 메모리 할당 및 해제
</details>

<details>
<summary>2. 파일 조작 (File Manipulation)</summary>
<div markdown="1">
- 파일 생성 (create) / 삭제 (delete)
</div>
<div markdown="1">
- 열기 (open) / 닫기 (close) / 읽기 (read) / 쓰기 (write)
</div>
<div markdown="1">
- 위치 변경 (reposition)
</div>
<div markdown="1">
- 파일 속성 획득 (get file attribute) / 설정 (set file attribute)
</div>
</details>

<details>
<summary>3. 장치 관리 (Device Manipulation)</summary>
<div markdown="1">
- 하드웨어의 제어와 상태 정보를 얻음 (ioctl)
</div>
<div markdown="1">
- 장치를 요구 (request device) / 장치를 방출 (release device)
</div>
<div markdown="1">
- 읽기 (read) / 쓰기 (write) / 위치 변경
</div>
<div markdown="1">
- 장치 속성 획득 및 설정
</div>
<div markdown="1">
- 장치의 논리적 부착 및 분리
</div>
</details>

<details>
<summary>4. 정보 유지 (Information Maintenance)</summary>
<div markdown="1">
- getpid(), alarm(), sleep()
</div>
<div markdown="1">
- 시간과 날짜의 설정과 획득 (time)
</div>
<div markdown="1">
- 시스템 데이터의 설정과 획득 (date)
</div>
<div markdown="1">
- 프로세스 파일, 장치 속성의 획득 및 설정
</div>
</details>

<details>
<summary>5. 통신 (Communication)</summary>
<div markdown="1">
- pipe(), shm_open(), mmap()
</div>
<div markdown="1">
- 통신 연결의 생성, 제거
</div>
<div markdown="1">
- 메시지의 송신, 수신
</div>
<div markdown="1">
- 상태 정보 전달
</div>
<div markdown="1">
- 원격 장치의 부착 및 분리
</div>
</details>

<details>
<summary>6. 보호 (Protection)</summary>
<div markdown="1">
- chmod()
</div>
<div markdown="1">
- umask()
</div>
<div markdown="1">
- chown()
</div>
</details>

<br>

### 프로세스 생성과 제어를 위한 시스템 콜

- fork(), exec() -> 새로운 프로세스 생성과 관련

- wait() -> 프로세스(parent)가 만든 다른 프로세스(child)가 끝날 때까지 기다리는 명령어

### fork

> 새로운 프로세스를 생성할 때 사용

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid());    // pid : 29146

    int rc = fork();

    if (rc < 0) {
        exit(1);
    }                                 // (1) fork 실패
    else if (rc == 0) {                               // (2) child인 경우 (fork 값이 0)
        printf("child (pid : %d)", (int) getpid());
    }
    else {                                           // (3) parent case
        printf("parent of %d (pid : %d)", rc, (int) getpid());
    }
}
```

```
// 출력 결과

pid : 29146

parent of 29147 (pid : 29146)

child (pid : 29147)
```

> parent와 child의 순서는 non-deterministic(비결정적 : 항상 다른 결과가 나오는 것)하다.  
> scheduler가 결정한다.

#### 코드 해석

PID : 프로세스 식별자 (UNIX 시스템에서는 PID가 프로세스에게 명령할 때 사용)

fork()가 실행되는 순간, 프로세스가 하나 더 생긴다.  
이때 생긴 프로세스(child)는 fork()를 만든 프로세스(parent)와 동일한 복사본을 갖게 된다.

**이 때 운영체제는 위와 똑같은 2개의 프로그램이 동작한다고 생각**하고 **fork()가 return될 차례라고 생각**한다.

그 때문에 새로 생성된 프로세스(child)는 main에서 시작하지 않고, if문에서 시작하게 된다.

하지만 child와 parent의 fork() 값이 다르다는 차이점이 있다.  
따라서 완전 똑같은 복사본이라고 할 수 없다.

```
parent의 fork() 값 -> child의 pid 값

child의 fork() 값 -> 0
```

scheduler가 parent를 먼저 수행할지, child를 먼저 수행할지 확신할 수 없으므로

```
// 출력 결과

pid : 29146

child (pid : 29147)

parent of 29147 (pid : 29146)
```

<br>

### wait

> child 프로세스가 종료될 때까지 기다리는 작업

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid());    // pid : 29146

    int rc = fork();

    if (rc < 0) {
        exit(1);
    }                                 // (1) fork 실패
    else if (rc == 0) {                               // (2) child인 경우 (fork 값이 0)
        printf("child (pid : %d)", (int) getpid());
    }
    else {                                           // (3) parent case
        int wc = wait(NULL)
        printf("parent of %d (wc: %d / pid : %d)", wc, rc, (int) getpid());
    }
}
```

```
// 출력 결과

pid : 29146

child (pid : 29147)

parent of 29147 (wc: 29147 / pid : 29146)
```

wait()을 통해서 child의 실행이 끝날 때까지 기다려준다.  
parent가 먼저 실행되더라도, wait()은 child가 끝나기 전에는 return 하지 않기 때문에 반드시 child가 먼저 실행된다.

<br>

### exec

단순 fork()는 동일한 프로세스의 내용을 여러 번 동작할 때 사용한다.

child 에서는 parent 와 다른 동작을 하고 싶을 때 exec() 를 사용할 수 있다.

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid());    // pid : 29146

    int rc = fork();

    if (rc < 0) {
        exit(1);
    }                                 // (1) fork 실패
    else if (rc == 0) {                               // (2) child인 경우 (fork 값이 0)
        printf("child (pid : %d)", (int) getpid());
        char *myargs[3];
        myargs[0] = strdup("wc");               // 내가 실행할 파일 이름
        myargs[1] = strdup("p3.c");             // 실행할 파일에 넘겨줄 argument
        myargs[2] = NULL;                       // end of array
        execvp(myarges[0], myargs);             // wc 파일 실행
        printf("this shouldn't print out");     // 실행되지 않음
    }
    else {                                           // (3) parent case
        int wc = wait(NULL)
        printf("parent of %d (wc: %d / pid : %d)", wc, rc, (int) getpid());
    }
}
```
exec()가 실행되면, execvp( 실행 파일, 전달 인자 ) 함수는 code segment 영역에 실행 파일의 코드를 읽어와서 덮어 씌운다.

그 후에는 heap, stack, 다른 메모리 영역이 초기화되고, 운영체제는 그냥 실행한다.  
즉, 새로운 프로세스를 생성하지 않고, 현재 프로그램에 wc라는 파일을 실행한다.  
그로 인해, execvp() 이후의 부분은 실행되지 않는다.

<br>

#### 문제
시스템 콜이란 무엇인가?

<br>

##### [참고]
[운영체제, 시스템 콜](<https://brightstarit.tistory.com/13>)
