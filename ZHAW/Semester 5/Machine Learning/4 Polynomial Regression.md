#machinelearning #sem5

https://phonosync.github.io/mldm-notes/04_polynomial_regression.html
## Polynomial Models
How can we deal with data where the relation is not linear, for instance as shown in the figure below? In this case, we can try to fit a **Polynomial Model** to the data, i.e. instead of a linear hypothesis, we use a polynomial hypothesis. For instance, for the data in the figure we might use a polynomial of degree 3, i.e.
![[Pasted image 20241006153427.png#invert]]
$$h_{\theta}(x) = \theta_0 + \theta_1 x + \theta_2 x^2 + \theta_3 x^3$$
To formalize this, we first define **Artificial Variables**
$$z_1 = x, z_2 = x^2, z_3 = x^3$$
Using these, we can reformulate our hypothesis as
$$h_{\theta}(z) = \theta_0 z_0 + \theta_1 z_1 + \theta_2 z_2 + \theta_3 z_3$$
Hence, we can apply our methods from before - e.g. normal equation ([[2 Linear Regression]]), [[3 Gradient Descent]] etc. - to solve these problems.
For **Multivariate Linear Regression Model** (multiple input variables $x_1, .. x_n$) ([[2 Linear Regression]]):
$$h(x_1, .. x_n) = \theta_0 + \theta_1 x_1 + \theta_2 x_1^2x _3 + \theta_3 x_2 x_3^3 + \theta_4 \sqrt{x_2 x_3} +...$$
## Over- and Underfitting
If we take very large degrees, our [[Learning Curve]] will “jump around” a lot. While this model would have very good costs (close to zero), it is not really useful, since it “does not generalize” well (for new values) => **Overfitting**.
![[Pasted image 20241006153732.png#invert]]
### Regularization
In order to avoid overfitting, we can either decrease the degree of the polynomials - or we can, for a given degree, prevent the fitted [[Learning Curve]] from “jumping around” too much.
$$J(\theta) = \frac{1}{2 M} \left[ \sum_{𝑚=1}^𝑀(𝑦^{(m)}−h_{\theta}(x^{(m)}))^2 + \lambda \sum_{j = 1}^{n} \theta_j^2 \right] \tag{4.1}$$
![[Pasted image 20241006153910.png#invert]]
Note that the regularization term depends _only_ on the parameters $\theta_0$, not on the training samples. The **Hyperparameter** $\alpha$ determines “how much” regularization counts: The larger $\alpha$ , the more the values of $\theta_0$ contribute to the cost.
#### Example Python different degrees
```python
def calcWithPol(pol):
    poly = PolynomialFeatures(degree=pol)
    X_poly_train = poly.fit_transform(X_train)
    X_poly_test = poly.fit_transform(X_test)

    model = LinearRegression()
    y_predict_test = model.fit(X_poly_test, y_test).predict(X_poly_test)
    y_predict_train = model.fit(X_poly_train, y_train).predict(X_poly_train)

    mse_train_poly = mean_squared_error(y_train, y_predict_train)
    mse_test_poly = mean_squared_error(y_test, y_predict_test)
    return mse_train_poly, mse_test_poly

test_results = []
training_results =[]
for i in range(0,11):
    mse_train_poly, mse_test_poly = calcWithPol(i)
    test_results.append(mse_test_poly)
    training_results.append(mse_train_poly)

plt.plot(range(0,11), training_results, label='MSE training data', color='orange')
plt.plot(range(0,11), test_results, label='MSE test data', color='green')
plt.legend()
plt.show()
```