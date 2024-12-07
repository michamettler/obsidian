#machinelearning #sem5 
 
https://phonosync.github.io/mldm-notes/09_generative_models.html

c.f [[Probability Theory]]
## Discriminative vs. Generative
In generative models, we estimate two key components:

$P(X | Y)$: The likelihood of observing features $X$ given a particular class label $Y$.

$P(Y)$: The prior probability of each class label $Y$.

Generative models correspond to the approach of someone who studies dogs and cats, aiming to understand them so well that they could draw a typical representative of each. Discriminative models correspond to the approach of someone who focuses on the key differences between dogs and cats, so they can quickly point out those differences, without really understanding each animal.
### Discriminative
1. Learning. Learn the boundary that separates dog images from cat images without modeling the individual distributions.
2. Inference. Given a new image, determine on which side of the boundary it falls to classify it as a dog or cat.
### Generative
1. Learning - prior probabilities.
2. Learning - likelihoods. Calculate probabilities of features (like pointy ears) occurring in different classes, (dogs vs. cats).
3. Inference. Given a new image, calculate the probability of it being in a particular class (a cat or dog) based on the observed features.
![[Pasted image 20241201221620.png#invert]]
## Naive Bayes
Naive Bayes is a generative model used in supervised machine learning for classification tasks (assuming all features are conditionally independent).
$$P(class | features) = [P(features | class) * P(class)] / P(features)$$
$P(class | features)$: is the posterior probability, the probability of the data point belonging to the class given its features. This is what the model wants to predict.
$P(features | class)$: is the likelihood, the probability of observing those features given that the data point belongs to that class.
$P(class)$: is the prior probability of that class, the probability of a randomly selected data point belonging to that class. This is usually calculated based on the distribution of classes in the training set.
$P(features)$: is the evidence, the probability of observing those features regardless of the class. This term is often ignored in calculations as it is a constant for all classes and does not affect the relative probabilities.
![[Pasted image 20241201221505.png#invert]]

Naive Bayes typically uses maximum likelihood estimation (MLE) to determine the values of the model parameters (prior probabilities and likelihoods) (it is also possible to use MAP to incorporate prior knowledge).
### Types
**Bernoulli Naive Bayes**: This classifier is employed for binary data, where features are represented as present or absent (1 or 0). It is well-suited for binary/boolean feature sets, where the frequency of a feature is not important, but rather its presence or absence.

**Multinomial Naive Bayes**: This classifier is suitable for count data, such as word counts in text documents. It is frequently used for tasks like spam detection, where the frequency of words or terms plays a crucial role in classification.

**Gaussian Naive Bayes**: This classifier is utilized for continuous data, and assumes that features follow a Gaussian (normal) distribution. This type is appropriate for datasets with numerical features.