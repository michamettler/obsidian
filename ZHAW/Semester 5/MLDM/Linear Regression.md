#machinelearning #sem5 

https://phonosync.github.io/mldm-notes/02_linear_regression.html
https://github.com/michamettler/zhaw-mldm/blob/main/L02/L02_Linear_Regression_ASSIGNMENT.ipynb
## Univariate Linear Regression
One of the simplest cases of model-based learning is **Univariate Linear Regression** (also called **Simple Linear Regression**). Here, the output depends only on one input variable x, and the hypothesis is a linear combination of two parameters $\theta_0$ and $\theta_1$ and the input value $x$:
$$h_{\theta_0,\theta_1}(x)=\theta_0+\theta_1 x$$
Note that in the literature, $\hat{y}$ is usually used for the predicted value (as computed by the model), whereas $y$ would be used for the true value.
### Loss Function
For linear regression, the **Residual Sum of Squares RSS** (also called **Sum of Residuals** or **Sum of Squared Errors**) is typically used
$$ℒ_{RSS}(𝜃_0,𝜃_1;\{x^{(m)},y^{(m)}\}) = \sum_{𝑚=1}^𝑀(𝑦^{(m)}−\hat{𝑦}^{(m)})^2 = \sum_{𝑚=1}^M \varepsilon_𝑚^2$$
with
$$\varepsilon^{(m)} = y^{(m)} - \hat{y}^{(m)}$$
### Cost Function
The learning (training) consists of minimizing a **Cost Function $J$**, which is a function of the model parameters and depends implicitly on the training data. In the simplest case, the cost function is equal to the loss function and a normalising factor for mathematical convenience:
$$J(𝜃_0,𝜃_1)=\frac{1}{2 M} \sum_{𝑚=1}^𝑀(𝑦^{(m)}−\hat{𝑦}^{(m)})^2 \tag{2.1}$$
Minimizing the cost function results in specific values for the model parameters $\theta_0$ and $\theta_1$, which can then be used for predicting the output for new data samples (also called **Inference**):
$$\hat{y}=h_{\hat{\theta}_0,\hat{\theta}_1}(x)=\hat{\theta}_0+\hat{\theta}_1 x$$
### Closed Form Solution for Univariate Linear Regression
Using these equations we can simple compute the optimal values for parameters $\theta_0$ and $\theta_1$  for the $M$ given training samples ${(𝑥^{(m)},𝑦^{(m)})}$.
$$\hat{\theta}_0=\mu_y-\theta_1\mu_x \ $$
and
$$\hat{\theta}_1=\frac{\sum_{m=1}^M(x^{(m)}-\mu_x)(y^{(m)}-\mu_y)}{\sum_{m=1}^M(x^{(m)}-\mu_x)^2}= \frac{\tilde{s}_{xy}}{\tilde{s}_x^2} \tag{2.2}$$
#### Example Calculation $\theta_1$
Data Set:
![[Pasted image 20241006145655.png#invert]]
Calculation (vgl. $2.2$):
![[Pasted image 20241006145723.png#invert]]
#### Example Calculation Python

```python
class UnivariateLinearRegression:

  def __init__(self):
    self.theta_0: float = 0.
    self.theta_1: float = 0.

  def predict(self, x):
    y_pred = self.theta_0 + self.theta_1 * x
    return y_pred

  def fit(self, x, y):
    x_mean = np.mean(x)
    y_mean = np.mean(y)

    num = np.sum((x - x_mean) * (y - y_mean))
    denom = np.sum((x - x_mean) ** 2)

    self.theta_1 = num / denom
    self.theta_0 = y_mean - self.theta_1 * x_mean

    return self

lin_reg_uni = UnivariateLinearRegression()
lin_reg_uni.fit(x, y1)
y_pred = lin_reg_uni.predict(x)

def plot_model(x, y_pred, y_true):
  # scatter plot of the true data points
  plt.scatter(x, y_true)
  # plot the fitted line
  plt.plot(x, y_pred, c="r")
  # label axes
  plt.xlabel("x")
  plt.ylabel("y")
  plt.show()

plot_model(x=x, y_pred=y_pred, y_true=y1)
```
### Normal Equation
Alternatively to the approach resulting in $2.2$ we can use the computation of the residuals to derive a closed form for computing the optimal parameters.
$$\begin{pmatrix}
\varepsilon^{(1)} \\
\varepsilon^{(2)} \\
\vdots \\
\varepsilon^{(M)}
\end{pmatrix}=
\begin{pmatrix}
y^{(1)} \\
y^{(2)} \\
\vdots \\
y^{(M)}
\end{pmatrix}
-
\begin{pmatrix}
1 & x^{(1)} \\
1 & x^{(2)} \\
1 & \vdots \\
1 & x^{(M)}
\end{pmatrix}
\begin{pmatrix}
\theta_0 \\
\theta_1
\end{pmatrix}$$
or shorter as
$$\boldsymbol{\varepsilon} = \boldsymbol{y} - \boldsymbol{X} \boldsymbol{\theta}$$
with a corresponding matrix $X$, where the first column contains values $1$ and the second column contains the input values from the training set, and y contains the corresponding expected output values.

This leads to a closed form-expression for the optimal parameters:
$$\boldsymbol{\theta} = (\boldsymbol{X}^T \boldsymbol{X})^{−1} \boldsymbol{X}^T \boldsymbol{y} \tag{2.3}$$
We can now use this **Normal Equation** to directly compute the solution for a linear regression problem.

## Multivariate Linear Regression
**Multivariate Linear Regression**, also called **Multiple Linear Regression**, is the natural extension of the simple linear regression framework to more than one predictor variables (features).

Thus, we now extend our simple approach for one input variable to the general case with $N$ input variables (features). The $N>1$ features can be combined into a single linear combination. The model then takes the following form for the $m$’th sample (we denote the $i$’th feature of the $m$’th sample as xi(m)):
$$\hat{y}^{(m)} = h_{\theta}(x^{(m)}) = \theta_0 x_{0}^{(m)} + \theta_1 x_{1}^{(m)} + \theta_2 x_{2}^{(m)} + ... + \theta_N x_{N}^{(m)}  = \boldsymbol{\theta}^T\boldsymbol{X}_{m,:}  \tag{2.4}$$
ere, we introduce a new artificial feature variable $x_{0}^{(m)} := 1$ for all $m=1,...,M$ to simplify the notation (i.e., writing the sum as a vector product).
$$\boldsymbol{y} = \boldsymbol{X} \boldsymbol{\theta} + \boldsymbol{\varepsilon}$$
#### Example
![[Pasted image 20241006151311.png#invert]]
This can be expressed using the corresponding matrices:
$$\boldsymbol{X}=\begin{pmatrix}
1 & 29932.5 & 4.8 & 70160 & 18 \\
1 & 31007.8 & 1 & 104458 & 16.4 \\
1 & 32181.2 & 1 & 232666 & 16.9
\end{pmatrix}
\ \ \
\boldsymbol{\theta} = \begin{pmatrix}
\theta_0 \\
\theta_1 \\
\theta_2 \\
\theta_3 \\
\theta_4
\end{pmatrix}
\ \ \
\boldsymbol{y} = \begin{pmatrix}
5.9 \\
5.6 \\
5.4
\end{pmatrix}$$
#### Example Calculation Python
```python
import time
sizes = []
times = []
n = 1000
for m in [10, 50, 100, 200, 250, 500, 1000, 10000]:
  X, y = create_random_data(m, n)

  start_time = time.monotonic()

  theta = (np.linalg.inv(X.T @ X) @ X.T) @ y
  # theta = np.linalg.pinv(X) @ y
  # theta = np.linalg.solve(X.T @ X, X.T @ y)

  elapsed = time.monotonic() - start_time

  problem_size = m

  sizes.append(problem_size)
  times.append(elapsed)

plt.scatter(sizes, times)
plt.xlabel('Problem-Size')
plt.ylabel('Runtime (s)')
plt.show()
```
## Residual Plots
![[Pasted image 20241006151454.png#invert]]
## Basic Assumptions
### Linearity:
The relationship between $X$ and $y$ is linear.
![[Pasted image 20241006151545.png#invert]]

### Independence:
The residuals are independent of each other.
![[Pasted image 20241006151604.png#invert]]
### Normality:
The expected output values are normally distributed.
![[Pasted image 20241006151625.png#invert]]
### Homoscedasticity (equality of variance):
The variance of the residual is the same for any value of $X$
![[Pasted image 20241006151652.png#invert]]
## Evaluating Regression Models
There are several metrics that can be used to quantify how well the expected and predicted output values correspond:
### Mean Absolute Error (MAE)
$$MAE=\frac{\sum_{𝑖=1}^𝐼|𝑦^{(i)}−\hat{𝑦}^{(i)}|}{𝐼}$$
### Mean Squared Error (MSE)
$$MSE=\frac{\sum_{𝑖=1}^𝐼(𝑦^{(i)}−\hat{𝑦}^{(i)})^2}{𝐼}$$
#### Example Python
```python
def mse(y_pred, y_true):
    return np.mean((y_pred - y_true)**2)
```
### Root Mean Squared Deviation (RMSD)
$$𝑅𝑀𝑆𝐷=\sqrt{MSE}=\sqrt{\frac{\sum_{𝑖=1}^𝐼(𝑦^{(i)}−\hat{𝑦}^{(i)})^2}{𝐼}}$$
with $I$ number of samples in the independent test set.