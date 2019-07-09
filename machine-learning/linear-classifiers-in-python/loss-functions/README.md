# Linear Classifiers in Python

## Chapter 2 : Loss Functions

### Changing the model coefficients
```python
# Set the coefficients
model.coef_ = np.array([[-1,1]])
model.intercept_ = np.array([-3])
```
>>

### Minimizing Loss Function
```python
# The squared error, summed over training examples
def my_loss(w):
    s = 0
    for i in range(y.size):
        # Get the true and predicted target values for example 'i'
        y_i_true = y[i]
        y_i_pred = w@X[i]
        s = s + (y_i_true - y_i_pred)**2
    return s

# Returns the w that makes my_loss(w) smallest
w_fit = minimize(my_loss, X[0]).x
print(w_fit)

# Compare with scikit-learn's LinearRegression coefficients
lr = LinearRegression(fit_intercept=False).fit(X,y)
print(lr.coef_)
```
>>[-9.16299112e-02  4.86754828e-02 -3.77698794e-03  2.85635998e+00
 -2.88057050e+00  5.92521269e+00 -7.22470732e-03 -9.67992974e-01
  1.70448714e-01 -9.38971600e-03 -3.92421893e-01  1.49830571e-02
 -4.16973012e-01]
[-9.16297843e-02  4.86751203e-02 -3.77930006e-03  2.85636751e+00
 -2.88077933e+00  5.92521432e+00 -7.22447929e-03 -9.67995240e-01
  1.70443393e-01 -9.38925373e-03 -3.92425680e-01  1.49832102e-02
 -4.16972624e-01]

### Comparing the logistic and hinge losses
```python
# Mathematical functions for logistic and hinge losses
def log_loss(raw_model_output):
   return np.log(1+np.exp(-raw_model_output))
def hinge_loss(raw_model_output):
   return np.maximum(0,1-raw_model_output)

# Create a grid of values and plot
grid = np.linspace(-2,2,1000)
plt.plot(grid, log_loss(grid), label='logistic')
plt.plot(grid, hinge_loss(grid), label='hinge')
plt.legend()
plt.show()
```
>>![](/img/logistic-loss-and-hinge-loss.png)

### Implementing logistic regression
```python
# The logistic loss, summed over training examples
def my_loss(w):
    s = 0
    for i in range(y.size):
        raw_model_output = w@X[i]
        s = s + log_loss(raw_model_output * y[i])
    return s

# Returns the w that makes my_loss(w) smallest
w_fit = minimize(my_loss, X[0]).x
print(w_fit)

# Compare with scikit-learn's LogisticRegression
lr = LogisticRegression(fit_intercept=False, C=1000000).fit(X,y)
print(lr.coef_)
```
>>[ 1.03592182 -1.65378492  4.08331342 -9.40923002 -1.06786489  0.07892114
 -0.85110344 -2.44103305 -0.45285671  0.43353448]
[[ 1.03731085 -1.65339037  4.08143924 -9.40788356 -1.06757746  0.07895582
  -0.85072003 -2.44079089 -0.45271     0.43334997]]

### 
```python

```
>>
