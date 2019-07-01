# Unsupervised Learning in Python

## Chapter 2 : Visualization with hierarchical clustering and t-SNE

### Hierarchical clustering of the grain data

```python
# Perform the necessary imports
from scipy.cluster.hierarchy import linkage, dendrogram
import matplotlib.pyplot as plt

# Calculate the linkage: mergings
mergings = linkage(samples, method = 'complete')

# Plot the dendrogram, using varieties as labels
dendrogram(mergings,
           labels=varieties,
           leaf_rotation=90,
           leaf_font_size=6,
)
plt.show()
```
>>![Hierarchical Clustering](/img/hierarchical-clustering.png)

```python
# Perform the necessary imports
import matplotlib.pyplot as plt
from scipy.cluster.hierarchy import linkage, dendrogram

# Calculate the linkage: mergings
mergings = linkage(samples, method = 'complete')

# Plot the dendrogram
dendrogram(mergings,
           labels = country_names,
           leaf_rotation = 90,
           leaf_font_size = 6)
plt.show()
```
>>![Hierarchical Clustering](/img/hierarchical-clustering-with-single-method.png)

### Extracting the cluster labels
```python
# Perform the necessary imports
import pandas as pd
from scipy.cluster.hierarchy import fcluster
from scipy.cluster.hierarchy import linkage, dendrogram
import matplotlib.pyplot as plt

# Use fcluster to extract labels: labels
labels = fcluster(mergings, 6, criterion = 'distance')

dendrogram(mergings,
           labels = varieties,
           leaf_rotation = 90,
           leaf_font_size = 6)
plt.show()

# Create a DataFrame with labels and varieties as columns: df
df = pd.DataFrame({'labels': labels, 'varieties': varieties})

# Create crosstab: cta
ct = pd.crosstab(df['labels'], df['varieties'])

# Display ct
print(ct)
```
>>![Hierarchical Clustering](/img/hierarchical-clustering-and-cross-tabulation.png)

>>|varieties|  Canadian wheat|  Kama wheat|  Rosa wheat|
>>|---|---|---|---|
>>|1|                      14|           3|           0|
>>|2|                       0|           0|          14|
>>|3|                       0|          11|           0|

### t-SNE for 2-dimensional maps

```python
# Import TSNE
from sklearn.manifold import TSNE

# Create a TSNE instance: model
model = TSNE(learning_rate = 200)

# Apply fit_transform to samples: tsne_features
tsne_features = model.fit_transform(samples)

# Select the 0th feature: xs
xs = tsne_features[:,0]

# Select the 1st feature: ys
ys = tsne_features[:,1]

# Scatter plot, coloring by variety_numbers
plt.scatter(xs, ys, c = variety_numbers)
plt.show()
plt.clf()
```
>>
