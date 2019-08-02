# Introduction to Databases in Python

## Chapter 2 : Applying Filtering, Ordering and Grouping to Queries

### Filtering and Targeting Data

### Connecting to a PostgreSQL Database

```python
`engine = create_engine('postgresql+psycopg2://path')`
```

### Filter data selected from a Table - Simple

```python
`stmt = select([table_name])`

`stmt = stmt.where(table_name.columns.column_name==conditon')`
`results = connection.execute(stmt).fetchall()`
```

### Ordering by a Single Column

```python
`stmt = select([table_name.columns.column_name]).order_by(table_name.columns.column_name)`
```

### Ordering in Descending Order by a Single Column

```python
`stmt.order_by(desc(table_name.columns.column_name))`
```

### Counting, Summing and Grouping Data

### Counting Distinct Data

A method called .scalar() for getting just the value of a query that returns only one row and column.

```python
`stmt = select([func.count(table_name.columns.column_name)])`

`count = connection.execute(stmt).scalar()`
```

Furthermore, if you only want to count the distinct values of pop2008, you can use the .distinct() method:

```python
`stmt = select([func.count(table_name.columns.column_name.distinct())])`
```

```python
`stmt = stmt.group_by(table_name.columns.column_name)`
```
