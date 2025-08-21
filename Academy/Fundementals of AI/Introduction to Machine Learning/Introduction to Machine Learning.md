# Artificial Intelligence (AI)
The scope of AI, just to make sure you don't confuse it with Machine Learning (ML).
![](Pasted%20image%2020250820104136.png)

**AI as a field is focused on developing an intelligent system to do tasks that requires human intelligence**. Some key areas:
- `Natural Language Processing` (`NLP`): Enabling computers to understand, interpret, and generate human language.
- `Computer Vision`: Allowing computers to "see" and interpret images and videos.
- `Robotics`: Developing robots that can perform tasks autonomously or with human guidance.
- `Expert Systems`: Creating systems that mimic the decision-making abilities of human experts.

# Machine Learning
**ML is a subfield of AI that focuses on making a system that could do tasks on its own without explicit programming where it learns from data.**

Categories of ML:
- `Supervised Learning`: The algorithm learns from labeled data, where each data point is associated with a known outcome or label. Examples include:
    - Image classification
    - Spam detection
    - Fraud prevention
- `Unsupervised Learning`: The algorithm learns from unlabeled data without providing an outcome or label. Examples include:
    - Customer segmentation
    - Anomaly detection
    - Dimensionality reduction
- `Reinforcement Learning`: The algorithm learns through trial and error by interacting with an environment and receiving feedback as rewards or penalties. Examples include:
    - [Game playing](https://youtu.be/DmQ4Dqxs0HI)
    - [Robotics](https://www.youtube.com/watch?v=K-wIZuAA3EY)
    - [Autonomous driving](https://www.youtube.com/watch?v=OopTOjnD3qY)

ML has a wide range of applications across various industries, including:
- `Healthcare`: Disease diagnosis, drug discovery, personalized medicine
- `Finance`: Fraud detection, risk assessment, algorithmic trading
- `Marketing`: Customer segmentation, targeted advertising, recommendation systems
- `Cybersecurity`: Threat detection, intrusion prevention, malware analysis
- `Transportation`: Traffic prediction, autonomous vehicles, route optimization
# Deep Learning (DL)
`Deep Learning` (`DL`) is a subfield of ML that uses neural networks with multiple layers to learn and extract features from complex data. These deep neural networks can automatically identify intricate patterns and representations within large datasets, making them particularly powerful for tasks involving unstructured or high-dimensional data, such as images, audio, and text.

Key characteristics of DL include:

- `Hierarchical Feature Learning`: DL models can learn hierarchical data representations, where each layer captures increasingly abstract features. For example, lower layers might detect edges and textures in image recognition, while higher layers identify more complex structures like shapes and objects.
- `End-to-End Learning`: DL models can be trained end-to-end, meaning they can directly map raw input data to desired outputs without manual feature engineering.
	📌 **Example (Speech Recognition):**
	- Old ML approach → convert audio to hand-crafted features (like MFCCs), then train a classifier.
    - DL approach → feed in the **raw audio waveform**, and the network learns both the features (phonemes, tones) and the mapping to words → end-to-end.
- `Scalability`: DL models can scale well with large datasets and computational resources, making them suitable for big data applications.

Common types of neural networks used in DL include:
- `Convolutional Neural Networks` (`CNNs`): Specialized for image and video data, CNNs use convolutional layers to detect local patterns and spatial hierarchies.
- `Recurrent Neural Networks` (`RNNs`): Designed for sequential data like text and speech, RNNs have loops that allow information to persist across time steps.
- `Transformers`: A recent advancement in DL, transformers are particularly effective for natural language processing tasks. They leverage self-attention mechanisms to handle long-range dependencies.