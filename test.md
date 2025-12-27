
| 점수대      | 명수 |
| -------- | -- |
| 90 ~ 100 | 2  |
| 80 ~ 90  | 2  |
| 70 ~ 80  | 2  |
| 60 ~ 70  | 1  |
| 0 ~ 60   | 2  |


```sql
SELECT 
    T.SCORES AS 점수대,
    COUNT(*) AS 명수
FROM 
    (
        SELECT
            CASE
                WHEN SCORE >= 90 AND SCORE <= 100 THEN '90 ~ 100'
                WHEN SCORE >= 80 AND SCORE < 90 THEN '80 ~ 90'
                WHEN SCORE >= 70 AND SCORE < 80 THEN '70 ~ 80'
                WHEN SCORE >= 60 AND SCORE < 70 THEN '60 ~ 70'
                ELSE '0 ~ 60'
            END AS SCORES
        FROM STUDENT_SCORES
    ) T
GROUP BY T.SCORES
ORDER BY T.SCORES DESC;
```