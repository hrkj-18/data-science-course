# Importing Data in Python (Part 2)

## Chaper 2 : Interacting with APIs to import data from the web

### Importing JSONs

```python
import json
`with open("a_movie.json") as json_file:
    `json_data=json.load(json_file)

`for k in json_data.keys():
    `print(k + ': ', json_data[k])
```
>>prints the whole dictionary

### APIs
```python
import requests
url='http://www.omdbapi.com/?apikey=72bc447a&t=the+social+network'

r = requests.get(url)
print(r.text)
```
>>Prints the whole file

```python
url = 'http://www.omdbapi.com/?apikey=72bc447a&t=social+network'
r=requests.get(url)

json_data=r.json()

for k in json_data.keys():
    print(k + ': ', json_data[k])
```
>>prints whole dict
