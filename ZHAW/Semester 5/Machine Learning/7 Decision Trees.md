#machinelearning #sem5

https://phonosync.github.io/mldm-notes/07_trees.html
## Predictions from a Classification Tree
Decision trees provide nice, simple classification rules that can even be applied manually (White-Box-Algorithm). As an introductory example we work with the iris flower dataset (3 species (Setosa, Versicolor, and Virginica)) described by 4 numerical variables: petal length, width and sepal length, width.
![[Pasted image 20241101210519.png#invert]]

The figure above shows a decision tree based on only two features: petal width and petal length. Setosa (depth 1, right). is (petal length <= 2.45) a **leaf node** (i.e., it does not have any child nodes), so it does not ask any questions, but outputs the **majority class** of its samples as a **prediction**. If it has child nodes, it's called a **split node** and it goes further down.
A node’s gini attribute measures its [[#Gini impurity]]: a node is **pure** (gini=0) if all training instances it applies to belong to the same class. For example, since the depth-1 left node applies only to Iris Setosa training samples, it is pure and its Gini impurity is 0. On the other extreme, the root node is a maximally **impure** node: Each of the three classes is present with the same amount of samples (50), which leads to a [[#Gini impurity]] equal to ≈ 0.667.
![[Pasted image 20241101211253.png#invert]]
Decision boundaries of the decision tree. The vertical boundary represents the decision of the root node (depth 0) at petal length = 2.45 cm. Since the lefthand area is pure (only Iris Setosa), it cannot be split any further.
A decision tree can also estimate the probability that a sample belongs to a particular class k. For example, for a flower whose petals are 5 cm long and 1.5 cm wide. The corresponding leaf node is the depth-2 left node so the decision tree outputs the following probabilities: 0% for Iris setosa (0/54), 90.7% for Iris versicolor (49/54), and 9.3% for Iris virginica (5/54).
## Impurity Measures For Classification
$$p_{ik} = \frac{1}{M_i}\sum_{y\in Q_i} I(y=k)$$
If $i$ is a leaf node, $p_{ik}$ is the predicted probability for this region of the feature space. By default, the `DecisionTreeClassifier` in scikit-learn uses the
![[Pasted image 20241106192533.png#invert]]
### Gini impurity
$$G\left(Q_i\right)=1-\sum_{k=1}^K p_{i,k}^2 \tag{7.1}$$
The example above as a Gini impurity equal to $1 – (0/54)2 – (49/54)2 – (5/54)2 \approx 0.168$. The highest Gini impurity for a given number of classes is reached, when each class has the same number of samples. Faster and therefore a good default.
### Entropy
$$H\left(Q_i\right)=-\sum_{k=1}^K p_{i,k} \log_2 p_{i,k} \tag{7.2}$$
For example, the depth-2 left node in the example above has an entropy equal to $–(49/54) \log_2 (49/54) – (5/54) \log_2 (5/54) \approx 0.445$.

[[#Gini impurity]] and entropy behave very similarly. When all samples belong to the same class, both metrics are zero and both have their maximum at $p=0.5$, when the classes have the same number of samples.
## Training a Decision Tree for Classification
Scikit-learn uses the [[5 Classification with Logistic Regression]] and [[2 Linear Regression]] Tree (**CART**) algorithm to train decision trees.
How does the algorithm choose the feature $n$ and threshold $t_i$ for each split? It searches for the pair $t_i$ that produces the purest subsets, weighted by their size.
To achieve this, it sorts all unique values of feature n among the samples at node $i$ and calculates the midpoints between adjacent values. Each of those midpoints is evaluated as a threshold $t_i$ in a candidate split $\theta=(n,t_{i})$. And those candidate splits $\theta=(n,t_{i})$ partition the samples on the node into two subsets (greater and lesser than the threshold value).
$$Q_i^{\text{left}}(\theta) = \{(x,y)| x_n \leq t_i \} \ \text{ and } \ Q_i^{\text{right}}(\theta) = Q_i \setminus Q_i^{\text{left}}(\theta)$$

The quality of a candidate split of node $i$ is then quantified by a cost function, which is the weighted average of the impurity of the left and right splits:
$$J(Q_i,\theta)=\frac{m^{\text{left}}_i}{m_i}G\left(Q^{\text{left}}_i\left(\theta\right)\right) + \frac{m^{\text{right}}_i}{m_i}G\left(Q^{\text{right}}_i\left(\theta\right)\right) \tag{7.3}$$
The CART algorithm is a greedy algorithm: it greedily searches for an optimum split at the top level, then repeats the process at each subsequent level. It does not check whether or not the split will lead to the lowest possible impurity several levels down.
## Predictions from a Regression Trees
Decision trees can also be used for regression tasks. The main difference to a classification tree is that instead of predicting a class in each node, it predicts a numerical value.
![[Pasted image 20241106193547.png#invert]]
The predictions are shown as red lines (vertical corresponds to a split node).
![[Pasted image 20241106193620.png#invert]]
The predicted value for each region is always the mean value of the training samples in that region, i.e. from that corresponding leaf node. That is, the regression tree approximates the training data as a step function with the steps corresponding to the leaf nodes.
## Training Regression Trees
$$MSE(Q_i)=\frac{1}{M_i}\sum_{y\in Q_i} \left(y-\bar{y}_i\right)^2  \tag{7.4}$$
$$\bar{y}_i=\frac{1}{M_i}\sum_{y\in Q_i} y$$
## Regularization
Decision trees make very few assumptions about the training data (as opposed to, for example, [[2 Linear Regression]] models, which assume that the data is linear). If left unconstrained, the tree structure will adapt itself to the training data, fitting it very closely, most likely even **overfitting** it (nonparametric).
In scikit-learn `max_depth` and a few other hyperparameters control the stopping conditions to restrict the maximum depth of the decision tree, which will regularize the model and thus reduce the risk of overfitting.
### Parameters
#### `max_depth`  
   The maximum depth of the tree. With the default value `None`, nodes are expanded until all leaves are pure or until all leaves contain less than `min_samples_split` samples.
#### `min_samples_split`  
   Minimum number of samples a node must have before it can be split
#### `min_samples_leaf`  
   Minimum number of samples a leaf node must have to be created
#### `min_weight_fraction_leaf`  
   same as `min_samples_leaf` but expressed as a fraction of the total number of weighted instances
#### `max_leaf_nodes`  
   maximum number of leaf nodes
#### `max_features`  
   sets the number of features that are evaluated for splitting at each node.
   
Increasing `min_*` hyperparameters or reducing `max_*` hyperparameters will regularize the model.
![[Pasted image 20241106194320.png#invert]]
![[Pasted image 20241106194448.png#invert]]
## Random Forests
Random Forests are a type of ensemble methods, that are composed of individual decision trees.
![[Pasted image 20241106194706.png#invert]]
Generally, the individual trees are trained by the **bagging** (short for Bootstrap AGGregatING) method. The bootstrap refers to the strategy of **generating diversity** among the trees (different subset). In the bagging approach this sampling is performed with replacement. On the other hand, if the sampling is done without replacement it is called **pasting**.
Once all trees are trained, the ensemble can make a prediction for a new instance by aggregating the predictions of all trees. For regression tasks (`RandomForestRegressor`) this is done by **averaging** the predicted values. For classification tasks (`RandomForestClassifier` in scikit-learn) this is typically done by **hard voting** or **soft voting**.
![[Pasted image 20241106200322.png#invert]]
![[Pasted image 20241106200506.png#invert]]