## 6-2 가독성을 챙기기 위한 SQL 스타일 가이드

- 다른 사람과 쿼리를 공유하는 경우
    - 별도의 설명이 없어도 이해할 수 있게
    - 쿼리 변경 -> 특정 부분 or 전체 수정인지 파악 쉽게

- 스타일 가이드
    - 예약어는 대문자 작성 (SELECT, FROM, WHERE, 함수)
    - 컬럼 이름은 snake_case로 작성 (언더바) : 일관성
    - 별칭 지을 때는 명시적 이름 적용
    - 왼쪽 정렬
    - 예약어나 컬럼은 한 줄에 하나씩
    - 쉼표는 컬럼 바로 뒤에

## 6-3 가독성을 챙기기 위한 WITH문 & 파티션

- WITH 문
    - WITH 문을 사용하여 쿼리를 정의 -> 재사용
    - FROM 서브쿼리를 WITH temp_table AS ()로 재정의 하여 FROM temp_table로 활용
    - CTE라고 표현
    - SELECT 구문에 이름을 정해주는 것과 유사
    - 쿼리내 반복 사용 가능

- PARTITION
    - 쿼리 성능 향상 : 파이션 설정한 곳만 스캔
    - 데이터 관리 용이성
    - 비용 절감

## 6-4 데이터 결과 검증 정의

- 데이터 결과 검증 : SQL 쿼리 후 얻은 결과가 예상과 일치하는지 확인하는 과정
    - 목적 : 분석 결과의 정확성, 신뢰성 확보
    - 방법 
        - 내가 기대하는 예상 결과를 정의
        - 쿼리 작성
        - 두개 일치 비교
    - 문제를 잘 정의하고 미리 작성
    - 도메인 특수성 잘 파악
    - SQL 쿼리 템플릿과 유사 맥락

- 데이터 결과 검증에 자주 활용하는 SQL 쿼리
    - COUNT(*) : 행 수 확인
    - NOT NULL : 필드 값이 비어있는지 확인
    - DISTINCT : 데이터의 고유값 확인. 중복 제거
    - IF, CASE WHEN : 조건문
    - EX. SELECT COUNT(DISTINCT col), COUNT(col) : 두 컬럼을 보고 개수 비교

- 데이터 결과 검증 활용 방식
    - 특정 user_id로 필터링
    - 샘플 데이터 생성

## 6-5 데이터 결과 검증 예시

- 통합 데이터 생성
``` SQL
SELECT 
*
FROM (
    SELECT
        id AS battle_id,
        player1_id AS trainer_id,
        winner_id
    FROM 'basic.battle'
    UNION ALL
    SELECT
        id AS battle_id,
        player2_id AS trainer_id,
        winner_id
    FROM 'basic.battle'
)
ORDER BY battle_id
```

