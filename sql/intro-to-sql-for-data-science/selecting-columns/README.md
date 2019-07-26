# Intro to SQL for Data Science

## Chapter 1 : Selecting Columns

### SELECTing single columns
```sql
SELECT title FROM films
SELECT title, release_year FROM films
SELECT * FROM films
```
>>Gives only title column<br>Gives title and release_year column<br>Gives all columns

### SELECT DISTINCT
```sql
SELECT DISTINCT role FROM roles;
```
>>Gives the distinct elements

### Practice with COUNT
```sql
SELECT COUNT(*)
FROM people;
```
>>Gives the number of objects
