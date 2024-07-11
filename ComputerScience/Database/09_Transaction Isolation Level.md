# 트랜잭션 격리 수준 (Transaction Isolation Level)

### Isolation Level
여러 트랜잭션이 동시에 처리될 때, 특정 트랜잭션이 다른 트랜잭션에서 변경하거나 조회하는 데이터를 볼 수 있게 허용할지 여부를 결정하는 것

### Isolation Level 필요성

데이터베이스는 ACID 특징과 같이 트랜잭션이 독립적인 수행을 하도록 한다.  
(ACID : 데이터베이스 트랜잭션이 안전하게 수행된다는 것을 보장하기 위한 성질)  

따라서 무조건 locking으로 동시에 수행되는 수많은 트랜잭션들을 순서대로 처리하는 방식으로 구현하게 되면 데이터베이스의 성능은 떨어지게 될 것이다.  
그렇다고 해서, 성능을 높이기 위해 locking의 범위를 줄인다면, 잘못된 값이 처리될 문제가 발생하게 된다.  
-> 따라서 최대한 효율적인 locking 방법이 필요하다

### Isolation Level 종류
```
격리(고립) 수준이 낮음 - 레벨 0

shared lock : 읽기 잠금, 공유락
```

#### 1. Read Uncommitted (레벨 0)

> SELECT 문장이 수행되는 동안 해당 데이터에 shared lock이 걸리지 않는 계층

트랜잭션에 처리 중이거나, 아직 commit 되지 않은 데이터를 다른 트랜잭션이 읽는 것을 허용한다.

```
사용자 1이 데이터 A를 데이터 B로 변경하는 동안 사용자 2는 아직 완료되지 않은(uncommitted) 트랜잭션이지만 데이터 B를 읽을 수 있다.
```
데이터베이스의 일관성을 유지하는 것이 불가능하다.

#### 2. Read Committed (레벨 1)

> SELECT 문장이 수행되는 동안 해당 데이터에 shared lock이 걸리는 계층

트랜잭션이 수행되는 동안 다른 트랜잭션이 접근할 수 없어 대기하게 된다.  
commit 이 이루어진 트랜잭션만 조회 가능하다.  
대부분 SQL 서버가 default로 사용하는 Isolation Level이다.

```
사용자 1이 데이터 A를 데이터 B로 변경하는 동안 사용자 2는 해당 데이터에 접근이 불가능하다.
```

#### 3. Repeatable Read (레벨 2)

> 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 shared lock이 걸리는 계층

트랜잭션이 범위 내에서 조회한 데이터 내용이 항상 동일함을 보장한다.  
다른 사용자는 트랜잭션 영역에 해당되는 데이터에 대한 수정 불가능하다.  
MySQL에서 default로 사용하는 Isolation Level이다.

#### 4. Serializable (레벨 3)

> 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 shared lock이 걸리는 계층

완벽한 읽기 일관성 모드를 제공한다.  
다른 사용자는 트랜잭션 영역에 해당되는 데이터에 대한 수정 및 입력 불가능하다.

<br>

### 선택 시 고려사항

Isolation Level에 대한 조정은, 동시성과 데이터 무결성에 연관되어 있다.  
동시성을 증가시키면 데이터 무결성에 문제가 발생하고, 데이터 무결성을 유지하면 동시성이 떨어지게 된다.  
level을 높게 조정할수록 발생하는 비용이 증가한다.

<br>

### 낮은 단계 Isolation Level을 활용할 때 발생하는 현상들

- Dirty Read  
    - commit되지 않은 수정 중인 데이터를 다른 트랜잭션에서 읽을 수 있도록 허용할 때 발생하는 현상  
    - 어떤 트랜잭션에서 아직 실행이 끝나지 않은 다른 트랜잭션에 의한 변경사항을 보게 되는 경우  
    - 발생 Level : Read Uncommitted

- Non-Repeatable Read
    - 한 트랜잭션에서 같은 쿼리를 두 번 수행할 때 그 사이에 다른 트랜잭션 값을 수정 또는 삭제하면서 두 쿼리의 결과가 상이하게 나타나는 일관성이 깨진 현상
    - 발생 Level : Read Committed, Read Uncommitted

- Phantom Read
    - 한 트랜잭션 안에서 일정 범위의 레코드를 두 번 이상 읽었을 때, 첫 번째 쿼리에서 없던 레코드가 두 번째 쿼리에서 나타나는 현상
    - 트랜잭션 도중 새로운 레코드 삽입을 허용하기 때문에 나타나는 현상이다.
    - 발생 Level : Repeatable Read, Read Committed, Read Uncommitted

<br>

#### 문제
한 트랜잭션에서 같은 쿼리를 두 번 수행할 때 그 사이에 다른 트랜잭션 값을 수정 또는 삭제하면서 두 쿼리의 결과가 상이하게 나타나는 일관성이 깨진 현상이 나타나는 level을 모두 고르시오.
    
    1) Read Committed   2) Repeatable Read   3) Read Uncommitted

<br>

##### [참고]
[트랜잭션의 격리 수준(Isolation Level)에 대해 쉽고 완벽하게 이해하기](<https://mangkyu.tistory.com/299>)


