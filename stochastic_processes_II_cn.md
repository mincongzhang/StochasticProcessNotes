## Continuous-time stochastic process

https://www.youtube.com/watch?v=PPl-7_RL0Ko

https://ocw.mit.edu/courses/18-s096-topics-in-mathematics-with-applications-in-finance-fall-2013/resources/mit18_s096f13_lecnote17/


## 回顾

上篇我们讨论了马尔可夫链(Markov Chains)和鞅(Martingales), 那些都是离散随机过程(discrete-time stochastic process), 可表示为: $X_0, X_1, X_2, X_3, ...$ . 

接下来我们看连续随机过程(continuous-time stochastic process)可表示为: $\\{ X_t \\} _{t \ge 0}$. 其中t是实数(real number)而不是整数(integer).

## 连续随机过程难点: 如何描述概率分布(how to describe the probability distribution)

和离散随机过程相比, 连续随机过程的第一个难点是如何描述概率分布(probability distribution).

补充: 离散随机过程概率分布的意思是: 比如一台机器连续运转365天后坏掉和继续运转的的概率, 100轮赌博后盈亏多少的概率. 又或者说是每个随机路径到终点不同位置的概率汇总. 

拿简单随机游走(simple random walk)举例, 画出一个可能的路径:

$$
\begin{aligned}
X_{t+1} - X_{t} &= 1 \quad &\text{(P=0.5)} \\
                &= -1 \quad &\text{(P=0.5)} \\
\end{aligned}
$$

