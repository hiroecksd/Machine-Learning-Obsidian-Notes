# Probability Review
$p(A,B)$ is a joint distribution: Given two random variables that are on the same probability space, the joint distribution is the corresponding probability distribution on all possible pairs of outputs.**The probability of two events (variables) happening together**.
$p(A | B)$ is a condition distribution: What is the probability distribution of $A$ given that we already know $B$. 
## Example: 
Given $p(x,y)$ find $p(y)$. the process is called **marginalization** and $p(y)$ is the marginal distribution, discrete: $$p(y) = \sum_{x} p(x,y)$$ Continuous: $$p(y) = \int p(x,y) dx$$
# Expected Value
$E(X)$ is the expected value. How do you calculate the expected value? 
Discrete: 
$$E(X) = \sum_{x} xp(x)$$ Continuous: $$E(X) = \int xp(x) dx$$
## Conditional Expectation
Continuous: $$ E(X | Y) = \int xp(x|y)dx$$
Discrete: $$E(X | Y) = \sum_{x} xp(x | y)$$
## Expected value of a function
Discrete: $$E[g(x)] = \sum_{x}g(x)p(x) $$
Continuous: $$E[g(X)] = \int g(x)p(x)dx$$
## Example
Given: $$E(cX + Y) = cE(X) + E(Y)$$
The expected value is actually the true **mean** of $x$. 
# Monte Carlo Method
$$E(X) = \frac{1}{N} \sum^{N}_{i = 1} x_{i}$$ where $x_{i} \approx p(x)$. This is also known as the sample mean. 
# Bayes Rule
$$p(y|x) = \frac{p(x,y)}{p(x)} = \frac{p(x|y)p(y)}{\int p(x,y)dy} = \frac{p(x|y)p(y)}{\int p(x|y)p(y)dy}$$
# Mean Squared Error
$$ MSE = \frac{1}{N} \sum_{i = 1}^{N} (y_{i} - \hat{y_{i}})^{2}$$
# Gradient Descent
$$ w = w - \alpha \nabla_{w}J, \; J = MSE$$ 