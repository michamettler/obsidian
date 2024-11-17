#machinelearning #sem5 #neuralnetworks

https://phonosync.github.io/mldm-notes/08_neural_networks.html
## [[8 Neural Networks]] Simplified
![[Pasted image 20241117144427.png#invert]]
### Pre-Activation:
$$z^{(L)} = w^{(L)}\cdot a^{(L-1)} + b^{(L)}$$
### Output
Here with sigmoid function, could also be something like relu:
$$a^{(L)}=\zeta(z^{(L)}) = \frac{1}{1+e^{-z^{(L)}}} = \left(1+e^{-z^{(L)}}\right)^{-1}$$
### Cost Function
$$C = \left(y-a^{(L)}\right)^2$$
## Backpropagation
Now we need to quantify how changes in the model parameters affect the [[#Cost Function]] such that we can make the adjustments of the model parameters that lead to the most efficient decrease in the cost function. This is reflected in the partial derivatives of the [[#Cost Function]] with respect to all model parameters.
![[Pasted image 20241117150839.png#invert]]
### Chain-Rule
To get from $C$ to $w^{(L)}$:
$$\frac{\partial C}{\partial w^{(L)}} = \frac{\partial C}{\partial a^{(L)}} \cdot \frac{\partial a^{(L)}}{\partial z^{(L)}} \cdot \frac{\partial z^{(L)}}{\partial w^{(L)}}$$
#### Partial Derivatives
##### First
This needs to be changed accordingly if one uses another loss function (e.g. cross entropy).
$$\frac{\partial C}{\partial a^{(L)}} = -2\left(y-a^{(L)}\right) = 2\left(a^{(L)} - y\right)$$
##### Second (Activation Function)
This one is for the sigmoid function:
$$\begin{split}
\frac{\partial a^{(L)}}{\partial z^{(L)}} &= \frac{\partial }{\partial z^{(L)}} \left(1+e^{-z^{(L)}}\right)^{-1} = (-1) e^{-z^{(L)}} (-1) \left(1+e^{-z^{(L)}}\right)^{-2} =  \frac{e^{-z^{(L)}}}{(1+e^{-z^{(L)}})^2} \\
&=\frac{1}{1+e^{-z^{(L)}}} \cdot \frac{e^{-z^{(L)}} + 1 - 1}{1+e^{-z^{(L)}}} =\frac{1}{1+e^{-z^{(L)}}} \left( \frac{1+e^{-z^{(L)}}}{1+e^{-z^{(L)}}} - \frac{1}{1+e^{-z^{(L)}}} \right) \\
&=\frac{1}{1+e^{-z^{(L)}}} \left( 1- \frac{1}{1+e^{-z^{(L)}}}\right) = \zeta(z^{(L)}) \left(1 - \zeta(z^{(L)}) \right)
\end{split}$$
With generalization of the Activation-Function (last part of the equation above) as follows
$$\frac{\partial a^{(L)}}{\partial z^{(L)}} = \zeta'(z^{(L)})$$
##### Third (Linear Function $z$) [[#Pre-Activation]]
$$\frac{\partial z^{(L)}}{\partial w^{(L)}} = a^{(L-1)}$$
#### Chain-Rule Derived
##### Generalization
$$\frac{\partial C}{\partial w^{(L)}} = 2\left(a^{(L)} - y\right) \cdot \zeta'(z^{(L)}) \cdot a^{(L-1)}$$
##### With Sigmoid
$$\frac{\partial C}{\partial w^{(L)}} = \underbrace{2\left(a^{(L)} - y\right)}_{\frac{\partial C}{\partial{a^{(L)}}}} \cdot \underbrace{\zeta(z^{(L)}) \left(1 - \zeta(z^{(L)}) \right)}_{\frac{\partial a^{(L)}}{\partial z^{(L)}}} \cdot \underbrace{a^{(L-1)}}_{\frac{\partial z^{(L)}}{\partial w^{(L)}}}$$
### Chain-Rule including Bias
$$\frac{\partial C}{\partial b^{(L)}} =
{\color{orange}\frac{\partial C}{\partial a^{(L)}} }
\cdot {\color{orange}\frac{\partial a^{(L)}}{\partial z^{(L)}} }
\cdot \frac{\partial z^{(L)}}{\partial b^{(L)}}$$
which is equal to one
$$\frac{\partial z^{(L)}}{\partial b^{(L)}} = \frac{\partial }{\partial b^{(L)}} \left( w^{(L)}\cdot a^{(L-1)} + b^{(L)} \right) = 1$$
Meaning
$$\frac{\partial C}{\partial b^{(L)}} = {\color{orange} 2\left(a^{(L)} - y\right) \cdot \zeta(z^{(L)}) \left(1 - \zeta(z^{(L)}) \right) } \cdot 1$$
### Re-use Parameters
For upper layers, the terms marked in blue can be reused from the computations of the previous layer $L$:
$$\frac{\partial C}{\partial w^{(L-1)}} =
{\color{orange} \frac{\partial C}{\partial a^{(L)}} }
\cdot {\color{orange} \frac{\partial a^{(L)}}{\partial z^{(L)}} }
\cdot \frac{\partial z^{(L)}}{\partial a^{(L-1)}}
\cdot \frac{\partial a^{(L-1)}}{\partial z^{(L-1)}}
\cdot \frac{\partial z^{(L-1)}}{\partial w^{(L-1)}}$$
The remaining terms (in black) need to be derived:
$$\frac{\partial z^{(L)}}{\partial a^{(L-1)}} = w^{(L)}$$
$$\frac{\partial a^{(L-1)}}{\partial z^{(L-1)}} = \zeta\left(z^{(L-1)}\right) \left(1 - \zeta\left(z^{(L-1)}\right) \right)$$
$$\frac{\partial z^{(L-1)}}{\partial w^{(L-1)}} = a^{(L-2)}$$
#### Layer-by-Layer
##### $L-1$
$$\frac{\partial C}{\partial w^{(L-1)}} =
{\color{orange}
2\left(a^{(L)} - y\right) \cdot \zeta(z^{(L)}) \left(1 - \zeta(z^{(L)}) \right)
}
\cdot w^{(L)}
\cdot \zeta\left(z^{(L-1)}\right) \left(1 - \zeta\left(z^{(L-1)}\right) \right)
\cdot a^{(L-2)}$$
$$\frac{\partial C}{\partial b^{(L-1)}} =
{\color{orange}
2\left(a^{(L)} - y\right) \cdot \zeta(z^{(L)}) \left(1 - \zeta(z^{(L)}) \right)
\cdot w^{(L)}
\cdot \zeta\left(z^{(L-1)}\right) \left(1 - \zeta\left(z^{(L-1)}\right) \right)
}
\cdot 1$$
##### $L-2$
$$\frac{\partial C}{\partial w^{(L-2)}} =
{\color{orange} \frac{\partial C}{\partial a^{(L)}} }
\cdot {\color{orange} \frac{\partial a^{(L)}}{\partial z^{(L)}}  
\cdot \frac{\partial z^{(L)}}{\partial a^{(L-1)}}
\cdot \frac{\partial a^{(L-1)}}{\partial z^{(L-1)}}
}
\cdot \frac{\partial z^{(L-1)}}{\partial a^{(L-2)}}
\cdot \frac{\partial a^{(L-2)}}{\partial z^{(L-2)}}
\cdot \frac{\partial z^{(L-2)}}{\partial w^{(L-2)}}$$
$$\frac{\partial C}{\partial b^{(L-2)}} =
{\color{orange} \frac{\partial C}{\partial a^{(L)}} }
\cdot {\color{orange} \frac{\partial a^{(L)}}{\partial z^{(L)}}  
\cdot \frac{\partial z^{(L)}}{\partial a^{(L-1)}}
\cdot \frac{\partial a^{(L-1)}}{\partial z^{(L-1)}}
\cdot \frac{\partial z^{(L-1)}}{\partial a^{(L-2)}}
\cdot \frac{\partial a^{(L-2)}}{\partial z^{(L-2)}}
}
\cdot \frac{\partial z^{(L-2)}}{\partial b^{(L-2)}}$$
and so on...

**Note that in our simple example our training set had just one sample. When the training set has many samples, the partial derivatives are also averaged among all training samples. This is the case because the cost function is computed as the average over the individual costs for all training samples.**
## Overfitting
### Dropout
Deactivating a randomly selected proportion of the neurons during training (the deactivated neurons change per iteration). This randomness forces the network to not rely excessively on any specific set of neurons (=> more **robust**, less sensitive to specific weights). This is only applied in the training process. Dropout percentage is a hyperparameter (typically between 20-50%).
![[Pasted image 20241117152827.png#invert]]
### Early Stopping
Terminating the training process before the model has reached the point of overfitting (by periodical performance evaluation).
![[Pasted image 20241117153204.png#invert]]
### Data Augmentation
Approach used to increase the size and diversity of training data without actually collecting or labelling new data.
#### Images
- rotations, scaling, cropping, flipping, adjusting brightness or contrast, decolorizing
![[Pasted image 20241117153355.png#invert]]
#### Text
- synonym replacement or translation back and forth between different languages
![[Pasted image 20241117153405.png#invert]]
#### Audio
- frequency channels and time steps in the mel spectrogram
![[Pasted image 20241117153415.png#invert]]