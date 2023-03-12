## SQL-기본  
<br>
CS면접 예상 질문 정리  

- [데이터베이스](###-1.-데이터베이스)
- [쿼리문 순서](###-2.-쿼리문-순서)
- [데이터 베이스 언어](###-3.-데이터-베이스-언어)
- [스키마(Schema)](###-4.-스키마(Schema))
- [DROP, Truncate, delete 차이점](###-5.-Drop,-Truncate,-Delete-차이점)  
<br>

### 1. 데이터베이스  
여러 사람에 의해 공유되어 사용될 목적으로 통합하여 관리되는 데이터의 집합.   
특정 기업이나 조직 또는 개인이 필요에 의해 데이터를 일정한 형태로 저장해 놓은 것.   
<br>

### 2. 쿼리문 순서  
SELECT 칼럼명   
FROM 테이블명    
WHERE 조건식  
GROUP BY 칼럼/표현식   
HAVING 그룹조건식  
ORDER BY 칼럼/표현식 [ASC|DESC];  
<br>

### 3. 데이터 베이스 언어  
세가지 종류의 데이터 베이스 언어   
- 정의어(DDL : Data Definition Language) : 데이터 베이스 구조를 정의, 삭제, 수정 하는 언어(create, alter, drop)  
- 조작어(DML : Data Manipulation Language) : 자료 검색, 삽입, 갱신, 삭제를 위한 언어(select, insert, update, delete)  
- 제어어(DCL : Data Control Language) : 데이터에 대해 무결성, 병행 수행, 제어, 보호, 관리를 위한 언어(grant, revoke)  
(commit, rollback은 TCL, 굳이 나눈다면 DCL로 분류)  
<br>

### 4. 스키마(Schema)  
데이터베이스의 구조와 제약조건에 관해 전반적인 명세를 기술한 것.  
개체의 특성을 나타내는 속성(Attribute),    
속성들의 집합으로 이루어진 개체(Entity),     
개체 사이에 존재하는 관계(Relation)에 대한 정의와 이것들이 유지해야 할 제약조건을 기술한 것.  
데이터베이스 내에 어떤 구조로 데이터가 저장되는지를 나타내는 데이터베이스 구조.  
<br>

### 5. Drop, Truncate, Delete 차이점
- DELETE: 데이터는 지워지지만 테이블 용량은 줄어들지 않으며, 원하는 데이터만 지울 수 있음  
삭제 후 Rollback이 가능    
- TRUNCATE: 테이블은 삭제가 되지 않으며 데이터만 삭제(재사용 가능)  
삭제 후 Rollback이 되지 않음(초기화)    
- DROP: 테이블 전체를 삭제  
삭제 후 Rollback이 되지 않음(초기화)   
<br>


