## [가격이 제일 비싼 식품의 정보 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131115?language=oracle)

```sql
SELECT 
    * 
FROM food_product
WHERE price = (
            SELECT MAX(price) 
            FROM food_product
      );
```

## [최솟값 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/59038)

```sql
SELECT
    MIN(datetime) AS datetime
FROM animal_ins
```

## [동물 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/59406)

```sql
SELECT
    COUNT(animal_id) AS count
FROM animal_ins
```

## [중복 제거하기](https://school.programmers.co.kr/learn/courses/30/lessons/59408)

```sql
SELECT
    COUNT(DISTINCT name) AS count
FROM animal_ins
```

## [조건에 맞는 아이템들의 가격의 총합 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/273709)

```sql
SELECT
    SUM(price) AS total_price
FROM item_info
WHERE rarity = 'LEGEND';
```

## [연도별 대장균 크기의 편차 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/299310)

```sql
-- Oracle
SELECT
    TO_CHAR(differentiation_date, 'YYYY') AS year,
    MAX(size_of_colony) OVER (
        PARTITION BY TO_CHAR(differentiation_date, 'YYYY')
    ) - size_of_colony AS year_dev,
    id
FROM ecoli_data
ORDER BY year ASC, year_dev ASC;


-- MySQL
SELECT
    YEAR(differentiation_date) AS year,
    MAX(size_of_colony) OVER (
        PARTITION BY YEAR(differentiation_date)
    ) - size_of_colony AS year_dev,
    id
FROM ecoli_data
ORDER BY 
    year ASC, year_dev ASC;
```