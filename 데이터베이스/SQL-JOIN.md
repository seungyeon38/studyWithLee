## SQL-JOIN 
<br>

> 조인은 여러 개의 테이블을 연결하여 데이터를 검색하는 것


<br>  

### 조인 속성의 특징
조인 속성: 조인 검색을 위해 테이블을 연결해주는 속성    

- 연결하려는 테이블 간에 조인 속성의 이름은 달라도 되지만 도메인은 같아야 함 
- 일반적으로 외래키를 조인 속성으로 이용  

<br>
조인 검색에서는 같은 이름의 속성이 서로 다른 테이블에 존재할 수 있기 때문에,  

속성 이름 앞에 해당 속성이 소속된 테이블의 이름을 표시해야 함 (ex. ***주문***.주문고객)  

<br> 
<br>  

### 1) INNER JOIN
<br> 

두 테이블을 연결할 때 가장 많이 사용하는 것이 INNER JOIN(그냥 JOIN이라고 쓰면 INNER JOIN을 의미)   

INNER JOIN은 두 테이블이 ***모두 가지고 있는 데이터***만을 검색 결과로 함    

교집합과도 같다

<br> 

![img](https://velog.velcdn.com/images/letskuku/post/d4df7481-b221-4eba-a650-80457945ea4a/image.png)

```
SELECT 테이블이름.조회할속성, 테이블이름.조회할속성
FROM 기준테이블
INNER JOIN 조인테이블 ON 기준테이블.조인속성 = 조인테이블.조인속성
```
WHERE 절을 통해 INNER JOIN을 할 수도 있음

```
SELECT 테이블이름.조회할속성, 테이블이름.조회할속성
FROM 기준테이블, 조인테이블
WHERE 기준테이블.조인속성 = 조인테이블.조인속성
 ```  

<br>
<br> 

### 2) LEFT OUTER JOIN
<br>

INNER JOIN은 두 테이블에 모두 데이터가 있어야만 결과가 나오지만, OUTER JOIN은 한쪽에만 데이터가 있어도 결과가 나온다.

LEFT OUTER JOIN은 다음과 같이 ***왼쪽 테이블을 기준***으로 OUTER JOIN을 하는 것

<br>

![img](https://velog.velcdn.com/images/letskuku/post/f25b63ea-f440-426a-843a-971110dea2cf/image.png)

```
SELECT 테이블이름.조회할속성, 테이블이름.조회할속성
FROM 기준테이블
LEFT OUTER JOIN 조인테이블 ON 기준테이블.조인속성 = 조인테이블.조인속성
```

<br>

오른쪽 테이블에도 있는 데이터는 제외하고싶을 경우, WHERE 절에 조건을 추가

![img](https://velog.velcdn.com/images/letskuku/post/2397570e-cdd3-4b83-be29-50574c0e0e1f/image.png)

```
SELECT 테이블이름.조회할속성, 테이블이름.조회할속성
FROM 기준테이블
LEFT OUTER JOIN 조인테이블 ON 기준테이블.조인속성 = 조인테이블.조인속성
WHERE 조인테이블.조인속성 IS NULL 
```

<br>
<br>

### 3) RIGHT OUTER JOIN
<br>

RIGHT OUTER JOIN은 다음과 같이 ***오른쪽 테이블을 기준***으로 OUTER JOIN

<br>

![img](https://velog.velcdn.com/images/letskuku/post/07915a26-fdec-487d-bccb-6957234ef6c1/image.png)

```
SELECT 테이블이름.조회할속성, 테이블이름.조회할속성
FROM 기준테이블
RIGHT OUTER JOIN 조인테이블 ON 기준테이블.조인속성 = 조인테이블.조인속성
```

<br>

마찬가지로 왼쪽 테이블에도 있는 데이터는 제외하고싶을 경우, WHERE 절에 조건을 추가

![img](https://velog.velcdn.com/images/letskuku/post/07fa0398-a246-4938-ae51-e6059f687d25/image.png)

```
SELECT 테이블이름.조회할속성, 테이블이름.조회할속성
FROM 기준테이블
RIGHT OUTER JOIN 조인테이블 ON 기준테이블.조인속성 = 조인테이블.조인속성
WHERE 기준테이블.조인속성 IS NULL
```

<br>
<br>

### 4) FULL OUTER JOIN
<br>

FULL OUTER JOIN은 두 테이블이 가지고 있는 데이터를 모두 검색할 수 있다.  

합집합과 같다

<br>

![img](https://velog.velcdn.com/images/letskuku/post/e8cd2517-cc94-470f-9246-6369b89babb3/image.png)

```
SELECT 테이블이름.조회할속성, 테이블이름.조회할속성
FROM 기준테이블
FULL OUTER JOIN 조인테이블 ON 기준테이블.조인속성 = 조인테이블.조인속성
```

<br>

두 테이블이 공통으로 가지고 있는 데이터를 제외하고싶을 경우, WHERE 절에 조건을 추가

![img](https://velog.velcdn.com/images/letskuku/post/83a20ad5-8625-4fdd-b039-5a0461ee731a/image.png)

```
SELECT 테이블이름.조회할속성, 테이블이름.조회할속성
FROM 기준테이블
FULL OUTER JOIN 조인테이블 ON 기준테이블.조인속성 = 조인테이블.조인속성
WHERE 기준테이블.조인속성 IS NULL OR 조인테이블.조인속성 IS NULL
```
<br>

※ MySQL에서는 FULL OUTER JOIN이 없으므로,

LEFT OUTER JOIN 과 RIGHT OUTER JOIN을 UNION 하는 식으로 하여 FULL OUTER JOIN을 만들어야 한다.

```
SELECT 테이블이름.조회할속성, 테이블이름.조회할속성
FROM 기준테이블
LEFT OUTER JOIN 조인테이블 ON 기준테이블.조인속성 = 조인테이블.조인속성
UNION
SELECT 테이블이름.조회할속성, 테이블이름.조회할속성
FROM 기준테이블
RIGHT OUTER JOIN 조인테이블 ON 기준테이블.조인속성 = 조인테이블.조인속성
```

<br>
<br>

### 5) CROSS JOIN
<br>

CROSS JOIN은 한 테이블의 모든 행과 다른 테이블의 모든 행을 조인 

결과의 전체 행 개수는 두 테이블의 각 행의 개수를 곱한 것과 같다. 

CROSS JOIN을 카티션 곱(CARTESIAN PRODUCT)라고도 한다.

다음과 같이 왼쪽 테이블의 행이 3개, 오른쪽 테이블의 행이 4개이면 CROSS JOIN에 대한 결과는 총 12개의 행으로 이루어진다.

<br>

![img](https://velog.velcdn.com/images/letskuku/post/fa47dc62-4094-499b-b3ad-548fef1e85f8/image.png)

```
SELECT 테이블이름.조회할속성, 테이블이름.조회할속성
FROM 기준테이블
CROSS JOIN 조인테이블
```

<br>
CROSS JOIN할 테이블을 FROM 절에 단순 나열하는 방식으로도 작성할 수 있다.  

```
SELECT 테이블이름.조회할속성, 테이블이름.조회할속성
FROM 기준테이블, 조인테이블
```
<br>

### 6) SELF JOIN
<br>

SELF JOIN에서는 한 테이블이 자기 자신과 조인   

따라서 하나의 테이블을 사용하고, 하나의 테이블을 여러 번 복사하여 조인한다고 생각하면 쉽다.  

테이블과 컬럼 이름이 모두 동일하기 때문에 식별을 위해 반드시 테이블 별칭(Alias)을 사용해야 함

<br>

```
SELECT ALIAS명1.컬럼이름1, ALIAS명2.컬럼이름2
FROM 테이블1 ALIAS명1, 테이블1 ALIAS명2
WEHRE ALIAS명1.컬럼이름1 = ALIAS명2.컬럼이름2
```