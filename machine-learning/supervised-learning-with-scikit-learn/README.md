1. [Classification]()

```python
from sklearn.neighbors import KNeighborsClassifier
from sklearn import datasets
from sklearn.model_selection import train_test_split

X = digits.data
y = digits.target

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state=42, stratify=y)

knn = KNeighborsClassifier(n_neighbors=7)
knn.fit(X_train,y_train)

print(knn.score(X_test, y_test))

print(knn.predict(X_test[0]))
```

2. [Regression]()
3. [Fine-tuning your model]()
4. [Preprocessing and pipelines]()