![image](https://github.com/user-attachments/assets/ce0c71e2-73ac-47fd-ac2f-9fa5b37a3c74)


注意到我们描述的不是随机游走走出以上这样特定路径的概率, 而是每一时刻和下一时刻(t和t+1)往上或者往下变动的概率. 在整个过程结束, 把所有步骤结合起来我们才获得概率分布.

总结: 在离散随机过程中, 我们可以计算从t到t+1时刻改变多少的概率(上一篇说的矩阵 $A$), 把每个时间变化的概率都合并起来 ($A^n$), 我们就能得到概率分布. 

但是在连续随机过程中, 不存在t和t+1, 那我们也没法描述两个时刻之间变化的概率, 如果把时间区间所有的变化都算完需要做无穷多次计算. 

解决方案是用概率密度函数(probability density function), 我们可以尝试用 $P(\omega)$ 来描述. 

## 布朗运动(Brownian motion)

布朗运动最开始是由英国植物学家布朗观察到水中悬浮的花粉的不规则运动而命名的. 布朗运动也叫维纳过程(Wiener process). 

在给出复杂定义之前, 我们可以从简单随机游走引申一下. 如果我们的简单随机游走取极限, 比如一个固定区间, 我们定义一个n步(n steps)随机游走过程, 把n扩展到无限大, 那么这个随机游走的结果就是布朗运动.

物理现象例子: 假如我们观察一些物理现象的时候, 我们通过观察记录非常精细的离散时间点的现象(也就是n尽量无限大, 比如每个间隔百万分之一秒), 发现结果近似布朗运动, 我们就可以确定其为布朗运动. 

股票例子: 布朗运动也可以用来给股票建模, 虽然股票交易频率是有限制的, 但只要我们把时间拉长, 它就可以看作是布朗运动. 

用术语描述: 定义一个简单随机游走 ${Y_0, Y_1, ...,Y_n}$ 的均值(mean)为0, 方差(variance)为1. 定义 $Z$ 为一个实数 $\mathbb{R}$ 上 $\[ 0, 1 \]$ 的分段函数(piecewise linear function):

$$Z \left( \frac{t}{n} \right) = Y_t$$

并且我们线性扩展 $t=0,...,n$ 到非常大, 这时候 $Z$ 的路径的分布就会逐渐接近布朗运动. 通过中心极限定理(central limit theorem), 我们可以发现 $Z(1)$ 的分布会收敛到标准正态分布 $N(0,1)$ . 更加一般化来看, $Z(t)$ 会收敛到 $N(0,t)$. 

补充解释：
- 提到的 $\[ 0, 1 \]$ 其实也就是 $\frac{t}{n}$ 的取值范围
- 总结上述就是普通随意游走取极限得到的连续方程可以看作是标准布朗运动


### 定理

最后我们给出布朗运动最精确的的定义:

在这样 $\mathbb{R}_{\ge 0} \rightarrow \mathbb{R}$ (就是时间轴为正实数 $\ge 0$ 映射到Y轴任意实数) 的连续函数集合里, 存在一个概率分布满足以下条件:

1. $B \(0\) = 0$ (也就是初始值为0).
2. 平稳性(stationary): 对所有 $0 \le s < t$ , $B (t) - B (s)$ 的概率分布是均值为0方差为 $t-s$ 的正态分布. 
3. 独立增量(independent increment): 如果区间 $\[ s_i, t_i \]$ 没有重叠(overlapping), 随机变量(random variables) $B \( t_i \) - B \( s_i \)$ 是互相独立的 (mutually independent).

满足这样分布的随机过程即为布朗运动. 布朗运动中一条特定的路径我们称其为样本布朗路径(sample Brownian path).

下面是一些布朗运动的特点:
1. 经常穿过x轴
2. 分布大部分都在曲线 $x=y^2$ 内 (不会超出范围太多)
3. 处处不可微(nowhere differentiable). 因为所有的微积分都是基于求微分(differentiation), 处处不可微也意味着用微积分没法用了. 

如下图, 在 $t_0$ 时刻的概率分布符合 $N(0, t_0)$ (均值为0, 标准差为 $sqrt{t_0}$)的正态分布. 所以大部分值都会处于这个区间之内. 

![image](https://github.com/user-attachments/assets/92423743-c8c9-4f2f-9aa3-fd64c6931fcc)


### Proposition
Define $M \( t \) = \max_{0 \le s \le t} B \( s \)$, and note that  $M \( t \)$ is well-defined since $B$ is continuous and $\[ 0, t \]$ is compact. 

(意思就是 $M \( t \)$ 是这一段时间里的最大值)

(compact: compact space, the closed interval $\[ 0, 1 \]$ would be compact)
    
$\Phi \( t \)$ is the cumulative distribution function of the normal random variable.

The following holds:

$$P \( M \( t \) \ge a \) = 2 P \( B \( t \) \ge a \) = 2 - 2 \Phi \( \frac {a}{\sqrt{t} } \)$$

Proof:

Let $\tau_a = min_s \\{ s: B \( s \) = a \\}$ and note that $\tau_a$ is a stopping time. Note that for all $0 \le s < t$, we have

$$P\( B \( t \) - B \( s \) > 0 \) = P\( B \( t \) - B \( s \) < 0 \) $$

Hence we see that

$$P\( B \( t \) - B \( \tau_a \) > 0 | \tau_a < t \) = P\( B \( t \) - B \( \tau_a \) < 0 | \tau_a < t \) $$

Here we assumed that the distribution of $B \( t \) - B \( \tau_a \)$ is not affected by the fact that we conditioned on $\tau_a < t$. This is called the __Strong Markov Property__ of the Brownian motion

补充解释：

__Strong Markov Property__: 直观上讲，停时是描述某种随机现象发生的时刻，它是普通时间变量的随机化。例如，考察从圆心出发的平面上的布朗运动，要研究首次到达圆周的时刻t以前的事件和以后的事件的条件独立性，这里的t就是停时，并认为t是“现在”。这种把“现在”推广为停时情形的“现在”，且在已知“现在”的条件下，“将来”与“过去”无关的特性被称为强马尔可夫性

This can be rewritten as 

$$P\( B \( t \) > a | \tau_a < t \) = P\( B \( t \) < a | \tau_a < t \) $$

And is also known as the __"Reflection principle"__

Now observe that

$$
\begin{aligned}
P\( M_t \ge a \) &= P\( \tau_a < t \) \\
                 &= P\( B \( t \) > a | \tau_a < t \) + P\( B \( t \) < a | \tau_a < t \) \\
                 &= 2 P\( B \( t \) > a | \tau_a < t \) 
\end{aligned}
$$

Since 
$$P\( B \( t \) > a | \tau_a < t \) = P\( B \( t \) > a \)$$

Our claim follows

$$P\( M_t \ge a \) = 2 P\( B \( t \) > a \) $$

### 额外部分: CDF的计算

接下来我们看看 

$$2 P \( B \( t \) \ge a \) = 2 - 2 \Phi \( \frac {a}{\sqrt{t} } \)$$
也就是 

$$P \( B \( t \) \ge a \) = 1 - \Phi \( \frac {a}{\sqrt{t} } \)$$

其实也就是高斯分布中在 $a$ 右半边的面积或是积分, 下面我们推出左半边面积的公式, 之后用 $1$ 减去就可以得到右半边面积: 

![image](https://github.com/mincongzhang/Quant100Public/assets/5571030/8849f4b7-7ebe-4ee2-a392-0dbd832e66e0)

参考: https://www.probabilitycourse.com/chapter4/4_2_3_normal.php#:~:text=The%20CDF%20of%20the%20standard%20normal%20distribution%20is%20denoted%20by,is%20widely%20used%20in%20probability.

根据前面的定理
1. $B \(0\) = 0$
2. Stationary: for all $0 \le s < t$, the distribution of $B \( t \) - B \( s \)$ is the normal distribution with mean 0 and variance $t-s$

我们可知 $B \(t \)$ 是服从均值为0, 方差为 $t$, 标准差为 $\sqrt{t}$ 的高斯分布:

$$B \(t\) \sim N \( 0, t \)$$

根据高斯累积分布函数(Cumulative Distribution Function, CDF):

如果 $X$ 符合高斯分布 $X \sim N \( \mu, \sigma^2 \)$, 那么随机变量 $Z = \frac{X-\mu}{\sigma}$ 就是一个标准的正态分布随机变量, i.e.
$Z \sim N \( 0, 1 \)$. 我们可以通过以下得到 $X \sim N \( \mu, \sigma^2 \)$ 的CDF:

$$
\begin{aligned}
F_X(x) &= P \(X \le x) \\
       &= P\( \sigma Z + \mu \le x \) \\
       &= P\( Z \le \frac{x-\mu}{\sigma} \) \\
       &= \Phi \( \frac{x-\mu}{\sigma} \)
\end{aligned}
$$

带入我们的均值为0, 方差为 $t$, 我们就得到了: 
$$P \( B \( t \) \le a \) = \Phi \( \frac {a}{\sqrt{t} } \)$$

也就是 

$$P \( B \( t \) \ge a \) = 1 - \Phi \( \frac {a}{\sqrt{t} } \)$$

### Proposition
The above proposition can help us prove the following result

For each $t \ge 0$, the Brownian motion is almost surely note differentiable at $t$

Proof:

Fix a real $t_0$ and suppose that the Brownian motion $B$ is differentiable at $t_0$. 
Then there exist constant $A$ and $\varepsilon_0$ such that for all $0 < \varepsilon < \varepsilon_0 $, $B \( t \) - B\( t_0 \) \le A \varepsilon$ 
holds for all $0< t-t_0 \le \varepsilon$

Let $E_{\varepsilon, A}$ denote this event, and $E_A = \cap_\varepsilon E_{\varepsilon, A}$. Note that

$$
\begin{aligned}
P \( E_{\varepsilon, A} \) &= P \( E \( t \) - E \( t_0 \) \le A \varepsilon, for \ all \ 0< t-t_0 \le \varepsilon  \) \\
                           &= P\( M \( \varepsilon \) \le A \varepsilon \) \\
                           &= 1- P\( M \( \varepsilon \) \ge A \varepsilon \) \\
                           &= 1- 2 \( 1 - \Phi \( A \varepsilon \) \) \\
                           &= 2 \Phi \( A \varepsilon \) - 1 
\end{aligned}
$$

where the right hand side tends to zero as $\varepsilon$ goes to zero. Therefore, $P \( E_A \) = 0$

By countable additivity, we see that there can be no constant A satisfying above (it suffices to consider integer values of A)

```
Dvoretsky, Erdos,and Kakutani in fact proved a stronger statment asserting that the Brownian motion $B$ 
is no where differentiable with probability 1.
Hence a sample Brownian path is continuous but nowhere differentiable!
The proof is slightly more involved and requires a lemma from probability theory (Borel-Cantellilemma).
```

### Theorem: Quadratic Variation

#### Quadratic Variation for a continuously differentiable function

For a partition $\Pi = \\{ t_0, t_1, ..., t_j \\}$ of an interval $\[0,T\]$, and for a __continuously differentiable__ function $f \( t \)$, we define its __quadratic variation__  as:

$$ \sum_{t}^{} \( f\( t_{i+1} \) - f\( t_{i} \)  \) ^2$$

Then according to mean value theorem (中值定理), we have:

$$
\begin{aligned}
\sum_{t}^{} \( f\( t_{i+1} \) - f\( t_{i} \)  \) ^2 & \le \sum_{t}^{} \(  t_{i+1} -  t_{i}  \) ^2 f' \(s \)^2 \\
                                                    & \le \max_{s \in \[0,T\]} f' \(s \)^2 \cdot \sum_{t}^{} \(  t_{i+1} -  t_{i}  \) ^2 \\
                                                    & \max_{s \in \[0,T\]} f' \(s \)^2 \cdot \max_{i} \{{ t_{i+1} - t_i  \}} \cdot T
\end{aligned}
$$

As $\max \\{ t_{i+1} - t_i \\} \to 0$, we see that the above tends to zero. 

#### Quadratic Variation for a Brownian motion

For a partition $\Pi = \\{ t_0, t_1, ..., t_j \\}$ of an interval $\[0,T\]$, let $|\Pi| = \max_i \( t_{i+1} - t_i \)$.  
A Brownian motion $B_t$ satisfies the following equation with probability 1:

$$\lim_{ |\Pi| \to 0} \sum_{t}^{} \( B_{t_{i+1}} - B_{t_{i}}  \) ^2 = T$$

(也就是说 $|\Pi|$ 是这些时间小段落中最长的一段, 并且 $\lim_{ |\Pi| \to 0}$ 表明最长的一段都趋近无穷小)

Proof:

For simplicity, here we only consider partitions where the gaps $t_{i+1} - t_{i}$ are uniform. In this case, the sum

$$\sum_{t}^{} \( B_{t_{i+1}} - B_{t_{i}}  \) ^2$$

is a sum if $i.i.d.$ random variables with mean $t_{i+1} - t_i$, and __finite second moment__ (细节看下面补充说明, 意思其实就是存在有限的方差)

Therefore, by the law of large numbers(大数定理), as $\max \\{ t_{i+1} - t_i \\} \to 0$, we have

$$\sum_{t}^{} \( B_{t_{i+1}} - B_{t_{i}}  \) ^2 = T$$

with probability 1.

Hence this shows that Brownian motion fluctuates a lot. The above can be summarized by the differential equation

$$\( dB \)^2 = dt$$

##### 补充说明 二次变分（Quadratic Variation)
上面的白话解释就是, 连续可微函数的二次变分是 $0$, 作为一个随机过程, 布朗运动的二次变分是 $T$ 而不是 $0$. 

根据下图再理解, 其中蓝色曲线为布朗运动的轨迹，红点为时间划分点对应的该轨迹的位移. $\( B_{t_{i+1}} - B_{t_{i}}  \) ^2$ 为任意相邻两个时间点的位移差的平方. 二次变分就是这些逐段位移差的累计平方和. 

![image](https://github.com/mincongzhang/Quant100Public/assets/5571030/06e0c8b2-9b95-4dc3-a038-ab98e5af7775)

对比一个普通的连续可微函数，随着对区间T越来越细的划分，它的二次变分趋于 $0$. 

![image](https://github.com/mincongzhang/Quant100Public/assets/5571030/043ba5d1-81af-47a4-abf1-596728901361)


对于布朗运动，其非零的二次变分说明随机性使得它的波动太频繁, 以至于不管我们如何细分区间, 得到多么微小的划分区间, 这些微小区间上的位移差的平方逐段累加起来的总和都不会消失（即二次变分不为 0），而是等于这个区间的长度 $T$!

这将会对之后的伊藤引理的推导起到很重要的作用. 

参考: 布朗运动、伊藤引理、BS 公式（前篇）
https://zhuanlan.zhihu.com/p/38293827

##### 补充说明 有限二阶矩（finite second moment)

下面是对finite second order moments的解释和证明:

What does it mean for a random variable to have finite second order moments?

the k-th moment of a random variable $X$ is $E\( X^k \)$. We say that this moment exists if $E\( |X|^k \)$ is a finite value (note the absolute value).

If a random variable has a finite K-th moment $E\( X^K \)$, the moments $E\( X^k \), for \ k \le K$ are also finite, proof:

If $0 \le k \le K$ then $|X|^k \le 1 + |X|^K$, so $E\( |X|^k \) \le 1 + E\( |X|^K \)$, and $E\( |X|^k \)$ is finite.

The variance is $Var \( X \) = E \( X^2 \) - E \( X \)^2 = E \( X^2 \) - E \( X^1 \)^2$. By the definition above and the property,
if $X$ has a finite 2nd order moment, it has a variance (and conversely).

https://math.stackexchange.com/questions/4118090/what-does-it-mean-for-a-random-variable-to-have-finite-second-order-moments


下面是知乎对moment(矩)的解释. 其实一阶矩就是期望值, 二阶矩就是方差. 那么finite second moment(有限二阶矩)意思就是存在有限的方差而已. 

概率论中，「矩」（moment）的实际含义是什么？高阶矩表示数据的哪些状态？
https://www.zhihu.com/question/23236070/answer/2319043296


#### 二次变分的更多解释

https://zhuanlan.zhihu.com/p/38293827

### Brownian motion with drift

Let $B\(t\)$ be a Brownian motion, and let $\mu$ be a fixed real. The process $X\(t\) = B\(t\) + \mu t$ is called a Brownian motion with drift $\mu$. 
By definition, it follows that $\mathbb{E} \[ X \( t \) \] = \mu t$.

Question: as time passes, which term will dominate? $B\(t\)$ or $\mu t$? It can be shown that $\mu t$ dominates the behavior of $X\(t\)$. 
For example, for all fixed $\varepsilon > 0$, after long enough time, the Brownian motion will always be between the lines $y=\(\mu - \varepsilon\) t$ and $y=\(\mu + \varepsilon\) t$.

When modelling the price of a stock, it's more reasonable to assume that the percentile change follows a normal distribution. 
This can be written in the following differential equation:

$$dS_t = \sigma S_t d B_t $$

Can we write the distribution os $S_t$ in terms of the distribution of $B_t$? Is it $S_t = e^{\sigma B_t}$? Suprisingly, the answer is no. 
