## 2-3 데이터 탐색(SELECT, FROM, WHERE)

### SQL 쿼리 구조
SELECT : <!--테이블의 어떤 컬럼을 선택할 것인가-->
    COL1 AS new_name, <!--AS는 컬럼 별칭. 따옴표 안 씀-->
    COL2,
    COL3 <!--여러 컬럼 명시 가능-->
FROM Dataset.Table <!--어떤 테이블에서 데이터를 확인할 것인가?-->
WHERE : <!--원하는 조건은 어떤 조건인가가?-->
    COL = 1 <!--조건문-->

* : 모든 컬럼을 출력하겠다 <!--데이터 확인용. 열,행이 많으면 비용↑ 여서 잘 안 씀 -->

SELECT
    * EXCEPT(제외할 컬럼이름)

집합 개념으로 생각하면 쉬움

### 실습
세부정보 - 테이블 정보 - 최종 수정 시간 : 데이터 동기화 시점
미리보기 : 데이터 다 보이므로 * 사용 안해도 됨
; : 쿼리문 끝
드래그하고 실행하면 해당 범위만 실행 가능

## 2-4 SELECT 연습 문제

1.
SELECT 
  * 
FROM `my-project-1-454109.basic.trainer` 

2.
SELECT
  name
FROM `basic.trainer`

3.
SELECT
  name
FROM `basic.trainer`

4.
SELECT
  name,
  age,
  hometown
FROM basic.trainer
WHERE id = 3

5.
SELECT
  attack,
  hp
FROM basic.pokemon
WHERE kor_name = "피카츄"

## 2-5 집계(GROUP BY + HAVING + SUM/COUNT)

### 집계와 그룹화
- 집계 : 모아서 계산하다
- GROUP BY : 같은 값끼리 모아서 그룹화한다
    ex. GROUP BY 색상
- 특정 컬럼을 기준으로 모으면서 다른 컬럼에선 집계 가능 (ex. 같은 색상의 가로의 합)
- 집계 후 정렬 : ORDER BY
- 그룹화 한 값에 조건 설정 가능 : HAVING

### SQL 코드
SELECT
    집계할 컬럼,
    AVG(attack) AS avg_attack, <!--집계함수수-->
    Count(id) AS cnt
FROM Pokemon
GROUP BY
    type 1 <!--집계할 컬럼을 SELECT에 명시하고 그 컬럼을 꼭 GROUP BY에 작성-->

### 집계 함수 종류
AVG, COUNT, COUNTIF(특정조건 row 세기), MAX, MIN, SUM

### DISTINCT : 고유값을 알고 싶은 경우
- 중복 제거
- GROUP BY 와 동일 기능
- ex. COUNT(DISTINCT count할 컬럼)

### GROUP BY 연습문제
1.
SELECT
    COUNT(id) AS cnt
FROM basic.pokemon

2.
SELECT
    generation,
    COUNT(id) AS cnt
FROM basic.pokemon
GROUP BY
    generation

3.
SELECT
    type1
    COUNT(id) AS cnt
FROM basic.pokemon
GROUP BY
    type1
HAVING cnt>=10
ORDER BY cnt DESC

4.
SELECT
    type1,
    COUNT(id) AS cnt
FROM basic.pokemon
GROUP BY 
    type 1
HAVING cnt >= 10
ORDER BY cnt DESC

### 집계 활용
일자별, 연령대별, 특정 타입별, 앱 화면별(어떤 화면에 유저가 많이 접근)

### 조건 설정
- WHERE : Table에 바로 조건을 설정하고 싶을 때
    SELECT - FROM - WHERE
- HAVING : GROUP BY한 후에 조건 설정
    SELECT - FROM - GROUP BY - HAVING

### 서브 쿼리
- SELECT문 안에 존재하는 SELECT 쿼리
- FROM 절에 SELECT문 넣을 수 있음
- 괄호로
- 서브 쿼리 작성하고, 서브 쿼리 바깥에서 WHERE 조건 = 서브쿼리에서 HAVING

### ORDER BY
- 쿼리의 맨 마지막
- ORDER BY <컬럼> <순서>
- DESC(내림차순) OSC(오름차순)

### LIMIT
- 쿼리문의 결과 Row 수 제한
- 쿼리문의 제일 마지막
- ORDER BY
  LIMIT

### 정리
- 집계 : GROUP BY + 집계함수
- 고유값 : DISTINCT
- 조건 : WHERE/HAVING
- 정렬 : ORDER

![SQL_week1](https://github.com/user-attachments/assets/1326f851-f42a-433c-8468-66a63a515f11)