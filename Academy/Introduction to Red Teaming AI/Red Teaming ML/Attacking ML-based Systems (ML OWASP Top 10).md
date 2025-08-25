Just like for [Web Applications](https://owasp.org/www-project-top-ten/), [Web APIs](https://owasp.org/www-project-api-security/), and [Mobile Applications](https://owasp.org/www-project-mobile-top-10/), OWASP has published a Top 10 list of security risks regarding the deployment and management of ML-based Systems, the [Top 10 for Machine Learning Security](https://owasp.org/www-project-machine-learning-security-top-10/). We will briefly discuss the ten risks to obtain an overview of security issues resulting from ML-based systems.

| ID   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ML01 | `Input Manipulation Attack`: Attackers modify input data to cause incorrect or malicious model outputs.                                                                                                                                                                                                                                                                                                                                                                                          |
| ML02 | `Data Poisoning Attack`: Attackers inject malicious or misleading data into training data, compromising model performance or creating backdoors.                                                                                                                                                                                                                                                                                                                                                 |
| ML03 | `Model Inversion Attack`: Attackers train a separate model to reconstruct inputs from model outputs, potentially revealing sensitive information.                                                                                                                                                                                                                                                                                                                                                |
| ML04 | `Membership Inference Attack`: Attackers analyze model behavior to determine whether data was included in the model's training data set, potentially revealing sensitive information.<br><br>A **membership inference attack** means the attacker doesn’t steal the model itself, but instead uses it to figure out **who’s in the training data** — which can reveal private or sensitive information.                                                                                          |
| ML05 | `Model Theft`: Attackers train a separate model from interactions with the original model, thereby stealing intellectual property.                                                                                                                                                                                                                                                                                                                                                               |
| ML06 | `AI Supply Chain Attacks`: Attackers exploit vulnerabilities in any part of the ML supply chain.                                                                                                                                                                                                                                                                                                                                                                                                 |
| ML07 | `Transfer Learning Attack`: Attackers manipulate the baseline model that is subsequently fine-tuned by a third-party. This can lead to biased or backdoored models.<br><br>### 🔹 What is a _Transfer Learning Attack_?<br><br>- If an attacker provides or tampers with the **baseline model**, they can secretly insert **biases** or **backdoors**.<br>    <br>- When a third-party later fine-tunes this model on their own dataset, the malicious changes persist — but are hard to notice. |
| ML08 | `Model Skewing`: Attackers skew the model's behavior for malicious purposes, for instance, by manipulating the training data set.                                                                                                                                                                                                                                                                                                                                                                |
| ML09 | `Output Integrity Attack`: Attackers manipulate a model's output before processing, making it look like the model produced a different output.<br><br>It’s when an attacker **doesn’t change the model itself**, but instead **alters the output after the model has made a prediction**, so the downstream system (or user) sees a **fake or manipulated result**.                                                                                                                              |
| ML10 | `Model Poisoning`: Attackers manipulate the model's weights, compromising model performance or creating backdoors.                                                                                                                                                                                                                                                                                                                                                                               |
## Input Manipulation Attack (ML01)
As the name suggests, input manipulation attacks comprise any type of attack against an ML model that results from manipulating the input data. Typically, the result of these attacks is unexpected behavior of the ML model that deviates from the intended behavior. The impact depends highly on the concrete scenario and circumstances in which the model is used. It can range from financial and reputational damage to legal consequences or data loss. For more details on this attack vector, check out [this](https://arxiv.org/pdf/1707.08945) and [this](https://arxiv.org/pdf/2307.08278) paper.

![](Pasted%20image%2020250825123125.png)

## Data Poisoning Attack (ML02)
Data poisoning attacks on ML-based systems involve injecting malicious or misleading data into the training dataset to compromise the model's accuracy, performance, or behavior. As such, these attacks can cause a model to make incorrect predictions, misclassify certain inputs, or behave unpredictably in specific scenarios.

More details about installing backdoors through data poisoning attacks are discussed in [this](https://arxiv.org/pdf/2408.13221) paper.

## Model Inversion Attack (ML03)

In model inversion attacks, an adversary trains a separate ML model on the output of the target model to reconstruct information about the target model's inputs. Since the model trained by the adversary operates on the target model's output and reconstructs information about the inputs, it `inverts` the target model's functionality, hence the name `model inversion attack`.

An approach for model inversion of language models is discussed in [this](https://arxiv.org/pdf/2311.13647) paper.

## Membership Inference Attack (ML04)

Membership inference attacks seek to determine whether a specific data sample was included in the model's original training data set.

An extensive assessment of the performance of membership inference attacks on language models is performed in [this](https://arxiv.org/pdf/2402.07841) paper.

![](Pasted%20image%2020250825123732.png)

## Model Theft (ML05)

Model theft or model extraction attacks aim to duplicate or approximate the functionality of a target model without direct access to its underlying architecture or parameters.

For more details on the effectiveness of model theft attacks on a specific type of neural network, check out [this](https://arxiv.org/pdf/2305.13584) paper.

![](Pasted%20image%2020250825123849.png)

## AI Supply Chain Attacks (ML06)

Supply chain attacks on ML-based systems target the complex, interconnected ecosystem involved in creating, deploying, and maintaining ML models. These attacks exploit vulnerabilities in any part of the ML pipeline, such as third-party data sources, libraries, or pre-trained models, to compromise the model's integrity, security, or performance.
## Transfer Learning Attack (ML07)

Open-source pre-trained models are used as a baseline for many ML model deployments due to the high computational cost of training models from scratch. New models are then built on top of these pre-trained models by applying additional training to fine-tune the model to the specific task it is supposed to execute. In transfer learning attacks, adversaries exploit this transfer process by manipulating the pre-trained model. Security issues such as backdoors or biases may arise if these manipulations persist in the fine-tuned model. Even if the data set used for fine-tuning is benign, malicious behavior from the pre-trained model may carry over to the final ML-based system.

## Model Skewing (ML08)

In model skewing attacks, an adversary attempts to deliberately skew a model's output in a biased manner that favors the adversary's objectives. They can achieve this by injecting biased, misleading, or incorrect data into the training data set to influence the model's output toward maliciously biased outcomes.

In particular, an attacker might add their own malware binary with a `benign` label to the training data to evade detection by the trained model.

## Output Integrity Attack (ML09)

If an attacker can alter the output produced by an ML-based system, they can execute an output integrity attack. This attack does not target the model itself but only the model's output. More specifically, the attacker does not manipulate the model directly but intercepts the model's output before the respective target entity processes it.

As an example, consider the ML malware classifier again. Let us assume that the system acts based on the classifier's result and deletes all binaries from the disk if classified as malware. If an attacker can manipulate the classifier's output before the succeeding system acts, they can introduce malware by exploiting an output integrity attack. After copying their malware to the target system, the classifier will classify the binary as malicious. The attacker then manipulates the model's output to the label `benign` instead of `malicious`. Subsequently, the succeeding system does not delete the malware as it assumes the binary was not classified as malware.
## Model Poisoning (ML10)

While data poisoning attacks target the model's training data and, thus, indirectly, the model's parameters, model poisoning attacks target the model's parameters directly. As such, an adversary needs access to the model parameters to execute this type of attack. The impact of model poisoning attacks is similar to data poisoning attacks, as it can lead to incorrect predictions, misclassification of certain inputs, or unpredictable behavior in specific scenarios.

For more details regarding an actual model poisoning attack vector, check out [this](https://arxiv.org/pdf/2405.20975) paper.


