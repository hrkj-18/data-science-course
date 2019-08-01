# Interactive Data Visualization with Bokeh

## Chapter 3 : Building interactive apps with Bokeh

### 
```python
# Perform necessary imports
from bokeh.plotting import figure
from bokeh.io import curdoc

# Create a new plot: plot
plot = figure()

# Add a line to the plot
plot.line([1,2,3,4,5], [2,5,4,6,7])

# Add the plot to the current document
curdoc().add_root(plot)
```
```
bokeh serve script.py
```

### 
```python

```
>>![](img/.png)

### 
```python

```
>>![](img/.png)

### 
```python

```
>>![](img/.png)

### 
```python

```
>>![](img/.png)
