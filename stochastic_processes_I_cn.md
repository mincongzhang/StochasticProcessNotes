### 材料
https://ocw.mit.edu/courses/18-s096-topics-in-mathematics-with-applications-in-finance-fall-2013/resources/mit18_s096f13_lecnote5/

## 随机过程
### 定义

随机过程指的是一系列按时间排序的随机变量(A collection of random variables indexed by time).


离散随机过程(Discrete-time stochastic process)可表示为: $X_0, X_1, X_2, X_3, ...$

连续随机过程(Continuous-time stochastic process)可表示为: $\\{ X_t \\} _{t \ge 0}$

### 另一种定义
在一系列空间路径上的概率分布(Probability distribution over a space of paths).

### 一系列有趣的问题

通过学习随机过程我们就可以讨论下面这些有趣的问题:

1. 我们可以关注随机过程变量的依赖性. 比如过去股票的价格如何影响未来的股票价格?
2. 我们可以关注随机过程变量在一长段时间中的平均值. 比如一个运行的机器中途闲置的比例(更现代化的例子, 一台24小时运行的电脑/服务器闲置的比例).
3. 我们可以关注边界事件. 比如在特定的一个小时内电话系统里所有的电话线都忙的可能性是多少?


## 简单随机游走
### 定义 

我们定义一个独立同分布的随机变量:

$$Y_i: i.i.d 随机变量$$

```
i.i.d: independent and identically distributed (独立同分布)
```

使得 $Y_i$ 有50%的概率 等于 1 和 -1.

让 $X_0 = 0$, 并且对每一个 $k$, 我们有

$$X_k = \sum_{i=1}^{k} Y_i$$

那么我们可以把这些 $X_0, X_1, X_2, X_3, ...$ 称为 __一维简单随机游走__ (one-dimensional simple random walk). 这之后我们就把它简称为 __随机游走__ (random walk).

如果我们用上中心极限定理(central limit theorem, CLT), 对于一个足够大的 $n$, $X_n$的均值(mean)是0, 方差(variance)是 $n$, 标准差(standard deviation)是 $\sqrt{n}$. 

略作修改, 对于一个足够大的 $n$, $\frac{1}{\sqrt{n}} X_n$的收敛为正态分布(normal distribution), 均值(mean)是0, 方差(variance)是1, 标准差(standard deviation)是1. 


补充: 在概率论中，中心极限定理 (CLT) 确认，在许多情况下，对于独立并同样分布的随机变量，即使原始变量本身不是正态分布，标准化样本均值的抽样分布也趋向于标准正态分布. 

补充方差计算公式: $\sigma ^2 = \frac { \sum (x_i - \mu) ^ 2 }{N}$


### 性质
1. $E \( X_k \) = 0$

2. Independent increment: $0 t_0 \le t_1 \le ... \le t_k $, then $X_{t_{i+1}} - X_{t_{i}}$ are mutually independent

3. Stationary: for all $h \ge 1, t \le 0$, the distribution of $X_{t+h} - X_t$ is the same as the distribution of $X_h$

### Example

Coin tose game: head you win $1, tail you lose $1. If each coin toss is independent, then the balance of the gambler has the distribution of the simple random walk. 

For 2 positive integers A and B, what's the probability that the random walk reaches A before it reaches -B? 

Let $\tau$ be the first time at which the random walk reaches either A or -B. Then $X_{\tau} = A \ or \ -B$. Define

$$f(k) = P \(X_{\tau} = A | X_0 = k \)$$

And we want to compute $f(0)$.

Let's see what we have:

1. Consider the outcome of the first coin toss, we have the recursive formula: $f(k) = \frac{1}{2}f(k+1) + \frac{1}{2}f(k-1)$
2. we have the boundary condition: $f(A) = P \(X_{\tau} = A | X_0 = A \) = 1$ 
3. we have the boundary condition: $f(-B) = P \(X_{\tau} = A | X_0 = B \) = 0$

