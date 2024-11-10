#machinelearning #sem5 

https://phonosync.github.io/mldm-notes/08_neural_networks.html
## Softmax Regression
The label $\mathbf{y}^{(m)}$ is now a $K \times 1$ binary vector encoding the label (class) of sample m. For example, if we have three classes $\{1, 2, 3\}$, and the first sample belongs to class 2 then its label will be $\mathbf{y}^{(1)}=[0,1,0]$. This is referred to as the **one-hot encoding**. The goal of multi-class classification is to predict the label correctly.
![[Pasted image 20241108164941.png#invert]]
=> Generalization with [[#Softmax Regression]]:
![[Pasted image 20241108165008.png#invert]]
For each different class, it computes a separate linear combination of the inputs, and then applies the [[#Softmax Regression]] function defined as:
$$softmax(\mathbf{z})_k=\dfrac{\exp{(z_k)}}{\sum_{i=1}^{K}\exp{(z_i)}}$$
to each linear combination to obtain the prediction for each class. The softmax function has the nice properties of scaling the values it is applied on to the $[0,1]$ interval in a way that they sum up to one (can be interpreted as probabilities).
### Loss-Function (Entropy)
$$\textrm{Loss}(\hat{\mathbf{y}}^{(m)}, \mathbf{y}^{(m)}) = - \sum_{k=1}^{K}{y_k^{(m)} \log(\hat{y}_{k}^{(m)})}$$
$$J(\mathbf{W}) = \frac{1}{M} \sum_{m=1}^M \textrm{Loss}(\hat{\mathbf{y}}_{m}, \mathbf{y}_m).$$
The model parameters are then obtained by minimizing the cross entropy cost function by **gradient descent**.
![[Pasted image 20241108165448.png#invert]]
## Feed-forward Neural Networks
### Neuron
![[Pasted image 20241108165651.png#invert]]
The [[#Neuron]] has several inputs and one output. The output is computed by applying an **activation function** on the linear combination (weighted sum) of the inputs and adding a bias term (the offset) depicted in violet (sum also referred as **preactivation**).
The activation function regulates the value of the output (is it non-zero, how large its value is, …). Another way to depict the neuron is by adding an additional node with a value of one to the inputs with its corresponding weight representing the bias term:
![[Pasted image 20241108165825.png#invert]]
### Neuronal Network
A neural network consists of many connected neurons organized in layers. The number of hidden layers defines the **depth** of the network. In feed-forward neural networks, subsequent layers are **fully conected**. The model parameters of a neural network comprise the weights and biases of all neurons in the network (number of edges/connections).
![[Pasted image 20241108170043.png#invert]]
### Output
The structure of the output layer depends on the task. For **regression tasks** [[Linear Regression]] and **binary classification problem** [[Classification with Logistic Regression]],  the output is a single node (prediction or result of sigmoid). When addressing a **multiclass classification problem** [[Classification with Logistic Regression]], the number of nodes in the output layer equals the number of different classes. The predicted class label corresponds to the class with the highest probability.
![[Pasted image 20241108170500.png#invert]]
## Activation Functions
The activation function is the function applied in each neuron to the linear combination of its inputs (typically a non-linear).
![[Pasted image 20241108170747.png#invert]]
$$\hat{y}=f[x, \mathbf{\phi}]=b_{0}^{(2)}+w_{00}^{(2)} \zeta[b_{0}^{(1)} + w_{00}^{(1)}x] + w_{01}^{(2)} \zeta[b_{1}^{(1)}+w_{10}^{(1)}x] + w_{02}^{(2)} \zeta[b_{2}^{(1)}+w_{20}^{(1)}x]$$
where
$$\mathbf{\phi}=\{b_{0}^{(1)}, b_{1}^{(1)}, b_{2}^{(1)}, w_{00}^{(1)}, w_{10}^{(1)}, w_{20}^{(1)}, b_{0}^{(2)}, w_{00}^{(2)}, w_{01}^{(2)}, w_{02}^{(2)}\}$$
are the model parameters, $\zeta$ is the activation function and $a_{i}^{(1)}=\zeta[b_{i}^{(1)}+w_{i1}^{(1)}x]$ for $i \in \{0,1,2\}$.
![[Pasted image 20241108171043.png#invert]]
 A neural network model is non-linear only when it has least one hidden layer with non-linear activation function.
![[Pasted image 20241108171253.png#invert]]
 **Universality theorem (Hornik, 1991)**: A neural network with one hidden layer using nonlinear activation function can approximate any given continuous function to any desired level of accuracy given enough hidden units.
## Activation Functions
### Regression Task
$$MSE = \frac{1}{M}\sum_{m=1}^{M}(y^{(m)}-\hat{y}^{(m)})^2$$
### Binary Classification Task
$$L_{logistic}=-\sum_{m=1}^{M}[y^{(m)}log(\hat{y}^{(m)})+(1-y^{(m)})log(1-\hat{y}^{(m)})]$$
### Multi-class (multinomial) Classification
$$L_{CE}=-\sum_{m=1}^{M}\sum_{k=1}^{K}y^{(m)}_k log(\hat{y}^{(m)}_k)=-\sum_{m=1}^{M}log\frac{\exp{(\mathbf{w}^T_{c_m}\mathbf{x}^{(m)})}}{\sum_{k=1}^{K}\exp{(\mathbf{w}^T_k\mathbf{x}^{(m)})}}$$
where $c_m$ the correct class (label) for the $m$-th sample.
## Training Neural Networks
Training a neural network translates to finding the model parameters that minimize the cost function. In practice the minimization is computed using **gradient descent**:

1. Initialize all network parameters (the weights) randomly
2. Compute the **gradient of the cost function** with respect to each of the model parameters
3. **Adjust the model parameters** by a small step α (the learning rate) in the opposite direction of the gradient:
   $$\mathbf{w} = \mathbf{w} - \alpha \frac{\partial L}{\partial \mathbf{w}}$$
![[Pasted image 20241108181504.png#invert]]