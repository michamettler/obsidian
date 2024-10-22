#machinelearning #sem5 

https://phonosync.github.io/mldm-notes/05_logistic_regression.html
## Logistic Regression
We will now introduce a different supervised learning problem, namely **classification**. As with regression, the training data comes in pairs. In contrast to regression, the target values $y$ belong to a _finite_ set. In **binary classification**, we typically call one class “positive” and the other class “negative” – how you name these is up to you.
## Logistic Regression
Like [[Linear Regression]], a logistic regression model has a parameter vector $\theta_0$. Once it is trained (and we will describe how training works momentarily), you can apply it to a (unidimensional) input $x$ as follows:
$$\hat{y} = h_\theta(x) = g(\theta_0+ \theta_1 x) = \frac{1}{1 + e^{-(\theta_0 + \theta_1 x)}}$$
There is also a straightforward multidimensional generalization: If x is a vector of numbers, then
$$\hat{y} = h_{\boldsymbol{\theta(x)}} = g({\boldsymbol{\theta}}^T \boldsymbol{x}) = \frac{1}{1 + e^{-{\boldsymbol{\theta}}^T \boldsymbol{x}}}$$
where $\boldsymbol{\theta}^T \boldsymbol{x} = \theta_0 x_0 + \theta_1 x_1 + ... + \theta_n x_n$. Here, as in the multivariate linear regression, x is a vector consisting of $x_0, x_1, x_2, ...$ and $x_0=1$, which enables the vector representation of the parameters $\theta_0$. In other words, to compute the prediction $\hat{y}$ for an input $x$, we must:

1. Compute the scalar product between the parameter vector  $\theta_0$ and the input vector $x$.
2. Pass the resulting scalar product to the logistic function

