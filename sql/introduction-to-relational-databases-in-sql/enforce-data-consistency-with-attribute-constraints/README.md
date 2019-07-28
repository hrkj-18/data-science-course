# Introduction to Relational Databases in SQL

## Chapter 2 : Enforce data consistency with attribute constraints

### Type CASTs
```sql
-- Calculate the net amount as amount + fee
SELECT transaction_date, amount + CAST(fee AS integer) AS net_amount 
FROM transactions;
```

### Change types with ALTER COLUMN
```sql
-- Specify the correct fixed-length character type
ALTER TABLE professors
ALTER COLUMN university_shortname
TYPE char(3);
```

### Convert types USING a function
```sql
-- Convert the values in firstname to a max. of 16 characters
ALTER TABLE professors 
ALTER COLUMN firstname 
TYPE varchar(16) 
USING SUBSTRING(firstname FROM 1 FOR 16);
```

### Disallow NULL values with SET NOT NULL
```sql
-- Disallow NULL values in firstname
ALTER TABLE professors 
ALTER COLUMN firstname SET NOT NULL;
```

### Make your columns UNIQUE with ADD CONSTRAINT
```sql
CREATE TABLE table_name (
 column_name UNIQUE
);

-- Make universities.university_shortname unique
ALTER TABLE universities
ADD CONSTRAINT university_shortname_unq UNIQUE(university_shortname);
```
