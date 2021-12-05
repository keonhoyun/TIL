# TIL_DB



## Database

- 데이터베이스는 체계화된 데이터의 모임이다.
- 몇 개의 자료 파일을 조직적으로 통합, 중복을 없애고 구조화한 집합체



### 데이터베이스의 장점

- 중복 최소화
- 데이터 무결성
- 데이터 일관성
- 데이터 표준화
- 보안 유지



## RDB

### 관계형 데이터베이스(RDB)

- 키와 값들의 간단한 관계를 표 형태로 정리한 데이터베이스
- 관계형 모델에 기반

| 고유번호 | 이름   | 주소 | 나이 |
| -------- | ------ | ---- | ---- |
| 1        | 정은원 | 인천 | 22   |
| 2        | 노시환 | 경남 | 21   |
| 3        | 하주석 | 신일 | 28   |



### 스키마(schema)

- 데이터베이스에서 자료의 구조, 표현방법, 관계등 전반적인 명세를 기술한 것

| column  | datatype |
| ------- | -------- |
| id      | INT      |
| name    | TEXT     |
| address | TEXT     |



### 테이블(Table)

- 열(컬럼/필드)와 행(레코드/값)의 모델을 사용해 조직된 데이터 요소들의 집합

| id   | name   | address |
| ---- | ------ | ------- |
| 1    | 정은원 | 인천    |
| 2    | 노시환 | 경남    |
| 3    | 하주석 | 신일    |

#### 열(컬럼 / 필드)

- 각 열에는 고유한 데이터 형식이 지정됨
- 위에서 name필드에 고객의 이름(TEXT) 정보가 저장됨



#### 행(로우 / 레코드)

- 실제 데이터가 저장되는 형태
- 위에서 3개의 레코드가 저장



#### 기본키(PK)

- 각 행의 고유 값
- 반드시 설정, 관계 설정시 주요하게 활용



## RDBMS

### 관계형 데이터베이스 관리 시스템(RDBMS)

- 관계형 모델을 기반으로 하는 데이터베이스 관리시스템
  - MySQL
  - SQLite
  - ORACLE
  - MS SQL



## SQL

### SQL

- RDBMS의 데이터 관리를 위해 설계된 프로그래밍 언어
- 스키마 생성 및 수정
- 검색 및 관리
- 객체 접근 조정 관리



### DDL

- Data Definition Language(데이터 정의 언어)
- 구조(테이블, 스키마)를 정의
  - CREATE / DROP / ALTER



### DML

- Data Manipulation Language(데이터 조작 언어)
- 데이터를 저장, 수정, 삭제 등을 실행
  - INSERT / SELECT / UPDATE / DELETE



### DCL

- Data Control Language(데이터 제어 언어)
- 사용자 권한 제어
  - GRANT / REVOKE / COMMIT / ROLLBACK



## 테이블 생성 및 삭제

### CREATE TABLE

- 테이블 생성

> CREATE TABLE classmates (
>
> id INTEGER PRIMARY KEY,
>
> name TEXT NOT NULL (NOT NULL은 선택사항),
>
> age INT NOT NULL
>
> );

- 스키마 조회

> .schema classmates

- 결과

> CREATE TABLE classmates (
>
> id INTEGER PRIMARY KEY,
>
> name TEXT
>
> );



### DROP TABLE

- 테이블 제거

> DROP TABLE classmates;



## CRUD

### CREATE

#### INSERT

- 특정 테이블에 레코드(행) 생성

>INSERT INTO 테이블 이름 (칼럼1, 칼럼2, ...) Values (값1, 값2, ...)

- 모든 열에 데이터가 있는 경우

> INSERT INTO 테이블 이름 Values (값1, 값2, ...)

- 여러개 넣기

> INSERT INTO classmates VALUES
>
> ('김민우', 25, '용마')
>
> ('문동주', 20, '진흥')
>
> ('김범수', 27, '북일');



### READ

#### SELECT

> SELECT * FROM classmates; (id 표시 X), (모든 칼럼 조회)

> SELECT rowid, * FROM classmates; (id 표시 O)

> SELECT 칼럼1, 칼럼2,.. FROM classmates; (특정 칼럼 조회)

##### LIMIT

- 쿼리에서 반환되는 행 수를 제한
- OFFSET 키워드와 함께 사용

> SELECT 칼럼1, 칼럼2,.. FROM classmates LIMIT 숫자; (숫자만큼 조회)

