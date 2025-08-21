`Recurrent Neural Networks` (`RNNs`) are a class of artificial neural networks specifically designed to handle sequential data, where the order of the data points matters.
## Handling Sequential Data
![](Pasted%20image%2020250821092151.png)
The key to understanding how RNNs handle sequential data lies in their recurrent connections. These connections create loops within the network, allowing information to persist and be passed from one step to the next. Imagine an RNN processing a sentence word by word. As it encounters each word, it considers the current input and incorporates information from the previous words, effectively "remembering" the context.

This process can be visualized as a chain of repeating modules, each representing a time step in the sequence. At each step, the network takes:
    
    1. The **current input** (e.g., a word).
        
    2. The **hidden state** (memory) from the previous step.
        
-It produces:
    
    1. An **output** for the current step.
        
    2. An **updated hidden state** (memory) to carry forward.

For example, consider the sentence, "The cat sat on the mat." An RNN processing this sentence would:

1. Start with an initial hidden state (usually set to 0).
2. Process the word "The," and update its hidden state based on this input.
3. Process the word "cat," considering both the word itself and the hidden state now containing information about "The."
4. Continue processing each word this way, accumulating context in the hidden state at each step.

## The Vanishing Gradient Problem
- **Backpropagation Through Time (BPTT):** trains RNNs by sending error signals backwards through all time steps.
    
- Problem: as the error signal goes back further, it often becomes **tiny (vanishes)**.
    
- Result: the network can’t properly update weights for **earlier inputs**, so it struggles to learn **long-term dependencies** (things far back in the sequence).
### LSTMs and GRUs
To address the vanishing gradient problem, researchers have developed specialized RNN architectures, namely `Long-Short-Term Memory (LSTM)` and `Gated Recurrent Unit (GRU)` networks. These architectures introduce gating mechanisms that control the flow of information through the network, allowing them to better capture long-term dependencies.
![](Pasted%20image%2020250821092544.png)
`LSTMs` incorporate memory cells that can store information over extended periods. These cells are equipped with three gates:

- `Input gate:` Regulates the flow of new information into the memory cell.
- `Forget gate:` Controls how much of the existing information in the memory cell is retained or discarded.
- `Output gate:` Determines what information from the memory cell is output to the next time step.
![](Pasted%20image%2020250821092627.png)
`GRUs` offer a simpler alternative to LSTMs, with only two gates:

- `Update gate:` Controls how much of the previous hidden state is retained.
- `Reset gate:` Determines how much of the previous hidden state is combined with the current input.
## Bidirectional RNNs
In addition to the standard RNNs that process sequences in a forward direction, there are also `bidirectional RNNs`. These networks process the sequence in both forward and backward directions simultaneously.

