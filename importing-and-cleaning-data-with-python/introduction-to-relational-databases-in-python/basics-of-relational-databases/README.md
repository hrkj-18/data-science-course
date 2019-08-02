# Introduction to Relational Databases in Python

## Chapter 1 : Basics of Relational Databases

### Basic Connections
```python
`from sqlalchemy import create_engine`

`engine = create_engine('sqlite:///db_name.sqlite')`

`print(engine.table_names())`
```
>>Prints all the table names in a list

### Autoloading Tables from a Database
```python
`from sqlalchemy import Table`

#Reflect the census table by using the Table object with the arguments: <br>
#The name of the table as a string ('census'). <br>
#The metadata, contained in the variable metadata. <br>
#autoload=True <br>
#The engine to autoload with - in this case, engine.

`table = Table('table_name', metadata, autoload=True, autoload_with=engine)`

`print(repr(table))`
```
>>Details of the particular table

### Viewing Table Details

```python
`print(table_name.columns)`
```
>>Prints names of columns in a list

The metadata gets created and a metadata.tables dictionary is present which has meta data about all the tables in the database
```python
print(repr(metadata.tables['table_name']))
```
>>Prints mmetadata of the the table table_name

### Selecting data from a Table: raw SQL
```python
`connection = engine.connect()`
`stmt = 'select * from table_name'

`results = connection.execute(stmt).fetchall()`
`print(results)`
```
>>prints the result

### Selecting data from a Table with SQLAlchemy
```python
`from sqlalchemy import select`

`stmt = select([table_name])`
`print(stmt)`
```
>>select * from table_name
```python
print(connection.execute(stmt).fetchall())`
```
>>prints the result
