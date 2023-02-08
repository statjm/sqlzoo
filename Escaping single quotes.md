[!info]
You can't put a single quote in a quote string directly. You can use two single quotes within a quoted string.

---
# 문제
- Find all details of the prize won by EUGENE O'NEILL

어떤 프로그래밍 언어를 다루든 간에 텍스트가 포함한 작은 따옴표, 큰 따옴표 때문에 구글을 찾게 됨. sql에서는 작은 따옴표 두개를 표기함으로서, 작은 따옴표를 표기할 수 있음

# 답안
```sql
SELECT *
FROM nobel
WHERE winner = 'EUGENE O''NEILL'
```