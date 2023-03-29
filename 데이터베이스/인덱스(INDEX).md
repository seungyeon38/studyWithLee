# 인덱스(INDEX)

RDBMS에서 검색 속도를 높이기 위해 사용하는 기술.  
테이블의 컬럼을 색인화(따로 파일로 저장)하여 검색시 해당 테이블의 레코드를 전부 스캔하는 것이 아니라 색인화 되어있는 인덱스 파일을 검색하여 검색 속도를 빠르게 한다.  
Tree구조를 활용하여 색인화 하며 B-Tree에서 파생된 B+Tree를 주로 사용한다.

</br>

## 목적

RDBMS의 검색 속도를 높이는 것이다.  
Select쿼리의 Where절이나 Join 예약어를 사용했을 때만 인덱스를 사용하게 되며 Select쿼리의 검색 속도를 빠르게 하는 것이 목적이다.

_Delete, Insert, Update 쿼리에는 인덱스 사용시 느려지는 경우가 많다._

</br>

## 구성

테이블을 생성 할 때 FRM, MYD, MYI 3가지 파일이 생성된다.

- FRM : 테이블 구조 저장 파일
- MYD : 실제 데이터 파일
- MYI : Index 정보 파일 (Index 사용 시 생성됨)

Select쿼리로 인덱스를 사용하는 쿼리를 작성시 Tree로 정리해 놓은 MYI파일의 내용을 검색한다.

</br>

## 장점

- 키 값을 기초로 하여 테이블에서 검색과 정렬 속도를 향상시킨다.
- 그룹화 작업의 속도를 향상시킨다.
- 인덱스를 사용하면 테이블 행의 고유성을 강화시킬 수 있다.
- 테이블의 기본 키는 자동으로 인덱스 된다.
- 여러 필드로 이루어진(다중 필드) 인덱스를 사용하면 첫 필드 값이 같은 레코드도 구분할 수 있다.

</br>

## 단점

- Index 생성시, .mdb 파일 크기가 증가한다.
- 한 페이지를 동시에 수정할 수 있는 병행성이 줄어든다.
- 인덱스 된 Field에서 Data를 업데이트하거나, Record를 추가 또는 삭제시 성능이 떨어진다.
- 인덱스를 생성하는데 시간이 많이 소요될 수 있다.
- 데이터 변경 작업이 자주 일어나는 경우, Index를 재작성해야 하므로 성능에 영향을 미친다.

다른 필드에 대한 인덱스를 만들게 되면 성능이 별로 향상되지 않을 수도 있다. 예를 들어, 테이블에 회사 이름 필드와 성 필드가 이미 인덱스 된 경우에 우편 번호 필드를 추가로 인덱스에 포함해도 성능이 거의 향상되지 않습니다. 만드는 쿼리의 종류와 관계 없이 가장 고유한 값을 갖는 필드만 인덱스 해야 합니다.

</br>

## 언제 사용해야 될까?

- 사용하면 좋은 경우

  1. Where 절에서 자주 사용되는 Column

  2. 외래키가 사용되는 Column

  3. Join에 자주 사용되는 Column

- Index 사용을 피해야 하는 경우

  1. Data 중복도가 높은 Column (ex. 성별)

  2. DML이 자주 일어나는 Column

</br>

## DML을 사용 했을 때

- INSERT

  index split 현상이 발생할 수 있음.

  기존 Block에 여유가 없을 때, 새로운 Data가 입력된다.

  → 인덱스는 데이터가 순서대로 정렬 되어야 한다.

  → 새로운 Block을 할당 받은 후, Key를 옮기는 작업을 수행한다.

  → Index split 작업 동안, 해당 Block의 Key 값에 대해서 DML이 블로킹 된다. (대기 이벤트 발생)

- DELETE

  테이블에서 데이터가 delete 될 경우 - 지워지고 다른 데이터가 그 공간을 사용 가능

  index에서 데이터가 delete 될 경우 - 데이터가 지워지지 않고, 사용 안 됨 표시만 해 둔다.

  ->즉, 테이블에 데이터가 1만건 있는 경우, 인덱스에는 2만건이 있을 수 있다.(테이블의 데이터 수와 인덱스의 데이터 수가 다를 수 있다.)

- UPDATE (인덱스에는 update 개념이 없다.)

  테이블에 update가 발생할 경우

  → 인덱스에서는 delete가 먼저 발생한 후 새로운 작업의 insert 작업이 발생한다.  
  (delete와 insert 두 개의 작업이 인덱스에 동시에 일어나 다른 DML보다 더 큰 부하를 주게 됨.)

</br>

## 인덱스의 종류

- **B-Tree 인덱스**

  1. Unique Index  
     고유 인덱스는 유일한 값을 갖는 컬럼에 대해서 생성하는 인덱스로 고유 인덱스를 지정하려면 UNIQUE 옵션을 지정해야 된다.  
     SQL> CREATE UNIQUE INDEX idx_ukempno_emp ON emp(empno);

  2. Non Unique Index  
     중복되는 데이터가 들어가야 하는 경우  
     SQL > create index idx_prof_position 2 on professor(position);

  3. Function Based Index  
     SAL*12와 같이 컬럼에 어떠한 산술식을 수행했을 때 사용한다.  
     SAL컬럼에 INDEX가 걸려있다해도 SAL*12은 INDEX를 타지 못한다. 이럴 때 함수 기반 인덱스를 생성한다.  
     SQL> CREATE INDEX idx_annsal_emp ON emp(sal\*12);

  4. Descending Index  
     내림차순으로 인덱스를 생성하여 큰 값을 많이 조회하는 SQL에 사용하는 것이 좋다.  
     SQL> create index idx_prof_pay 2 on professor(pay desc);

  5. Composite Index  
     결합 인덱스는 두 개 이상의 컬럼으로 인덱스를 구성하는 것이다.  
     SQL> CREATE INDEX idx_dept_com ON index_dept(deptno, dname);

- Bitmap 인덱스

  데이터의 값의 종류가 적고 동일한 데이터가 많을 경우에 사용
