## [가장 비싼 상품 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131697)

```sql
SELECT 
    MAX(PRICE) AS MAX_PRICE
FROM PRODUCT
```

## [최댓값 구하기]()

```sql
SELECT
    MAX(DATETIME) AS DATETIME
FROM ANIMAL_INS
```

## [잡은 물고기 중 가장 큰 물고기의 길이 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/298515)
```sql
--Oracle
SELECT 
    MAX(LENGTH) || 'cm' AS MAX_LENGTH
FROM FISH_INFO;


--MySQL (Oracle은 CONCAT 인자 두개만 가능)
SELECT 
    CONCAT(MAX(LENGTH), 'cm') AS MAX_LENGTH
FROM FISH_INFO;
```