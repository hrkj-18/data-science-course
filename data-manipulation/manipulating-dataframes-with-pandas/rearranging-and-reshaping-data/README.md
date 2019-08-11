# Manipulating dataframes with Pandas

## Chapter 3 : Rearranging and Reshaping Data

###
```python
print(users)
```
>>  weekday    city  visitors  signups
>>0     Sun  Austin       139        7
>>1     Sun  Dallas       237       12
>>2     Mon  Austin       326        3
>>3     Mon  Dallas       456        5


```python
# Pivot the users DataFrame: visitors_pivot
visitors_pivot = users.pivot(index='weekday', columns='city', values='visitors')

# Print the pivoted DataFrame
print(visitors_pivot)
```
>>city     Austin  Dallas
>>weekday                
>>Mon         326     456
>>Sun         139     237


```python
# Pivot users with signups indexed by weekday and city: signups_pivot
signups_pivot = users.pivot(index='weekday', columns='city', values='signups')

# Print signups_pivot
print(signups_pivot)
```
>>city     Austin  Dallas
>>weekday                
>>Mon           3       5
>>Sun           7      12


```python
# Pivot users pivoted by both signups and visitors: pivot
pivot = users.pivot(index='weekday', columns='city')

# Print the pivoted DataFrame
print(pivot)
```
>>        visitors        signups       
>>city      Austin Dallas  Austin Dallas
>>weekday                               
>>Mon          326    456       3      5
>>Sun          139    237       7     12


### Stacking & unstacking DataFrames
```python
print(users)
```
>>                visitors  signups
>>city   weekday                   
>>Austin Mon           326        3
>>       Sun           139        7
>>Dallas Mon           456        5
>>       Sun           237       12

```python
# Unstack users by 'weekday': byweekday
byweekday = users.unstack(level='weekday')

# Print the byweekday DataFrame
print(byweekday)
```
>>        visitors      signups    
weekday      Mon  Sun     Mon Sun
city                             
Austin       326  139       3   7
Dallas       456  237       5  12

```python
# Stack byweekday by 'weekday' and print it
print(byweekday.stack(level='weekday'))
```
>>                visitors  signups
>>city   weekday                   
>>Austin Mon           326        3
>>       Sun           139        7
>>Dallas Mon           456        5
>>       Sun           237       12


###
```pthon
bycity = users.unstack(level='city')

# Print the bycity DataFrame
print(bycity)
```
>>        visitors        signups       
>>city      Austin Dallas  Austin Dallas
>>weekday                               
>>Mon          326    456       3      5
>>Sun          139    237       7     12

###
```pthon
# Stack bycity by 'city' and print it
print(bycity.stack(level='city'))
```
>>                visitors  signups
>>weekday city                     
>>Mon     Austin       326        3
>>        Dallas       456        5
>>Sun     Austin       139        7
>>        Dallas       237       12

### Rstoring the index order
```pthon
# Stack 'city' back into the index of bycity: newusers
newusers = bycity.stack(level='city')

# Swap the levels of the index of newusers: newusers
newusers = newusers.swaplevel(0, 1)

# Print newusers and verify that the index is not sorted
print(newusers)
```
>>                visitors  signups
>>city   weekday                   
>>Austin Mon           326        3
>>Dallas Mon           456        5
>>Austin Sun           139        7
>>Dallas Sun           237       12

```pthon
# Sort the index of newusers: newusers
newusers = newusers.sort_index()

# Print newusers and verify that the index is now sorted
print(newusers)
```
>>                visitors  signups
>>city   weekday                   
>>Austin Mon           326        3
>>       Sun           139        7
>>Dallas Mon           456        5
>>       Sun           237       12

```pthon
print(newusers.equals(users))
```
>>True

###
```pthon
print(visitors_by_city_weekday)
```
>>city     Austin  Dallas
weekday                
Mon         326     456
Sun         139     237

###
```pthon
# Reset the index: visitors_by_city_weekday
visitors_by_city_weekday = visitors_by_city_weekday.reset_index() 

# Print visitors_by_city_weekday
print(visitors_by_city_weekday)
```
>>city weekday  Austin  Dallas
0        Mon     326     456
1        Sun     139     237

###
```pthon
# Melt visitors_by_city_weekday: visitors
visitors = pd.melt(visitors_by_city_weekday, id_vars=['weekday'], value_name='visitors')

# Print visitors
print(visitors)
```
>>  weekday    city  visitors
0     Mon  Austin       326
1     Sun  Austin       139
2     Mon  Dallas       456
3     Sun  Dallas       237

###
```pthon
print(users)
```
>>  weekday    city  visitors  signups
0     Sun  Austin       139        7
1     Sun  Dallas       237       12
2     Mon  Austin       326        3
3     Mon  Dallas       456        5

###
```pthon
# Melt users: skinny
skinny = pd.melt(users, id_vars=['weekday' ,'city'])

# Print skinny
print(skinny)
```
>>  weekday    city  variable  value
0     Sun  Austin  visitors    139
1     Sun  Dallas  visitors    237
2     Mon  Austin  visitors    326
3     Mon  Dallas  visitors    456
4     Sun  Austin   signups      7
5     Sun  Dallas   signups     12
6     Mon  Austin   signups      3
7     Mon  Dallas   signups      5

### Obtaining key-value pairs with melt()
```pthon
# Set the new index: users_idx
users_idx = users.set_index(['city', 'weekday'])

# Print the users_idx DataFrame
print(users_idx)
```
>>                visitors  signups
city   weekday                   
Austin Sun           139        7
Dallas Sun           237       12
Austin Mon           326        3
Dallas Mon           456        5

###
```pthon
# Obtain the key-value pairs: kv_pairs
kv_pairs = pd.melt(users_idx, col_level=0)

# Print the key-value pairs
print(kv_pairs)
```
>>   variable  value
0  visitors    139
1  visitors    237
2  visitors    326
3  visitors    456
4   signups      7
5   signups     12
6   signups      3
7   signups      5

### Setting up a pivot table
```pthon
print(users)
```
>>  weekday    city  visitors  signups
0     Sun  Austin       139        7
1     Sun  Dallas       237       12
2     Mon  Austin       326        3
3     Mon  Dallas       456        5

```python
# Create the DataFrame with the appropriate pivot table: by_city_day
by_city_day = users.pivot_table(index='weekday', columns='city')

# Print by_city_day
print(by_city_day)
```
>>        signups        visitors       
city     Austin Dallas   Austin Dallas
weekday                               
Mon           3      5      326    456
Sun           7     12      139    237


### 
```python
# Use a pivot table to display the count of each column: count_by_weekday1
count_by_weekday1 = users.pivot_table(index='weekday', aggfunc='count')

# Print count_by_weekday
print(count_by_weekday1)
```
>>         city  signups  visitors
weekday                         
Mon         2        2         2
Sun         2        2         2


### 
```python
# Replace 'aggfunc='count'' with 'aggfunc=len': count_by_weekday2
count_by_weekday2 = users.pivot_table(index='weekday', aggfunc=len)

# Verify that the same result is obtained
print(count_by_weekday1.equals(count_by_weekday2))
```
>>True


### 
```python
# Add in the margins: signups_and_visitors_total 
signups_and_visitors_total = users.pivot_table(index='weekday', aggfunc=sum, margins=True)

# Print signups_and_visitors_total
print(signups_and_visitors_total)
```
>>         signups  visitors
weekday                   
Mon            8       782
Sun           19       376
All           27      1158
