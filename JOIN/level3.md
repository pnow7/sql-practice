## [있었는데요 없었습니다](https://school.programmers.co.kr/learn/courses/30/lessons/59043?language=oracle)

```sql
SELECT 
    T1.animal_id,
    T1.name
FROM animal_ins T1
JOIN animal_outs T2
    ON T1.animal_id = T2.animal_id
WHERE T1.datetime > T2.datetime
ORDER BY T1.datetime;
```