The particular value $\hat{y}$ that you obtain also gives you a sense of how _confident_ the machine is about its judgment.  
$\hat{y}>0.95$ or $\hat{y}<0.05$ would be considered “confident” whereas $0.4 < \hat{y} < 0.6$ would be considered “not confident”.
![[Pasted image 20241007164412.png#invert]]
## Training
In contrast to linear regression, there is no “normal equation” to find the optimal parameter $\theta_0$ in closed form. Instead, we have to use an iterative method such as gradient descent. For the cost function, instead of residual sum of squares (RSS), we will use a new function called the “log loss”:
$$\textrm{Loss}(h_\theta(x), y) = \begin{cases}-\log(h_\theta(x)) & \quad \textrm{if}\quad y=1 \\
                                            -\log(1 - h_\theta(x)) & \quad \textrm{if}\quad y=0 \end{cases}$$
This is often written instead as:
$$\textrm{Loss}(h_\theta(x), y) = -y \log(h_\theta(x)) - (1 - y) \log(1 - h_\theta(x))$$
With the probabilistic interpretation, it can be also written as:
$$\textrm{Log-Loss} = -y \log(p) - (1 - y) \log(1 - p)$$
![[Pasted image 20241007165054.png#invert]]
Taking the average log-loss over all examples in the training set, we arrive at the cost function
$$J(\theta) = \frac{1}{M} \sum_{m=1}^M \textrm{Loss}(h_\theta(x^{(m)}), y^{(m)})$$
This then gives rise to the gradient descent algorithm for logistic regression:

1. Initialize (randomly): $\theta_0$, $\theta_1$
2. Repeat until convergence:
$$\text{Update} \: \theta_0 = \theta_0 - \alpha \frac{1}{M} \sum_{m=1}^{M}(h_{\theta}(x^{(m)}) - y^{(m)})$$
$$\text{Update} \: \theta_1 = \theta_1 - \alpha \frac{1}{M} \sum_{m=1}^{M}(h_{\theta}(x^{(m)}) - y^{(m)})x^{(m)} \tag{5.3}$$
Here, $h_\theta(x_m)$ is the output $\hat{y}$ (a real number between 0 and 1) of the logistic regress-or.
### Python Example
```python
import numpy as np
import sklearn.linear_model

# Cholesterol levels of patients; need to ensure X is (M x 1) matrix.
X = np.atleast_2d([ 100, 233, 150, 280, 80, 320, 135, 93, 224, 178 ]).T
# Labels of whether they had heart pain in the next year
y = np.array([ 0, 1, 1, 1, 0, 1, 1, 0, 1, 0 ])

# Train model
logr = sklearn.linear_model.LogisticRegression()
logr.fit(X, y)

# We must pack the input x into a 2-d array of size (M x 1). Here, M=1.
yhat = logr.predict([ [ 190 ] ])  # gives 0/1 binary prediction
yhat_prob = logr.predict_proba([ [ 190 ] ])  # gives probabilistic prediction
print(yhat, yhat_prob)


# Example Lab
import sklearn.linear_model

trainingAccuracies = []
testingAccuracies = []
Mvalues = np.arange(100, 2001, 100)

for M in Mvalues:
  logisticRegressor = sklearn.linear_model.LogisticRegression(max_iter=500)
  logisticRegressor.fit(trainingFaces[:M,:], trainingLabels[:M])
  
  trainingAccuracies.append(logisticRegressor.score(trainingFaces[:M,:], trainingLabels[:M]))
  testingAccuracies.append(logisticRegressor.score(testingFaces, testingLabels))

plt.plot(Mvalues, trainingAccuracies)
plt.plot(Mvalues, testingAccuracies)
plt.legend([ "Training", "Testing" ])
plt.show()
```
### Hyperparameter
A _hyperparameter_ is any variable that can influence the _training process_ but that is _not_ contained in the model itself; after the training has finished, the hyperparameters no longer have any relevance. The most common hyperparameters are the learning rate α and the number of gradient descent iterations.
#### Hyperparameter Optimization
[[Data Partitioning]]
- **Training Set**: Given a fixed value of your hyperparameters $\alpha = 0.1$, this is the dataset $\{(x^{(m)},y^{(1)}),\ldots,(x^{(M)},y^{(M)})\}$ you use to optimize the model’s parameters (e.g. the parameters θ in gradient descent).
- **Validation Set (also called Development Set)**: this is the dataset that you use to measure how good the model for the _particular_ choice of hyperparameters is, i.e., give the model that you trained on the training set for $\alpha = 0.01$, you compute the _validation accuracy_ of this model on the validation set. Typically, you iterate over many choices for the hyperparameters, measure how good each choice is on the validation set, and then pick the best one. You have then “committed” to that hyperparameter choice, and you will use it on the test set.
- **Testing**: this is the dataset you use _only at the very end_ of hyperpameter optimization to estimate how good your model is on _unseen_ data: Once you have identified the best hyperparameters using the validation set, you train a model using that hyperparameter choice, and then calculate how good this model is on the test set. In this training step, you use the _union of training set and validation set_ as training data. After evaluating on the test set, you are “done” – you simply report the result (e.g., the proportion-correct accuracy, the MSE, etc. – whatever is relevant for your application), and stop.

```python
# training
bestAccuracy = -1
# Try each alpha
for alpha in [ 0.0001, 0.001, 0.01 ]:
    # Train on training data
    model = train(dataTrain, alpha)
    # Evaluate on validation data
    accuracy = evaluate(dataValid, model)
    # Keep track of best alpha
    if accuracy > bestAccuracy:
        bestAlpha = alpha
        bestAccuracy = accuracy
# Since we are done with hyperparameter search, it's
# legitimate to "add" the validation data to our training data
# (which tends to improve the accuracy on the test set).
bestModel = train(dataTrain + dataValid, bestAlpha)
accuracy = evaluate(dataTest, bestModel)

# optimize
bestAccuracy = -1
# Try each alpha
for alpha in [ 0.0001, 0.001, 0.01 ]:
    for lambda in [ .01, .1, 1 ]:
        # Train on training data
        model = train(dataTrain, alpha, lambda)
        # ...
```
## Multi-class Classification
### One-vs-rest Classification
![[Pasted image 20241007165819.png#invert]]
## Sensitivity of Linear Regression to Outliers
![[Pasted image 20241007165854.png#invert]]
![[Pasted image 20241007165902.png#invert]]