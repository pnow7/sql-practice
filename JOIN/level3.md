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
