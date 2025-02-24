#machinelearning #sem5

https://phonosync.github.io/mldm-notes/03_gradient_descent.html
https://github.com/michamettler/zhaw-mldm/blob/main/L03/L03_Gradient_Descent_ASSIGNMENT.ipynb

If we cannot use the normal equation to solve an instance of linear regression explicitly, we can try to find an “as good as possible” solution, i.e. values for the parameters $\theta_0$ such that the corresponding model approximates an optimal model.
![[Pasted image 20241006152315.png#invert]]
## Gradient Descent Algorithm
One of the most well-known algorithms to solve this task is **Gradient Descent**. The figure below shows the core idea for a function where we have two parameters that we need to find, $\theta_0$ and $\theta_1$. The image shows for each parameter combination the corresponding cost $J(\theta_0, \theta_1)$  (note that the image shows the cost function of a non-linear model; for a linear model, the cost function would be convex).
![[Pasted image 20241006152407.png#invert]]
### Gradient Descent for Univariate [[2 Linear Regression]]
Plugging the two formulas above into the gradient descent algorithm yields:
Important, use MAE and not MSE ([[ZHAW/Semester 5/Machine Learning/1 Introduction]]).

1. Initialize: $\theta_0$ and $\theta_1$ (randomly)
2. Repeat until convergence:
$$\text{Update} \: \theta_0 = \theta_0 - \alpha \frac{1}{M} \sum_{m=1}^{M}(h_{\theta}(x^{(m)}) - y^{(m)})$$
$$\text{Update} \: \theta_1 = \theta_1 - \alpha \frac{1}{M} \sum_{m=1}^{M}(h_{\theta}(x^{(m)}) - y^{(m)})x^{(m)} \tag{3.2}$$

Alternative formulas (easier to read):
$$\theta_{0}^{(t+1)} = \theta_{0}^{(t)} - \alpha (\theta_{0}^{(t)} + \theta_{1}^{(t)} x_t - y_t)$$
$$\theta_{1}^{(t+1)} = \theta_{1}^{(t)} - \alpha (\theta_{0}^{(t)} + \theta_{1}^{(t)} x_t - y_t) x_t$$
#### Example Calculation
##### Parameter
![[Pasted image 20241006152920.png#invert]]
$\theta_0$ = 1
$\theta_1$ = 0.5
$\alpha$ = 0.1 (learning rate)

##### Calculation
![[Pasted image 20241006152931.png#invert]]
#### Example Calculation with Python
```python
class SGDUnivariateLinearRegression:

  def __init__(self):
    self.theta_0: float = 0.
    self.theta_1: float = 0.
    self.rng = np.random.default_rng(RANDOM_SEED)

  def predict(self, x):
    y = self.theta_0 + self.theta_1 * x
    return y

  def fit(self, x, y, n_iter: int = 100, learning_rate: float = 1.0):
    for t in range(n_iter):
      sample_ix = self.rng.integers(0, len(x))

      xt = x[sample_ix]
      yt = y[sample_ix]

      theta_0 = self.theta_0 - learning_rate * (self.predict(xt) - yt)
      theta_1 = self.theta_1 - learning_rate * (self.predict(xt) - yt) * xt

      self.theta_0 = theta_0
      self.theta_1 = theta_1

    return self
```
### Learning Rate
he partial derivatives in gradient descent determine in which direction we need to adapt the parameters $\theta_0$ in order to reduce the cost function $J$. The larger the magnitude of the gradient, the steeper the descent, and the more we change the values of $\theta_0$ in a single step. Unfortunately, we can sometimes “overstep” if the gradient is too large.
![[Pasted image 20241006153241.png#invert]]
#### Example Python different Learning Rates
```python
_iters = [50, 100, 200, 500, 1000, 2000]
learning_rates = [1., .1, .01]

# we plot the MSE achieved by the closed form model as a reference
closed_form = UnivariateLinearRegression()
closed_form.fit(x, y1)
mse_base = mse(y_pred=closed_form.predict(x), y_true=y1)
plt.plot(n_iters, np.ones_like(n_iters) * mse_base, label="closed form", linestyle='--', c='b')

for alpha in learning_rates:
  mses = []
  for n_iter in n_iters:
    # fit a SGDUnivariateLinearRegression model using n_iter=n_iter and
    # learning_rate=alpha
    sdg = SGDUnivariateLinearRegression()
    y_pred = sdg.fit(x, y1, n_iter=n_iter, learning_rate=alpha).predict(x)

    # compute its mse and append the mse value to the mses list
    mse_ = mse(y_pred, y1)
    mses.append(mse_)
  plt.plot(n_iters, mses, label=f"alpha = {alpha:.2f}")

plt.xlabel("n_iter")
plt.ylabel("MSE")
plt.legend()
plt.show()
```