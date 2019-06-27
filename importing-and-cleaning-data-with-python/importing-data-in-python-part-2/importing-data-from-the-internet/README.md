# Importing Data in Python (Part 2)

## Chaper 1 : Importing data from the Internet

### Importing flat files from the web
```python
from urllib.request import urlretrieve
import pandas as pd

url='https://s3.amazonaws.com/assets.datacamp.com/production/course_1606/datasets/winequality-red.csv'
urlretrieve(url,'winequality-red.csv')`
```
>>Saves the data locally in 'winequality-red.csv'

### Importing non-flat files from the web
```python
# Import package
import pandas as pd

url='http://s3.amazonaws.com/assets.datacamp.com/course/importing_data_into_r/latitude.xls'
xl=pd.read_excel(url,sheetname=None)

print(xl.keys())
```
>>dict_keys(['1700', '1900'])

```python
from urllib.request import urlopen, Request
url = "http://www.datacamp.com/teach/documentation"

request=Request(url)
response=urlopen(request)

print(type(response))
response.close()
```
>><class 'http.client.HTTPResponse'>

```python
html_doc = response.read()
print(html_doc)
```
>>HTML Code of the url

### Using requests
```python
import requests
url="http://www.datacamp.com/teach/documentation"

r=requests.get(url)

html_doc=r.text
print(html_doc)
```
>> Whole HTML code

### BeautifulSoup
```python
from bs4 import BeautifulSoup
soup=BeautifulSoup(html_doc)

pretty_soup=soup.prettify()
print(pretty_soup)
```

```python
guido_title=soup.title
print(guido_title)
```
>><title> Some title of the page </title>

```python
guido_text=soup.get_text()
print(guido_text)
```
>>All the text in the web page

```python
a_tags=soup.find_all('a')

for link in a_tags:
    print(link.get('href'))
```
>>All the links in web page without the a tag
