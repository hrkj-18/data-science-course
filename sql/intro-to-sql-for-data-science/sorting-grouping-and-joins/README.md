# Intro to SQL for Data Science

## Chapter 4 : Sorting, Grouping and Joins

### Sorting columns
```sql
SELECT name
FROM people
ORDER BY name;
```

### GROUP BY 
```sql
SELECT sex, count(*)
FROM employees
GROUP BY sex
ORDER BY count DESC;
```

### HAVING
aggregate functions can't be used in WHERE clauses
```sql
SELECT release_year
FROM films
GROUP BY release_year
WHERE COUNT(title) > 10;

SELECT release_year
FROM films
GROUP BY release_year
HAVING COUNT(title) > 10;
```
