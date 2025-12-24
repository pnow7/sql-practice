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

## [조건에 부합하는 중고거래 상태 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/164672?language=oracle)

```sql
-- Oracle
SELECT 
    board_id,
    writer_id,
    title,
    price,
    CASE 
        WHEN status = 'SALE' THEN '판매중'
        WHEN status = 'RESERVED' THEN '예약중'
        WHEN status = 'DONE' THEN '거래완료'
    END AS STATUS
FROM used_goods_board
WHERE TO_CHAR(created_date, 'YYYY-MM-DD') = '2022-10-05'
ORDER BY board_id DESC;
```

## [루시와 엘라 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59046?language=oracle)

```sql
-- Oracle
SELECT
    animal_id,
    name,
    sex_upon_intake
FROM animal_ins
WHERE name = 'Lucy' OR 
      name = 'Ella' OR 
      name = 'Pickle' OR 
      name = 'Rogan' OR 
      name = 'Sabrina' OR 
      name = 'Mitty'
ORDER BY animal_id
```

## [이름에 el이 들어가는 동물 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59047?language=oracle)

```sql
-- Oracle
SELECT
    animal_id,
    name
FROM animal_ins
WHERE UPPER(name) LIKE '%EL%' AND 
      animal_type = 'Dog'
ORDER BY name;
```

## [중성화 여부 파악하기](https://school.programmers.co.kr/learn/courses/30/lessons/59409?language=oracle)

```sql
-- Oracle
SELECT
    animal_id,
    name,
    CASE 
        WHEN sex_upon_intake LIKE 'Neutered%' OR
             sex_upon_intake LIKE 'Spayed%' THEN 'O'
        ELSE 'X'
    END AS 중성화
FROM animal_ins
ORDER BY animal_id;
```
