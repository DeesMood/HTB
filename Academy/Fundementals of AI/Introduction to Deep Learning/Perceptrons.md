The `perceptron` is a fundamental building block of neural networks. It is a simplified model of a biological neuron that can make basic decisions.
## Structure of a Perceptron
![](Pasted%20image%2020250821085509.png)
A perceptron consists of the following components:

- `Input Values (x1​, x2​, ..., xn​):` These are the initial data points fed into the perceptron. Each input value represents a feature or attribute of the data.
- `Weights (w1, w2, ..., wn):` Each input value is associated with a weight, determining its strength or importance. Weights can be positive or negative and influence the output of the perceptron.
- `Summation Function (∑):` The weighted inputs are summed together as `∑(wi * xi)` . This step aggregates the weighted inputs into a single value.
- `Bias (b):` A bias term is added to the weighted sum to shift the activation function. It allows the perceptron to activate even when all inputs are zero.
- `Activation Function (f):` The activation function introduces non-linearity into the perceptron. It takes the weighted sum plus the bias as input and produces an output based on a predefined threshold.
- `Output (y):` The final output of the perceptron, typically a binary value (0 or 1) representing a decision or classification.

## Deciding to Play Tennis

Let's illustrate the functionality of a perceptron with a simple example: deciding whether to play tennis based on weather conditions. We'll consider four input features:

- `Outlook`: Sunny (0), Overcast (1), Rainy (2)
- `Temperature`: Hot (0), Mild (1), Cool (2)
- `Humidity`: High (0), Normal (1)
- `Wind`: Weak (0), Strong (1)

Our perceptron will take these inputs and output a binary decision: `Play Tennis` (1) or `Don't Play Tennis` (0).

For simplicity, let's assume the following weights and bias:

- `w1` (Outlook) = 0.3
- `w2` (Temperature) = 0.2
- `w3` (Humidity) = -0.4
- `w4` (Wind) = -0.2
- `b` (Bias) = 0.1

![](Pasted%20image%2020250821085657.png)
![](Pasted%20image%2020250821085712.png)

![](Pasted%20image%2020250821085724.png)

## The Limitations of Perceptrons
While perceptrons provide a foundational understanding of neural networks, single-layer perceptrons have significant limitations that restrict their applicability to more complex tasks.

A classic example is the XOR problem. The XOR function returns true (1) if only one of the inputs is true and false (0) otherwise. It's impossible to draw a single straight line that separates the true and false outputs of the XOR function. This limitation severely restricts the types of problems a single-layer perceptron can solve.
