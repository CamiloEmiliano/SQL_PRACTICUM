<!--## Sections
1. [SELECT basics](#1-select-basics)
2. [SELECT FROM world](#2-select-from-world)
3. [SELECT FROM Nobel Tutorial](#3-select-from-nobel-tutorial)-->
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
## [3. SELECT from Nobel Tutorial](https://sqlzoo.net/wiki/SELECT_from_Nobel_Tutorial)
3.1. **Winners from 1950**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Display the `year`, `subject`, and `winner` of the Nobel prizes for 1950
```sql
SELECT
  yr as "year", subject, winner
FROM
  nobel
WHERE
  yr = 1950
```
3.2. **1962 Literature**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show who won the 1962 prize for literature. 
```sql
SELECT
  winner
FROM
  nobel
WHERE
  yr = 1962
AND
  subject = 'literature'
```
3.3. **Albert Einstein**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the `year` and `subject` that won 'Albert Einstein' his prize
```sql
SELECT
  yr AS "year", subject
FROM
  nobel
WHERE
  winner = 'Albert Einstein'
```
3.4. **Recent Peace Prizes**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Give the name of the 'peace' winners since the year 2000, including 2000.
```sql
SELECT
  winner
FROM
  nobel
WHERE
  yr >= 2000
AND
  subject = 'peace'
```
3.5. **Literature in the 1980's**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show all details (`yr`, `subject`, `winner`) of the literature prize winners for 1980 to 1989 inclusive. 
```sql
SELECT
  *
FROM
  nobel
WHERE
  yr >= 1980
AND
  yr <= 1989
AND
  subject = 'literature'
```
3.6. **Only Presidents**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show all details of the presidential winners:
* Theodore Roosevelt
* Thomas Woodrow Wilson
* Jimmy Carter
* Barack Obama
```sql
SELECT
  *
FROM
  nobel
WHERE
  winner IN (
      'Theodore Roosevelt',
      'Thomas Woodrow Wilson',
      'Jimmy Carter',
      'Barack Obama'
  )
```
3.7. **John**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the winners with first name John 
```sql
SELECT
  winner
FROM
  nobel
WHERE
  winner LIKE 'John %'
```
3.8. **Chemistry and Physics from different years**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the `year`, `subject`, and `name` of physics winners for 1980 together with the chemistry winners for 1984.
```sql
SELECT
  yr AS "year", subject, winner AS "name"
FROM
  nobel
WHERE
  (subject = 'physics'   AND yr = 1980)
OR
  (subject = 'chemistry' AND yr = 1984)
```
3.9. **Exclude Chemists and Medics**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the `year`, `subject`, and `name` of winners for 1980 excluding chemistry and medicine
```sql
SELECT
  yr AS "year", subject, winner AS "name"
FROM
  nobel
WHERE
  subject NOT IN ('chemistry', 'medicine')
AND
  yr = 1980
```
3.10. **Early Medicine, Late Literature**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show `year`, `subject`, and `name` of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004)
```sql
SELECT
  yr AS "year", subject, winner AS "name"
FROM
  nobel
WHERE
  (yr <  1910 AND subject = 'medicine')
OR
  (yr >= 2004 AND subject = 'literature')
```
3.10. **Umlaut**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Find all details of the prize won by PETER GRÜNBERG
```sql
SELECT
  *
FROM
  nobel
WHERE
  winner = N'Peter Grünberg'
```
3.11. **Apostrophe**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Find all details of the prize won by EUGENE O'NEILL 
```sql
SELECT
  *
FROM
  nobel
WHERE
  winner = 'Eugene O''Neill'
```
3.12. **Knights of the realm**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
List the winners, `year` and `subject` where the `winner` starts with Sir. Show the the most recent first, then by name order.
```sql
SELECT
  winner, yr AS "year", subject
FROM
  nobel
WHERE
  winner LIKE 'Sir%'
ORDER BY yr DESC, winner ASC
```
3.13. **Chemistry and Physics last**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the 1984 winners and `subject` ordered by `subject` and `winner` name; but list chemistry and physics last.
```sql
SELECT 
  winner, 
  subject
FROM
  nobel
WHERE
  yr = '1984'
ORDER BY
  subject IN ('chemistry','physics'), subject, winner;
```
## [4. SELECT withing Select Tutorial](https://sqlzoo.net/wiki/SELECT_within_SELECT_Tutorial)
4.1. **Bigger than Russia**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
List each country name where the population is larger than that of 'Russia'. 
```sql
SELECT
  name
FROM
  world
WHERE
  population > (
    SELECT
      population
    FROM
      world
    WHERE
      name='Russia'
  )
```
4.2. **Richer than UK**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.
```sql
SELECT
  name
FROM
  world
WHERE
  continent = 'Europe'
AND
  (gdp / population) > (
    SELECT
      gdp / population
    FROM
      world
    WHERE
      name = 'United Kingdom'
  )
```
4.3. **Neighbours of Argentina and Australia**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
List the `name` and `continent` of countries in the continents containing either Argentina or Australia. Order by name of the country.
```sql
SELECT
  name, continent
FROM
  world
WHERE
  continent IN (
    SELECT
      continent
    FROM
      world
    WHERE
      name = 'Argentina'
)
OR
  continent IN (
    SELECT
      continent
    FROM
      world
    WHERE
      name = 'Australia'
)
ORDER BY name ASC
```
4.4. **Between Canada and Poland**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Which country has a population that is more than United Kingdom but less than Germany? Show the `name` and the `population`.
```sql
SELECT
  name, population
FROM
  world
WHERE
  population > (
    SELECT
      population
    FROM
      world
    WHERE
      name = 'United Kingdom'
)
AND
  population < (
    SELECT
      population
    FROM
      world
    WHERE
      name = 'Germany'
)
```
4.5. **Percentages of Germany**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the `name` and the `population` of each country in Europe. Show the population as a percentage of the population of Germany.
```sql
SELECT 
  name,
  CONCAT(
    ROUND(
      100 * population / (SELECT population FROM world WHERE name = 'Germany'),
      0
    ),
    '%'
  ) AS percentage
FROM
  world
WHERE
  continent = 'Europe'
```
4.6. **Bigger than every country in Europe**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Which countries have a GDP greater than every country in Europe? 
```sql
SELECT
  name
FROM
  world
WHERE
  gdp > (
    SELECT
      MAX(gdp)
    FROM
      world
    WHERE
      continent = 'Europe'
  )
```
4.7. **Largest in each continent**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Find the largest country (by area) in each continent, show the `continent`, the `name` and the `area`
```sql
SELECT
  continent, name, area
FROM
  world x
WHERE
  area >= ALL (
  SELECT
    area
  FROM
    world y
  WHERE
    y.continent = x.continent
)
```
4.8. **First country of each continent (alphabetically)**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
List each `continent` and the `name` of the country that comes first alphabetically.
```sql
SELECT
  continent, name
FROM
  world x
WHERE name <= ALL(
  SELECT
    name 
  FROM
    world y
  WHERE 
    x.continent = y.continent
)
```
4.9. **Continents with populated countries**<br>
Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show `name`, `continent` and `population`. 
&nbsp;&nbsp;&nbsp;&nbsp;
```sql
SELECT
  name, continent, population
FROM
  world
WHERE 
  continent IN (
  SELECT
    continent
  FROM
    world
  GROUP BY
    continent
  HAVING
    MAX(population) <= 25000000
)
```
4.9. **Three times bigger**<br>
Some countries have populations more than three times that of all of their neighbours (in the same continent). Give the countries and continents.
&nbsp;&nbsp;&nbsp;&nbsp;
```sql
SELECT
  name, continent
FROM
  world x
WHERE
  population > ALL (
    SELECT
      3*population
    FROM
      world y 
    WHERE
      x.continent = y.continent 
    AND
      x.name <> y.name
)
```
## [5. SUM and COUNT](https://sqlzoo.net/wiki/SUM_and_COUNT)
5.1. **Total world population**<br>
Show the total population of the world. 
&nbsp;&nbsp;&nbsp;&nbsp;
```sql
SELECT
  SUM(population) AS "total population of the world"
FROM
  world
```
5.2. **List of continents**<br>
List all the continents - just once each. 
&nbsp;&nbsp;&nbsp;&nbsp;
```sql
SELECT
  DISTINCT(continent)
FROM
  world
```
5.3. **GDP of Africa**<br>
Give the total GDP of Africa 
&nbsp;&nbsp;&nbsp;&nbsp;
```sql
SELECT
  SUM(gdp) AS "GDP of Africa"
FROM
  world
WHERE
  continent = 'Africa'
```
5.4. **Count the big countries**<br>
How many countries have an area of at least 1000000 
&nbsp;&nbsp;&nbsp;&nbsp;
```sql
SELECT
  COUNT(name)
FROM
  world
WHERE
  area > 1000000
```
5.5. **Baltic states population**<br>
What is the total population of ('Estonia', 'Latvia', 'Lithuania') 
&nbsp;&nbsp;&nbsp;&nbsp;
```sql
SELECT
  SUM(population) AS "total population"
FROM
  world
WHERE
  name IN ('Estonia', 'Latvia', 'Lithuania')
```
5.6. **Counting the countries of each continent**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
For each continent show the `continent` and `number of countries`
```sql
SELECT
  continent, COUNT(name) AS "number of countries"
FROM
  world
GROUP BY
  continent
```
5.7. **Counting big countries in each continent**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
For each continent show the continent and number of countries with populations of at least 10 million.
```sql
SELECT
  continent, COUNT(name) AS "number of countries"
FROM
  world
WHERE
  population > 10000000
GROUP BY
  continent
```
5.8. **Counting big continents**<br>
&nbsp;&nbsp;&nbsp;&nbsp;
List the continents that have a total population of at least 100 million.
```sql
SELECT
  continent
FROM
  world
GROUP BY
  continent
HAVING
  SUM(population) > 100000000
```