If we let $f(-B+1) = \alpha$, then we have:
1. $f(-B+1) = \frac{1}{2}f(-B+1+1) + \frac{1}{2}f(-B+1-1) = \frac{1}{2}f(-B+2) + \frac{1}{2}f(-B)  =\frac{1}{2}f(-B+2) + 0 = \frac{1}{2}f(-B+2) = \alpha$
2. $f(-B+2) = 2 \alpha$
3. $f(-B+2) = \frac{1}{2}f(-B+2+1) + \frac{1}{2}f(-B+2-1) = \frac{1}{2}f(-B+3) + \frac{1}{2}f(-B+1)  =\frac{1}{2}f(-B+3) + \frac{1}{2}\alpha = 2 \alpha$
4. $f(-B+3) = 3 \alpha$
5. ...
6. $f(-B+r) = \alpha r$, for all $r \le A+B$

Also we have $f(A) = f(-B+A+B) = \alpha (A+B) = 1$, we can get $\alpha = \frac{1}{A+B}$

Finally we can get $f(0) = f(-B+B) = \alpha B = \frac{B}{A+B}$, i.e.

$$f(0) = \frac{B}{A+B}$$

## Markov chain
### Definition:

Simple random walk, effect of the past on the future is summarized only by the current state, rather than the whole history. 

Or:

The distribution of $X_{k+1}$ depended only on $X_k$, not on the whole set of $X_0, X_1, ..., X_k$, A stochastic process with such property is called a Markov chain

More formally, let $X_0, X_1, ...$ be a discrete-time stochastic process where each $X_i$ takes value in some discrete set S (this is not the case in the simple random walk). The set S is called the __state space__.

We say that the stochastic process has the __Markov property__ if:
$$P \( X_{n+1} = i | X_n, X_{n-1}, ..., X_0 \) = P \( X_{n+1} = i | X_n \)$$

for all $n \le 0$ and $i \in S$

Let's look into the Markov chain more:

A stochastic process with the Markov property is called a Markov chain. Note that a finite Markov chain can be described in terms of the transition probabilities.

$$p_{ij} = P \( X_{n+1} = j | X_n = i \) \ \ i,j \in S$$

One can easily see that

$$\sum_{i \in S} p_{ij} = 1, \forall i \in S$$

All the elements of a Markov chain model can be encoded in a transition probability matrix

![image](https://github.com/mincongzhang/Quant100/assets/5571030/7ef7bbcd-28c2-4d6b-9baf-858e3ce2c661)

Where the sum of each column is equal to 1

### Example 1
Machine can be either working or broken on a day:

1. if it's working, next day break down prob 0.01, continue working prob 0.99
2. if it breaks down, will get repaired, next day break down prob 0.2, continue working prob 0.8

We can model this by a Markov chain with 2 states: 1) working 2) broken down

Transition probability matrix:

