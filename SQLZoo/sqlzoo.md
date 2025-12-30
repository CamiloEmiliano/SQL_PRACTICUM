## Sections
1. [SELECT basics](#1-select-basics)
2. [SELECT FROM world](#2-select-from-world)

## [1. SELECT basics](https://sqlzoo.net/wiki/SELECT_basics)
1.1. **Introducing the `world` table of countries**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the population of Germany.
```sql
SELECT
  population
FROM
  world
WHERE
  name = 'Germany'
```
1.2. **Scandinavia**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the name and the population for 'Sweden', 'Norway', and 'Denmark'.
```sql
SELECT
  name, population
FROM
   world
WHERE
  name IN ('Sweden', 'Norway', 'Denmark')
```
1.3. **Just the right size**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the country and area for countries with an area between 200,000 and 250,000.
```sql
SELECT
  name, area
FROM world
  WHERE area BETWEEN 200000 AND 250000
```
## [2. SELECT from world](https://sqlzoo.net/wiki/SELECT_name)
2.1. **Introduction**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the name, continent and population of all countries
```sql
SELECT
  name, continent, population
FROM
  world
```
2.2. **Large Countries**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the name for the countries that have a population of at least 200 million
```sql
SELECT
  name
FROM
  world
WHERE
  population > 200000000
```
2.3. **Per capita GDP**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Give the `name` and the `per capita GDP` for those countries with a population of at least 200 million
```sql
SELECT
  name, gdp/population as "per capita GDP"
FROM
  world
WHERE
  population > 200000000
```
2.4. **South America in millions**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the `name` and `population` in millions for the countries of the `continent` 'South America'.
```sql
SELECT
  name, population/1000000 AS "pop (1e6)"
FROM
  world
WHERE
  continent = 'South America'
```
2.5. **France, Germany, Italy**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the `name` and `population` for France, Germany, Italy 
```sql
SELECT
  name, population
FROM
  world
WHERE
  name IN ('France', 'Germany' ,'Italy')
```
2.6. **United**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the countries which have a `name` that includes the word 'United' 
```sql
SELECT
  name
FROM
  world
WHERE
  name LIKE '%United%'
```
2.7. **Two ways to be big**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
A country is big if it has an area of more than 3 million sq km or it has a population of more than 250 million.<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the countries that are big by area or big by population. Show `name`, `population` and `area`.
```sql
SELECT
  name, population, area
FROM
  world
WHERE
  area > 3000000 OR population > 250000000
```
2.8. **One or the other (but not both)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both.
&nbsp;&nbsp;&nbsp;&nbsp;
Show `name`, `population` and `area`.
```sql
SELECT
  name, population, area
FROM
  world
WHERE
  (area > 3000000) <> (population > 250000000)
```
2.9. **Rounding**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the `name` and `population` in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.
```sql
SELECT 
  name,
  ROUND(population/1000000, 2) AS "pop*1e6",
  ROUND(gdp/1000000000, 2) AS "gdp*1e9"
FROM
  world
WHERE
  continent = 'South America'
```
2.10. **Trillion dollar economies**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the `name` and `per-capita GDP` for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.
```sql
SELECT
  name,
  ROUND(gdp/population, -3) AS "per-capita GDP"
FROM
  world
WHERE
  gdp > 1000000000000
```
2.11. **Name and capital have the same length**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the `name` and `capital` where the name and the capital have the same number of characters.
```sql
SELECT
  name, capital
FROM
  world
WHERE 
  LENGTH(name) = LENGTH(capital)
```
2.12. **Matching name and capital**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the `name` and the `capital` where the first letters of each match. Don't include countries where the name and the capital are the same word.
```sql
SELECT
  name, capital
FROM
  world
WHERE
  LEFT(capital, 1) = LEFT(name, 1)
AND
  capital <> name
```
2.13. **All the vowels**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Find the country that has all the vowels and no spaces in its name.
```sql
SELECT
  name
FROM
  world
WHERE
  name NOT LIKE '% %'
AND
  name LIKE '%a%'
AND
  name LIKE '%e%'
AND
  name LIKE '%i%'
AND
  name LIKE '%o%'
AND
 name LIKE '%u%'
```