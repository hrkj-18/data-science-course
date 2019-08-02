# Introduction to Databases in Python
 
## Chapter 3 : Advanced SQLAlchemy Queries

### Calculating Values in a Query

### Calculating a Difference between Two Columns

```python
# Build query to return state names by population difference from 2008 to 2000: stmt
stmt = select([census.columns.state, (census.columns.pop2008-census.columns.pop2000).label('pop_change')])

# Append group by for the state: stmt_grouped
stmt_grouped = stmt.group_by(census.columns.state)

# Append order by for pop_change descendingly: stmt_ordered
stmt_ordered = stmt_grouped.order_by(desc('pop_change'))

# Return only 5 results: stmt_top5
stmt_top5 = stmt_ordered.limit(5)

# Use connection to execute stmt_top5 and fetch all results
results = connection.execute(stmt_top5).fetchall()

# Print the state and population change for each record
for result in results:
    print('{}:{}'.format(result.state, result.pop_change))
```
>>California:105705 <br>
>>Florida:100984 <br>
>>Texas:51901 <br>
>>New York:47098 <br>
>>Pennsylvania:42387 <br>

### Determining the Overall Percentage of Females
```python
# import case, cast and Float from sqlalchemy
from sqlalchemy import case, cast, Float

# Build an expression to calculate female population in 2000
female_pop2000 = func.sum(
    case([
        (census.columns.sex == 'F', census.columns.pop2000)`
    ], else_=0))

# Cast an expression to calculate total population in 2000 to Float
total_pop2000 = cast(func.sum(census.columns.pop2000), Float)

# Build a query to calculate the percentage of females in 2000: stmt
stmt = select([female_pop2000 / total_pop2000* 100])

# Execute the query and store the scalar result: percent_female
percent_female = connection.execute(stmt).scalar()

# Print the percentage
print(percent_female)
```
>>51.0946743229

### Automatic Joins with an Established Relationship
If you have two tables that already have an established relationship, you can automatically use that relationship by just adding the columns we want from each table to the select statement.

```python
stmt = select([census.columns.pop2000, state_fact.columns.abbreviation])

# Execute the statement and get the first result: result
results = connection.execute(stmt).fetchmany(5)

# Loop over the keys in the result object and print the key and value
for result in results:
    for key in result.keys():
        print(key, getattr(result, key))
    
print(results)
```
>>pop2000 89600 <br>
>>abbreviation IL <br>
>>pop2000 89600 <br>
>>abbreviation NJ <br>
>>pop2000 89600 <br>
>>abbreviation ND <br>
>>pop2000 89600 <br>
>>abbreviation OR <br>
>>pop2000 89600 <br>
>>abbreviation DC <br>
>>[(89600, 'IL'), (89600, 'NJ'), (89600, 'ND'), (89600, 'OR'), (89600, 'DC')]

### Joins

census
>>['state', 'sex', 'age', 'pop2000', 'pop2008']

state_fact
>>['id', 'name', 'abbreviation', 'country', 'type', 'sort', 'status', 'occupied', 'notes', 'fips_state', 'assoc_press', 'standard_federal_region', 'census_region', 'census_region_name', 'census_division', 'census_division_name', 'circuit_court']

```python
stmt = select([census, state_fact])

# Add a select_from clause that wraps a join for the census and state_fact
# tables where the census state column and state_fact name column match
stmt_join = stmt.select_from(
    census.join(state_fact, census.columns.state == state_fact.columns.name))

# Execute the statement and get the first result: result
result = connection.execute(stmt_join).first()
```
>>first row of the whole joined table

### Using alias to handle same table joined queries
Often, you'll have tables that contain hierarchical data, such as employees and managers who are also employees. For this reason, you may wish to join a table to itself on different columns. The .alias() method, which creates a copy of a table, helps accomplish this task. Because it's the same table, you only need a where clause to specify the join condition.

### Working on Blocks of Records

```python
# Start a while loop checking for more results
while more_results:
    # Fetch the first 50 results from the ResultProxy: partial_results
    partial_results = results_proxy.fetchmany(50)

    # if empty list, set more_results to False
    if partial_results == []:
        more_results = False

    # Loop over the fetched records and increment the count for the state
    for row in partial_results:
        if row.state in state_count:
            state_count[row.state] += 1
        else:
            state_count[row.state] = 1

# Close the ResultProxy, and thus the connection
results_proxy.close()

# Print the count by state
print(state_count)
```
