# Importing Data in Python (Part 1)

## Chapter 3 : Working with relational databases in Python

### Creating a database engine in Python

```python
from sqlalchemy import create_engine
engine=create_engine('sqlite:///Chinook.sqlite')
table_names=engine.table_names()
print(table_names)
```
>>['Album', 'Artist', 'Customer', 'Employee', 'Genre', 'Invoice', 'InvoiceLine', 'MediaType', 'Playlist', 'PlaylistTrack', 'Track']

```python
from sqlalchemy import create_engine
import pandas as pd

engine = create_engine('sqlite:///Chinook.sqlite')

con=engine.connect()
rs = con.execute('select * from Album')

df = pd.DataFrame(rs)

con.close()

print(df.head())
```
>>| |  0|                                      1|  2|
>>|---|---|---|---|
>>|0|  1|  For Those About To Rock We Salute You|  1|
>>|1|  2|                      Balls to the Wall|  2|
>>|2|  3|                      Restless and Wild|  2|
>>|3|  4|                      Let There Be Rock|  1|
>>|4|  5|                               Big Ones|  3|

```python
with engine.connect() as con:
    rs = con.execute('select LastName, Title from Employee')
    df = pd.DataFrame(rs.fetchmany(3))
    df.columns = rs.keys()

print(len(df))
print(df.head())
```
>>| | LastName|                Title|
>>|---|---|---|
>>|0|    Adams|      General Manager|
>>|1|  Edwards|        Sales Manager|
>>|2|  Peacock|  Sales Support Agent|

### SQL Queries using Pandas
Previous block of code is same as this
```python
engine=create_engine('sqlite:///Chinook.sqlite')
df = pd.read_sql_query('select * from Album', engine)
```
