#machinelearning #sem5 

## Terminology
Any subset of the sample space is called an event. For example, if the experiment is tossing a coin, the sample space is $S = \{Heads, Tails\}$. The event of getting heads is a subset $\{Heads\}$.
### Axioms
![[Pasted image 20241201201217.png#invert]]
#### Union
Either A or B occurs, or both
$$𝑃(𝐴 ∪ 𝐵) = 𝑃(𝐴) + 𝑃(𝐵) − 𝑃(𝐴 ∩ 𝐵)$$
#### Intersection
both occur
$$A \cap B$$
#### Complement
Does not occur
$$A^c$$
The probability of the complement of an event is 1 minus the probability of the event.

### Joint and conditional probability
#### Marginal probability
is the probability of event occurring, $P(A)$, not conditioned on other events. For example, this is the probability that a card drawn from a deck of cards is red $P(red)=0.5$.
#### Joint Probability
This is the probability of two or more events happening at the same time. For **independent events** (events where the occurrence of one does not affect the occurrence of the other), the joint probability is calculated as the product of their individual probabilities ([[#Intersection]]):
$$P(A \text{ and } B) = P(A \cap B) = P(A) \cdot P(B)$$
For **dependent events** (events where the occurrence of one affects the occurrence of the other), the joint probability is calculated using **conditional probability**:
$$P(A \text{ and } B) = P(A) \cdot P(B \mid A)$$
#### Conditional Probability
This measures the probability of an event B occurring given that another event A has already happened, denoted as $P(B|A)$. It is calculated as:
$$P(B \mid A) = \frac{P(A \cap B)}{P(A)}$$
#### Law of Total Probability
Provides a way to calculate the probability of an event based on a partition of the sample space into disjoint subsets.
Let $B_1, B_2, ..., B_n$ be mutually exclusive and collectively exhaustive events, meaning no two events can occur at the same time, and one of these events must occur.
$$P(A) = P(A \mid B_1)P(B_1) + P(A \mid B_2)P(B_2) + ... + P(A \mid B_n)P(B_n)$$
## Bayes’ Theorem
**Bayes’ theorem** is a fundamental concept that describes how to update the probability of an event based on new evidence. It is stated as:
$$P(A \mid B) = \frac{P(A) \cdot P(B \mid A)}{P(B)}$$
## Estimating the parameters in probabilistic models
### Maximum Likelihood Estimation (MSE)
$$\theta_{\text{MLE}} = \underset{\theta}{\text{argmax}} \ P(X | \theta)$$
finding the parameter values that maximize the likelihood function. It aims to find the parameters that make the observed data most probable under the assumed statistical model.
#### Negative log-likelihood
$$\theta_{\text{MLE}} = \underset{\theta}{\text{argmin}} \{\ - \text{log} \ P(X | \theta) \}$$
### Maximum A Posteriori (MAP) Estimation
MAP estimation builds upon MLE and incorporates prior knowledge about the parameters using Bayesian principles. It seeks the parameter values that maximize the posterior probability, balancing the information from the observed data (likelihood) with our prior beliefs.
$$\theta_{\text{MAP}} = \underset{\theta}{\text{argmax}} \ P(\theta | X) = \underset{\theta}{\text{argmax}} \  \frac{P(X | \theta) \cdot P(\theta)}{P(X)}$$
![[Pasted image 20241201211800.png#invert]]
