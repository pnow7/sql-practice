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
