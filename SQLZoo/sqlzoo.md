## Sections
1. [SELECT basics](#1-select-basics)
2. [SELECT FROM world](#2-select-from-world)

## [1. SELECT basics](https://sqlzoo.net/wiki/SELECT_basics)
1.1. Introducing the `world` table of countries<br>
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
1.2. Scandinavia<br>
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
1.3. Just the right size<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the country and area for countries with an area between 200,000 and 250,000.
```sql
SELECT
  name, area
FROM world
  WHERE area BETWEEN 200000 AND 250000
```
## [2. SELECT from world](https://sqlzoo.net/wiki/SELECT_name)
2.1. Introduction<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the name, continent and population of all countries
```sql
SELECT
  name, continent, population
FROM
  world
```
2.2. Large Countries<br>
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
2.3. Per capita GDP<br>
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
2.4. South America in millions<br>
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
2.5. France, Germany, Italy<br>
&nbsp;&nbsp;&nbsp;&nbsp;
Show the name and population for France, Germany, Italy 
```sql
SELECT
  name, population
FROM
  world
WHERE
  name IN ('France', 'Germany' ,'Italy')
```