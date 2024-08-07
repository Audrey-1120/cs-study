# Anomaly

> 정규화를 해야하는 이유
-> 잘못된 테이블 설계로 인해 Anomaly (이상 현상)가 나타나기 때문이다.

<br>

| 학번 | 이름 | 나이 | 성별 | 강의코드 | 강의명 | 전화번호 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| 1011 | 이태호 | 23 | 남 | AC1 | 데이터베이스 개론 | 010-2627-8123 |
| 1012 | 강민정 | 20 | 여 | AC2 | 운영체제 | 010-4665-1941 |
| 1013 | 김현수 | 21 | 남 | AC3 | 자료구조 | 010-5223-4464 |
| 1013 | 김현수 | 21 | 남 | AC4 | 웹 프로그래밍 | 010-5223-4464 |
| 1014 | 이병철 | 26 | 남 | AC5 | 알고리즘 | 010-6305-2912 |

<br>

### 1. 삽입 이상

> 자료를 삽입할 때 의도하지 않은 자료까지 삽입해야만 자료를 테이블에 추가가 가능한 현상

강의를 아직 수강하지 않은 새로운 학생을 삽입할 경우 강의 코드와 강의명 속성에는 null값이 들어가야 하는 문제가 생긴다.  
-> 굳이 삽입을 위해서는 '미수강'에 관련된 강의코드를 만들어야 한다.

<br>

### 2. 갱신 이상

> 중복된 데이터 중 일부만 수정되어 데이터 모순이 일어나는 현상

강의 코드가 'AC3'인 김현수의 전화번호를 수정할 경우, 3번째 튜플의 데이터만 수정된다.  
그러면 3, 4번째 튜플은 같은 사용자의 데이터임에도 불구하고 전화번호가 다르게 된다.

<br>

### 3. 삭제 이상

> 어떤 정보를 삭제하면, 의도하지 않은 다른 정보까지 삭제되어버리는 현상

강의코드가 "AC1"인 데이터베이스 개론 강의를 삭제하게 되면, 이태호 학생의 데이터까지 삭제되어버린다.

<br>

#### 문제
중복된 데이터 중 일부만 수정되어 데이터 모순이 일어나는 현상은 이상 현상(Anomaly) 중 어떤 이상인가?
    
    1) 갱신 이상   2) 삭제 이상   3) 삽입 이상

<br>

##### [참고]
[이상 현상(Anomaly)이란?](<https://dev-coco.tistory.com/63>)
