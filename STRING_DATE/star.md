## [오랜 기간 보호한 동물(2)](https://school.programmers.co.kr/learn/courses/30/lessons/59411?language=oracle)

> 두개의 테이블을 이용해서 가장 오랫동안 보호된 동물 2마리 뽑아내는 문제

```sql
-- [Oracle]
-- 입양을 간 동물 중(animal_outs), 
-- 보호기간이 가장 길었던 
-- 동물 두마리의 아이디와 이름을 조회(animal_ints)

-- 서브 쿼리
SELECT
    T3.animal_id,
    T3.name
FROM (
      SELECT 
          T1.animal_id,
          T1.name,
          T2.datetime - T1.datetime AS stay_days
      FROM animal_ins T1
      INNER JOIN animal_outs T2
      ON T1.animal_id = T2.animal_id
      ORDER BY stay_days DESC
     ) T3
WHERE ROWNUM <= 2

-- 윈도우 함수
SELECT
    animal_id,
    name
FROM (
    SELECT
        T1.animal_id,
        T1.name,
        ROW_NUMBER() OVER (
            ORDER BY T2.datetime - T1.datetime DESC
        ) AS rn
    FROM animal_ins T1
    INNER JOIN animal_outs T2
    ON T1.animal_id = T2.animal_id
)
WHERE rn <= 2;
```