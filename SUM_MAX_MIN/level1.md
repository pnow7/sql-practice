## [가장 비싼 상품 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131697)

```sql
SELECT 
    MAX(price) AS max_price
FROM product
```

## [최댓값 구하기]()

```sql
SELECT
    MAX(datetime) AS datetime
FROM animal_ins
```

## [잡은 물고기 중 가장 큰 물고기의 길이 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/298515)
```sql
--Oracle
SELECT 
    MAX(length) || 'cm' AS max_length
FROM fish_info;


--MySQL (Oracle은 CONCAT 인자 두개만 가능)
SELECT 
    CONCAT(MAX(length), 'cm') AS max_length
FROM fish_info;
```