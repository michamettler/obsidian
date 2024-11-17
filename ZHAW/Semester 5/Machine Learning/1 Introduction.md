#machinelearning #sem5

https://phonosync.github.io/mldm-notes/01_intro_ml.html
![[Pasted image 20241006143659.png#invert]]
## Supervised Learning
In **Supervised Learning**, we use a dataset with _annotated_ training samples to “teach” a machine to perform a certain task.
![[Pasted image 20241006152859.png#invert]]
Dimension of $X$ : $M \times N$
$M$: training samples
$N$: features
$X$: data set
$y$: result


![[Pasted image 20241006143921.png#invert]]
## Unsupervised Learning
n **Unsupervised Learning** the training data does not contain any expected output values. The goal is to model the underlying distribution of the data X (describe the structure of the data), in order to explain it and to apply the model to new data. This brings additional challenges compared to supervised learning:

- The problem statement is much fuzzier
- The evaluation is more difficult without test data including expected output values
![[Pasted image 20241006143838.png#invert]]
## Reinforcement Learning
In **Reinforcement Learning**, the learning system, called an **Agent** in this context, can observe the **Environment**, select and perform **Actions**, and get **Rewards** in return (or penalties in the form of negative rewards), as shown in figure. It must then learn by itself what is the best strategy, called a **Policy**, to get the most reward over time. A policy defines what action the agent should choose when it is in a given situation.
![[Pasted image 20241006144410.png#invert]]
## Classification vs. Regression
In **Classification** the target variable is **categorical**, typically on a nominal scale (the classification algorithms discussed in this course treat ordinally scaled data on a nominal scale). The output values are assumed to belong to a set of discrete classes.
$$𝑦^{(m)} ∈ \{𝐶_1, 𝐶_2, …, 𝐶_𝐾 \}$$
[[2 Linear Regression]] is another supervised learning task, where the goal is to predict a _numeric_ (continuous) target value, i.e.
$$y^{(m)} ∈ ℝ$$
![[Pasted image 20241006144530.png#invert]]