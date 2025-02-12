### 材料
https://ocw.mit.edu/courses/18-s096-topics-in-mathematics-with-applications-in-finance-fall-2013/resources/mit18_s096f13_lecnote5/

## 随机过程 (Stochastic process)
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


## 简单随机游走 (Simple random walk)
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

补充: 方差计算公式: $\sigma ^2 = \frac { \sum (x_i - \mu) ^ 2 }{N}$


### 性质

1. 期望(Expectation): $\mathbb{E} [X_k] = 0$, 对所有 $k$, 期望都是0.

2. 独立增量(Independent increment): 对所有 $0 = t_0 \le t_1 \le ... \le t_k $, 随机变量(random variable) $X_{t_{i+1}} - X_{t_{i}}$ 是相互独立的(mutually independent).

3. 平稳性(Stationary): 对所有 $h \ge 1, t \le 0$, $X_{t+h} - X_t$ 的分布和 $X_h$ 的分布一样. 

只要增量 $Y_i$ 是相同且独立的(identical and independent), 并且均值为0, 那么这些性质就一直能成立. 

### 例子1: 投硬币

投硬币游戏: 赌徒连续投一枚均匀的硬币, 如果投到正面赚$1, 如果投到反面亏$1. 如果每次投硬币都是独立的, 那么赌徒盈亏的额度就服从简单随机游走分布. 

### 例子2: 股票价格

随机游走可以(没那么精确地)用于股票价格建模. 比如我们想知道股票在跌到 $-B$价格前, 涨到 $A$价格的概率是多少(也就是说假设跌到 $-B$价格的时候就爆仓).

我们也可以这么描述: 对于两个正整数(positive integers)A和B, 一个随机变量随机游走触碰到 $-B$之前, 游走到 $A$的概率是多少? 

假设 $\tau$是第一次随机游走到 $A$或者 $-B$的时刻(这也就是两个边界). 那么我们有 $X_{\tau} = A$ 或者 $X_{\tau} = -B$. 

定义:

$$f(k) = P \(X_{\tau} = A | X_0 = k \)$$

我们要计算 $f(0)$. 也就是设定条件初始0时刻 $X_0$的值为0, $\tau$时刻 $X_{\tau}$的值为 $A$的概率. 

来看看我们已有的条件:

1. 从上一个投硬币的例子我们可以总结出这个递归公式(因为是独立增量并且上下游走概率都为50%): $f(k) = \frac{1}{2}f(k+1) + \frac{1}{2}f(k-1)$
2. 我们有边界条件: $f(A) = P \(X_{\tau} = A | X_0 = A \) = 1$ 
3. 我们有边界条件: $f(-B) = P \(X_{\tau} = A | X_0 = B \) = 0$

从边界条件开始考虑 $f(-B) = P \(X_{\tau} = A | X_0 = B \) = 0$, 因为我们不想触碰到这个边界, 所以我们从这个边界往上考虑, 假设 $f(-B+1) = \alpha$, 那么我们有:
1. $f(-B+1) = \frac{1}{2}f(-B+1+1) + \frac{1}{2}f(-B+1-1) = \frac{1}{2}f(-B+2) + \frac{1}{2}f(-B)  =\frac{1}{2}f(-B+2) + 0 = \frac{1}{2}f(-B+2) = \alpha \Rightarrow f(-B+2) = 2 \alpha$
2. $f(-B+2) = \frac{1}{2}f(-B+2+1) + \frac{1}{2}f(-B+2-1) = \frac{1}{2}f(-B+3) + \frac{1}{2}f(-B+1)  =\frac{1}{2}f(-B+3) + \frac{1}{2}\alpha = 2 \alpha$
3. $f(-B+3) = 3 \alpha$
4. ...
5. $f(-B+r) = \alpha r$, 对所有的 $r \le A+B$

我们也有 $f(A) = f(-B+A+B) = \alpha (A+B) = 1$, 可以算得 $\alpha = \frac{1}{A+B}$

最后我们可以得到 $f(0) = f(-B+B) = \alpha B = \frac{B}{A+B}$, i.e.

$$f(0) = \frac{B}{A+B}$$

## 马尔可夫链 (Markov chain)

### 定义

简单随机游走(simple random walk)的一个重要性质是只有当前状态(current state)才能影响未来(future state), 在当前状态以前的历史状态不对未来状态产生影响. 

我们也可以说:

$X_{k+1}$ 的分布只依赖于 $X_k$, 而和这之前的集合无关 $X_0, X_1, ..., X_k$. 拥有这样性质的随机过程我们称之为马尔可夫链(Markov chain).

再正式一点, 对于 $X_0, X_1, ...$ 这么一个离散时间的随机过程(discrete-time stochastic process), 其中每一个 $X_i$ 取值于某一个离散集合(discrete set) $S$ (这和简单随机游走不同). 这个集合 $S$ 可称为 __状态空间__ (state space).

