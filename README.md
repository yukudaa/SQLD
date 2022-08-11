# **SQLD 최종 정리강의 1편 - SELECT문장 ~ 트랜잭션 관리 언어(TCL)**

## SQL 명령문 개괄

1) From - where - group by - having - select - orderby

2) DML - select, insert, delete, update

    DDL - alter, create, modify, drop

    TCL - rollback, commit

    DCL - grant, revote

## SELECT

1) distinct (집약) → 10

                          10         10

                          20    →    20

                          20         30           

                          30

  Distinct(deptno, mgr) ≒ group by(deptno, mgr)

2) As → select   1) as 생략가능 2) 컬럼명에 띄어쓰기

         → from     1) as 사용불가!

3) Concat(인수가 2개) → + SQL server

                                    →  || oracle

## 논리연산자

1) and     → a and b (둘다 먹기)

    or        → a or b    (둘중에 하나)

    not      → a,b (둘다 싫어)

 *연산순위   not → and → or (나오로 외우기)

## SQL 연산자

A **Between** 1 and 2 → 1≤ A ≤ 2

A **IN** (1,2,3) → A = 1 or A = 2 or A = 3

**LIKE  →**   _ ****미지의 한글자

         →  **%** 0이상 글자

         → escape  와일드카드 (- %)를 문자로 취급

            ex) ename like ‘A-A’ escape ⇒ ‘A@_A’ ‘@’

Rownum (oracle) 

 → (where) 1) Rownum -1 포함

TOP (SQL server)

 → (select) TOP(n) <컬럼명>

                    상위 n개

## NULL

### 1) null의 정의

 1)부재, 모르는값

 2) **산술연산**

 null + 2

 null - 4             = null

 null * null     

    **비교연산**   

 null = null

 null = 2

 → 알수없음(unknown)

 → where(조건) : 조건이 nuknown이면 → false

 3) 정렬상 의미

 oracle : ‘**∞’**

SQL server : ‘-**∞’**

 4) NVL                → 널뛰기       (값1, 값2)   값1 is null  → true 값2 false 값1

     NVL2              → 널뛰기       (값1,값2,값3) 값1 is null → 값3 , is not null 값2

     isNull              → 널뛰기       (값1, 값2)  NVL과 동일

     Null if              → 같이 놀자!      (값1, 값2)   같으면 null 다르면 값1

     coalesce          → 널 아닌 첫번째 값   (값1,값2, …..)   널 아닌 첫번째 값  

## 정렬

1) 정렬의 특성

1.가장 마지막에 실행

2.성능이 느려질 수 있다.

3.null값과의 관계 

2)컬럼 번호 정렬

출력되는 컬럼의 수보다 큰 값이 불허

3) 인수 2개 정렬

sal desc, ename asc

sal이 같으면 ename 오름차순

4) select ename X 

    orderby sal (가능)

## 숫자 함수

Round 자릿수

Round(138 94) ( ) 인수!

ceil(oracle)/ ceiling(Sql server)

## 문자열 함수

upper

lower

대소문자 구분

LPad

RPad

LTrim

RTrim

Substring

instr

실습만해보기

## 날짜 함수

To_Char

To_date 

실습 ‘형변환’

sysdate (oracle)

Getdate() (sql server)

날짜데이터 + 100 : 100일 이후 (day로 인식)

## DECODE/CASE

Case만!

다 만족 안하면 null

## 집계함수*

null 과의 관계

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6e4b270c-c15a-4269-bdd0-15403fc68571/Untitled.png)

## GROUP BY

그룹수준 정보를 바꾼다

집약기능

## JOIN

1) natural join, using → 중복된 컬럼 하나, 제일 앞에 등장, alius 사용 X

2) left outer Join

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3f971454-adbe-448b-aa62-483525176130/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cd6cafdb-b370-4b43-bb48-6d1ad99752e0/Untitled.png)

## 서브쿼리

select               Scalar

from                Inline view     → 메인쿼리의 컬럼 사용가능

where               거의 모든 서브쿼리 가능 (중첩 서브쿼리) 

group by           X

having               거의 모든 서브쿼리 가능 (중첩 서브쿼리) 

orderby             Scalar

In

any/some

all

exist

## 집합연산자

union       → 정렬 작업O 느리다

intersect  → 정렬 작업O 느리다

minus      → 정렬 작업O 느리다

union all → (중복데이터 존재) 정렬작업X 빠르다

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/db6a63e8-e103-4268-840f-0439580d8308/Untitled.png)

## DDL

TCL

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4733479f-50fd-4c59-94d5-af68152108e7/Untitled.png)

## DML

insert

update

delete

merge

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/145b2c59-48d8-43c1-9423-f0f73b7c8280/Untitled.png)

## 제약 조건*

PK        = 하나만 존재

unique

notnull

## DCL

grant

revoke

role 특징

## VIEW

독편부

독립성, 편리성, 보안성

## 그룹함수*

roll up

cube

groupingsets

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/75725603-5795-41b1-91a5-568b98305545/Untitled.png)

## TCL

commit 

roleback
