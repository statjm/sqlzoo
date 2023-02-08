[!info]
- The % is a _wild-card_ it can match any characters
- You can use the underscore as a single character wildcard- 
---
# Table
<table class="db_ref">
<tbody><tr><th>name</th><th>continent</th></tr>
<tr><td>Afghanistan</td><td>Asia</td></tr>
<tr><td>Albania</td><td>Europe</td></tr>
<tr><td>Algeria</td><td>Africa</td></tr>
<tr><td>Andorra</td><td>Europe</td></tr>
<tr><td>Angola</td><td>Africa</td></tr>
<tr>
<td colspan="2">....</td>
</tr>
</tbody></table>
# 문제
- Find the countries that have "t" as the second character
- Find the countries that have two "o" characters separated by two others.
- Find the countries that have exactly four characters.

매우 당황. underscore를 wildcard 써본 적이 없었기에, 문제를 풀다가 처음 알게 되었음.

# 답안
```sql
SELECT name FROM world
 WHERE name LIKE '_t%'
ORDER BY name

SELECT name FROM world
 WHERE name LIKE '%o__o%'

SELECT name FROM world
 WHERE name LIKE '____'
```

# 문제
- Find the capital and the name where the capital includes the name of the country.
- Show the name and the extension where the capital is an extension of name of the country.

concat이라는 함수는 SELECT 문에서만 써보았기에, 기존에 갖고 있던 개념을 바꾸게 된 문제

# 답안
```sql
SELECT capital, name
FROM world
WHERE capital LIKE concat('%',name,'%')

SELECT name,replace(capital, name, '')
FROM world 
WHERE capital LIKE concat(name,'%_')
```