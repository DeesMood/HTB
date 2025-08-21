`Diffusion models` are a class of generative models that have gained significant attention for their ability to generate high-quality images.
## How Diffusion Models Work
![](Pasted%20image%2020250821095428.png)
Diffusion models function by gradually adding noise to an input image and then learning to reverse this process to generate new images.

To generate an image from a textual prompt, diffusion models typically integrate a text encoder, such as a `Transformer` or `CLIP`, to convert the text into a latent representation. This latent representation then conditions the denoising process, ensuring the generated image aligns with the prompt.

1. `Text Encoding:` The first step is to encode the textual prompt using a pre-trained text encoder. For example, the prompt "a cat in a hat" is converted into a high-dimensional vector that captures the semantic meaning of the text. This vector serves as a conditioning input for the diffusion model.
2. `Conditioning the Denoising Process:` The latent representation of the text is used to condition the denoising network. During the reverse process, the denoising network predicts the noise to be removed and ensures that the generated image aligns with the textual prompt. This is achieved by modifying the loss function to include a term that measures the discrepancy between the generated image and the text embedding.
3. **Sampling (denoising)** → The model starts from random noise and, step by step, removes noise while using the text meaning as a guide.
    
4. **Final image** → After many steps, the noise becomes a clear image that matches the prompt.

![](Pasted%20image%2020250821095918.png)
![](Pasted%20image%2020250821095931.png)
![](Pasted%20image%2020250821095952.png)
### Denoising Network
The denoising network is a neural network that learns to predict the noise at each time step. This network is typically a deep convolutional neural network (CNN) or a transformer, depending on the complexity of the data. The input to the network is the noisy data `x_t`, and the output is the predicted noise `hat{ε}`.
### Training
Training a diffusion model involves minimizing the loss function over multiple time steps. This is done using gradient descent and backpropagation. The training process can be computationally intensive, especially for high-resolution images, but it results in a model that can generate high-quality samples.

The training process can be summarized as follows:

1. `Initialize the Model:` Start with an initial set of parameters `θ` for the denoising network.
2. `Forward Process:` Add noise to the original data using the noise schedule.
3. `Reverse Process:` Train the denoising network to predict the noise at each time step.
4. `Loss Calculation:` Compute the loss between predicted and actual noise.
5. `Parameter Update:` To minimize the loss, update the model parameters using gradient descent.
6. `Iterate:` Repeat the process for multiple epochs until the model converges.
### Sampling
![](Pasted%20image%2020250821100130.png)
![](Pasted%20image%2020250821100144.png)
## Data Assumptions
- `Markov Property:` The diffusion process exhibits the Markov property. This means that each step in both the forward (adding noise) and reverse (removing noise) processes depends only on the immediately preceding step, not the entire history of the process.
- `Static Data Distribution:` Diffusion models are trained on a fixed dataset, and they learn to represent the underlying distribution of this data. This data distribution is assumed to be static during training.
- `Smoothness Assumption:` While not a strict requirement, diffusion models often perform well when the data distribution is smooth. This means that small changes in the input data result in small changes in the output. This assumption helps the model learn the underlying structure of the data and generate realistic samples.


