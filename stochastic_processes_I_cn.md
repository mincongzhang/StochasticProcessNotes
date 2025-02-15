TODO: 回头看静止分布有什么用处来着?

TODO: 全期望定理那里视频里是怎么说的?

# MIT随机过程笔记[1]:从随机游走到鞅
### 前言

MIT公开课里随机过程和伊藤引理这两部分讲得还是非常清晰易懂的. 我参考了他们的教学视频和教案整理翻译成中文发在这里. 

参考材料:

视频: https://www.youtube.com/watch?v=TuTmC8aOQJE

教案: https://ocw.mit.edu/courses/18-s096-topics-in-mathematics-with-applications-in-finance-fall-2013/resources/mit18_s096f13_lecnote5/

## 随机过程 (Stochastic process)
### 定义

随机过程指的是一系列按时间排序的随机变量(A collection of random variables indexed by time).


离散随机过程(discrete-time stochastic process)可表示为: $X_0, X_1, X_2, X_3, ...$

连续随机过程(continuous-time stochastic process)可表示为: $\\{ X_t \\} _{t \ge 0}$

### 另一种定义
如果我们想更便于计算, 我们可以说: 随机过程是一系列空间路径上的概率分布(Probability distribution over a space of paths).

### 例子

1. 函数 $f(t) = t$ 是一个确定的过程(a deterministic process), 它不是随机过程(stochastic process)
2. 函数 $f(t)$ 对所有的 $t$, 有50%的概率 $f(t) = t$ 50%的概率 $f(t) = -t$, 是一个随机过程(stochastic process). 
3. 函数 $f(t)$ 对每一个 $t$, 有50%的概率 $f(t) = t$ 50%的概率 $f(t) = -t$, 是一个随机过程(stochastic process)

### 一系列有趣的问题

通过学习随机过程我们就可以讨论下面这些有趣的问题:

1. 我们可以关注随机过程变量的依赖性. 比如过去股票的价格如何影响未来的股票价格?
2. 我们可以关注随机过程变量在一长段时间中的平均值. 比如一个运行的机器中途闲置的比例(更现代化的例子, 一台24小时运行的电脑/服务器闲置的比例).
3. 我们可以关注边界事件(boundary events). 也就是一些极端情况的发生概率. 比如一个股票连续5天跌超过10%的概率是多少? 比如在特定的一个小时内电话系统里所有的电话线都忙的可能性是多少?


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


也就是说, 虽然这是随机游走, 但是根据中心极限定理, 随机游走的路径依然是在0这个中间点上下的, 并且上下幅度不会很大, 也就保持在正态分布的范围内. 把随机游走每一条可能的路径画成图的话大概是下面这样:


