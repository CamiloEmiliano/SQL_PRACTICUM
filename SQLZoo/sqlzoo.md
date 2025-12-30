## Sections
1. [SELECT basics](#1-select-basics)
## [1. SELECT basics](https://sqlzoo.net/wiki/SELECT_basics)

1.1. Show the population of Germany.
```sql
SELECT
   population
FROM
  world
WHERE
    name = 'Germany'
```

1.2. Show the name and the population for 'Sweden', 'Norway', and 'Denmark'.
```sql
SELECT
  name, population
FROM
   world
WHERE
  name IN ('Sweden', 'Norway', 'Denmark');
```