> SELECT 칼럼1, 칼럼2,.. FROM classmates LIMIT 숫자 OFFSET 숫자; (특정부분에서 원하는 수) 
>
> EX) 세번째에 있는 값 하나 조회하기 >  LIMIT 1 OFFSET 2

##### WHERE

- 특정 검색 조건을 지정

> SELECT 칼럼1, 칼럼2,.. FROM classmates WHERE 조건; 
>
> SELECT name FROM classmates WHERE address='서울';
>
> SELECT name FROM classmates WHERE address='서울' AND age=20;
>
> 

##### SELECT DISTINCT

- 중복 행을 제거

> SELECT DISTINCT 칼럼 FROM 테이블이름;
>
> SELECT DISTINCT age FROM classmates;



### DELETE

> DELETE FROM 테이블이름 WHERE 조건;
>
> DELETE FROM classmates WHERE rowid=5;

- id값은 삭제 후 재사용
- AUTOINCREMENT로 재사용 방지

> CREATE TABLE classmates (
>
> id INTEGER PRIMARY KEY AUTOINCREMENT,



### UPDATE

> UPDATE 테이블 이름 SET 칼럼1=값1, 칼럼2=값2, .... WHERE 조건;
>
> UPDATE classmates SET name='강재민', address='단국' WHERE rowid=5;



CSV파일 정보 테이블에 적용하기

> .mode csv
>
> .import users.csv users (적용)
>
> .tables (테이블 확인)



## Sqlite Aggregate Functions

- COUNT = 그릅의 항목 수 
- AVG = 평균 값
- MAX = 최대 값
- MIN = 최소 값
- SUM = 모든 값의 합

> SELECT COUNT(칼럼) FROM 테이블 이름;
>
> SELECT AVG(칼럼) FROM 테이블 이름;
>
> SELECT COUNT(*) FROM users; (모든 레코드 조회)
>
> SELECT AVG(age) FROM users WHERE age>=30;
>
> SELECT name, MAX(balance) FROM users;



## LIKE

- 패턴 일치를 기반으로 데이터 조회
  - % : 0개 이상의 문자
  - _ : 임의의 단일 문자

> SELECT * FROM 테이블 WHERE 칼럼 LIKE '와일드카드패턴';
>
> SELECT * FROM 테이블 WHERE 칼럼 LIKE '2%'; (2로 시작)
>
> SELECT * FROM 테이블 WHERE 칼럼 LIKE '%2'; (2로 끝)
>
> SELECT * FROM 테이블 WHERE 칼럼 LIKE '%2%'; (2가 들어감)
>
> SELECT * FROM 테이블 WHERE 칼럼 LIKE '_2%'; (아무 값이 하나 있고 두번째가 2로 시작)
>
> SELECT * FROM 테이블 WHERE 칼럼 LIKE '1___'; (1로 시작, 4자리인 값)
>
> SELECT * FROM 테이블 WHERE 칼럼 LIKE '2_%; (2로 시작, 적어도 2자리인 값)

> SELECT * FROM  users WHERE age LIKE '2_'; (20대)



## ORDER BY

- 집합을 정렬
- SELECT문에 추가
  - ASC
  - DESC

> SELECT * FROM 테이블 ORDER BY 칼럼 ASC;
>
> SELECT * FROM users ORDER BY age ASC LIMIT 10; (상위 10개)
>
> SELECT * FROM users ORDER BY age, last_name ASC LIMIT 10; (나이 순, 성 순)



## GROUP BY

- 요약 행 집합을 만듦
- where절 뒤에 작성

> SELECT 칼럼1, aggreate_function(칼럼2) FROM 테이블 GROUP BY 칼럼1, 칼럼2;
>
> SELECT last_name, COUNT(*) FROM users GROUP BY last_name;
>
> SELECT last_name, COUNT(*) AS name_count FROM users GROUP BY last_name;
>
> (users에서 각 성씨가 몇 명씩 있는지 구하기)



## ALTER TABLE

- 테이블 이름 변경
- 새 칼럼 추가
- 칼럼 이름 수정

> ALTER TABLE table_name
>
> RENAME COLUMN current_name TO new_name;

> ALTER TABLE 기존 테이블 이름 RENAME TO 새 이름;
>
> ALTER TABLE articles 이름 RENAME TO news;

> ALTER TABLE 테이블 이름 ADD COLUMN 칼럼 이름 데이터 타입설정;
>
> ALTER TABLE news ADD COLUMN created_at TEXT;
>
> ALTER TABLE news ADD COLUMN created_at TEXT NOT NULL DEFAULT '소재목'; (NOT NULL은 추가할 수 없기 때문)