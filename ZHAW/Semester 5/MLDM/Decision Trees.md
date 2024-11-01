#machinelearning #sem5 

https://phonosync.github.io/mldm-notes/07_trees.html
## Predictions from a Classification Tree
As an introductory example we work with the iris flower dataset (3 species (Setosa, Versicolor, and Virginica)) described by 4 numerical variables: petal length, width and sepal length, width.
![[Pasted image 20241101210519.png#invert]]

The figure above shows a decision tree based on only two features: petal width and petal length. Setosa (depth 1, right). is (petal length <= 2.45) a **leaf node** (i.e., it does not have any child nodes), so it does not ask any questions, but outputs the **majority class** of its samples as a **prediction**. If it has child nodes, it's called a **split node** and it goes further down.
A node’s gini attribute measures its **Gini impurity**: a node is **pure** (gini=0) if all training instances it applies to belong to the same class. For example, since the depth-1 left node applies only to Iris Setosa training samples, it is pure and its Gini impurity is 0. On the other extreme, the root node is a maximally **impure** node: Each of the three classes is present with the same amount of samples (50), which leads to a Gini impurity equal to ≈ 0.667.
![[Pasted image 20241101211253.png#invert]]
Decision boundaries of the decision tree. The vertical boundary represents the decision of the root node (depth 0) at petal length = 2.45 cm. Since the lefthand area is pure (only Iris Setosa), it cannot be split any further.
A decision tree can also estimate the probability that a sample belongs to a particular class k. For example, for a flower whose petals are 5 cm long and 1.5 cm wide. The corresponding leaf node is the depth-2 left node so the decision tree outputs the following probabilities: 0% for Iris setosa (0/54), 90.7% for Iris versicolor (49/54), and 9.3% for Iris virginica (5/54).