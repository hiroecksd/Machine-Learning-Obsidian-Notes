# What is the problem?
We have two opposing forces. 
* Collect data (exploration)
* select choice with highest win-rate (exploit)
It is the explore-exploit dilemma. What applications does it have? 
* Comparing things to see which one is better. Quantitatively compare things. 
# Gaussian vs. Bernoulli
Bernoulli is good for measuring success rates while Gaussian is better for continuous variables. 
# Epsilon-Greedy
Our problem is that we need to balance the explore / exploit ratio. If we only take the best maximum likelihood estimate win rate then it won't work.  We could get lucky or not which could exploit something suboptimal. That is called the **greedy**. Means to be short-sighted. Being greedy for us means that we just pick the bandit with the highest MLE win-rate without any regard to confidence in prediction or amount of data collected. **Epsilon-Greedy says that instead of always taking the greedy option, we are gonna have a small probability of doing something random (non-greedy) which is given by $\epsilon$**. Usually some amount like 5-10%.  Here is some pseudocode:

```python
## Greedy Method
while True:
	j = argmax(predicted bandit means)
	x = play bandit j and get reward
	bandits[j].update_mean(x)

## Epsidlon - Greedy
while True:
	p = random number in [0,1]
	if p < epsilon
		j = choose a random bandit
	else: 
		j = argmax(predicted bandit means)
	x = play bandit and get reward
	bandits[j].update_mean(x)
```
The reason we want to explore with a nonzero epsilon is so we can collect data about each bandit being as accurate as possible. Sometimes we can use a decaying epsilon to help with selecting a bandit arm. They all decrease over time. 
# Sample Mean Calculation
$$\bar{X}_{N} = \frac{1}{N} \sum_{i = 1}^{N} X_{i}$$
Calculating the sample mean naively is a bad idea because we need an infinite amount of space and we don't have that. More data we have, the longer it will take. Sample mean at time $N$ can be evaluated in constant space and time. We only need to store the previous mean, the newest sample, and the number of sample. 
# Epsilon-Greedy Exercise
