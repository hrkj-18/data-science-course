# Introduction to Relational Databases in Python

## Chapter 4 : Creating and Manipulating your own Databases

### Creating Tables with SQLAlchemy

```python
from sqlalchemy import Table, Column, String, Integer, Float, Boolean

# Define a new table with a name, count, amount, and valid column: data
data = Table('data', metadata,
             Column('name', String(255), unique=True),
             Column('count', Integer(), default=1),
             Column('amount', Float()),
             Column('valid', Boolean(), default=False)
)

# Use the metadata to create the table
metadata.create_all(engine)

# Print table details
print(repr(data))
```
>>Table('data', MetaData(bind=None), Column('name', String(length=255), table=<data>), Column('count', Integer(), table=<data>), Column('amount', Float(), table=<data>), Column('valid', Boolean(), table=<data>), schema=None)

### Inserting Data in Database

```python
insert_stmt = insert(table_name).values(column_name1='Value1'....)
```

### Inserting multiple values at once

```python
values_list = [
    {'name': 'Anna', 'count': 1, 'amount': 1000.00, 'valid': True},
    {'name': 'Taylor', 'count': 1, 'amount': 750.00, 'valid': False}
]
stmt = insert(data)

results = connection.execute(stmt, values_list)
```

### Loading a csv in a table

```python
stmt = insert(census)

# Create an empty list and zeroed row count: values_list, total_rowcount
values_list = []
total_rowcount = 0

# Enumerate the rows of csv_reader
for idx, row in enumerate(csv_reader):
    #create data and append to values_list
    data = {'state': row[0], 'sex': row[1], 'age': row[2], 'pop2000': row[3],
            'pop2008': row[4]}
    values_list.append(data)

    # Check to see if divisible by 51 done to load 50 at 
    # time due to memory
    if idx % 51 == 0:
        results = connection.execute(stmt, values_list)
        total_rowcount += results.rowcount
        values_list = []
```
### Updating Individual & Multiple records

```python
stmt = update(table_name).values(column_name = value)

stmt = stmt.where(table_name.columns.column_name == value)
```
### Removing Data From a Database

### Deleting all the records from a table

```python
from sqlalchemy import delete
stmt = delete(census)
results = connection.execute(stmt)
```

### Deleting specific records

```python
stmt = delete(table_name)
stmt_del = stmt_del.where(
    `and_(if_any)
)
```

### Deleting a Table Completely

```python
# Drop the table_name tables
table_name.drop(engine)

# Check to see if table_name exists
print(table_name.exists(engine))
```

```python
# Drop all tables
metadata.drop_all(engine)

# Check to see if table_name exists
print(table_name.exists(engine))
