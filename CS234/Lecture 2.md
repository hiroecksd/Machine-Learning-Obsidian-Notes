# Markov Process/Chain
A **Markov process** is a memoryless random process. It is a process for which predictions can be made regarding future outcomes based solely on its present state and most importantly such prediction are just as good as the ones that could be made knowing processes full history. Conditional on the present state of the system, and past states are independent. Because we have not formally defined what we mean by dynamics/transitions I will do it here. A **transition** are the changes of state of the system. We define $S$ as a finite set of states with $s \in S$. Then we can define $P$ as the transition or dynamics model which specifies $$ p(s_{t + 1} = s' | s_{t} = s)$$ One thing you should know that if there is no rewards, there will be no actions. Given that we have a finite number ($N$) of states, the transition model $P$ can be expressed as a matrix: $$ P = \begin{pmatrix} P(s_{1} | s_{1}) & \cdots & P(s_{N} | s_{1}) \\ \vdots & \ddots & \vdots \\ P(S_{1} | s_{N}) & \cdots & P(s_{N} | s_{N}) \end{pmatrix} $$
# Markov Reward Process (MRP)
An MRP is a Markov chain that has rewards. Including the variables we denoted earlier we have two more to add. The Reward function ($R$) which is given by: $$R(s{t} = s) = \mathbb{E}[r_{t}|s_{t} = s]$$ and mentioned in previous notes you saw the discount factor $\gamma \in [0,1]$. If there is a finite number ($N$) of states, we can express $R$ as a vector. There are no actions here. 
## Return 
What is a horizon? A horizon is the number of time steps in each episodes in a process. A horizon can be infinite, although, familiarly if it is finite it is known as a Markov reward process. So, what is return? Well return for MRP is the discounted sum of rewards from each time step $t$ to horizon $H$. The return function is denoted by $G_{t}$ and is given by: $$G_{t} = r_{t} + \gamma' r_{t + 1} + \gamma^{2'}  r_{t + 2} + \cdots + \gamma^{H - 1}r_{t + H - 1}$$
## Value Function
The **state value function** is the expected return from starting in state $s$ which is following the policy $\pi$. Our value function is denoted by $V(s)$ and given by the following: $$V(s) = \mathbb{E}[G_{t}|s_{t} = s] = \mathbb{B}[r_{t} + \gamma r_{t + 1} + \gamma^{2}  r_{t + 2} + \cdots + \gamma^{H - 1}r_{t + H - 1}| s_{t} = s]$$
## Discount Factor
We use a discount factor because it is mathematically convenient as it avoids infinite returns and values. If episodes lengths are always finite you should know that you can use $\gamma = 1$. 
## How to compute a MRP
We have been learning how to understand the mathematics of an MRP but how is it computed? We need our MRP value function to satisfy the following: $$V(s) = \underbrace{R(s)}_{\text{Immediate Reward}} + \underbrace{\gamma \sum_{s' \in S} P(s' | s) V(s')}_{\text{Discounted sum of future rewards.}}$$ 
### Bellman Equation
The Bellman equation is a necessary condition for optimality associated with mathematical optimization method. It writes the value of decision problem at a certain point in time in terms of the payoff from some initial choices and the value of the remaining decision problem that results from those initial choices. This point of this is that **it breaks a dynamic optimization problem into a sequence of simpler subproblems**. 
## Bellman for MRP
Now that we have a general understanding of what the Bellman equation is we can apply it to MRP for our use: $$
\left(\begin{array}{c}
V\left(s_{1}\right) \\
\vdots \\
V\left(s_{N}\right)
\end{array}\right)=\left(\begin{array}{c}
R\left(s_{1}\right) \\
\vdots \\
R\left(s_{N}\right)
\end{array}\right)+\gamma\left(\begin{array}{ccc}
P\left(s_{1} \mid s_{1}\right) & \cdots & P\left(s_{N} \mid s_{1}\right) \\
P\left(s_{1} \mid s_{2}\right) & \cdots & P\left(s_{N} \mid s_{2}\right) \\
\vdots & \ddots & \vdots \\
P\left(s_{1} \mid s_{N}\right) & \cdots & P\left(s_{N} \mid s_{N}\right)
\end{array}\right)\left(\begin{array}{c}
V\left(s_{1}\right) \\
\vdots \\
V\left(s_{N}\right)
\end{array}\right)
$$ This probably looks very daunting but we can break it down into pieces and understand it. We are obviously turning our value function into a matrix equation here. At its core we can see that the equation is: $$V = R + \gamma PV $$ If we want a complete analytic solution we will need to do some linear algebra but essentially it comes down to: $$ V = (I - \gamma P)^{-1}R $$ where $I$ is your identity matrix. If you solve directly you will need to take a matrix inverse which is $O(N^{3})$. You should also know that what is inside the parenthesis is invertible. So how can we look at this from a dynamic programming approach? **Dynamic Programming** is a technique that helps to efficiently solve a class of problems that have overlapping subproblems and optimal substructure property. Your pseudo-code for this would be something like this
```
v = 0
for k = 1 until convergence
	for all s in S
		v(s)
```
which is basically our $V(s)$ but in programming terms. The big $O$ for this would be $O(|S|^{2})$ for each iteration where $(|S| = N)$.  
