Now that we have explored common security vulnerabilities that arise from improper implementation of ML-based systems let us take a look at a practical example. We will explore how an ML model reacts to changes in input data and training data to better understand how vulnerabilities related to data manipulation arise. These include input manipulation attacks (ML01) and data poisoning attacks (ML02).

We will use the spam classifier code from the [Applications of AI in InfoSec](https://academy.hackthebox.com/module/details/292) module as a baseline. Therefore, it is recommended that you complete that module first.
## Manipulating the Input

The code contains training and test data sets in CSV files. In the file `main.py`, we can see that a classifier is trained on the provided training set and evaluated on the provided test set:

```python
model = train("./train.csv")
acc = evaluate(model, "./test.csv")
print(f"Model accuracy: {round(acc*100, 2)}%")
```

Running the file, the classifier provides a solid accuracy of `97.2%`.

To understand how the model reacts to certain words in the input, let us take a closer look at an inference run on a single input data item. We can utilize the function `classify_messages` to run inference on a given input message. The function also supports a keyword argument `return_probabilities`, which we can set to `True` if we want the function to return the classifier's output probabilities instead of the predicted class. We will look at the output probabilities since we are interested in the model's reaction to the input. The function `classify_messages` returns a list of probabilities for all classes. We are using a spam classifier that only classifies into two classes: ham (class `0`) and spam (class `1`). The class predicted by the classifier is the one with the higher output probability.

Let us adjust the code to print the output vulnerabilities for both classes for a given input message:

```python
model = train("./train.csv")

message = "Hello World! How are you doing?"

predicted_class = classify_messages(model, message)[0]
predicted_class_str = "Ham" if predicted_class == 0 else "Spam"
probabilities = classify_messages(model, message, return_probabilities=True)[0]

print(f"Predicted class: {predicted_class_str}")
print("Probabilities:")
print(f"\t Ham: {round(probabilities[0]*100, 2)}%")
print(f"\tSpam: {round(probabilities[1]*100, 2)}%")
```
![](Pasted%20image%2020250825125823.png)

As we can see, the model is very confident about our input message. This intuitively makes sense, as our input message does not look like spam. Let us change the input to something we would identify as spam, like: `Congratulations! You won a prize. Click here to claim: https://bit.ly/3YCN7PF`.

![](Pasted%20image%2020250825125948.png)

In an input manipulation attack, our aim as attackers is to provide input to the model that results in misclassification. In our case, let us try to trick the model into classifying a spam message as ham. We will explore two different techniques in the following.

#### Rephrasing

First, we should determine how the model reacts to certain parts of our input message. For instance, if we remove everything from our input message except for the word `Congratulations!`, we can see how this particular word influences the model. Interestingly, this single word is already classified as spam:

![](Pasted%20image%2020250825130108.png)

We should continue this with different parts of our input message to get a feel for the model's reaction to certain words or combinations of words. From there, we know which words to avoid to get our input past the classifier:

| Input Message                                 | Spam Probability | Ham Probability |
| --------------------------------------------- | ---------------- | --------------- |
| `Congratulations!`                            | 64.97%           | 35.03%          |
| `Congratulations! You won a prize.`           | 99.73%           | 0.27%           |
| `Click here to claim: https://bit.ly/3YCN7PF` | 99.34%           | 0.66%           |
| `https://bit.ly/3YCN7PF`                      | 87.29%           | 12.71%          |
From this knowledge, we can try different words and phrases with a low probability of being flagged as spam. In our particular case, we are successful with a different scenario for the reasons outlined before. If we change the input message to `Your account has been blocked. You can unlock your account in the next 24h: https://bit.ly/3YCN7PF`, the input will (barely) be classified as ham:

![](Pasted%20image%2020250825130247.png)

This technique works particularly well in cases where we can hide the appended message from the victim. Think of websites or e-mails that support HTML where we can hide words from the user in HTML comments while the spam classifier may not be HTML context-aware and thus still base the spam verdict on words contained in HTML comments.

#### Overpowering

Another technique is overpowering the spam message with benign words to push the classifier toward a particular class. We can achieve this by simply appending words to the original spam message until the ham content overpowers the message's spam content.

```
Congratulations! You won a prize. Click here to claim: https://bit.ly/3YCN7PF. But I must explain to you how all this mistaken idea of denouncing pleasure and praising pain was born and I will give you a complete account of the system, and expound the actual teachings of the great explorer of the truth, the master-builder of human happiness.
```
## Manipulating the Training Data

After exploring how manipulating the input data affects the model output, let us move on to the training data. To achieve this, let us create a separate training data set to experiment on. We will shorten the training data set significantly so our manipulations will have a more significant effect on the model. Let us extract the first 100 data items from the training data set and save it to a separate CSV file:

```shell-session
head -n 101 train.csv  > poison.csv
```

Afterward, we can change the training data set in `main.py` to `poison.csv` and run the Python script:

```shell-session
Model accuracy: 94.4%
```

As we can see, the model's accuracy drops slightly to `94.4%`, which is impressive for the tiny size of the training data set. The drop in accuracy can be explained by the significant reduction in training data, making the classifier less representative and more sensitive to changes. However, this sensitivity to changes is exactly what we want to demonstrate by injecting fake spam entries to the data set (`poisoning`). To observe the effect of manipulations on the training data set, let us adjust the code as we did before to print the output probabilities for a single input message:

```python
model = train("./poison.csv")

message = "Hello World! How are you doing?"

predicted_class = classify_messages(model, message)[0]
predicted_class_str = "Ham" if predicted_class == 0 else "Spam"
probabilities = classify_messages(model, message, return_probabilities=True)[0]

print(f"Predicted class: {predicted_class_str}")
print("Probabilities:")
print(f"\t Ham: {round(probabilities[0]*100, 2)}%")
print(f"\tSpam: {round(probabilities[1]*100, 2)}%")
```

If we run the script, the classifier classifies the input message as ham with a confidence of `98.7%`. Now, let us manipulate the training data so that the input message will be classified as spam instead.

To achieve this, we inject additional data items into the training data set that facilitate our goal. For instance, we could add fake `spam` labeled data items with the two phrases of our input message to the CSV file:

```
spam,Hello World
spam,How are you doing?
```

After rerunning the script, the model now produces the following result:

![](Pasted%20image%2020250825131118.png)

As we can see, this minor tweak to the training data set was already sufficient to change the classifier's prediction. We can increase the confidence further by appending two additional fake data items to the training data set. This time, we will use a combination of both phrases:

```
spam,Hello World! How are you
spam,World! How are you doing?
```

![](Pasted%20image%2020250825131216.png)

As a final experiment, let us add the evaluation code back in to see how our training data set manipulation affected the overall model accuracy:

```python
model = train("./poison.csv")

acc = evaluate(model, "./test.csv")
print(f"Model accuracy: {round(acc*100, 2)}%")

message = "Hello World! How are you doing?"

predicted_class = classify_messages(model, message)[0]
predicted_class_str = "Ham" if predicted_class == 0 else "Spam"
probabilities = classify_messages(model, message, return_probabilities=True)[0]

print(f"Predicted class: {predicted_class_str}")
print("Probabilities:")
print(f"\t Ham: {round(probabilities[0]*100, 2)}%")
print(f"\tSpam: {round(probabilities[1]*100, 2)}%")
```

![](Pasted%20image%2020250825131516.png)

We forced the classifier to misclassify a particular input message by manipulating the training data set. We achieved this without a substantial adverse effect on model accuracy, which is why data poisoning attacks are both powerful and hard to detect. Remember that we deliberately shrunk the training data set significantly so that our manipulated data items had a higher effect on the model. In larger training data sets, many more manipulated data items are required to affect the model in the desired way.
#### Questions
Manipulate the fixed input message by appending data to trick the classifier into classifying the message as ham.

Congratulations! You've won a $1000 Walmart gift card. Go to https://bit.ly/3YCN7PF to claim now. A turtle is a fascinating reptile known for its protective shell, which serves as both armor and shelter. Unlike many animals, turtles carry their homes on their backs, with the top part called the carapace and the bottom known as the plastron. They are found in a wide variety of environments, from oceans and rivers to forests and deserts, and their diet can range from plants and algae to insects and small fish, depending on the species. Turtles are also remarkable for their longevity, with some living well over a hundred years. Their slow, deliberate movements and calm demeanor have made them symbols of wisdom, patience, and endurance in many cultures around the world.

HTB{9b8de0fd17f2166743cd59f7ec876ac7}

Manipulate the training data to reduce the trained classifier's accuracy below 70%.
![](training_data%20(1).csv)
HTB{8ba5eff39c343c3b0170e6bb1704df02}

 Exploit a flaw in the web application to steal the trained model. Submit the file's MD5 hash as the flag.

Check the source code of the page

Flag: 8007cd6c209a40399cf3ca82dd7db02c



