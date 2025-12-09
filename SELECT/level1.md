## [평균 일일 대여 요금 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/151136?language=oracle)

```sql
SELECT 
    ROUND(AVG(DAILY_FEE), 0) AS AVERAGE_FEE
FROM CAR_RENTAL_COMPANY_CAR
WHERE CAR_TYPE = 'SUV';
```

## [조건에 부합하는 중고거래 댓글 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/164673?language=oracle)

```sql
SELECT
    T1.TITLE,
    T1.BOARD_ID,
    T2.REPLY_ID,
    T2.WRITER_ID,
    T2.CONTENTS,
    TO_CHAR(T2.CREATED_DATE, 'YYYY-MM-DD') AS CREATED_DATE
FROM USED_GOODS_BOARD T1
INNER JOIN USED_GOODS_REPLY T2 
    ON T1.BOARD_ID = T2.BOARD_ID
WHERE T1.CREATED_DATE 
    BETWEEN TO_DATE('2022-10-01', 'YYYY-MM-DD') 
    AND TO_DATE('2022-10-31', 'YYYY-MM-DD')
ORDER BY T2.CREATED_DATE ASC, T1.TITLE ASC;
```

## [인기있는 아이스크림](https://school.programmers.co.kr/learn/courses/30/lessons/133024)

```sql
SELECT
    FLAVOR
FROM FIRST_HALF
ORDER BY TOTAL_ORDER DESC, SHIPMENT_ID;
```

