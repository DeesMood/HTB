![](Pasted%20image%2020250821073709.png)
`Linear Regression` is a fundamental `supervised learning` algorithm that predicts a continuous target variable by establishing a linear relationship between the target and one or more predictor variables.

Imagine you're trying to predict a house's price based on size. Linear regression would attempt to find a straight line that best captures the relationship between these two variables. As the size of the house increases, the price generally tends to increase. Linear regression quantifies this relationship, allowing us to predict the price of a house given its size.

# **What is Regression?**

Regression analysis is a type of supervised learning where the goal is to predict a continuous target variable.

Examples of regression problems include:

- Predicting the price of a house based on its size, location, and age.
- Forecasting the daily temperature based on historical weather data.
- Estimating the number of website visitors based on marketing spend and time of year.

# Simple Linear Regression

![](Pasted%20image%2020250821073727.png)
- Nathan asking
    - What is the difference between predictor and target variable?
        - **Predictor variables (inputs / features):**
            - Size of the house (sq. ft)
            - Number of bedrooms
            - Location score
            - Age of the house
        - **Target variable (output):**
            - Price of the house

# Multiple Linear Regression
![](Pasted%20image%2020250821073752.png)
# **Ordinary Least Squares**

![](Pasted%20image%2020250821073808.png)
# Assumptions of Linear Regression

Linear regression relies on several key assumptions about the data:

- `Linearity:` A linear relationship exists between the predictor and target variables.
- `Independence:` The observations in the dataset are independent of each other.
    - Example: In time series data, today’s value often depends on yesterday’s → this would violate independence.
- `Homoscedasticity:` The variance of the errors is constant across all levels of the predictor variables. This means the spread of the residuals should be roughly the same across the range of predicted values.
- `Normality:` The errors are normally distributed. This assumption is important for making valid inferences about the model's coefficients.
- Nathan asking
    - What is residuals?
        ![](Pasted%20image%2020250821073846.png)        