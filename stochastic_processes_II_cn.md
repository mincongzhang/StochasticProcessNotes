# MIT随机过程笔记[2]:连续时间随机过程-布朗运动

## 前言

MIT公开课里随机过程和伊藤引理这两部分讲得还是非常清晰易懂的. 我参考了他们的教学视频和教案整理翻译成中文发在这里. 


视频: https://www.youtube.com/watch?v=PPl-7_RL0Ko

教案: https://ocw.mit.edu/courses/18-s096-topics-in-mathematics-with-applications-in-finance-fall-2013/resources/mit18_s096f13_lecnote17/


## 回顾

上篇我们讨论了马尔可夫链(Markov Chains)和鞅(Martingales), 那些都是离散随机过程(discrete-time stochastic process), 可表示为: 

$$X_0, X_1, X_2, X_3, ...$$ 

接下来我们要了解的连续随机过程(continuous-time stochastic process)可表示为: 

$$\\{ X_t \\} _{t \ge 0}$$

其中t是实数(real number)而不是整数(integer).

## 连续随机过程难点: 如何描述概率分布(how to describe the probability distribution)

连续随机过程的第一个难点是如何描述概率分布(probability distribution).

回顾离散随机过程的概率分布. 离散随机过程概率分布的意思是, 比如一台机器连续运转365天后坏掉和继续运转的的概率, 或者100轮赌博后盈亏多少的概率, 又或者说是每个随机路径到终点不同位置的概率. 概率分布描述的是经过多个离散步骤之后结果的概率汇总.

在简单随机游走(simple random walk)这个例子中, 我们用50%描述每一时刻和下一时刻(t和t+1)往上或者往下变动的概率, 在过程结束, 所有步骤结合起来后, 我们才获得概率分布:

$$
\begin{aligned}
X_{t+1} - X_{t} &= 1 \quad &\text{(P=0.5)} \\
                &= -1 \quad &\text{(P=0.5)} \\
\end{aligned}
$$

