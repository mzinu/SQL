## 3-4. 오류를 디버깅하는 방법

### BigQuery Error
- Syntax Error (문법 오류)
    - Expected end of input but got keyword
        - SELECT : SELECT는 쿼리 당 1개. 쿼리가 끝나는 부분에 ; 붙이고 해당 부분만 드래그해서 실행.
        - WHERE : LIMIT은 쿼리 젤 마지막에.
    - Expected ")" but got end of script at [8:11] : 괄호 작성 안 했을 때
- SELECT list must not be empty at [10:1] : SELECT할 컬럼이 안 적혀있을 때
- Number of arguments(인자) does not match for aggregate function COUNT : 함수 인자 수가 다를 때
- SELECT list expression references column type 1 a which is neither grouped nor aggregated : GROUP BY에 적절한 컬럼을 명시하지 않을 때

### 오류 메시지 해결의 핵심
- 오류 발생 : 오류 메시지와 함께
- 오류 메시지 검색 : 구글, 공식 문서, ChatGPT 


## 4-2. 데이터 타입과 데이터 변환

### 데이터 타입

- 종류
    - 숫자(정수, 소수점)
    - 문자
    - 시간, 날짜
    - 부울(논리값. 참/거짓)

- 중요한 이유 : 보이는 것과 저장된 것의 차이를 조정 

### 함수

- 자료 타입 변경 : CAST 함수

```SQL
SELECT
    CAST(1 AS STRING) # 숫자 1을 문자 1로 변경경
```
    - 문자형은 숫자형으로 변경 불가능 
    - SAFE_CAST : SAFE_가 붙으면 변환 실패일 경우 NULL 반환

- 수학 함수
    - 나누기 : X/Y -> SAFE_DIVIDE(X,Y)
    - X,Y 중 하나라도 0인 경우 그냥 나누면 ZERO ERROR 발생 -> 함수쓰면 NULL 반환


## 4-3. 문자열 함수(CONCAT, SPLIT, REPLACE, TRIM, UPPER)

### 문자열(STRING) 함수

- 문자열 연산
    - 붙이기 :CONCAT(안녕,하세요,!) -> 안녕하세요!
    - 분리하기 : SPLIT("가, 나, 다, 라", ",") -> 가나다라를 행 하나씩으로 쉼표 기준 분리.
    - 특정 단어 수정 : REPLACE("안녕하세요","안녕","실천") -> 실천하세요
    - 문자열 자르기 : TRIM("안녕하세요","하세요") -> 안녕 
    - 영어 대문자 변환 : UPPER("abc") -> ABC # 보통 ID에서 같은 이름인데 대소문자 때문에 구분 되는 경우 방지


## 4-4. 날짜 및 시간 데이터 이해하기(1)(타임존, UTC, Millisecond, TIMESTAMP/DATETIME)

### 날짜 및 시간 데이터 타입 파악 : DATE, DATETIME, TIMESTAMP

- DATE : 2023-12-31
- DATETIME : DATE + TIME(Time Zone 정보 없음), 2023-12-31 14:00:00 
- TIME : 날짜와 무관하게 시간만 표시, 23:59:59.00

### 날짜 및 시간 데이터 관련 알면 좋은 내용 : UTC, Millisecond

- 타임존
    - GMT : 그리니치 기준 시간차(ex. 한국: GMT +9)
        - 영국 근처에서 주로 사용
    - UTC : 국제적인 표준 시간(ex. 한국: UTC +9)
        - 협정 세계시
    - TIMESTAMP : UTC부터 경과한 시간
        - TIMEZONE 정보 있음
        - 2023-12-31 14:00:00 UTC

- 단위
    - milisecond(ms) : 시간 단위. 천 분의 1초.
        - Milisecond -> TIMESTAMP -> DATETIME으로 변경
    - microsecond(뮤s) = 1/1,000ms = 1/1,000,000초
    - ex. 1704176819711ms -> 2024-01-02 15:26:59
        ```sql
        SELECT
            TIMESTAMP_MILLIS(1704176819711) AS milli_to_timestamp_value,
            TIMESTAMP_MICROS(1704176819711000) AS micro_to_timestamp_value, -- TIMESTAMP라 UTC. 한국시간으로 적용하려면 -9시간간 --          
            DATETIME(TIMESTAMP_MICROS(1704176819711000)) AS datetime_value; -- DATETIME라 타임존 정보 없음. T만 나옴 --
            DATETIME(TIMESTAMP_MICROS(1704176819711000),'Asia/Seoul') AS datetime_value_asia; -- 자동으로 +9시간 해서 한국시간으로 조정해줌 --
        ```

![Image](https://github.com/user-attachments/assets/e9077f44-6d47-438b-8592-8eef12011437)
