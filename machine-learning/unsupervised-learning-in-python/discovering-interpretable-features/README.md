# Unsupervised Learning in Python

## Chapter 4 : Discovering interpretable features

### Non-negative matrix factorization (NMF)

### NMF applied to Wikipedia articles
```python
# Import NMF
from sklearn.decomposition import NMF

# Create an NMF instance: model
model = NMF(n_components=6)

# Fit the model to articles
model.fit(articles)

# Transform the articles: nmf_features
nmf_features = model.transform(articles)

# Print the NMF features
print(nmf_features)
```
>>[[0.00000000e+00 0.00000000e+00 0.00000000e+00 0.00000000e+00
  0.00000000e+00 4.40623130e-01]
 [0.00000000e+00 0.00000000e+00 0.00000000e+00 0.00000000e+00
  0.00000000e+00 5.66807830e-01]
 [3.82006369e-03 0.00000000e+00 0.00000000e+00 0.00000000e+00
  0.00000000e+00 3.98789405e-01]]

### NMF features of the Wikipedia articles
```python
# Import pandas
import pandas as pd

# Create a pandas DataFrame: df
df = pd.DataFrame(nmf_features, index=titles)

# Print the row for 'Anne Hathaway'
print(df.loc['Anne Hathaway'])

# Print the row for 'Denzel Washington'
print(df.loc['Denzel Washington'])
```
>>0    0.003845
1    0.000000
2    0.000000
3    0.575711
4    0.000000
5    0.000000
Name: Anne Hathaway, dtype: float64
0    0.000000
1    0.005601
2    0.000000
3    0.422380
4    0.000000
5    0.000000
Name: Denzel Washington, dtype: float64

### NMF learns topics of documents
```python
# Import pandas
import pandas as pd

# Create a DataFrame: components_df
components_df = pd.DataFrame(model.components_, columns=words)

# Print the shape of the DataFrame
print(components_df.shape)

# Select row 3: component
component = components_df.iloc[3]

# Print result of nlargest
print(component.nlargest())

```
>>    (6, 13125)
    film       0.627877
    award      0.253131
    starred    0.245284
    role       0.211451
    actress    0.186398
    Name: 3, dtype: float64

### Explore the LED digits dataset
```python

```
>>


### 
```python

```
>>

### 
```python

```
>>

### 
```python

```
>>

### 
```python

```
>>


### 
```python

```
>>

### 
```python

```
>>

### 
```python

```
>>

### 
```python

```
>>


### 
```python

```
>>

### 
```python

```
>>

### 
```python

```
>>

### 
```python

```
>>
