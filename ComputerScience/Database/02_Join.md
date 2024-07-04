# JOIN
> 두 개 이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법

테이블을 연결하려면, 적어도 하나의 칼럼을 서로 공유하고 있어야 하므로 이를 이용하여 데이터 검색에 활용한다.  
(<u>조회할 때 필요한 칼럼</u>이 2개 이상의 테이블에 존재할 때 조인을 사용한다.)

조인 조건을 이용해서 각 테이블을 조인한다.

<br>

## JOIN 종류

- INNER JOIN : 조회할 테이블에 모두 존재하는 데이터를 대상으로 조인
- OUTER JOIN : 어느 한 테이블에만 존재하는 데이터를 조회 대상에 포함

<br>

- ### INNER JOIN (내부 조인)

    <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile9.uf.tistory.com%2Fimage%2F99799F3E5A8148D7036659">

    > 교집합으로, 기준 테이블과 join 테이블의 중복된 값을 보여준다.

    - 조인하는 두 테이블에 모두 존재하는 데이터만 조회된다.
    - 어느 한 테이블에만 존재하는 데이터는 조회되지 않는다.

    ```sql
    -- ANSI 문법
    SELECT 조회할 칼럼, ...
      FROM 테이블1 INNER JOIN 테이블2
        ON 조인조건
    ```
    ```sql
    SELECT A.NAME, B.AGE
      FROM EX_TABLE A INNER JOIN JOIN_TABLE B
        ON A.NO_EMP = B.NO_EMP
    ```

<br>

- ### OUTER JOIN (외부 조인)
    > 어느 한 테이블에만 존재하는 데이터는 조회된다.
  
    - ### LEFT OUTER JOIN

        <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile6.uf.tistory.com%2Fimage%2F997E7F415A81490507F027">

        > 왼쪽 테이블 기준으로 JOIN 한다.

        ```sql
        -- ANSI 문법
        SELECT 조회할 칼럼, ...
        FROM 테이블1 LEFT OUTER JOIN 테이블2
            ON 조인조건
        ```
        ```sql
        SELECT A.NAME, B.AGE
        FROM EX_TABLE A LEFT OUTER JOIN JOIN_TABLE B
            ON A.NO_EMP = B.NO_EMP
        ```

    <br>

    - ### RIGHT OUTER JOIN

        <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F9984CE355A8149180ABD1D">

        > 오른쪽 테이블 기준으로 JOIN 한다.

        ```sql
        -- ANSI 문법
        SELECT 조회할 칼럼, ...
        FROM 테이블1 RIGHT OUTER JOIN 테이블2
        ON 조인조건
        ```
        ```sql
        SELECT A.NAME, B.AGE
        FROM EX_TABLE A RIGHT OUTER JOIN JOIN_TABLE B
        ON A.NO_EMP = B.NO_EMP
        ```

    <br>

    - ### FULL OUTER JOIN

        <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile24.uf.tistory.com%2Fimage%2F99195F345A8149391BE0C3">

        > 합집합을 말한다.  
        > A와 B 테이블의 모든 데이터가 검색된다.  
        -> 기준 테이블의 의미가 없다.

        ```sql
        SELECT A.NAME, B.AGE
          FROM EX_TABLE A FULL OUTER JOIN JOIN_TABLE B
            ON A.NO_EMP = B.NO_EMP
        ```

<br>

- ### CROSS JOIN

    <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile10.uf.tistory.com%2Fimage%2F993F4E445A8A2D281AC66B">

    > 모든 경우의 수를 전부 표현해주는 방식  
    > 기준 테이블이 A이면, A 테이블 데이터 중 한 ROW를 B 테이블 데이터 전체와 JOIN 하는 방식  
    -> A 테이블 데이터가 3개, B 테이블 데이터가 4개면 총 3 * 4 = 12개의 데이터가 검색된다.

    ```sql
    SELECT A.NAME, B.AGE
      FROM EX_TABLE A CROSS JOIN JOIN_TABLE B

    SELECT A.NAME, B.AGE
      FROM EX_TABLE A, JOIN_TABLE B
    ```
<br>

- ### SELF JOIN

    <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F99341D335A8A363D0614E8">

    > 자기 자신과 자기 자신을 조인하는 것  
    -> 하나의 테이블을 여러 번 복사해서 조인한다고 생각하면 편하다.<br><br>
    > 자신이 갖고 있는 칼럼을 다양하게 변형시켜 활용할 때 자주 사용한다.

    ```sql
    SELECT A.NAME, B.AGE
      FROM EX_TABLE A, EX_TABLE B
    ```

<br>

#### 문제
기준 테이블과 join 테이블의 중복된 값을 보여주는 JOIN은 어떤 JOIN인가?
    
    1) OUTER JOIN   2) INNER JOIN   3) CROSS JOIN   4) SELF JOIN

