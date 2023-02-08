[!info]
서브쿼리란, 쿼리 안에 쿼리가 포함되어 있는 쿼리를 말한다

---
# Table
world(name, continent, area, population, gdp)

# 문제
- List each country **name** where the **population** is larger than that of 'Russia'.

간만에 서브쿼리를 다룬다. 이정도는 뭐..

# 답안
```sql
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')
```

# 문제
- Which countries have a GDP greater than every country in Europe? Give the **name** only. (Some countries may have NULL gdp values)

서브쿼리의 결과와 비교를 하기 위해서는 다중 행 비교 연산자가 필요하다고 함. (처음 써보고, 처음 들었음. 하지만 많이 보던 친구들이 있었음. IN, EXISTS. 너희들이 다중 행 비교 연산자라는 애들이었구나)

# 답안
```sql
SELECT name
FROM world
WHERE gdp > ALL(
SELECT gdp
FROM world
WHERE continent = 'Europe'
AND gdp > 0
)
```

서브쿼리를 숙달되지 않으면, WHERE 절에 있는 쿼리에서 MAX함수를 이용하여 가장 큰 값을 돌려보고, 메..모..했다가 한번 더 쿼리를 실행시키지 않았을까함

# 문제
- Find the largest country (by area) in each continent, show the **continent**, the **name** and the **area**:
- Some countries have populations more than three times that of all of their neighbours (in the same continent). Give the countries and continents.

# 답안
```sql
SELECT continent, name, area FROM world x
  WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent
          AND area>0)

SELECT name, continent
FROM world x
WHERE population >= ALL(
SELECT population * 3
FROM world y
WHERE x.continent = y.continent
AND x.name <> y.name
)
```