![image](https://github.com/user-attachments/assets/933cdb61-849e-4baa-a806-9a2f87049dc5)

参考: https://www.kaisataipale.net/blog/2015/12/15/random-walks-in-python/




补充: 中心极限定理(central limit theorem, CLT): 在概率论中，中心极限定理确认，在许多情况下，对于独立并同样分布的随机变量，即使原始变量本身不是正态分布，标准化样本均值的抽样分布也趋向于标准正态分布. 

补充: 方差计算公式: $\sigma ^2 = \frac { \sum (x_i - \mu) ^ 2 }{N}$


### 性质

1. 期望(Expectation): $\mathbb{E} [X_k] = 0$, 对所有 $k$, 期望都是0.

2. 独立增量(Independent increment): 对所有 $0 = t_0 \le t_1 \le ... \le t_k $, 随机变量(random variable) $X_{t_{i+1}} - X_{t_{i}}$ 是相互独立的(mutually independent).

3. 平稳性(Stationary): 对所有 $h \ge 1, t \ge 0$, $X_{t+h} - X_t$ 的分布和 $X_h$ 的分布一样. 也就是不管你怎么选取起始点( $0$ 或者任意 $t$ ), 只要段落(interval)长短一致(都是 $h$), 那么这两段的分布(distribution)都是一样的. 而且如果这两段不重叠(do not overlap), 那么他们还互相独立(independent).

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

$$ A = 
\begin{bmatrix}
0.99 & 0.8 \\
0.01 & 0.2 
\end{bmatrix}
$$

有了这个转移矩阵, 我们就可以问, 在连续运转365天或者3650天, 直到连续运转n天后这个机器坏掉的概率分布是怎么样的? 也就是有多大概率中途坏掉, 有多大概率一直不坏? 

TODO: https://youtu.be/TuTmC8aOQJE?t=2957

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

对所有的 $i,j \in S$, 如果 $p_{ij} \gt 0$, 那么就存在一个单一的平稳分布(a unique stationary distribution of the system). 进一步:  

$$\lim_{n \to \infty} r_{ij} \( n \) = \pi_j, \forall i,j \in S $$

但如果我们考虑无限的状态空间(infinite state spaces)这个定理就不成立. 

TODO: https://youtu.be/TuTmC8aOQJE?t=3250


## 鞅(Martingale)

### 定义

如果以下成立:

$$X_t = \mathbb{E} \[ X_{t+1} | F_t \]$$

其中:

$F_t = \{ X_0, ..., X_t \}$ 

那么一个离散时间随机过程 $\{ X_0, X_1, ... \}$ 可被看作是一个鞅(martingale).

可以看出 $X_t = \mathbb{E} \[ X_{t+1} | F_t \]$ 是依赖于初始条件 $F_t = \{ X_0, ..., X_t \}$ 的(conditioning on the initial segment of the process). 

这说明期望收益(expected gain)永远是0. 如果一个赌博游戏可以看作是一个鞅过程, 说明这个赌博是公平(fair)的, 也就是说在大量多次赌局后参与者的收益是不亏不赚的. 但如果在大量多次赌局后参与者收益的期望是负的, 那说明这个赌博对参与者是不公平的, 如果期望是正的那这个赌博对庄家是不公平的.  

### 命题(Proposition)

可以通过 $t+1$ 推导到一般情况, 对所有的 $t \ge s$, 我们有

$$X_s = \mathbb{E} \[ X_{t} | F_s \]$$

这说明未来任何一个时刻的状态的期望都等于现在的状态.

### 例子

1. 随机游走就是一个鞅(Random walk is a martingale).
2. 轮盘赌博玩家的收益不是一个鞅, 因为这个赌博就是设计成赌徒的期望收益是负的: $\mathbb{E} [ X_{k+1} | F_k ] < X_k$
3. 设 $Y_1, Y_2, ...$ 为独立同分布(i.i.d)的随机变量, 并且有 $\frac{1}{3}$ 的概率  $Y_i = 2$, $\frac{2}{3}$ 的概率 $Y_i = \frac{1}{2}$ (也就是说 $Y_i$ 的期望等于1). 设 $X_0 = 0$, 我们有

$$X_k = \prod_{i=1}^{k} Y_i$$

那么 $\{ X_0, X_1, ... \}$ 就是一个鞅(martingale).

## 鞅停止定理/可选停时定理 (Optional stopping theorem)

我们通过以下定理再次说明如果一个赌博过程是鞅, 那说明这是一个公平的赌博, 也就是从期望上来说你不赚不亏. 

在一个鞅的赌博过程中, 不管你试图用什么策略, 想法设法用什么高级策略试图赚钱或者试图亏钱, 长期来说你的收益期望都是固定的, 不会亏钱也不会赚钱. 

### 定义

真的赚不到钱嘛? 我们来试图设计一个策略从鞅赌博过程中赚钱, 在那之前我们定义以下概念:

停时(Stopping time): 给定一个随机过程 $\{ X_0, X_1, ... \}$, 和一个非零整数随机变量(a non-negative integer-valued random variable) $\tau$. 对每个整数 $k \ge 0$, 事件(the event) $\tau \le k$ 只依赖于事件(events)  $\{ X_0, X_1, ..., X_k \}$. 那么我们称 $\tau$ 为停时(stopping time). 

### 例子

通过停时这个概念, 我们设计以下策略: 

- 在投硬币游戏里, 如果一个赌徒每一局都赌1美元. 设 $\tau$ 为第一次赌徒收益达到100美元的时刻. 那么 $\tau$ 就是一个停时(stopping time).
- 或者我们在达到100美元或者-50美元的时候停止赌博. 也就是设置了止盈止损. 这么一个时刻 $\tau$ 是一个停时. 

- 同样的赌徒/赌局: 设 $\tau$ 为第一次赌徒收益达到第一个峰值(first peak, local maximum). 那么 $\tau$ 就不是一个停时. 因为你要在 $\tau$ 时刻停止, 那么你必须依赖于 $\tau + 1$ 的信息, 也就是它获取了未来的信息才知道前面那个收益是峰值. 所以 $\tau$ 不是一个停时.
- 同样的赌徒/赌局: 如果设定 $\tau -1$ 是第一个峰值(first peak, local maximum), 但是 $\tau$ 是第一个峰值后下降的时刻, 这种情况下的 $\tau$ 是一个停时.

### 定理: Doob可选停时定理, 弱化形式 (Doob's optional stopping time theorem, weak form)

以上的策略能赚到钱吗? 

假设 ${ X_0, X_1, ... }$ 是鞅序列 (martingale sequence),  $\tau$ 是一个时停并且满足 $\tau \le T$, 其中 $T$ 是一个常数(constant), 也就是说这个赌博不能无限玩下去. 那么 $\mathbb{E} [ X_{\tau} ] = \mathbb{E} [ X_0 ]$

也就是即使我们试图止盈止损, 我们期望上也赚不到钱. 


证明: 

注意到

$$X_{\tau} = X_0 + \sum_{i=0}^{T-1} \( X_{i+1} - X_i \) \cdot 1_{ \\{ \tau \ge i + 1 \\} } $$

其中 $1_{ \\{ \tau \ge i + 1 \\} }$ 是一个指示函数(indicator function), 意思是 $1_{ \\{ true \\} } = 1, 1_{ \\{ false \\} } = 0$. 并且我们还有 $\tau \le T$. 

上面函数描述的就是从 $0$ 时刻的本金加上下一时刻的收益/亏损, 一直到 $\tau$ 时刻停止的总收益. 

因为总时间 $T$ 是一个常数,通过期望的线性传导性质(linearity of expectation), 我们可以得到:

$$\mathbb{E} \[ X_{\tau} \] = \mathbb{E} \[ X_0 \] + \sum_{i=0}^{T-1} \mathbb{E} \[ \( X_{i+1} - X_i \) \cdot 1_{ \\{ \tau \ge i + 1 \\} } \] $$

观察到 $\tau \ge i+1$ 是由 $X_0, X_1, ...X_i$ 决定的. 所以: 

$$
\begin{aligned}
\mathbb{E} \[ \( X_{i+1} - X_i \) \cdot 1_{ \\{ \tau \ge i + 1 \\} } \] &= \mathbb{E} \[ \mathbb{E} \[ \( X_{i+1} - X_i \) \cdot 1_{ \\{ \tau \ge i + 1 \\} } | Fi \] \] \\
                                                                        &= \mathbb{E} \[ \mathbb{E} \[ \( X_{i+1} | Fi \] - X_i \) \cdot 1_{ \\{ \tau \ge i + 1 \\} }  \] \\
                                                                        &= \mathbb{E} \[ 0 \cdot 1_{ \\{ \tau \ge i + 1 \\} }  \] = 0 
\end{aligned}
$$

所以

$$\mathbb{E} \[ X_{\tau} \] = \mathbb{E} \[ X_0 \]$$


参考: 全期望定理(Law of total expectation): $\mathbb{E} \[ X \] = \mathbb{E} \[ \mathbb{E} \[ X|Y \] \]$ ,类似于全概率定理(law of total probability)


并且条件还可以更进一步的弱化(further weakened). 参考这本教材 <R.Durrett, Probability: Theory and Examples, 3rd edition.> 

从中我们可以学到的是如果一个赌博过程完全符合鞅过程(公平赌局), 那么不可能有赢的策略. 最后的盈亏的期望都是0. 另一方面, 如果我们发现一个赌博过程不完全符合鞅过程, 如果赌赢的期望大于0.5, 那么不管这个优势有多么小, 在多次长时间博弈的过程中, 收益永远都是正的. 现实案例就是高频交易, 只要高频交易盈利的期望是正的, 那么只要少量多次, 那么永远都能盈利. 或者从赌场的角度看, 所有的赌博游戏只要设计成期望是负的, 那么多人多次赌博后, 从期望上看, 赌场永远是赚的. 

### 练习1

再回到我们的例子:

- 在投硬币游戏里, 如果一个赌徒每一局都赌1美元. 如果赌徒的策略是第一次收益达到100美元就停止赌博. 这样根据定义我们的期望是 $\mathbb{E} \[ X_{\tau} \] = 100$. 这和我们的可选停时定理(optional stopping theorem)岂不是冲突了? 如何反驳?

首先题干里没有提及限制条件 $\tau \le T$, 如果没有边界的话那么盈亏期望确实可能就是100. 

但如果我们加上了限制条件 $\tau \le T$, 这就回到了 $$\mathbb{E} \[ X_{\tau} \] = \mathbb{E} \[ X_0 \] = 0$$


### 练习2

我们再增加止盈止损策略, 我们在达到100美元或者-50美元的时候停止赌博. 这样可以赚钱吗? 这个问题可以看作 $X_\tau = 100$ 或者  $X_\tau = -50$ 的概率是多少?

我们初始盈亏期望是0, 根据之前推导的: 

$$\mathbb{E} \[ X_{\tau} \] = \mathbb{E} \[ X_0 \] = 0$$

我们假设达到100美元结束的概率是 $P$, 那么达到-50美元结束的概率是 $1-P$. 我们有

$$\mathbb{E} \[ X_{\tau} \] = \mathbb{E} \[ X_0 \] = 0 = P \times 100 + (1-P) \times (-50)$$

$$150P-50 = 0$$

$$P = \frac{1}{3}$$

推导到一般形式, 我们有两个正整数 $a$ 和 $b$, 我们盈利达到 $a$ 或者亏损达到 $b$ 的时候就停止赌博. 设停时为 $\tau$ . 求 $X_\tau$ 的概率分布? 也就是求 $X_\tau = a$ 的概率和 $X_\tau = b$ 的概率. 


$$P \times a + (1-P) \times (-b) = 0$$
$$(a+b)P - b = 0$$
$$ P = \frac{b}{a+b}$$


## TODO
Total Expectation: Inf

The gain is inf, so it's all about how you'd like to pay. And it's more like a discussion, it has no right answer.

https://zh.wikipedia.org/wiki/%E5%9C%A3%E5%BD%BC%E5%BE%97%E5%A0%A1%E6%82%96%E8%AE%BA

数学期望大于零的游戏一定能赚钱吗 - 陈墨瞳nono的文章 - 知乎
https://zhuanlan.zhihu.com/p/579732711
