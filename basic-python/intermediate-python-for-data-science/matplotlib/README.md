# Intermediate Python for Data Science

## Chapter 1 : Matplotlib

### Matplotlib
```python
import matplotlib.pyplot as plt
plt.plot(x,y)
plt.show()
```
>>![Matplotlib Example](/img/matplotlib-example.png)

### ScatterPlot
```python
import matplotlib.pyplot as plt
plt.scatter(x,y)

plt.show()
```
>>![Scatterplot Example](/img/scatterplot.png)

### Histograms
```python
plt.hist(x,y) #y is numbe of bins
plt.show()
```
>>![Histogram Example](/img/histogram-example.png)

### Labels
```python
plt.scatter(x,y)

xlab = 'Description of X Axis'
ylab = 'Description of Y Axis'
title = 'Title of the Plot'

plt.xlabel(xlab)
plt.ylabel(ylab)

plt.title(title)

plt.show()
```
>>![Labels on a Scatterplot](/img/labels-example.png)

### Ticks
```python
tick_val = [1000,10000,100000]
tick_lab = ['1k','10k','100k']

plt.xticks(tick_val,tick_lab)
```
>>![Ticks](/img/ticks-plot-example.png)

### Size
```python
plt.scatter(x,y,s=number or list)
```

### Colors
```python
plt.scatter(x,y,c=color or list or dict,alpha=0-1)
```

### Aditional Customizations
```python
plt.text(x,y,'text')

plt.grid(True) # to add a grid
```
