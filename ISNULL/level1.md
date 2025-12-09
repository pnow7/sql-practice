## [경기도에 위치한 식품창고 목록 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131114)

```sql
-- oracle
SELECT 
    warehouse_id,
    warehouse_name,
    address,
    NVL(freezer_yn, 'N') AS freezer_yn
FROM food_warehouse
WHERE address LIKE '경기도%'
ORDER BY warehouse_id;

-- MySQL
SELECT 
    warehouse_id,
    warehouse_name,
    address,
    IFNULL(freezer_yn, 'N') AS freezer_yn
FROM food_warehouse
WHERE address LIKE '경기도%'
ORDER BY warehouse_id;
```