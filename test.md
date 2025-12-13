
| 점수대      | 명수 |
| -------- | -- |
| 90 ~ 100 | 2  |
| 80 ~ 90  | 2  |
| 70 ~ 80  | 2  |
| 60 ~ 70  | 1  |
| 0 ~ 60   | 2  |


```sql
SELECT 
    T.scores AS 점수대,
    COUNT(*) AS 명수
FROM 
    (
        SELECT
            CASE
                WHEN score >= 90 AND score <= 100 THEN '90 ~ 100'
                WHEN score >= 80 AND score < 90 THEN '80 ~ 90'
                WHEN score >= 70 AND score < 80 THEN '70 ~ 80'
                WHEN score >= 60 AND score < 70 THEN '60 ~ 70'
                ELSE '0 ~ 60'
            END AS scores
        FROM student_scores
    ) T
GROUP BY T.scores
ORDER BY T.scores DESC;
```