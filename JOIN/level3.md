# JOIN

<details>
<summary></summary>
- FROM: 왼쪽
- JOIN: 오른쪽
</details>

## [있었는데요 없었습니다](https://school.programmers.co.kr/learn/courses/30/lessons/59043?language=oracle)

```sql
SELECT 
    T1.ANIMAL_ID,
    T1.NAME
FROM ANIMAL_INS T1
JOIN ANIMAL_OUTS T2
    ON T1.ANIMAL_ID = T2.ANIMAL_ID
WHERE T1.DATETIME > T2.DATETIME
ORDER BY T1.DATETIME;
```

## [조건에 맞는 도서와 저자 리스트 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/144854)

```sql
-- ORACLE
SELECT
    T1.BOOK_ID,
    T2.AUTHOR_NAME,
    TO_CHAR(T1.PUBLISHED_DATE, 'YYYY-MM-DD') AS PUBLISHED_DATE
FROM BOOK T1
JOIN AUTHOR T2
    ON T1.AUTHOR_ID = T2.AUTHOR_ID
WHERE T1.CATEGORY = '경제'
ORDER BY T1.PUBLISHED_DATE;
```

## [상품 별 오프라인 매출 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131533)

```sql
-- 상품코드 별 매출액(판매가 * 판매량) 합계를 출력
-- 매출액을 기준으로 내림차순 정렬
-- 매출액이 같다면 상품코드를 기준으로 오름차순

-- ORACLE
SELECT
    T1.PRODUCT_CODE,
    SUM(T2.SALES_AMOUNT * T1.PRICE) AS SALES
FROM PRODUCT T1
JOIN OFFLINE_SALE T2
ON T1.PRODUCT_ID = T2.PRODUCT_ID
GROUP BY T1.PRODUCT_CODE
ORDER BY SALES DESC, T1.PRODUCT_CODE ASC;
```

## [없어진 기록 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59042)

```sql
-- ORACLE
SELECT
    T2.ANIMAL_ID,
    T2.NAME
FROM ANIMAL_OUTS T2
LEFT JOIN ANIMAL_INS T1
ON T2.ANIMAL_ID = T1.ANIMAL_ID
WHERE T1.ANIMAL_ID IS NULL
ORDER BY T2.ANIMAL_ID;
```