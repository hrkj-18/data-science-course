# Introduction to Relational Databases in SQL

## Chapter 3 : Uniquely identify records with key constraints

### ADD key CONSTRAINTs to the tables
```sql
-- Rename the organization column to id
ALTER TABLE organizations
RENAME COLUMN organization TO id;

-- Make id a primary key
ALTER TABLE organizations
ADD CONSTRAINT organization_pk PRIMARY KEY (id);
```

### Add a SERIAL surrogate key
```sql
ALTER TABLE professors 
ADD COLUMN id serial;

-- Make id a primary key
ALTER TABLE professors 
ADD CONSTRAINT professors_pkey PRIMARY KEY (id);
```
