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