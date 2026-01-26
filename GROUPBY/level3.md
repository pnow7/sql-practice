## [자동차 대여 기록에서 대여중/대여 가능 여부 구분하기]] (https://school.programmers.co.kr/learn/courses/30/lessons/157340)

```sql
-- ORACLE
SELECT 
    CAR_ID, 
    CASE
        WHEN MAX(
            CASE 
                WHEN START_DATE <= '2022-10-16'
                 AND END_DATE >= '2022-10-16'
                THEN 1 ELSE 0
            END
        ) = 1 THEN '대여중'
        ELSE '대여 가능'
    END AS AVAILABILITY
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
GROUP BY CAR_ID
ORDER BY CAR_ID DESC;
```

## [즐겨찾기가 가장 많은 식당 정보 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131123)

```sql
-- ORACLE
SELECT
    T.FOOD_TYPE,
    T.REST_ID,
    T.REST_NAME,
    T.FAVORITES
FROM (
    SELECT
        FOOD_TYPE,
        REST_ID,
        REST_NAME,
        FAVORITES,
        RANK() OVER(PARTITION BY FOOD_TYPE ORDER BY FAVORITES DESC) AS RANKING
    FROM REST_INFO
    ORDER BY FAVORITES DESC
) T
WHERE RANKING = 1
ORDER BY FOOD_TYPE DESC
```

## [대여 횟수가 많은 자동차들의 월별 대여 횟수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/151139)

<details>

- ⭐⭐⭐
1. **자동차 거르기 (서브쿼리)**: 8~10월 사이에 총 5번 이상 빌려진 차가 누구인지 먼저 명단을 뽑기

2. **데이터 범위 제한 (메인 쿼리)**: 명단에 있는 차라도 8~10월 사이의 기록만 

3. **월별로 쪼개기 (GROUP BY)**: 그 기록들을 다시 MONTH와 CAR_ID로 그룹화해서 개수 세기

<summary></summary>
</details>

```sql
-- ORACLE
SELECT
    TO_NUMBER(TO_CHAR(START_DATE, 'MM')) AS MONTH,
    CAR_ID,
    COUNT(*) AS RECORDS
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY 
WHERE START_DATE BETWEEN TO_DATE('20220801', 'YYYYMMDD') 
  AND TO_DATE('20221031', 'YYYYMMDD')
  AND CAR_ID IN (
    SELECT
        CAR_ID
    FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
    WHERE START_DATE BETWEEN TO_DATE('20220801', 'YYYYMMDD') 
      AND TO_DATE('20221031', 'YYYYMMDD')
    GROUP BY CAR_ID
    HAVING COUNT(*) >= 5
)
GROUP BY TO_NUMBER(TO_CHAR(START_DATE, 'MM')), CAR_ID
ORDER BY MONTH, CAR_ID DESC
```

## [카테고리 별 도서 판매량 집계하기](https://school.programmers.co.kr/learn/courses/30/lessons/144855)

<details>
- ⭐⭐
<summary></summary>
</details>

```sql
-- ORACLE
SELECT 
    T1.CATEGORY, 
    SUM(T2.SALES) AS TOTAL_SALES
FROM BOOK T1
JOIN BOOK_SALES T2 
  ON T1.BOOK_ID = T2.BOOK_ID
WHERE T2.SALES_DATE >= TO_DATE('2022-01-01', 'YYYY-MM-DD')
  AND T2.SALES_DATE < TO_DATE('2022-02-01', 'YYYY-MM-DD')
GROUP BY T1.CATEGORY 
ORDER BY T1.CATEGORY
```