## 4. SELECT within SELECT Tutorial
![](../images/SELECT_within_SELECT_pic_1.png)

1.List each country name where the population is larger than that of 'Russia'.
```sql
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia');
```

2.Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.
```sql
SELECT name
FROM world
WHERE continent = 'Europe' AND gdp/population >(SELECT gdp/population FROM world WHERE name='United Kingdom');
```

3.List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.
```sql
SELECT name, continent
FROM world WHERE continent IN (SELECT continent FROM world WHERE name='Argentina' or name='Australia') ORDER BY name;
```

4.Which country has a population that is more than Canada but less than Poland? Show the name and the population.
```sql
SELECT name, population
FROM world
WHERE population > (SELECT population FROM world WHERE name='Canada') AND population < (SELECT population FROM world WHERE name='Poland');
```

5.Germany (population 80 million) has the largest population of the countries in Europe. Austria (population 8.5 million) has 11% of the population of Germany.
Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.
```sql
SELECT name, CONCAT(round(100*population/(SELECT population FROM world WHERE name='Germany'),0),'%')
FROM world
WHERE continent='Europe';
```

6.Which countries have a GDP greater than every country in Europe? [Give the name only.] (Some countries may have NULL gdp values)
```sql
SELECT name
FROM world
WHERE gdp > (SELECT MAX(gdp) FROM world WHERE continent='Europe');
```

7.Find the largest country (by area) in each continent, show the continent, the name and the area:
```sql
SELECT continent, name, area 
FROM world AS x
WHERE x.area >= 
  (SELECT MAX(area) FROM world y
      WHERE y.continent=x.continent);
```

8.List each continent and the name of the country that comes first alphabetically.
```sql
SELECT continent, name
FROM world AS x
WHERE x.name = 
  (SELECT name FROM world y
      WHERE y.continent=x.continent ORDER BY name LIMIT 1);
```

9.Find the continents where all countries have a population <= 25000000. 
Then find the names of the countries associated with these continents. Show name, continent and population.
```sql
SELECT name, continent, population
FROM world AS x
WHERE 25000000 > ALL (
  SELECT y.population
  FROM world AS y
  WHERE x.continent = y.continent);
```

10.Some countries have populations more than three times that of any of their neighbours 
(in the same continent). Give the countries and continents.
```sql
SELECT name, continent
FROM world AS x
WHERE x.population/3 > ALL (
  SELECT y.population
  FROM world AS y
  WHERE x.continent = y.continent
  AND x.name != y.name);
```