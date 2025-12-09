## [평균 일일 대여 요금 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/151136?language=oracle)

```sql
SELECT 
    ROUND(AVG(daily_fee), 0) AS average_fee
FROM car_rental_company_car
WHERE car_type = 'SUV';
```

## [조건에 부합하는 중고거래 댓글 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/164673?language=oracle)

```sql
SELECT
    T1.title,
    T1.board_id,
    T2.reply_id,
    T2.writer_id,
    T2.contents,
    TO_CHAR(T2.created_date, 'YYYY-MM-DD') AS created_date
FROM used_goods_board T1
INNER JOIN used_goods_reply T2 
    ON T1.board_id = T2.board_id
WHERE T1.created_date 
    BETWEEN TO_DATE('2022-10-01', 'YYYY-MM-DD') 
    AND TO_DATE('2022-10-31', 'YYYY-MM-DD')
ORDER BY T2.created_date ASC, T1.title ASC;
```

## [인기있는 아이스크림](https://school.programmers.co.kr/learn/courses/30/lessons/133024)

```sql
SELECT
    flavor
FROM first_half
ORDER BY total_order DESC, shipment_id;
```

