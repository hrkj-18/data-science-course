# Intro to SQL for Data Science

## Chapter 3 : Aggregate Functions

### SUM, AVG, MIN, MAX
```sql
SELECT SUM(duration)
FROM films;

SELECT AVG(duration)
FROM films;

SELECT MIN(duration)
FROM films;

SELECT MAX(duration)
FROM films;
```

### Combining aggregate functions with WHERE
to get the total budget of movies made in the year 2010 or later
```sql
SELECT SUM(budget)
FROM films
WHERE release_year >= 2010;
```
>>

### AS
```sql
SELECT MAX(budget) AS max_budget,
       MAX(duration) AS max_duration
FROM films;
```
