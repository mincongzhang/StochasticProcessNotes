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
3. 处处不可微(nowhere differentiable). 因为所有的微积分都是基于求微分(differentiation), 处处不可微也意味着用微积分没法用了. 之后我们会说到的伊藤积分(Ito Calculus)可以解决这个问题. 

如下图, 在 $t_0$ 时刻的概率分布符合 $N(0, t_0)$ (均值为0, 标准差为 $\sqrt{t_0}$)的正态分布. 所以大部分值都会处于这个区间之内. 

![image](https://github.com/user-attachments/assets/92423743-c8c9-4f2f-9aa3-fd64c6931fcc)

再用python画一些随机游走路径来更直观感受一下, 我们可以看见随机游走是呈正态分布的, 并且大部分处于曲线 $x=y^2$ 内:

<img width="900" height="600" alt="image" src="https://github.com/user-attachments/assets/92956b5c-a36c-4d13-9bd9-d131c9d0380f" />


## 例子: 用布朗运动给日内股票价格建模(Use Brownian motion as a model for daily stock price)

来看一个股票日内价格变化的例子, 假设股票交易从9:30am开始到4:00pm结束, 股价初始值为 $S_0$, 并且股价符合布朗运动. 我们如何获得日内最小值和最大值的概率分布?

![image](https://github.com/user-attachments/assets/4671c135-a9ff-4572-b4cb-fd654d1efee9)

我们就只算一下日内最大值的概率分布. 定义日内最大值的概率分布 $M(t) = \max_{0 \le s \le t} B(s)$. 可以发现 $M(t)$ 是一个新的基于布朗运动 $B(s)$ 的随机过程.

我们有结论如下, $\forall t \gt 0$ 和 $a \ge 0$:

$$ P ( M(t) \ge a ) = 2 P ( B (t) \ge a )$$

这个结论说的是日内最大值达到或超过a的概率分布是布朗运动达到或超过a的概率分布的两倍. 为什么呢? 

我们先画图臆测一下, 假设一段随机路径第一次达到了最大值 $\tau_a$ , 之后继续遵循布朗运动. 又因为是布朗运动, 所以之后路径高于和低于 $\tau_a$ 的概率一样, 那我们就去掉高于 $\tau_a$ 的路径概率, 算两遍低于 $\tau_a$ 的概率. 

也就是说我们只要把布朗运动里超过a的部分的概率分布, 都反射到a以下就完事了. 这样最大值到a的概率分布就等于布朗运动达到a的概率分布的两倍. 这就是所谓的 __反射原理(Reflection principle)__. 下面我们证明一下.

![image](https://github.com/user-attachments/assets/381a35c9-40bd-49a1-975c-b2c01cd82a74)

### 证明

定义 $\tau_a$ 是一个停时(stopping time): $\tau_a = min_s \\{ s: B ( s ) = a \\}$, 意思就是随机过程第一次达到 a 的时刻 (可能还有第二/三次达到a但是我们只记录第一次). 

对于所有的 $0 \le s < t$, 我们有:

$$P(B (s) > B (t)) = P(B (s) < B (t))$$

也就是:

$$P(B (t) - B (s) > 0) = P(B (t) - B (s) < 0) $$

那么在 $\tau_a < t$的条件下:

$$P(B (\tau_a) > B (t)) = P(B (\tau_a) < B (t))$$

也就是:

$$P(B (t) - B (\tau_a) > 0 | \tau_a < t) = P(B (t) - B (\tau_a) < 0 | \tau_a < t)$$

收集齐了这些前置条件, 以及 $P(B (t) \ge a | \tau_a < t) = P(B (t) \ge a)$, 还有 $B (\tau_a) = a$, 我们可以得出: 

$$
\begin{aligned}
P(M(t) \ge a) &= P(\tau_a < t) \\
              &= P(B (t) - B (\tau_a) > 0 | \tau_a < t) + P(B (t) - B (\tau_a) < 0 | \tau_a < t) \\
              &= 2 P(B (t) - B (\tau_a) > 0 | \tau_a < t) \\
              &= 2 P(B (t) > a | \tau_a < t)
\end{aligned}
$$


其中当 $B (t) > a$ 发生的时候, 因为 $B (\tau_a) = a$, t必然已经超过了 $\tau_a$, 所以条件 $\tau_a < t$ 可以忽略了. 所以我们就有了:

$$ P(M(t) \ge a) = 2 P(B (t) > a | \tau_a < t) = 2 P(B (t) > a)$$


补充: 这个例子里我们假设 $B ( t ) - B ( \tau_a )$ 的分布不被 $\tau_a < t$ 这个条件影响, 也就是说这个布朗运动具有 __强马尔可夫性质(Strong Markov Property)__. 

再补充: 假如 $\tau_a$ 这个停时是"现在", $s<\tau_a$ 是"过去", $s>\tau_a$ 是"未来". 在已知"现在"的条件下，"将来"与"过去"无关的特性被称为强马尔可夫性. 早这个日内股票价格例子里, 假如我们现在是中午, 下午的股价变动和早上已知的股价变动没关系, 这种理想情况下的股价变动具有强马尔科夫性.


### 计算

接下来我们把以上概率分布算出来: 

$$P(M(t) \ge a) = 2 P (B (t) \ge a)$$

其实只需要计算:

$$P (B (t) \ge a)$$

根据前面的定理:
1. $B \(0\) = 0$
2. 平稳性(stationary): 对所有 $0 \le s < t$ , $B (t) - B (s)$ 的概率分布是均值为0方差为 $t-s$ 的正态分布. 

那么 $B (t)$的概率分布就是均值为0方差为 $t$ 的正态分布. 

在计算 $P (B (t) \ge a)$ 之前我们先回顾一下背景知识. 

先看离散型均匀分布(discrete uniform distribution):

假设我们有一个均匀骰子, 每个面对应的数字出现的概率都是1/6, 我们可以画出数字的概率质量函数(Probability mass function).

以及对应的累积分布函数(Cumulative distribution function, CDF), 含义是小于等于x的概率. 比如投出小于等于1的概率是1/6, 小于等于2的概率是2/6, 小于等于6的概率是6/6也就是100%. 

![image](https://github.com/user-attachments/assets/d34d159d-aeac-47c5-b9f6-83b9c6a89587)

再看连续型均匀分布(continuous uniform distribution), 这里可以看作0到6之前出现任何一个实数的概率都是1/6. 我们可以画出数字的概率密度函数(Probability density function, PDF).

以及对应的累积分布函数(Cumulative distribution function, CDF), 含义是小于等于x的概率. 出现小于等于x的数字的概率是1/x, 小于等于6的概率是6/6也就是100%. 

![image](https://github.com/user-attachments/assets/5efe4b33-a5a7-4084-937c-d81d21dfed09)


最后回到我们的股价涨跌 $B(t)$ 的概率密度函数((Probability density function, PDF)), 为均值为0方差为 $t$ 的正态分布, 以及累积分布函数(Cumulative distribution function, CDF). 

我们可以看出小于等于x的概率为 $\Phi (\frac {x}{\sqrt{t} })$. 

![image](https://github.com/user-attachments/assets/399e81f1-3442-4da1-af26-ae5894fb5660)


我们可以得到大于等于 $a$ 的概率: 

$$P (B (t) \ge a) = 1 - \Phi (\frac {a}{\sqrt{t} })$$

根据之前提到的反射原理(Reflection principle), 日内股价大于等于a的概率为:

$$P(M(t) \ge a) = 2 P (B (t) \ge a) =  2 \times (1 - \Phi (\frac {a}{\sqrt{t} }) )$$

参考: https://www.probabilitycourse.com/chapter4/4_2_3_normal.php#:~:text=The%20CDF%20of%20the%20standard%20normal%20distribution%20is%20denoted%20by,is%20widely%20used%20in%20probability.


### 性质2: 不可微 (Not differentiable)

根据前面的性质, 我们可以推导出以下结论. 

布朗运动对任意 $t \ge 0$ 都不可微 (not differentiable). 

在证明之前我们看看可微的定义. 简单来说如果以下极限存在, 我们可以说某个函数 $f(x)$ 在 $x=t$ 这个点可微:

$$\lim_{\delta \to 0} \frac{f(t+\delta) - f(t)}{\delta}$$

再严谨一些, 对所有 $\epsilon > 0$, 存在一个 $\delta > 0$ 使得下面条件满足, 我们可以说这个函数在这个点可微, 并且 $A$ 是 $f(x)$ 在 $x=t$ 的导数(derivative):

$$\| \frac{f(t+\delta) - f(t)}{\delta} - A \| < \epsilon$$

回到布朗运动, 我们假设布朗运动在 $t$ 点可微, 并且微分结果为 $A$, 那么我们如下结果和示意图:

$$\frac{dB}{dt}(t) = A$$

<img width="537" height="377" alt="image" src="https://github.com/user-attachments/assets/76704744-1fa4-4300-aff6-324946cd2988" />

根据本篇开头示意图(也就是随机游走和 $x=y^2$ 边界的示意图), 我们可以猜测:


<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/3f5c7cf4-5349-4f89-92c1-bac90c2acdd9" />

如果 $B(t)$ 可微, 那么对任意 $\epsilon > 0$, 存在 $\delta >0$, 使得 $| \[B(t+\delta) - B(t)\]/\delta - A | < \epsilon $.

我们有 $| B(t+\delta) - B(t)| < \delta*A + \epsilon $, 根据之前的Epsilon-Delta定义, 


证明: 

![image](https://github.com/user-attachments/assets/07e95bbb-6a1c-4673-b04a-5f1a02e1d2f2)

![image](https://github.com/user-attachments/assets/dd4e39d0-bf87-441a-aa85-2e157703320e)

![image](https://github.com/user-attachments/assets/ee0f93f3-ce34-4b65-af76-3ff29fd61a43)


https://youtu.be/PPl-7_RL0Ko?si=cCr7sO7CoL6PyakE&t=2553

The above proposition can help us prove the following result

For each $t \ge 0$, the Brownian motion is almost surely not differentiable at $t$

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
