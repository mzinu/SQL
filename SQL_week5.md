## 5-2. JOIN 이해하기

### SQL JOIN
- JOIN : 서로 다른 데이터 테이블을 연결하는 것
- EX. 트레이너가 포획한 포켓몬 기준 트레이너 데이터 연결
    - 연결키 : trainer_id, id
    - 해당 trainer_id에 맞게 행을 붙여서 열이 추가
- 공통적으로 존재하는 컬럼(=key)가 있으면 JOIN 가능
- 보통 id 값, 특정범위(date)
- 해야하는 이유
    - 관계형 데이터베이스 설계시 정규화 과정을 거침
    - 정규화는 중복을 최소화하게 데이터를 구조화
- 최근엔 데이터 웨어하우스에서 JOIN + 연산으로 데이터 마트 만들어서 활용

## 5-3. 다양한 JOIN 방법 (LEFT, RIGHT, INNER, CROSS JOIN)

- (INNER) JOIN : 두 테이블의 공통 요소만 연결
- LEFT/RIGHT (OUTER) JOIN : 왼쪽/오른쪽 테이블 기준으로 연결
    - 해당 테이블은 고정. 모두 포함
- FULL (OUTER) JOIN : 양쪽 기준으로 연결
- CROSS JOIN : 두 테이블의 각각의 요소 곱하기
![Image](https://github.com/user-attachments/assets/2e586879-adf0-49ee-90e5-45164c5d0446)

## 5-4. JOIN 쿼리 작성하기

- 테이블 확인 : 테이블에 저장된 데이터, 컬럼 확인
- 기준 테이블 정의 : 가장 많이 참고할 기준 테이블 정의(LEFT)
- JOIN KEY 찾기 : 여러 테이블과 연결할 KEY(ON) 정리
- 결과 예상 및 쿼리 작성

```SQL
SELECT
    A.col1,
    A.col2,
FROM table1 AS A
LEFT JOIN table2 AS B
ON A.key = B.key # 테이블 이름 Alias(별칭) 이용가능
```

![Image](https://github.com/user-attachments/assets/d0293419-aafd-4be5-9adf-4933cb424536)



