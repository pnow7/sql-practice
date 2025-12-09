## [자동차 대여 기록에서 장기/단기 대여 구분하기](https://school.programmers.co.kr/learn/courses/30/lessons/151138)

```sql
-- Oracle
SELECT
    history_id,
    car_id,
    TO_CHAR(start_date, 'YYYY-MM-DD') AS start_date,
    TO_CHAR(end_date, 'YYYY-MM-DD') AS end_date,
    CASE 
        WHEN end_date - start_date >= 29 THEN '장기 대여'
        ELSE '단기 대여'
    END AS rent_type
FROM car_rental_company_rental_history
WHERE TO_CHAR(start_date, 'YYYY-MM') = '2022-09'
ORDER BY history_id DESC;


-- MySQL
SELECT
    history_id,
    car_id,
    DATE_FORMAT(start_date, '%Y-%m-%d') AS start_date,
    DATE_FORMAT(end_date, '%Y-%m-%d') AS end_date,
    CASE 
        WHEN DATEDIFF(end_date, start_date) >= 29 THEN '장기 대여'
        ELSE '단기 대여'
    END AS rent_type
FROM car_rental_company_rental_history
WHERE start_date LIKE '2022-09%'
ORDER BY history_id DESC;
```

## [특정 옵션이 포함된 자동차 리스트 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/157343?language=oracle)

```sql
SELECT 
    * 
FROM car_rental_company_car
WHERE options LIKE '%네비게이션%'
ORDER BY car_id DESC;
```