![image](https://github.com/mincongzhang/Quant100/assets/5571030/4a0eeaba-697e-452e-82a6-a340fe96d47d)

### Example 2
Transition probability for simple random walk:

A simple random walk is an example of a Markov chain. But since the sample space is infinite there is no transition probability matrix. Let's try another way:

Let $r_{ij} \( n \) = P \( X_n = j | X_0 = i \)$ be the n-th step transition probabilities. These probabilities satisfy the recurrence relation:

$$r_{ij} \( n \) = \sum_{k=1}^{m} r_{ik} \( n - 1 \) p_{kj} \ \ for \ n \gt 1, \ where \  r_{ij} \( 1 \) = p_{ij}  $$

怎么理解呢? 我们可以看:
$$r_{ij} \( 2 \) = \sum_{k=1}^{m} r_{ik} \( 1 \) p_{kj} = \sum_{k=1}^{m} p_{ik} p_{kj} $$

其实就是 $i$ 到 $j$ 中途所有可能的路径概率的总和.

Hence the n-step transition probability matrix can easily be shown to be:
$$A^n$$

### Example 3
#### Stationary distribution 静止分布
A stationary distribution of a Markov chain is a probability distribution over the state space $S$ (where $P \( X_0 = j \) = \pi_j$) such that 

$$\pi_{j} \( n \) = \sum_{k=1}^{m} \pi_{k} p_{kj} \ \( \forall j \in S \)  $$

注意 $P \( X_0 = j \) = \pi_j$ 其实就是去掉了条件概率, 所以静止分布的意思就是到达 $j$ 状态的所有可能性之和.

Let $S = \mathbb{Z}_n$ (integer number, 整数) and $X_0 = 0$ . Consider the Markov chain $X_0, X_1, X_2, ...$ such that $X_{n+1} = X_n + 1$ with probability 0.5 and $X_{n+1} = X_n - 1$ with probability 0.5. 

Then the stationary distribution of this Markov chain is:

$$\pi_i = \frac{1}{n} \ for \ all \ i$$

每一个状态的概率都相等, 所以n步的每一个状态的静止分布就是 $\frac{1}{n}$

### Theorem

Note that the vector $\( \pi_1, \pi_2, ..., \pi_m \)$ is an eigenvector of A with eigen value 1. Hence the following therom can be deduced from the Perron-Frobenius theorem.

If $p_{ij} \gt 0$ for all $i,j \in S$, then there exists a unique stationary distribution of the ststem. Moreover, 

$$\lim_{n \to \infty} r_{ij} \( n \) = \pi_j, \forall i,j \in S $$


But if we have infinite state spaces the theorem is not true. 


## Martingale

### Definition:

A discrete-time stochastic process $\{ X_0, X_1, ... \}$ is a martingale if 
$$X_t = \mathbb{E} \[ X_{t+1} | F_t \]$$

where $F_t = \{ X_0, ..., X_t \}$  (hence we are conditioning on the initial segment of the process)

This says that our expected gain in the process is zero at all times.  We can also view this definition as a Mathematical formalization of a game of chance being fair. 

也就是未来状态的期望等于现在状态, 并且期望的收益是0

### Proposition

For all $t \ge s$, we have $X_s = \mathbb{E} \[ X_{t} | F_s \]$

this easily follows from induction. 

未来任何一个时刻的状态的期望都等于现在的状态

### Example

1. Random walk is a martingale
2. The balance of a rouleete player is not a martingale, we always have $X_k > \mathbb{E} \[ X_{k+1} | F_k \]$  为啥? 期望总是在亏钱?

- Let $Y_1, $Y_2, ...$ be i.i.d random variables such that $Y_i = 2$ with probability $\frac{1}{3}$ and $Y_i = \frac{1}{2}$ with probability $\frac{2}{3}$. (so expectation is 1). Let $X_0 = 0$, and 

$$X_k = \prod_{i=1}^{k} Y_i$$

- Then $\{ X_0, X_1, ... \}$ forms a martingale.

## Optional stopping theorem
### Definition
(Stopping time) Given a stochastic process $\{ X_0, X_1, ... \}$, a non-negative integer-valued random variable $\tau$ is called a stopping time if for every integer $k \ge 0$,
the event $\tau \le k$ depends only on the events  $\{ X_0, X_1, ..., X_k \}$

感觉就是马尔可夫破产问题, 一旦到某条线(并且之前不曾到达过), 破产或者收手离场. 

### Example
1. In the coin toss game, consider a gambler who bets $1 all the time. Let $\tau$ be the first time at which the balance of the gambler becomes $100. 
Then $\tau$ is a stopping time.
2. Same gambler: Let $\tau$ be the time of the first peak(local maximum) of the banalce of the gambler. Then $\tau$ is not a stopping time.

### Theorem: Doob's optional stopping time theorem, weak form
Suppose that $\{ X_0, X_1, ... \}$ is a martingale sequence and $\tau$ is a stopping time such that $\tau \le T$ for some constant $T$, Then $\mathbb{E} \[ X_{\tau} \] = \mathbb{E} \[ X_0 \]$

Proof:

Note that

$$X_{\tau} = X_0 + \sum_{i=0}^{T-1} \( X_{i+1} - X_i \) \cdot 1_{ \\{ \tau \ge i + 1 \\} } $$

Where 

$$1_{ \\{ \tau \ge i + 1 \\} }$$

is a indicator function, means $1_{true} = 1, 1_{false} = 0$

And we used the fact $\tau \le T$. 

Since $T$ is a constant, by linear of expectation we have

$$\mathbb{E} \[ X_{\tau} \] = \mathbb{E} \[ X_0 \] + \sum_{i=0}^{T-1} \mathbb{E} \[ \( X_{i+1} - X_i \) \cdot 1_{ \\{ \tau \ge i + 1 \\} } \] $$

The main observation is that  $\tau \ge i+1$ is determined by $X_0, X_1, ...X_i$ . Hence

$$
\begin{aligned}
\mathbb{E} \[ \( X_{i+1} - X_i \) \cdot 1_{ \\{ \tau \ge i + 1 \\} } \] &= \mathbb{E} \[ \mathbb{E} \[ \( X_{i+1} - X_i \) \cdot 1_{ \\{ \tau \ge i + 1 \\} } | Fi \] \] \\
                                                                        &= \mathbb{E} \[ \mathbb{E} \[ \( X_{i+1} | Fi \] - X_i \) \cdot 1_{ \\{ \tau \ge i + 1 \\} }  \] \\
                                                                        &= \mathbb{E} \[ 0 \cdot 1_{ \\{ \tau \ge i + 1 \\} }  \] = 0 
\end{aligned}
$$

Hence

$$\mathbb{E} \[ X_{\tau} \] = \mathbb{E} \[ X_0 \]$$

(check Law of total expectation where $\mathbb{E} \[ X \] = \mathbb{E} \[ \mathbb{E} \[ X|Y \] \]$ , similar to law of total probability)

The condition can be further weakened (see R.Durrett,Probability:Theory and Examples,3rd edition.) The lesson to lean is that "a mortal being has no winning strategy (when the game is fair)". On the other hand, if one has some advantage over an opponent in some game, then no matter how small that advantage is, he/she will win in the long run. 


### Exercise

In the coin toss game, consider the following strategy. The gambler stops playing the first time at which the balance becomes $100. 

Note that by definition, we have $\mathbb{E} \[ X_{\tau} \] = 100$. Does this contradict the optional stopping theorem?


chatgpt answer:

```
The optional stopping theorem, also known as the stopping time theorem, is a mathematical result that applies to certain types of stochastic processes. It states that under certain conditions, if a gambler follows a strategy that stops the game at a particular stopping time, the expected value of the gambler's final wealth is the same regardless of when they stop.

In the case of the coin toss game, where the gambler stops playing once their balance reaches $100, the optional stopping theorem does not apply. The theorem assumes that the stopping time is chosen independently of the outcomes of the game. However, in this strategy, the stopping time is directly tied to the outcome of the game (the balance reaching $100).

The optional stopping theorem is typically applicable to processes that have certain properties, such as being a martingale or a Markov process. In the coin toss game, where the outcome of each toss is independent of previous tosses, the game does not possess these properties.

Therefore, the strategy of stopping the game when the balance reaches $100 does not contradict the optional stopping theorem because the theorem does not apply to this particular scenario.
```

### Exercise

For two positive integers $a$ and $b$, consider the following strategy for the coin toss game. A player stops at the first time the balance equals either to $a$ or $-b$. Let this time be $\tau$ . What is the probability distribution of $X_\tau$?
(i.e. what are the probabilities that $X_\tau = a$ and $X_\tau = b$?)
