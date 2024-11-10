#machinelearning #sem5

https://phonosync.github.io/mldm-notes/06_svm.html
https://github.com/michamettler/zhaw-mldm/blob/main/L06/l06_svm_lab_assignment.ipynb
## Hyperplane
In $N$-dimensional space, a hyperplane is a flat affine subspace of **dimensions** $N−1$. For instance, in two dimensions, a hyperplane is a one-dimensional subspace - a line.
$$b + w_1 x_1 + w_2 x_2 = 0 \tag{6.1}$$
The formulation can be easily extended to the $N$-dimensional setting:
$$b + w_1 x_1 + w_2 x_2 + \dots + w_N x_N = 0 \tag{6.2}$$
Also the w’s can be expressed as a $N$-dimensional parameter vector and the scalar (dot) product $\langle\mathbf{w},\mathbf{x}\rangle=\mathbf{w}^T\mathbf{x} = \sum_{n=1}^N w_n x_n$ allows to express in compact form:
$$b + \mathbf{w}^T\mathbf{x} = 0 \tag{6.3}$$
Now, suppose that x does not satisfy; rather, $b + \mathbf{w}^T\mathbf{x} > 0.$ Then this tells us that x lies on one side of the hyperplane. On the other hand, if $b + \mathbf{w}^T\mathbf{x} < 0,$ then x lies on the other side of the hyperplane.
![[Pasted image 20241022210457.png#invert]]
Three separating hyperplanes, out of many possible, are shown in white.
![[Pasted image 20241022210639.png#invert]]
The goal of the learning algorithm is to find the optimal values $\hat{\mathbf{w}}$ and $\hat{b}$ for parameters $w$ and $b$. Once the learning algorithm has identified these optimal values, some new input feature vector $\mathbf{x}^{(\ast)}$ can be classified by:
$$f(\mathbf{x}^{\ast})= \hat{b} + \hat{\mathbf{w}}^T\mathbf{x}^{(\ast)}$$
If $f(\mathbf{x}^{\ast})$ is positive, the test sample is assigned to class $+1$, and if $f(\mathbf{x}^{\ast})$ is negative, then it is assigned to class $−1$.
## Margin Classifiers
### Maximal Margin Classifier
 $\hat{\mathbf{w}}$ and $\hat{b}$ are found by solving a constrained optimization problem: The [[#Hyperplane]] should separate positive examples from negative ones with the largest **margin**. The final constraint minimization problem is:
$$\underset{b, \mathbf{w}}{\text{min}}\frac{1}{2}||\mathbf{w}||^2 \tag{6.7}$$
$$\text{subject to} \ y^{(m)}\left(b + \mathbf{w}^T\mathbf{x}^{(m)} \right) \geq 1 \ \forall \ m=1,\dots,M \tag{6.8}$$
Naturally, a classifier that is based on a separating hyperplane leads to a linear **decision boundary**.
![[Pasted image 20241022211407.png#invert]]
There are two classes of samples, shown in blue and in red. The maximal margin [[#Hyperplane]] is shown as a solid line. The margin is the distance from the solid line to either of the dashed lines. The two blue points and the red point that lie on the dashed lines are the support vectors, and the distance from those points to the hyperplane is indicated by grey solid lines. The red and blue grid indicates the decision rule made by a classifier based on this separating hyperplane.
#### Python Example

```python
X, y = datasets.make_blobs(n_samples=50, centers=2,
                  random_state=0, cluster_std=0.60)

y[np.where(y==0)] = -1

fig, ax = plt.subplots(figsize=(5, 5))
ax.scatter(X[:, 0], X[:, 1], c=y, s=50, cmap=cmap)

ax.set_xlabel(r'$x_1$', fontsize=16)
ax.set_ylabel(r'$x_2$', fontsize=16)

plt.show()

model = svm.SVC(kernel='linear', C=1000, tol=0.0001) # initialize the model
model.fit(X, y) # fit the model = learn the decision boundaries
print("w = ", model.coef_)
print("b = ", model.intercept_)
X[model.support_]
model.support_vectors_

b = model.intercept_
w = model.coef_
for m in model.support_:
    print(y[m] * (b + np.dot(w, X[m])))  # Formula (6.8)
```
### Soft Margin Classifier
In many cases no separating [[#Hyperplane]] exists, that is, the optimization problem has no solution. In fact, even if a separating [[#Hyperplane]] does exist, a hard margin classifier might not always be desirable (sensitivity to individual samples or outliers). Moreover, the fact that the [[#Maximal Margin Classifier]] [[#Hyperplane]] is extremely sensitive to a change in a single sample suggests that it may have **overfit** the training data.

- greater robustness to individual samples, and
- better generalizability.

For the [[#Soft Margin Classifier]] **slack variables** $\mathbf{\epsilon}=\begin{pmatrix}\epsilon_1 & \epsilon_2 & \dots & \epsilon_M\end{pmatrix}^T, \epsilon_m\geq0$ are introduced. They allow a few individual samples to be on the wrong side of the margin. The larger their value, the further the respective sample reaches onto the wrong side of the margin $\epsilon_m\gt0$. They can be even on the wrong side of the hyperplane $\epsilon_m\gt 1$.  
The new objective becomes
$$\underset{b, \mathbf{w}, \mathbf{\epsilon}}{\text{min}}\frac{1}{2}||\mathbf{w}||^2 + C \sum_{m=1}^M\epsilon_m  \tag{6.9}$$
$$\text{subject to }\epsilon_m \geq0, \ y^{(m)}\left( b + \mathbf{w}^T\mathbf{x}^{(m)} \right) \geq 1-\epsilon_m \tag{6.10}$$
where $C$ is nonnegative and acts as a regularization parameter. **A sample that lies strictly on the correct side of the margin does not affect the soft margin classifier!**
The value of $C$ affects the **bias-variance trade-off** of the model: When $C$ is small, the margin is wide (fig. a). This amounts to fitting the data less hard and obtaining a classifier with low variance but potentially high bias.
In practice, $C$ is treated as a tunable hyperparameter that is generally chosen via cross-validation. [[Data Partitioning]]
![[Pasted image 20241022213001.png#invert]]
#### Python Example

```python
X, y = datasets.make_blobs(n_samples=50, centers=2,
                  random_state=0, cluster_std=0.60)

_, ax = plt.subplots(figsize=(5, 5))
ax.scatter(X[:, 0], X[:, 1], c=y, s=50, cmap=cmap)
ax.set_xlabel(r'$x_1$', fontsize=16)
ax.set_ylabel(r'$x_2$', fontsize=16)
plt.show()

model = svm.SVC(kernel='linear', C=0.1) # initialize the model
model.fit(X, y) # fit the model = learn the decision boundaries

_, ax = plt.subplots(figsize=(5, 5))
plot_svc_decision_function(model, X, y, ax)
plt.show()

# With Regularization
for c in [0.001, 0.01, 0.1, 1, 10, 100, 1000]:
    # create an instance of SVC and set its parameter C
    # call its .fit method to train it on X and y
    model = svm.SVC(kernel='linear', C=c)
    model.fit(X, y)

    _, ax = plt.subplots(figsize=(5, 5))
    plot_svc_decision_function(model, X, y, ax)
    ax.set_title(f"C={c}")
    plt.show()
```
## Support Vector Machines and the Kernel Trick
![[Pasted image 20241022213112.png#invert]]
Many classification problems ([[Classification with Logistic Regression]]) are not linearly separable. It is clear that a support vector classifier or any linear classifier will perform poorly here. **kernels** (kernel functions) are the solution to this dilemma. They allow to efficiently work in higher-dimensional spaces without going through the transformations explicitly.

Instead of transforming the scalar product of the original feature vectors can be computed directly and then squared to get the same result. This results in much fewer and more efficient computations.
$$\mathcal{K}(\mathbf{x}^{(m)},\mathbf{x}^{(m')})=\left(1+\sum_{n=1}^N x^{(m)}_n x^{(m')}_n\right)^d \tag{6.15}$$
where the degree $d$ is a positive integer. Using such a kernel with $d>1$, instead of the standard linear kernel, in the support vector classifier algorithm leads to a much more flexible decision boundary. When the support vector classifier is combined with a non-linear kernel such as (6.15) the resulting classifier is known as a **support vector machine**.

Another popular choice for a non-linear kernel function is the **rbf kernel** (rbf: short for Radial Basis Function, also just called radial or Gaussian kernel):
$$\mathcal{K}\left(\mathbf{x}^{(m)},\mathbf{x}^{(m')}\right)=\exp\left(-\gamma ||\mathbf{x}^{(m)} -\mathbf{x}^{(m')}||^2 \right), \tag{6.16}$$
  
 $\gamma$ in is a positive constant inversely proportional to the variance of the Gaussian $\gamma=\frac{1}{\sigma^2}$. That is, with larger values for $\gamma$ the Kernel has a smaller spread and influences the classification only in the immediate surrounding of each sample. This makes the decision boundary typically rougher - leading to low bias, but high variance (a small change in the data has a large effect).
  
 $\gamma$ and $d$ are hyperparameters that are typically tuned along with $C$ via cross-validation. [[Data Partitioning]]
![[Pasted image 20241022213953.png#invert]]
(One-versus-all approach also possible for more than two classes). [[Classification with Logistic Regression]]
#### Python Example
```python
X_non_linear, y_non_linear = datasets.make_circles(100, factor=.1, noise=.1)

_, ax = plt.subplots(figsize=(5, 5))
ax.scatter(X_non_linear[:, 0], X_non_linear[:, 1], c=y_non_linear, cmap=cmap)
plt.show()

r = np.exp(-(X_non_linear ** 2).sum(1))

fig1=plt.figure(figsize=(10, 10))
ax = fig1.add_subplot(projection='3d')
ax.scatter3D(X_non_linear[:, 0], X_non_linear[:, 1], r,
             c=y_non_linear, s=50, cmap=cmap)
ax.view_init(elev=15, azim=60)
ax.set_xlabel('x')
ax.set_ylabel('y')
ax.set_zlabel('r')

plt.show()

X_3d =  np.c_[X_non_linear, r]
clf_3d = svm.SVC(kernel='linear').fit(X_3d, y_non_linear)

# get the parameters from the optimised model that specify the decision boundary
w = clf_3d.coef_[0]

b=clf_3d.intercept_[0]

fig1=plt.figure(figsize=(10, 10))
ax = fig1.add_subplot(projection='3d')
ax.scatter3D(X_non_linear[:, 0], X_non_linear[:, 1], r,
             c=y_non_linear, s=50, cmap=cmap)
ax.view_init(elev=15, azim=60)
ax.set_xlabel('x')
ax.set_ylabel('y')
ax.set_zlabel('r')

# Surface plot of the decision boundary (a plane) from the
# optimised parameters
xx, yy = np.meshgrid(np.linspace(-1,1,2),np.linspace(-1,1,2))
# 0=b+w_0*x+w_1*y+w_2*z  ->  rearrange for z
z = -(b + w[0]*xx * w[1]*yy) / w[2]
ax.plot_surface(xx, yy, z, alpha=0.5)

plt.show()
```
## SVMs for Regression
To use SVMs for regression instead of classification, the trick is to tweak the objective: Instead of trying to fit the largest possible street between two classes while limiting margin violations, SVM regression tries to fit as many instances as possible on the street while limiting margin violations.
The width of the street is controlled by a hyperparameter, $\epsilon$. To tackle nonlinear regression tasks, kernelized SVM models can be employed.