如果以下成立, 我们可以说随机过程具有马尔可夫性质(Markov property):

对所有的 $n \le 0$ 和 $i \in S$, 满足

$$P \( X_{n+1} = i | X_n, X_{n-1}, ..., X_0 \) = P \( X_{n+1} = i | X_n \)$$

### 深入马尔可夫链

拥有马尔可夫性质的随机过程可被称为马尔可夫链. 

值得注意的是, 一个有限的(finite)马尔可夫链可以用转移概率来描述: 

$$p_{ij} = P \( X_{n+1} = j | X_n = i \) \ \ i,j \in S$$

可以注意到, 

$$\sum_{i \in S} p_{ij} = 1, \forall i \in S$$

马尔可夫链模型里的所有元素都可以被写进转移概率矩阵(transition probability matrix)里:

$$
A = \begin{pmatrix} 
p_{11} & p_{21} & \dots & p_{m1} \\
p_{12} & p_{22} & \dots & p_{m2} \\
\vdots & \vdots & \ddots & \vdots \\
p_{1m} & p_{2m} & \dots & p_{mm}
\end{pmatrix}
$$

其中每一列的元素之和都是1. 


### 例子1

一个机器一天可以正常运转也有可能坏掉: 

1. 如果当天它正常运转, 那么第二天坏掉的概率是0.01, 继续正常运转的概率是0.99
2. 如果当天它坏掉了, 它会被修好, 那么第二天坏掉的概率是0.2, 继续正常运转的概率是0.8

我们可以用马尔可夫链建模, 其中包含两个状态: 1)正常运转 2)坏掉

转移概率矩阵(transition probability matrix):

$$
\begin{bmatrix}
0.99 & 0.8 \\
0.01 & 0.2 
\end{bmatrix}
$$

### 例子2
简单随机游走的转移概率(Transition probability for simple random walk):

一个简单随机游走也是马尔可夫链. 但是因为简单随机游走的样本空间(sample space)是无限的, 所以我们没法写出转移概率矩阵. 那我们试试另一种方法:

我们把 $r_{ij} \( n \) = P \( X_n = j | X_0 = i \)$ 表示为n阶(n-th step)转移概率. 这些概率满足递推关系(recurrence relation):

对所有的 $n \gt 1$, 

$$r_{ij} (n) = \sum_{k=1}^{m} r_{ik} (n - 1) p_{kj}$$

其中 $r_{ij} (1) = p_{ij}$


怎么理解呢? 首先第1个状态是 $r_{ij} (1) = p_{ij}$, 我们可以从第2个状态倒推回第1个状态:
$$r_{ij} \( 2 \) = \sum_{k=1}^{m} r_{ik} \( 1 \) p_{kj} = \sum_{k=1}^{m} p_{ik} p_{kj} $$

可以发现, 这其实就是 $i$ 到 $j$ 中途所有可能的路径概率的总和. 类比就是有很多分叉的小路, 能达到目的地的所有随机游走路径的概率总和. 

所以, n阶(n-step)转移概率矩阵可以写成该矩阵的n次方: 

$$A^n$$

回到例子1里的矩阵, 机器运作两天后的概率矩阵应该是:

$$
\begin{bmatrix}
0.99 & 0.8 \\
0.01 & 0.2 
\end{bmatrix} ^ 2 = 
\begin{bmatrix}
0.9881 & 0.952 \\
0.0119 & 0.048 
\end{bmatrix}
$$

### 例子3
#### 定义: 静止分布 (Stationary distribution)
马尔可夫链的静止分布是在状态空间(state space) $S$ 上的概率分布, 其中 $P ( X_0 = j ) = \pi_j$, 使得: 

$$\pi_{j} (n) = \sum_{k=1}^{m} \pi_{k} p_{kj} \ ( \forall j \in S )$$


注意 $P (X_0 = j) = \pi_j$ 其实就是前面例子里 $r_{ij} (n) = P ( X_n = j | X_0 = i )$ 去掉了条件概率, 所以静止分布的意思就是到达 $j$ 状态的所有可能性之和(注意是不带路径的).

#### 例子

选取一个整数集合(integer numbers)的状态空间 $S = Z_n$ 并且 $X_0 = 0$. 再选取一个马尔可夫链 $X_0, X_1, X_2, ...$ 其中有50%的概率 $X_{n+1} = X_n + 1$ 以及50%的概率 $X_{n+1} = X_n - 1$.

那么对所有的 $i$, 这个马尔可夫链的静止分布(stationary distribution)是:

$$\pi_i = \frac{1}{n}$$

因为每一个状态的概率都相等, 所以第n步的每一个状态的静止分布就是 $\frac{1}{n}$

#### 定理

注意到这个向量(vector) $\( \pi_1, \pi_2, ..., \pi_m \)$ 是 $A$ 的特征向量(eigen vector), 它的特征值(eigen value)是1. 所以通过Perron-Frobenius定理我们可以推导出以下定理.

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
