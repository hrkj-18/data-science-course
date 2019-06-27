# Intermediate Python for Data Science

## Chapter 2 : Dictionaries And Pandas

### Dictionaries
```python
my_dict = {
"key1":"value1",
"key2":"value2",
}
```

```python
print(my_dict['key1'])
```
>>value1

```python
my_dict.keys()
```
>>dict_keys(['key2', 'key1'])


```python
my_dict['key3']='value3'
print(my_dict)
```
>>{
>>"key1":"value1",
>>"key2":"value2",
>>"key3":"value3"
>>}

```python
del(my_dict['key3']
print(my_dict)
```
>>{<br>
>>"key1":"value1",<br>
>>"key2":"value2",<br>
>>}<br>
   
### Pandas
```python
names = ['United States', 'Australia', 'Japan', 'India', 'Russia', 'Morocco', 'Egypt']
dr =  [True, False, False, False, True, True, True]
cpc = [809, 731, 588, 18, 200, 70, 45]

my_dict={'country' : names,
'drives_right' : dr,
'cars_per_cap' : cpc}

cars=pd.DataFrame(my_dict)

row_labels = ['US', 'AUS', 'JAP', 'IN', 'RU', 'MOR', 'EG']

print(cars)
```
>>|     |cars_per_cap    |    country | drives_right|
>>|   ---  |   ---   |  ---   |  ---   |
>>|US    |        809 | United States  |        True|
>>|AUS     |      731 |     Australia  |       False|
>>|JAP      |     588  |        Japan   |      False|
>>|IN       |      18 |         India    |     False|
>>|RU     |       200 |        Russia   |       True|
>>|MOR     |       70 |       Morocco   |       True|
>>|EG       |      45  |        Egypt    |      True|

```python
cars=pd.read_csv('cars.csv')
print(cars)
```
>>|  |Unnamed: 0 | cars_per_cap |       country |  drives_right |
>>|---|---|---|---|---|
>>|0 |        US |          809 |  United States |        True |
>>|1 |       AUS |          731 |     Australia  |       False |
>>|2 |       JAP |          588 |         Japan  |       False |
>>|3 |        IN |           18 |         India  |       False |
>>|4 |        RU |          200 |        Russia  |        True |
>>|5 |       MOR |           70 |       Morocco  |        True |
>>|6 |        EG |           45 |         Egypt  |        True |

Specify the index_col argument inside pd.read_csv(): set it to 0, so that the first column is used as row labels.
```python
cars = pd.read_csv('cars.csv',index_col=0)
print(cars)
```
>>|     |cars_per_cap    |    country | drives_right|
>>|   ---  |   ---   |  ---   |  ---   |
>>|US    |        809 | United States  |        True|
>>|AUS     |      731 |     Australia  |       False|
>>|JAP      |     588  |        Japan   |      False|
>>|IN       |      18 |         India    |     False|
>>|RU     |       200 |        Russia   |       True|
>>|MOR     |       70 |       Morocco   |       True|
>>|EG       |      45  |        Egypt    |      True|

*Use single square brackets to print out the country column of cars as a Pandas Series.
*Use double square brackets to print out the country column of cars as a Pandas DataFrame.

```python
# Print out country column as Pandas Series
print(cars['country'])
```
>>| | |
>>|---|---|
>>|US   |    United States|
>>|AUS  |        Australia|
>>|JAP  |            Japan|
>>|IN   |            India|
>>|RU   |           Russia|
>>|MOR  |          Morocco|
>>|EG   |            Egypt|

>>Name: country, dtype: object


```python
# Print out country column as Pandas DataFrame
print(cars[['country']])
```
>>|   |        country|
>>|---|----|
>>|US|   United States|
>>|AUS |     Australia|
>>|JAP |         Japan|
>>|IN |          India|
>>|RU  |        Russia|
>>|MOR  |      Morocco|
>>|EG   |        Egypt|

```python
# Print out DataFrame with country and drives_right columns
print(cars[['country','drives_right']

```
>>|     |      country|  drives_right|
>>|---|---|---|
>>|US|   United States|          True|
>>|AUS|      Australia|         False|
>>|JAP|          Japan|         False|
>>|IN|           India|         False|
>>|RU|          Russia|          True|
>>|MOR|        Morocco|          True|
>>|EG|           Egypt|          True|

#### Slicing
```python
print(cars[3:6])
```
>>|  |   cars_per_cap|  country|  drives_right|
>>|---|--------------|---------|--------------|
>>|IN|             18|    India|         False|
>>|RU|            200|   Russia|          True|
>>|MOR|            70|  Morocco|          True|

#### loc & iloc
```python
print(cars.loc['JAP'])
         OR
print(cars.iloc[2])
```
>>cars_per_cap      588 <br>
>>country         Japan <br>
>>drives_right    False <br>
>>Name: JAP, dtype: object

```python
print(cars.loc[['AUS','EG']])
           OR
print(cars.iloc[[1,6]])
```
>>|  |   cars_per_cap|    country|  drives_right|
>>|---|---|---|---|
>>|AUS|           731|  Australia|         False|
>>|EG|            45|      Egypt|           True|

```python
print(cars.loc['MOR','drives_right'])
```
>>True

```python
print(cars.loc[['RU','MOR'],['country','drives_right']])
```
>>|   |  country|  drives_right|
>>|---|---|---|
>>|RU|    Russia|          True|
>>|MOR|  Morocco|          True|
