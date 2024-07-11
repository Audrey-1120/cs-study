# Index

### DB Index

#### 1. 목적

> RDBMS에서 검색 속도를 높이기 위한 기술

table의 **column을 색인화**한다.  
-> 모든 record를 scan하는 것이 아닌, B+ Tree(Balance Search Tree) 구조로 색인화된 index 파일 검색으로 검색 속도가 향상된다.

<br>

#### 2. 과정

> table을 생성하면, MYD, MYI, FRM 3개의 파일이 생성됨.

- FRM : 테이블 구조가 저장되어 있는 파일
- MYD : 실제 데이터가 있는 파일
- MYI : index 정보가 들어가 있는 파일

index를 사용하지 않는 경우, MYI 파일은 비어져 있다. 그러나 index한 경우, MYI 파일이 생성된다.  
-> 이후에 사용자가 SELECT 쿼리로 index를 사용하는 column을 탐색 시, MYI 파일의 내용을 검색한다.

<br>

#### 3. 단점
- index 생성 시, .mdb 파일 크기가 증가한다.
- 한 페이지를 동시네 수정할 수 있는 병행성이 줄어든다.
- index된 필드에서 데이터를 업데이트하거나, 레코드를 추가 또는 삭제 시 성능이 떨어진다.
- 데이터 변경 작업이 자주 일어나는 경우, index를 재작성해야 하므로, 성능에 영향을 미친다.

#### 4. index 사용 Good? Bad?

- #### 사용하면 좋은 경우
    - WHERE 절에서 자주 사용되는 칼럼
    - 외래키가 사용되는 칼럼
    - JOIN에 자주 사용되는 칼럼

- #### 사용을 피해야 하는 경우
    - 데이터 중복도가 높은 칼럼
    - DML이 자주 일어나는 칼럼

#### 5. DML이 일어났을 때의 상황

- #### INSERT
    기존 block에 여유가 없을 때, 새로운 데이터가 입력된다.  
    -> 새로운 block을 할당 받은 후, 키를 옮기는 작업을 수행한다. (**많은 양의 Redo가 기록**, 유발)  
    -> index split 작업 동안, 해당 block의 키 값에 대해서 DML이 블로킹 된다. (**대기 이벤트 발생**)

- #### DELETE
    [ table과 index 상황 비교 ]  
    table에서 데이터가 DELETE 되는 경우 : 데이터가 지워지고, 다른 데이터가 그 공간을 사용 가능  
    index에서 데이터가 DELETE 되는 경우 : 데이터가 지워지지 않고, 사용 안 됨 표시만 해둔다.  
    -> **table의 데이터 수와 index의 데이터 수가 다를 수 있다.**

- #### UPDATE
    table에서 UPDATE가 발생하면, index는 UPDATE 할 수 없다.  
    index에서는 **DELETE가 발생한 후, 새로운 작업의 INSERT 작업** -> 2배의 작업이 소요되어 힘들다.

<br>

#### 문제
index 사용하면 좋은 경우가 아닌 것은?
    
    1) WHERE 절에서 자주 사용되는 칼럼   
    2) DML이 자주 일어나는 칼럼   
    3) 외래키가 사용되는 칼럼  
    4) JOIN에 자주 사용되는 칼럼

<br>

##### [참고]
[DB Index란?](<https://lalwr.blogspot.com/2016/02/db-index.html>)
