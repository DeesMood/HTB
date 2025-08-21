![](Pasted%20image%2020250821085817.png)
To overcome the limitations of single-layer perceptron's, we introduce the concept of `neural networks` with multiple layers. These networks, also known as `multi-layer perceptrons` (`MLPs`), are composed of:

- An input layer
- One or more hidden layers
- An output layer
## Neurons
A `neuron` is a fundamental computational unit in neural networks. It receives inputs, processes them using weights and a bias, and applies an activation function to produce an output.

## Input Layer
![](Pasted%20image%2020250821085946.png)
The `input layer` serves as the entry point for the data. Each neuron in the input layer corresponds to a feature or attribute of the input data. The input layer passes the data to the first hidden layer.
## Hidden Layers
![](Pasted%20image%2020250821090011.png)
`Hidden layers` are the intermediate layers between the input and output layers. They perform computations and extract features from the data. Each neuron in a hidden layer:

1. Receives input from all neurons in the previous layer.
2. Performs a weighted sum of the inputs.
3. Adds a bias to the sum.
4. Applies an activation function to the result.
## Output Layer
![](Pasted%20image%2020250821090042.png)
The `output layer` produces the network's final result. The number of neurons in the output layer depends on the specific task:

- A binary classification task would have one output neuron.
- A multi-class classification task would have one neuron for each class.
## The Power of Multiple Layers
Multi-layer perceptrons (`MLPs`) overcome the limitations of single-layer perceptrons primarily by learning non-linear decision boundaries. By incorporating multiple hidden layers with non-linear activation functions, `MLPs` can approximate complex functions and capture intricate patterns in data that are not linearly separable.
## Activation Functions
- They take the weighted sum of inputs in a neuron and decide how much signal to pass forward.
    
- This adds **non-linearity**, letting the network learn complex patterns (not just straight lines).
### Types of Activation Functions
- `Sigmoid:` The sigmoid function squashes the input into a range between 0 and 1. It was historically popular but is now less commonly used due to issues like vanishing gradients.
- `ReLU (Rectified Linear Unit):` ReLU is a simple and widely used activation function. It returns 0 for negative inputs and the input value for positive inputs. ReLU often leads to faster training and better performance.
- `Tanh (Hyperbolic Tangent):` The tanh function squashes the input into a range between -1 and 1. It is similar to the sigmoid function but centered at 0.
- `Softmax:` The softmax function is often used in the output layer for multi-class classification problems. It converts a vector of raw scores into a probability distribution over the classes.
## Training MLPs
Training a multi-layer perceptron (`MLP`) involves adjusting the network's weights and biases to minimize the error between its predictions and target values. This process is achieved through a combination of `backpropagation` and `gradient descent`.
### Backpropagation
![](Pasted%20image%2020250821090531.png)
`Backpropagation` is an algorithm for calculating the gradient of the loss function concerning the network's weights and biases.
Here's a simplified overview of the backpropagation process:

1. `Forward Pass:` The input data is fed through the network, and the output is calculated.
2. `Calculate Error:` A loss function calculates the difference between the predicted output and the actual target value.
3. `Backward Pass:` The error signal is propagated back through the network. For each layer, the gradient of the loss function concerning the weights and biases is calculated using the calculus chain rule.
4. `Update Weights and Biases:` The weights and biases are updated to reduce errors. This is typically done using an optimization algorithm like gradient descent.
### Gradient Descent
![](Pasted%20image%2020250821090638.png)
`Gradient descent` is an iterative optimization algorithm used to find the minimum of a function. In the context of `MLPs`, the loss function is minimized.
Here's a simplified explanation of gradient descent:

1. `Initialize Weights and Biases:` Start with random values for the weights and biases.
2. `Calculate Gradient:` Use backpropagation to calculate the gradient of the loss function with respect to the weights and biases.
3. `Update Weights and Biases:` Subtract a fraction of the gradient from the current weights and biases. The learning rate determines the fraction.
4. `Repeat:` Repeat steps 2 and 3 until the loss function converges to a minimum or a predefined number of iterations is reached.

**Backpropagation and gradient descent work together to train `MLPs`. Backpropagation calculates the gradients, while gradient descent uses those gradients to update the network's parameters and minimize the loss function.**



