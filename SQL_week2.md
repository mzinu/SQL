## 2-6. 연습 문제

### 데이터 탐색 - 조건, 추출, 요약 연습 문제(1)

1. 

SELECT
    COUNT(id) AS cnt
FROM basic.pokemon
WHERE type2 IS NULL

2. 

<!--집계 함수는 GROUP BY 와 같이 다님. 집계하는 기준(컬럼)이 없으면 COUNT만 쓸 수 있으나, 집계하는 기준이 있다면 그 기준 컬럼을 GROUP BY에 써줘야 함-->

SELECT 
    type1,
    COUNT(id) AS cnt
FROM basic.pokemon
WHERE type2 IS NULL
GROUP BY type1
ORDER BY cnt DESC

3. 

SELECT 
    type1,
    COUNT(id) AS cnt
FROM basic.pokemon
GROUP BY type1

<!--DISTINCT는 중복 없이 값을 알고 싶을 때 -->

4. 

SELECT
    is_legendary,
    COUNT(id) AS cnt
FROM basic.pokemon
GROUP BY is_legendary

<!--GROUP BY(ORDER BY) 1 : 1은 SELECT의 첫 컬럼을 의미 -->

5. 

SELECT
    name,
    COUNT(name) AS cnt
FROM basic.trainer
GROUP BY name
HAVING cnt >= 2

<!--집계 후 조건 : HAVING -->

6. 

SELECT
    *    
FROM basic.trainer
WHERE name = 'Iris'

7. 

SELECT
    *    
FROM basic.trainer
WHERE name IN ('Iris','Whitney','Cynthia')

8. 

SELECT
    COUNT (id) AS cnt   
FROM basic.pokemon

9. 

SELECT
    generation,
    COUNT (id) AS cnt   
FROM basic.pokemon
GROUP BY generation

10. 

SELECT
  generation,
  COUNT(id) as cnt
FROM basic.pokemon

11.  

SELECT
  type1,
  COUNT(id) as cnt
FROM basic.pokemon
WHERE type2 IS NOT NULL
GROUP BY type1
ORDER BY cnt DESC
LIMIT 1

12. 

SELECT 
  type1,
  COUNT(id) as cnt
FROM basic.pokemon
WHERE type2 IS NULL
GROUP BY type1
ORDER BY cnt DESC
LIMIT 1

13. 

SELECT
  kor_name
FROM basic.pokemon
WHERE kor_name LIKE "파%"

14. 

SELECT
  COUNT(id) AS cnt
FROM basic.trainer
WHERE badge_count>= 6

15. 
SELECT
  trainer_id,
  COUNT(pokemon_id) AS cnt
FROM basic.trainer_pokemon
GROUP BY trainer_id

16. 
SELECT
  trainer_id,
  COUNT(pokemon_id) AS cnt
FROM basic.trainer_pokemon
WHERE status = "Released"
GROUP BY trainer_id
ORDER BY cnt DESC
LIMIT 1

17. 
SELECT 
  trainer_id,
  COUNTIF(status = 'Released') AS released_cnt,
  COUNT(pokemon_id) AS pokemon_cnt,
  COUNTIF(status = 'Released')/COUNT(pokemon_id) AS released_ratio
FROM basic.trainer_pokemon
GROUP BY trainer_id
HAVING released_ratio>=0.2

## 2-8. 새로운 집계 함수 소개
- GROUP BY ALL: 그룹화할 키를 추론. 기준 작성 불필요

## 3-2 SQL 쿼리 작성하는 흐름
- 지표 고민 : 문제 정의
- 지표 구체화 : 명확한 지표
- 지표 탐색 : 유사케이스 찾기
- 쿼리 작성

![Image](https://github.com/user-attachments/assets/316c64e7-9314-4870-aa2f-bc9f8a4b739d)
