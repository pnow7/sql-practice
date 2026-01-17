## [주문량이 많은 아이스크림 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/133027?language=oracle)

<details>

- HOLY FUCK

<summary></summary>
</details>

```sql
-- ORACLE
SELECT
    T3.FLAVOR
FROM (
    SELECT
        T1.FLAVOR,
        T1.TOTAL_SUM + T2.TOTAL_ORDER AS TOTAL
    FROM (
        SELECT
            FLAVOR,
            SUM(TOTAL_ORDER) AS TOTAL_SUM
        FROM JULY
        GROUP BY FLAVOR
    ) T1
    LEFT JOIN FIRST_HALF T2
    ON T1.FLAVOR = T2.FLAVOR
    ORDER BY TOTAL DESC
) T3
WHERE ROWNUM <= 3
```

## [특정 기간동안 대여 가능한 자동차들의 대여비용 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/157339?language=oracle)

<details>

⭐⭐⭐

<summary></summary>
</details>

```sql
-- CAR_RENTAL_COMPANY_CAR: 자동차 옵션 리스트
-- CAR_RENTAL_COMPANY_RENTAL_HISTORY: 자동차 대여 기록
-- CAR_RENTAL_COMPANY_DISCOUNT_PLAN: 자동차 대여 요금 할인 정책

-- 자동차 종류가 세단 또는 SUV인 자동차 중 2022년 11월 1일부터 2022년 11월 30일까지 대여 가능하고
-- 30일간의 대여 금액이 50만원 이상 200만원 미만인 자동차에 대해서
-- 자동차 ID, 자동차 종류, 대여 금액 리스트를 출력

-- 대여 금액을 기준으로 내림차순 정렬하고
-- 대여 금액이 같은 경우 자동차 종류를 기준으로 오름차순 정렬 
-- 자동차 종류까지 같은 경우 자동차 ID를 기준으로 내림차순 정렬

-- SELECT
--     DISTINCT
--     A.CAR_ID,
--     A.CAR_TYPE,
--     A.FEE
-- FROM (
--     SELECT
--         T1.CAR_ID,
--         T1.CAR_TYPE,
--         T1.DAILY_FEE * 30 * (100 - T3.DISCOUNT_RATE) * 0.01 AS FEE
--     FROM CAR_RENTAL_COMPANY_CAR T1
--     JOIN CAR_RENTAL_COMPANY_DISCOUNT_PLAN T3 
--       ON T1.CAR_TYPE = T3.CAR_TYPE
--     WHERE T1.CAR_TYPE IN ('세단', 'SUV')
--       AND T3.DURATION_TYPE = '30일 이상'
-- ) A
-- JOIN CAR_RENTAL_COMPANY_RENTAL_HISTORY B 
--   ON A.CAR_ID = B.CAR_ID
-- WHERE A.FEE >= 500000 AND A.FEE < 2000000
--   AND B.START_DATE <= TO_DATE('20221130', 'YYYYMMDD') 
--   AND B.END_DATE >= TO_DATE('20221101', 'YYYYMMDD')
-- ORDER BY FEE DESC, CAR_TYPE, CAR_ID DESC;

-- ORACLE
SELECT
    T1.CAR_ID,
    T1.CAR_TYPE,
    (T1.DAILY_FEE * 30 * (100 - T2.DISCOUNT_RATE) / 100) AS FEE
FROM CAR_RENTAL_COMPANY_CAR T1
JOIN CAR_RENTAL_COMPANY_DISCOUNT_PLAN T2
    ON T1.CAR_TYPE = T2.CAR_TYPE AND T2.DURATION_TYPE = '30일 이상'
WHERE T1.CAR_TYPE IN ('세단', 'SUV')
  AND T1.CAR_ID NOT IN (
      SELECT CAR_ID
      FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
      -- 대여가능한 기간 찾기
      WHERE START_DATE <= TO_DATE('20221130', 'YYYYMMDD')
        AND END_DATE >= TO_DATE('20221101', 'YYYYMMDD')
  )
GROUP BY T1.CAR_ID, T1.CAR_TYPE, T1.DAILY_FEE, T2.DISCOUNT_RATE
HAVING (T1.DAILY_FEE * 30 * (100 - T2.DISCOUNT_RATE) / 100) BETWEEN 500000 AND 1999999
ORDER BY FEE DESC, CAR_TYPE ASC, CAR_ID DESC;
