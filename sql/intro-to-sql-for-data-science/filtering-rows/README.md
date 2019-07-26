# Intro to SQL for Data Science

## Chapter 2 : Filtering Rows

### Simple filtering
```sql
SELECT *
FROM films
WHERE release_year = 2016;
```
>>

### WHERE AND
```sql
SELECT title, release_year
FROM films
WHERE release_year < 2000
AND language = 'Spanish';
```
>>

### BETWEEN
```sql
SELECT title, release_year
FROM films
WHERE release_year BETWEEN 1990 AND 2000
AND budget > 100000000
AND language = 'Spanish';
```
>>

### WHERE IN
```sql
SELECT name
FROM kids
WHERE age = 2
OR age = 4
OR age = 6
OR age = 8
OR age = 10;

SELECT name
FROM kids
WHERE age IN (2, 4, 6, 8, 10);
```
>>

### NULL and IS NULL
```sql
SELECT COUNT(*)
FROM films
WHERE language IS NULL;
```
>>

### LIKE and NOT LIKE
Get the names of all people whose names begin with 'B'. The pattern you need is 'B%'
```sql
SELECT name
FROM people
WHERE name LIKE 'B%';
```

Get the names of people whose names have 'r' as the second letter. The pattern you need is '_r%'.
```sql
SELECT name
FROM people
WHERE name LIKE '_r%';
```

Get the names of people whose names don't start with A. The pattern you need is 'A%'
```sql
SELECT name
FROM people
WHERE name NOT LIKE 'A%';
```
