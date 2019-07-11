1. [Classification]()

```python
from sklearn.neighbors import KNeighborsClassifier
from sklearn import datasets
from sklearn.model_selection import train_test_split

X = digits.data
y = digits.target

# Split the data according to labels using stratify=y
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state=42, stratify=y)

model = KNeighborsClassifier(n_neighbors=7)
model.fit(X_train,y_train)

print(model.score(X_test, y_test))
print(model.predict(X_test[0]))
```

2. [Regression]()
```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.3, random_state=42)

model = LinearRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)

print(model.score(X_test, y_test))
print(mean_squared_error(y_test, y_pred))

```

```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import cross_val_score

model = LinearRegression()

cv_scores = cross_val_score(model,X,y,cv=5)
print(cv_scores)
```

```python
from sklearn.linear_model import Lasso
# Adds the sum of the absolute value of all coefficients multiplied by alpha to the loss function.
model = Lasso(alpha=0.4,normalize=True)

model.fit(X,y)

# Makes umimportant features zero
lasso_coef = model.coef_
print(lasso_coef)
```

```python
from sklearn.linear_model import Ridge
from sklearn.model_selection import cross_val_score

# Adds the sum of the squared value of all coefficients multiplied by alpha to the loss function.
model = Ridge(alpha=0.1, normalize=True)
ridge_cv_scores = cross_val_score(model, X, y, cv=10)
```

3. [Fine-tuning your model]()
```python

```

4. [Preprocessing and pipelines]()
```python

```
