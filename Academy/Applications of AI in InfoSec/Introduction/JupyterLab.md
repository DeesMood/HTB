`JupyterLab` is an interactive development environment that provides web-based coding, data, and visualization interfaces.
## Why JupyterLab?

- `Interactive Environment`: `JupyterLab` allows running code in individual cells, facilitating experimentation and iterative development.
- `Data Exploration and Visualization`: It integrates seamlessly with libraries like `matplotlib` and `seaborn` for creating visualizations and exploring data.
- `Documentation and Sharing`: `JupyterLab` supports markdown and LaTeX for creating rich documentation and sharing code with others.
`JupyterLab` can be easily installed using `conda`, if it isn't already installed:

  JupyterLab

```shell-session
JustSomeRedTeamer@htb[/htb]$ conda install -y jupyter jupyterlab notebook ipykernel 
```

Make sure you are running the command from within your ai environment.

To start `JupyterLab`, simply run:

  JupyterLab

```shell-session
JustSomeRedTeamer@htb[/htb]$ jupyter lab
```

This will open a new tab in your web browser with the `JupyterLab` interface.
## Using JupyterLab
`JupyterLab`'s primary component is the notebook, which allows combining code, text, and visualizations in a single document. Notebooks are organized into cells, where each cell can contain either code or markdown text.

- `Code cells`: Execute code in various languages (Python, R, Julia).
- `Markdown cells`: Create formatted text, equations, and images using markdown syntax.
- `Raw cells`: Untyped raw text.
Testing how python notebook works.
![](Pasted%20image%2020250821143200.png)
`Jupyter` notebooks use a `stateful` environment, which means that variables, functions, and imports defined in one cell remain available to all later cells. Once you execute a cell, any changes it makes to the environment, such as assigning new variables or redefining functions, persist as long as the kernel is running. This differs from a `stateless` model, where each code execution is isolated and does not retain information from previous executions.
![](Pasted%20image%2020250821143407.png)
![](Pasted%20image%2020250821143455.png)

Integrating libraries for computing and plotting.
```python
import pandas as pd

import matplotlib.pyplot as plt

import numpy as np

  

# Create a sample DataFrame

data = pd.DataFrame({

    "column1": np.random.rand(50),  # 50 random values for column1

    "column2": np.random.rand(50) * 10 # 50 random values (multiplied by 10) for column2

})

  

# Display the first few rows

print(data.head())

  

# Create a scatter plot

plt.scatter(data["column1"], data["column2"])

plt.xlabel("Column 1")

plt.ylabel("Column 2")

plt.title("Scatter Plot")

plt.show()
```
![](Pasted%20image%2020250821144235.png)

## Restarting the Kernel
`JupyterLab` uses a `kernel` to run your code. The `kernel` is a separate process responsible for executing code and maintaining the state of your computations. Sometimes, you may need to reset your environment if it becomes cluttered with variables or you encounter unexpected behavior.
To restart the `kernel`:

1. Open the `Kernel` menu in the top toolbar.
2. Select `Restart Kernel` to reset the environment while preserving cell outputs, or `Restart Kernel and Clear All Outputs` to also remove all previously generated outputs from the notebook.