![image](https://github.com/user-attachments/assets/ce0c71e2-73ac-47fd-ac2f-9fa5b37a3c74)

总结: 

- 在 __离散随机过程__ 中, 我们知道从 __t到t+1__ 时刻改变多少的概率(上一篇说的矩阵 $A$), 把每个时间变化的概率都合并起来 ($A^n$), 我们就能得到概率分布. 

- 但是在 __连续随机过程__ 中, __不存在t和t+1__, 那我们也没法描述两个时刻之间变化的概率, 如果把时间区间所有的变化都算完需要做 __无穷多次计算__ . 

我们可以用概率密度函数(probability density function)来描述概率分布, 可以表示如下:

$$P(\omega)$$

## 标准布朗运动(Standard Brownian motion)

背景: 布朗运动最开始是由英国植物学家布朗观察到水中悬浮的花粉的不规则运动而命名的. 布朗运动也叫维纳过程(Wiener process). 

物理现象例子: 假如我们观察一些物理现象的时候, 我们通过观察记录非常精细的离散时间点的现象(也就是n尽量无限大, 比如每个间隔百万分之一秒), 发现结果近似布朗运动, 我们就可以确定其为布朗运动. 

股票例子: 布朗运动也可以用来给股票建模, 虽然股票交易频率是有限制的, 但只要我们把时间拉长, 它就可以看作是布朗运动. 

在给出复杂定义之前, 我们可以从简单随机游走引申一下. 如果我们的简单随机游走取极限, 比如一个固定区间, 我们定义一个n步(n steps)随机游走过程, 把n扩展到无限大, 那么这个随机游走的结果就是布朗运动.

用术语描述: 定义一个简单随机游走 ${Y_0, Y_1, ...,Y_n}$ 的均值(mean)为0, 方差(variance)为1. 定义 $Z$ 为一个实数 $\mathbb{R}$ 上 $\[ 0, 1 \]$ 的分段函数(piecewise linear function):

$$Z \left( \frac{t}{n} \right) = Y_t$$

并且我们线性扩展 $t=0,...,n$ 到非常大, 这时候 $Z$ 的路径的分布就会逐渐接近布朗运动. 通过中心极限定理(central limit theorem), 我们可以发现 $Z(1)$ 的分布会收敛到标准正态分布 $N(0,1)$ . 更加一般化来看, $Z(t)$ 会收敛到 $N(0,t)$. 

补充解释：
- 提到的 $\[ 0, 1 \]$ 其实也就是 $\frac{t}{n}$ 的取值范围
- 总结上述就是普通随意游走取极限得到的连续方程可以看作是标准布朗运动


### 定义

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

再画一些随机游走路径来更直观感受一下, 我们可以看见大部分处于曲线 $x=y^2$ 内, 并且右图显示如果路径数量足够多， 结果确实呈现为正态分布:

<img width="900" height="600" alt="image" src="https://github.com/user-attachments/assets/de455511-070f-4348-8e30-2b7594894a72" />


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

$$
\begin{aligned}
P (B (t) \ge a) &= P(N(0,t) \ge a) \\
                &= 1 - \Phi (\frac {a}{\sqrt{t} })
\end{aligned}
$$

根据之前提到的反射原理(Reflection principle), 日内股价大于等于a的概率为:

$$
\begin{aligned}
P(M(t) \ge a) &=2 P (B (t) \ge a) \\
              &= 2 P(N(0,t) \ge a) \\
              &= 2 (1 - \Phi (\frac {a}{\sqrt{t} }) )
\end{aligned}
$$

参考: https://www.probabilitycourse.com/chapter4/4_2_3_normal.php#:~:text=The%20CDF%20of%20the%20standard%20normal%20distribution%20is%20denoted%20by,is%20widely%20used%20in%20probability.


### 性质: 不可微 (Not differentiable)

根据前面的性质, 我们可以得出以下结论. 

布朗运动对任意 $t \ge 0$ 都不可微 (not differentiable). 

```
更严谨地说是几乎确定(almost surely)不可微, 之后会解释.
```

在证明之前我们看看对一个函数可微的定义. 我们用经典的Epsilon-Delta来说明. 简单来说如果以下极限存在, 我们可以说某个函数 $f(x)$ 在 $x=t$ 这个点可微:

$$\lim_{\delta \to 0} \frac{f(t+\delta) - f(t)}{\delta}$$

再严谨一些, 对所有 $\epsilon > 0$, 存在 $\delta > 0$ 使得下面条件满足, 我们可以说这个函数在这个点可微, 并且 $A$ 是 $f(x)$ 在 $x=t$ 的导数(derivative):

$$\| \frac{f(t+\delta) - f(t)}{\delta} - A \| < \epsilon$$

回到布朗运动, 我们假设布朗运动 $B(t)$ 在 $t$ 点可微, 并且微分结果为 $A$, 也就是 $B(t)$ 在 $t$ 点的导数, 或者如下示意图里的斜率:

$$\frac{dB}{dt}(t) = A$$

<img width="486" height="340" alt="image" src="https://github.com/user-attachments/assets/baa1ee04-4123-4109-aee2-a45925e1d443" />


也就是说如果 $B(t)$ 可微, 那么对所有 $\epsilon > 0$, 存在 $\delta >0$, 使得:

$$| \frac{B(t+\delta) - B(t)}{\delta} - A | < \epsilon $$

也就是

$$| \frac{B(t+\delta) - B(t)}{\delta}  | < A + \epsilon $$

因为 $\epsilon$ 可以是任意大于0的数, 我们假设它很小就忽略掉它, 但可以用 $\le$ 表示:

$$| \frac{B(t+\delta) - B(t)}{\delta}  | \le A $$

接下来我们可以画图猜测一下. 我们画两条斜率为 $±A$ 的直线. 如果以上不等式成立, 那么布朗运动路径一定会在这两条直线相夹形成的锥形以内.

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/a331e132-a2c8-4b49-b3be-ad41ca1bc06c" />

可以看出因为随机游走, 路径有可能超出这个锥形, 也就是 $|\frac{B(t+\delta) - B(t)}{\delta}  | \le A$ 不成立. 所以 $B(t)$ 不可微. 下面我们再简单证明一下. 

还记得之前例子里股票大于等于 $a$ 的概率吗? 我们算出从0时刻到 $t$ 时刻中某一个时刻最大值 $M(t)$ 大于等于 $a$ 的概率为:

$$P(M(t) \ge a) = 2 P (B (t) \ge a) =  2 (1 - \Phi (\frac {a}{\sqrt{t} }) )$$

回到我们的例子, 我们想证明 $|\frac{B(t+\delta) - B(t)}{\delta}  | \le A$ 也就是 $|B(t+\delta) - B(t)  | \le A\delta$ 不成立.

把上面等式替换一下, 从 $t$ 时刻到 $t+\delta$ 时刻中某一个时刻最大值 $M(\delta)$ 大于等于 $A\delta$ 的概率为:

$$
\begin{aligned}
P(M(\delta) \ge A\delta) &= 2 P (B (\delta) \ge A\delta) \\
                         &= 2 P (N (0, \delta) \ge A\delta) \\
                         &= 2 (1 - \Phi (\frac {A\delta}{\sqrt{\delta} }) ) \\
                         &= 2 (1 - \Phi (A\sqrt{\delta}) )
\end{aligned}
$$

当 $\delta$ 趋近于0的时候, 右边等式趋近于 $2 (1 - \frac{1}{2}) = 1$. 也就是不管我们取多小的区间, $B(t)$ 都不会收敛, 也就是 $B(t)$ 几乎肯定不可微. 

对于我们直观的感受就是, 布朗运动函数不是一个光滑的函数(not a smooth function), 因为即使我们再缩小观测范围, 函数都会很毛糙.

```
再提"几乎肯定"(almost surely):
这三位大佬(Dvoretsky, Erdos,and Kakutani)更严谨地说明了B(t)在任何时刻都不可微. 也就是说布朗运动虽是连续的但处处不可微.
证明比较复杂并且需要用到波莱尔-坎泰利引理(Borel–Cantelli lemma), 有兴趣的话自己去搜搜吧.
```

### 二次变分 (Quadratic Variation)

#### 一般函数的二次变分

在了解布朗运动的二次变分之前, 我们看看一般的连续可微函数(continuously differentiable function)的二次变分(quadratic variation).

选取时间区间 $[0,T]$ 的一部分 $\Pi = \\{ 0 = t_0 < t_1 < ...< t_N \\}$. 对于一个连续可微函数 $f(t)$, 我们定义它的二次变分如下, 也就是这些逐段位移差的累计平方和:

$$ \sum_{t}^{N-1} ( f( t_{i+1} ) - f( t_{i} )  ) ^2$$

利用中值定理(Mean value theorem):

$$f'(s_i) = \frac{f( t_{i+1} ) - f( t_{i} )}{t_{i+1} - t_i}, s_i \in [t_i, t_{i+1}]$$

我们得到:

$$\sum_{t}^{N-1} ( f( t_{i+1} ) - f( t_{i} )  ) ^2 = \sum_{t}^{N-1} (t_{i+1}-t_{i}) ^2 f'(s_i)^2, s_i \in [t_i, t_{i+1}]$$

并且在时间区间 $[0,T]$ 取 $f'(s)$ 的上界(upper bound), 也就是最大值, 我们就可以得到以下不等式:

$$
\begin{aligned}
\sum_{t}^{N-1} ( f( t_{i+1} ) - f( t_{i} )  ) ^2 & =   \sum_{t}^{N-1} (t_{i+1}-t_{i}) ^2 f'(s_i)^2, s_i \in [t_i, t_{i+1}] \\
                                                 & \le \max_{s \in \[0,T\]} f'(s)^2 \sum_{t}^{N-1} (t_{i+1}-t_{i}) ^2
\end{aligned}
$$

进一步:

$$
\begin{aligned}
\sum_{t}^{N-1} ( f( t_{i+1} ) - f( t_{i} )  ) ^2 & =   \sum_{t}^{N-1} (t_{i+1}-t_{i}) ^2 f'(s_i)^2, s_i \in [t_i, t_{i+1}] \\
                                                 & \le \max_{s \in [0,T]} f'(s)^2 \sum_{t}^{N-1} (t_{i+1}-t_{i}) ^2 \\
                                                 & \le \max_{s \in [0,T]} f'(s)^2 \sum_{t}^{N-1} [(t_{i+1}-t_{i}) \cdot (t_{i+1}-t_{i})] \\
                                                 & \le \max_{s \in [0,T]} f'(s)^2  \cdot \max_{i} \\{{ t_{i+1} - t_i  \\}} \cdot \sum_{t}^{N-1} (t_{i+1}-t_{i}) \\
                                                 & \le \max_{s \in [0,T]} f'(s)^2 \cdot \max_{i} \\{{ t_{i+1} - t_i  \\}} \cdot T
\end{aligned}
$$

随着 $\max \\{{ t_{i+1} - t_i  \\}}$ 趋近于0, 以上不等式右边趋近于0. 这意味着随着我们越来越细地划分, 连续可微函数的二次变分 $\sum_{t}^{N-1} ( f( t_{i+1} ) - f( t_{i} )  ) ^2$ 趋近于0. 

总结, 连续可微函数的二次变分, 也就是逐段位移差的累积平方和为0. 二次变分可以用来描述函数是否平滑(smooth), 对于连续可微函数, 利用二次变分可以看出它在微观层面是平滑的. 

#### 布朗运动的二次变分

看完连续可微函数的二次变分, 回到布朗运动, 它虽然是连续的, 但是不可微, 根据我们之前的观察它在围观层面不是光滑的(smooth), 下面看看它的二次变分.

布朗运动在时间区间 $[0,T]$ 上划分的 $\Pi = \\{ 0 = t_0 < t_1 < ...< t_N \\}$ 的二次变分是:

$$ \sum_{t}^{N-1} ( B( t_{i+1} ) - B( t_{i} )  ) ^2$$

它的期望是:

$$\sum_{t}^{N-1} E[( B( t_{i+1} ) - B( t_{i} )) ^2]$$

回顾布朗运动的平稳性(stationary), 对所有 $0 \le t_i < t_{i+1}$ , $B (t_{i+1}) - B (t_i)$ 的概率分布是均值为0方差为 $t_{i+1}-t_i$ 的正态分布, 可表示为 $N(0, t_{i+1}-t_i)$. 并且正态分布 $X \sim N(\mu, \sigma^2)$ 平方的期望是 $E(X^2) = \mu^2 + \sigma^2$, 那么:

$$
\begin{aligned}
E(N(0, t_{i+1}-t_i)^2) & = E(N(0, \sqrt{t_{i+1}-t_i}^2)^2)  \\
                       & = 0^2 + \sqrt{t_{i+1}-t_i}^2 \\
                       & = t_{i+1}-t_i
\end{aligned}
$$

于是我们有:

$$
\begin{aligned}
\sum_{t}^{N-1} E[( B( t_{i+1} ) - B( t_{i} )) ^2] & = \sum_{t}^{N-1} E[N(0, t_{i+1}-t_i) ^2]  \\
                                                  & = \sum_{t}^{N-1} ( t_{i+1}-t_i)  \\
                                                  & = T
\end{aligned}
$$

写成微分方程形式:

$$(dB)^2 = dt$$

总结, 布朗运动的二次变分, 也就是逐段位移差的累积平方和为T, 在微观层面依然很粗糙, 这都是由随机性导致的.  

#### 对比

我们对比时间区间划分成20段和40段后, 布朗运动和平滑函数的二次变分:

<img width="1400" height="500" alt="image" src="https://github.com/user-attachments/assets/0485722f-d6aa-4300-9ed4-f3c1d60ffa4b" />

<img width="1400" height="500" alt="image" src="https://github.com/user-attachments/assets/3780ac2b-da30-47ad-9fe8-e083b200c384" />

当我们划分段落越来越多之后, 可以发现布朗运动的二次变分逐渐趋近于时间段T, 而平滑函数的二次变分逐渐趋近于0:

<img width="1000" height="600" alt="image" src="https://github.com/user-attachments/assets/c3a69b53-0da5-4cb1-98a6-dc2033609996" />



花费这么多笔墨了解完布朗运动的不可微以及二次变分, 都是为了之后伊藤引理的推导.


### 带漂移项的布朗运动 (Brownian motion with drift)

最后来看一个带漂移的布朗运动. 对布朗运动 $B(t)$, 我们加一个固定的实数(fixed real) $\mu$, 可以得到以下带漂移项 $\mu$ 的布朗运动:

$$X(t) = B(t) + \mu t$$

因为 $\mathbb{E} [B(t)] = 0$, 我们有:

$$\mathbb{E} [X(t)] = \mathbb{E}[B(t)] + \mathbb{E} [\mu t] = \mu t$$

问题:随着时间的推移, $X(t)$ 是受到 $B(t)$ 的影响更大, 还是受到 $\mu t$ 的影响更大? 

如下图, 我们可以看见 $\mu t$ 的影响更大, 对任意给定的 $\varepsilon > 0$, 随着时间推移, $X(t)$ 总会收敛于 $y=(\mu - \varepsilon) t$ 和  $y=(\mu + \varepsilon) t$ 之间.

<img width="1000" height="600" alt="image" src="https://github.com/user-attachments/assets/a0554c7c-aa50-49c3-8e4b-d9b05b917b61" />

<img width="1000" height="600" alt="image" src="https://github.com/user-attachments/assets/fdef7b44-8458-44b7-a57f-da799cc1ce6b" />

加上复利(compound interest), 基金投资中的资产增长预测大概也是这样来的吧.

<img width="802" height="401" alt="image" src="https://github.com/user-attachments/assets/9c04c8ca-9c4a-4c47-8ec4-d9b53e1a0a7b" />



When modelling the price of a stock, it's more reasonable to assume that the percentile change follows a normal distribution. 
This can be written in the following differential equation:

$$dS_t = \sigma S_t d B_t $$

Can we write the distribution os $S_t$ in terms of the distribution of $B_t$? Is it $S_t = e^{\sigma B_t}$? Suprisingly, the answer is no. 

参考:
https://zhuanlan.zhihu.com/p/38293827
