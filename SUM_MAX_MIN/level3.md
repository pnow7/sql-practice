## [물고기 종류 별 대어 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/293261)

```sql
SELECT
    T1.id,
    T2.fish_name,
    T1.length
FROM fish_info T1
JOIN fish_name_info T2 
    ON T1.fish_type = T2.fish_type
WHERE T1.length = (
    SELECT MAX(T3.length)
    FROM fish_info T3
    WHERE T3.fish_type = T1.fish_type
)
ORDER BY T1.id;
```