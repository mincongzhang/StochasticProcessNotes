伊藤积分 - 我们最后想利用它来给期权定价

用随机过程给股票价格建模

基于股票价格给期权价格建模

算得期权价格

微分方程边界限制(boundary):

【【官方双语】微分方程概论-第二章：什么是偏微分方程？】 https://www.bilibili.com/video/BV1q4411p7NX/?share_source=copy_web&vd_source=f2d7e2fc28ededdf63c1684a3b6d0c5f

偏微分方程有多个解, 添加边界才能解出我们想要的

27 【为什么衍生品定价必须用随机微积分？ - 路边一熊猫 | 小红书 - 你的生活兴趣社区】 😆 Ry8lR3wXqj1E2R2 😆 https://www.xiaohongshu.com/discovery/item/695d7f05000000001a028dcb?source=webshare&xhsshare=pc_web&xsec_token=ABSSxpaGp8gT3fszp5YWrTkKtYIAZdxLeh6f3RxzSZwqc=&xsec_source=pc_share

38 【从对冲需求真正理解N(d1)和Numeraire - 路边一熊猫 | 小红书 - 你的生活兴趣社区】 😆 A3NNC6G8k79yKBF 😆 https://www.xiaohongshu.com/discovery/item/69467c36000000001f006892?source=webshare&xhsshare=pc_web&xsec_token=ABPhz8SpeAxdjyvIwu8mO55R042LkRayzJUPsgsTQ7p40=&xsec_source=pc_share

参考:
https://zhuanlan.zhihu.com/p/38293827

https://zhuanlan.zhihu.com/p/38294971

---------------------------

# 给股票和期权建模

## 股票

利用之前的理论, 我们给股票价格建模. 最好用随机的百分比变化(percentile change)来描述股价, 否则极端情况可能就到负数了. 股票价格可以写成以下微分形式: 


$$\frac{dS_t}{S_t} = d B_t $$

$$dS_t = S_t d B_t $$

注意到以上是微分形式, 我们想要求解微分方程得到原函数, 以下是一个可能的解吗?

$$dS_t = e^{B_t} d B_t =  S_t d B_t$$

看起来没问题但实际是不对的. 因为布朗运动是不可微的. 那如何求解呢? 就联系到之后要说的伊藤积分(Ito Calculus)了.

```
补充:
如果忘了求解微分方程是什么意思:
微分方程是 y'=dy/dx=2x
求解可得 y = x^2 + C
```

## 期权

接下来看期权价格建模. 先看一般情况. 

对一个光滑函数(smooth function), 它的变量 $x$ 是一个布朗运动 $B_t$, 我们要怎么计算这样的函数的结果(Estimate the outcome)? 更准确的说, 我们如何估计它无穷小的微分(estimate infinitesimal differences)? 

$$f(B_t)$$

```
补充:
上篇文章提到的可微的函数就是光滑函数. 布朗运动不可微就不是光滑函数.
比如一个指数函数 f(x)=e^x 是一个光滑函数
```


回到期权. 假如 $B_t$ 是股票价格, $f(B_t)$ 是股票对应期权(option)的价格. 股票价格是随机的, 但是对应的看涨期权价格(忽略期权费)在 $S_0$ 之前是0, 在 $S_0$ 之后是线性的:

<img width="597" height="444" alt="image" src="https://github.com/user-attachments/assets/506cbb78-e87e-4ffc-a547-b63eb126029e" />


假设 $B_t$ 是可微的, 也就是 $\frac{dB_t}{dt}$ 是存在的, 那么通过链式法则(chain rule)我们可以得到以下结果. 但因为 $B_t$ 不可微, 下式不存在:

$$ \frac{df}{dt} = \frac{dB_t}{dt} \cdot f' (B_t)$$

$$df = \( \frac{dB_t}{dt} \cdot f' \(B_t\) \)dt$$

那换一种方法避免 $\frac{dB_t}{dt}$, 已知 $df$ 的微分可以按如下描述:

$$df = f'\(B_t\)dB_t$$

我们做一个泰勒展开(Taylor expansion):

$$f\(x + \Delta x \) - f\(x\) = \Delta x \cdot f'\(x\) + \frac{\Delta x^2}{2}f''\(x\) + \frac{\Delta x^3}{6}f'''\(x\)+...$$


# 伊藤积分(Ito's Calculus)

-------
# Ito's Calculus
https://ocw.mit.edu/courses/18-s096-topics-in-mathematics-with-applications-in-finance-fall-2013/resources/mit18_s096f13_lecnote18/

In the previous lecture, we have observed that a sample Brownian path is nowhere differentiable with probability 1. In other words, the differentiation 

$$\frac{dB_t}{dt}$$

does not exist. However, while studying Brownian motions, or when using Brownian motion as a model, the situation of estimating the difference of a function of the type

$$f\(B_t\)$$

over an infinitesimal(无穷小) time difference occurs quite frequently (suppose that $f$ is a smooth function). To be more precise, we are considering a function $f\(t, B_t\)$ which depends only on the second variable. 
Hence there exists an implicit dependence on time since the Brownian motion depends on time. 

If the differentiation $\frac{dB_t}{dt}$ existed, then we can easily do this by using chain rule:

$$df = \( \frac{dB_t}{dt} \cdot f' \(B_t\) \)dt$$

Since $\frac{dB_t}{dt}$ does not exist, the formula above makes no sense. 

One possible way to work around this problem is to try to descrbe the difference $df$ in terms of the difference $dB_t$. In this case, the equation above becomes
$$df = f'\(B_t\)dB_t$$

Our new formula at least makes sense, since there is no need to refer to the differentiation $\frac{dB_t}{dt}$ which does not exist. The only problem is that it does not quite work. 

Consider the Taylor expansion of $f$ to obtain

$$f\(x + \Delta x \) - f\(x\) = \Delta x \cdot f'\(x\) + \frac{\Delta x^2}{2}f''\(x\) + \frac{\Delta x^3}{6}f'''\(x\)+...$$

To deduce this equation $df = f'(B_t)dB_t$ from this formula, we must be able to say that the significant term is the firt term $\Delta x \cdot f'\(x\)$ and all other terms are of smaller order of magnitude. Is this true for $x = B_t$? For $x = B_t$ we have

$$\Delta f = \Delta B_t \cdot f'\(B_t\) + \frac{\Delta B_t^2}{2}f''\(B_t\) + \frac{\Delta B_t^3}{6}f'''\(B_t\)+...$$

Now consider the term $\Delta B_t ^2$. Since $B_t$ is a Brownian motion, we know that $\mathbb{E} \( \Delta B_t ^2 \) = \Delta t$. Since a difference in $B_t$ is necessarily accompanied by a difference in $t$, we see that the second term is no longer negligable. The theory of Ito calculus essentially tells us that we can make the substitution $\Delta B_t ^2 = \Delta t$, and the remaining terms are negligable. Hence the equation above becomes

$$\Delta f = \Delta B_t \cdot f'\(B_t\) + \frac{\Delta t}{2}f''\(B_t\) + ...$$

Which interms of infinitesimals becomes

$$df \( B_t \) = f'\(B_t\)dB_t + \frac{1}{2} f''\(B_t\)dt$$

This equation known as the __Ito's lemma__ is the main equation of Ito's calculus. 

More generally, consider a smooth function $`f(t,x)`$ which depends on two variables. In classical calculus, we will get

$$df = \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} dx$$

And suppose that we are interested in the differential of $`f(t, B_t)`$, but in Ito calculus, we need to consider the second term from the Taylor expansion

$$\frac{1}{2} \frac{\partial^2 f}{\partial x^2} \(dB_t\)^2$$

And so we will get

$$df \( t, B_t \) = \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} d B_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \(dB_t\)^2$$

Since we have $\Delta B_t ^2 = \Delta t$, and $\( d B_t\) ^2 = d t$

$$
\begin{aligned}
df \( t, B_t \) &= \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} d B_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \(dB_t\)^2 \\
                &= \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} d B_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} d t \\
                &= \left (\frac{\partial f}{\partial t} + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \right) dt + \frac{\partial f}{\partial x} d B_t
\end{aligned}
$$

## Theorem: Ito's lemma
The stochastic process $X_t = \mu_t t + \sigma_t B_t$ is known as the Brownian motion with drift $\mu$ and variance $\sigma$.
For this process, we have 

$$dX_t = \mu_t dt + \sigma_t dB_t$$

Let $`f(t,x)`$ be a smooth function of two variables, and let $x$ be a stochastic process satisfying $dX_t = \mu_t dt + \sigma_t dB_t$ for a Brownian motion $B_t$. 
Then

$$df \( t, X_t \) = \left( \frac{\partial f}{\partial t} + \mu_t  \frac{\partial f}{\partial x} + \frac{1}{2} \sigma_{t}^{2}  \frac{\partial^2 f}{\partial x^2} \right) dt + \sigma_t \frac{\partial f}{\partial x} dB_t$$

Proof:

We have 

$$dX_t = \mu_t dt + \sigma_t dB_t$$

And most importantly

$$\( d B_t\) ^2  = d t$$

And so 

$$
\begin{aligned}
df \( t, X_t \)  &= \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} d X_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \(dX_t\)^2  \\
                 &= \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} \( \mu_t dt + \sigma_t dB_t \) + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \( \mu_t dt + \sigma_t dB_t \)^2  \\
                 &= \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} \( \mu_t dt + \sigma_t dB_t \)  + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \left( \( \mu_t dt \)^2 + 2 \mu_t \sigma_t dt dB_t   + \(\sigma_t dB_t \)^2  \right)
\end{aligned}
$$

We can ignore the terms $dtdB_t$ and $\(dt\)^2$, then we have

$$df \( t, X_t \)  = \frac{\partial f}{\partial t} dt +\frac{\partial f}{\partial x} \( \mu_t dt + \sigma_t dB_t \)  + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \(\sigma_t dB_t \)^2 $$

And we can use $\( d B_t\) ^2  = d t$ to simplify

$$
\begin{aligned}
df \( t, X_t \)  &= \frac{\partial f}{\partial t} dt +\frac{\partial f}{\partial x} \( \mu_t dt + \sigma_t dB_t \)  + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \sigma_{t}^2 dt \\
                 &= \left( \frac{\partial f}{\partial t} + \frac{\partial f}{\partial x} \mu_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \sigma_{t}^2  \right) dt + \sigma_t \frac{\partial f}{\partial x} dB_t \\
                 &= \left( \frac{\partial f}{\partial t} + \mu_t  \frac{\partial f}{\partial x} + \frac{1}{2} \sigma_{t}^{2}  \frac{\partial^2 f}{\partial x^2} \right) dt + \sigma_t \frac{\partial f}{\partial x} dB_t
\end{aligned}
$$


## Example

### What we know

(i) The stochastic process $X_t = \mu_t t + \sigma_t B_t$ is known as the Brownian motion with drift $\mu$ and variance $\sigma$.
For this process, we have 

$$dX_t = \mu_t dt + \sigma_t dB_t$$

(ii) Ito's lemma

$$df \( t, X_t \) = \left( \frac{\partial f}{\partial t} + \mu_t  \frac{\partial f}{\partial x} + \frac{1}{2} \sigma_{t}^{2}  \frac{\partial^2 f}{\partial x^2} \right) dt + \sigma_t \frac{\partial f}{\partial x} dB_t$$

### Example questions

[starting from video 19:00 https://www.youtube.com/watch?v=Z5yRMMVUC5w TODO can be removed]

(i) Consider the function $`f(x)= x^2`$. Can we try to find out what is $d f \( B_t \)$?

We can think about it as a function of 2 variables but it doesn't depend on $t$

$$f\(t, x\)= x^2$$

We know that

$$\frac{\partial f}{\partial t} = 0, \frac{\partial f}{\partial x} = 2x, \frac{\partial^2 f}{\partial x^2} = 2 \ for \ f\(t, x\)= x^2$$

$$dX_t = \mu_t dt + \sigma_t dB_t, \mu = 0, \sigma_t = 1, for \ dX_t = dB_t$$


So we can plug them in 


$$
\begin{aligned}
df \( t, X_t \) &= \left( \frac{\partial f}{\partial t} + \mu_t  \frac{\partial f}{\partial x} + \frac{1}{2} \sigma_{t}^{2}  \frac{\partial^2 f}{\partial x^2} \right) dt + \sigma_t \frac{\partial f}{\partial x} dB_t \\
                &= \left( 0 + 0 \cdot  2 B_t + \frac{1}{2} 1^{2}  2 \right) dt + 1 \cdot 2 B_t dB_t \\
                &= dt + 2 B_t dB_t
\end{aligned}
$$


Let's try another approach

$$
\begin{aligned}
f \( B_t \)   &= \( B_t \)^2 \\
d f \( B_t \) &= f'\(B_t\)dB_t + \frac{1}{2} f''\(B_t\)dt \\
              &= \left( 2 \cdot B_t \right) dB_t + \frac{1}{2} \left( 2 \right) dt \\
              &= 2 B_t dB_t + dt
\end{aligned}
$$

(ii) Consider the function $`f(x)= \frac{1}{2} x^2`$. Can we try to find out what is $d f \( B_t \)$?

we see that 

$$
\begin{aligned}
f \( B_t \)   &= \frac{1}{2} \( B_t \)^2 \\
d f \( B_t \) &= f'\(B_t\)dB_t + \frac{1}{2} f''\(B_t\)dt \\
              &= \left( 2 \cdot \frac{1}{2}  B_t \right) dB_t + \frac{1}{2} \left( 1 \right) dt \\
              &= B_t dB_t + \frac{1}{2} dt
\end{aligned}
$$

Equivalently, 

$$\frac{1}{2} B_{T}^2 = \int_{0}^{T} B_t d B_t + \int_{0}^{T} \frac{1}{2} dt = \int_{0}^{T} B_t d B_t + \frac{T}{2} $$

This implies that 

$$\int_{0}^{T} B_t d B_t = \frac{1}{2} B_{T}^2 - \frac{T}{2}$$

Comparing with integral of a normal function

$$\int_{0}^{T} x d x = \frac{1}{2} x^2$$

We have an extra $- \frac{T}{2}$. This "violates" the fundamental theorem of calculus.

###  Model stock price using Brownian motion

We want to Model stock price $S_t$ using Brownian motion. But we don't want $S_t$ to be a Brownian motion, because stock price cannot go negative. Instead we can model the percentile difference of the stock price to be a Brownian motion, so that it can go negative. 

额外解释: 因为 $`X(t)`$, 或者 $`B(t)`$的取值随着时间 $t$ 的变化可以是负数, 但是股票的价格显然不能是负数. 股价虽然不能是负数, 但是股票的收益率却有正有负, 所以我们可以用$`X(t)`$来描述收益率. 

假设$`S(t)`$为股票的价格, 则$`dS(t)`$为股价在无穷小的时间间隔内的变化量, 而 $\frac{dS\(t\)}{S\(t\)}$就是这段间隔内的收益率, 因此我们有


$$\frac{dS\(t\)}{S\(t\)} = \mu_t dt + \sigma_t dB_t$$

同时我们想把股票当作一个纯martingale的随机过程 (expected value is 0 at all times), 所以我们想把 $\mu_t dt$ 这个随着时间偏移(drift)的项给搞掉. 所以我们想找到满足以下等式的方程:

$$\frac{dS\(t\)}{S\(t\)} = \sigma_t dB_t$$

那我们猜测

$$S\(t\) = e^{\sigma B_t}$$

符合我们需求, 但是带入算出

$$S\(t\) = \frac{1}{2} \sigma^2 dt + \sigma d B_t$$

这 $\frac{1}{2} \sigma^2 dt$ 又是一个偏移(drift)了. 我们并不想要它. 那我们尝试消除它： 

$$S\(t\) = e^{- \frac{1}{2} \sigma^2 t + \sigma B_t}$$

就完成了. 以上是一个 geometric Brownian motion without drift. 

[https://www.youtube.com/watch?v=Z5yRMMVUC5w at 28:00]

Let $`f(t,x) = e^{\mu t + \sigma x}`$. Can we try to find out what is $d f \( B_t \)$?

We know that 

$$\left( e^{g\(x\)} \right)' = g'\(x\)e^{g\(x\)}$$

Then

$$
\begin{aligned}
df \( t, B_t \) &= \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} d B_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \(dB_t\)^2 \\
                &= \frac{\partial f}{\partial t} dt + \frac{\partial f}{\partial x} d B_t + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} d t \\
                &= \left (\frac{\partial f}{\partial t} + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \right) dt + \frac{\partial f}{\partial x} d B_t \\
                & = \left ( \mu f + \frac{1}{2} \sigma^2 f \right) dt + \\sigma f d B_t \\
                & = \left ( \mu  + \frac{1}{2} \sigma^2  \right) f\(t, B_t \) dt + \\sigma f\(t, B_t \) d B_t
\end{aligned}
$$

[https://www.youtube.com/watch?v=Z5yRMMVUC5w at time 26:00]

## Definition: integration


We define integration as an inverse of differentiation, i.e.,

$$F\( t, B_t \) = \int f\( t, B_t \) d B_t + \int g\( t, B_t \) d t $$

if and only if

$$d F = f\( t, B_t \) d B_t + g\( t, B_t \) d t$$

Becasuse differentiation is now well-defined, we just define integration as the inverse of it, just as in classical calculus. 

So far it doesn't have that good meaning, other than being an inverse of it, but at least it's well defined. 

Now the question is, does there exist a __Riemannian sum type of description__?

### Background: integral in calculus 

We have a function $f$, and we try to get the integration from $a$ to $b$. 

According to the Riemannian sum description, sum the area of these boxes and take the limit

$$\int_{a}^{b} f\(x\) dx = \lim \(Riemannian \ sums\)$$

![image](https://github.com/mincongzhang/Quant100Public/assets/5571030/807cbb70-ee2f-4b84-b8e4-b42943abbeab)

Back to our question, if we define integral in $F\( t, B_t \) = \int f\( t, B_t \) d B_t + \int g\( t, B_t \) d t $, __do we have this Riemannian sum type description?__

In the Riemannian sum, it didn't matter which point you took in this interval. In the interval $a_i$ to $a_{i+1}$, you take any point in the middle and make a rectangle according to that point. And then no matter which point you take, when you go to the limit, you had exactly the same sum all the time. 

But in here $d F = f\( t, B_t \) d B_t + g\( t, B_t \) d t$, that's no longer true. If you take the left point all the time, or you take the right point all the time, the two limits are different. 

And again, that's due to the __quadratic variation__, because that much of variance can accumulate over time. 

### Ito integral definition

Ito integral is the limit of Riemannian sums when always take the __leftmost point of of each interval__. 

![image](https://github.com/mincongzhang/Quant100Public/assets/5571030/d0d8f7b2-a34d-456f-ba7e-42170423a0ec)

We won't go into details. But what if we take the __rightmost__ point all the time, we get an equivalent theory of calculus, and it's just like Ito's calculus and it's coherent itself.  So there is no logical flaw in it. But the only difference is the second order term turns from $+$ to $-$:

$$df \( t, X_t \)  = \frac{\partial f}{\partial t} dt +\frac{\partial f}{\partial x} \( \mu_t dt + \sigma_t dB_t \)  + \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \(\sigma_t dB_t \)^2 $$

It becomes 

$$df \( t, X_t \)  = \frac{\partial f}{\partial t} dt +\frac{\partial f}{\partial x} \( \mu_t dt + \sigma_t dB_t \)  - \frac{1}{2} \frac{\partial^2 f}{\partial x^2} \(\sigma_t dB_t \)^2 $$

__Remark:__ "Equivalent" of Ito calculus such that 

$$dB_{t}^2 = - dt$$

But why we use __leftmost__ more? Let's think about the stock price. In real world you have to make the decision at time $t_i$. Your choice __cannot depend on the future time__. 

![image](https://github.com/mincongzhang/Quant100Public/assets/5571030/3f0536cd-0039-4a27-afd2-d45782c6f5d5)


And by that we can introduce a new concept "adapted process", which means at time $t$, you are only allowed to use the information up to time $t$. And we will look into the properties of Ito Calculus. 

# Properties of Ito Calculus

First theorem can be seen as an extension of the fact that the sum of independent normal random variables is a random variable. 

## Theorem

Let $`B(t)`$ be a Brownian motion, and let $`\Delta(t)`$ be a nonrandom function of time. Suppose that a stochastic process $`I(t)`$ satisfies

$$dI = \Delta \(s\) d B_s \ i.e. \ I\(t\) = \int \Delta \(s\) d B_s$$

Where $`I(0) = 0`$. 

Then for each $t \le 0$, the random variable $`I(t)`$ is normally distributed. 

What happens when we allow $`\Delta (t)`$ to be a random function of time? Here is an interesting and natrual class of random variables $`\Delta (t)`$ that we consider. 

## Definition: Adapted Process

Let $X_t$ be a stochastic process. $`\Delta (t)`$ is adapted to $X_t$ if for all $t \le 0$, $`\Delta (t)`$ depends only on $`X_0 \sim X_t`$

For example, suppose that we model the price of a stock using a stochastic process, and are trying to find a strategy which has positive expected return. 
Consider a simple strategy where at each time $t$, we either buy or sell one stock based on the past values of your stock price, then that strategy is an adapted process. This defines the processes that are reasonable, that cannot see future. 

And think about what we said before, we always take the leftmost point, adaptive processes just also fit very well with Ito's calculus. 

### Adapted process examples
(i) The process $`\Delta (t) = X_t`$ is an adapted process (or we can say $X_t$ is adapted to $X_t$)

(ii)  $Y_t = X_{t+1}$ is not adapted to $X_t$

(iii) The process $`\Delta (t) = min {\{X_t, c\}}`$ is an adapted process (adapted to $X_t$, and $c$ is a constant)

(iv) The process $`\Delta (t) = \max_{0 \le t < T} X_t`$ is not an adapted process (it depends on the future $T$)

(v) If $\tau$ is a stopping time, then $X_\tau$ is an adapted process




### Review

1. Define Ito lemma, that means differentiation in Ito calculus.
2. Define integration using differentiation (inverse operation of the differentiation)
3. Integration has an alternative description in terms of Riemannian sums, where you take the leftmost point as the reference point for each interval.
4. so we use the adapted process to describe "using the leftmost point"

Now let's see what happens when you take the __integral of adapted processes__. 


## Theorem

The first thing is about normal distribution. Let's say we have this: $B_t$ has normal distribution of $0$ up to $t$: $`B(t) \sim N(0,t)`$

$$
\begin{aligned}
X\(t\) &= \sigma B\(t\)\sim N\(0,\sigma^2 t\) \\
       &= \int \sigma d B_t
\end{aligned}
$$

So $\sigma$ is a constant. When you take the Ito integral of $\sigma d B_t$ at each time you get a normal distribution. And a hidden fact is that the sum of normal distribution is also normal distribution. 

And that can be generalised.

If $`\Delta (t)`$ is a process depending only on the time variable (it doesn't depend on the Brownian motion), then 

$$X\(t\) = \int \Delta \(t\) d B \(t\)$$

has normal distribution at all time. 

## Theorem: Ito Isometry

Now how do we get the variance of the Ito integral? 

Let $B_t$ be a Brownian motion. Then for all adapted processes $`\Delta (t)`$, we have 

$$\mathbb{E} \left[  \left( \int_{0}^{t} \Delta \( s \) d B_s  \right)^2 \right] = \mathbb{E} \left[  \int_{0}^{t} \Delta \( s \)^2 d B_s  \right]$$

### Example

We are not going to prove it. But we can take one example to see how it likes.

Let $\Delta \( t \) = 1$. Then the left hand side of the theorem above is

$$\mathbb{E} \left[  \left( \int_{0}^{t} \Delta \( s \) d B_s  \right)^2 \right] = \mathbb{E} \left[  B_{t}^{2} \right] = t$$

And the right hand side of the above is

$$\mathbb{E} \left[  \int_{0}^{t} \Delta \( s \)^2 d B_s  \right] = \mathbb{E} \left[ t \right] = t$$

Note that $\int_{0}^{t} \Delta \( s \) d B_s = 0$ by the Theorem below. Hence Ito isometry tell us how to compute the variance of this integral. 

[so....actually...how to compute??? 所以难道等式左边按正常算结果是0， 但是如果有右边的帮助， 我们就可以算出真正的var=t?]


![image](https://github.com/mincongzhang/Quant100Public/assets/5571030/694b3ce6-d584-4c3a-a4b1-4ef59d974d3c)

## Theorem: When is Ito integral a martingale?

Firstly, what is a martingale?

Martingale means if you have a stochastic process, at any time $t$, whatever happens after that, the expected value at time $t$ equals to the value at $t_0$. 

Then the question is, when is Ito integral a martingale?

Let $B_t$ be a Brownian motion. Then for all adapted processes $`g(t, B_t)`$, the integral

$$\int g \( t, B_t \) dB_s$$

is a martingale, as long as $g$ is a "reasonable function". Formally, if $g \in L^2$, i.e. 

$$\int \int_{0}^{t} g^2 \( t, B_t \) dt dB_t < \infty $$

Let's look at a stochastic differential equation:

$$dX_t = \mu_t dt + \sigma_t dB_t$$

if it doesn't have a drift term ($\mu = 0$), it's a martingale. If it has a drift term it's not a martingale. 

It's useful in pricing theory. In pricing theory, you come up with this stochastic process or some strategy. You can build a portfolio without drift term, then it's a martingale. 

## Girsanov theorem (Change of measure)

### The underlying question

Suppose we have two Brownian motions:
1. one is without drift
2. the other is with drift

These are two probability distributions over paths. 

The question is can we switch from the distribution with drift to the disribution without drift, by a change of measure?

An example to show what it really means:

![image](https://github.com/mincongzhang/Quant100Public/assets/5571030/378c3ced-b557-4d74-bfc8-98285fae094e)


### More details: we need to define a concept of equivalent between 2 probability distribution

Suppose $P$ is a probability distribution over $\Omega$:

$$\( \Omega, P \) : probability \  distribution$$

$$\( \Omega, \tilde{P} \) : probability \  distribution$$

We define $P$ and $\tilde{P}$ to be equivalent if 

$$P \( A \) > 0 \Leftrightarrow \tilde{P} \( A \) > 0 for \ all \ A \subset \Omega$$

![image](https://github.com/mincongzhang/Quant100Public/assets/5571030/7ccfa6ff-ca06-4732-a178-acd0f4a9f19a)

__Example 1__

$$\Omega = \\{ 1,2,3 \\}$$

$$P\( 1 \) = \frac{1}{3}, P\( 2 \) = \frac{1}{3}, P\( 3 \) = \frac{1}{3}$$

$$\tilde{P}\( 1 \) = \frac{2}{3}, \tilde{P}\( 2 \) = \frac{1}{6}, \tilde{P}\( 3 \) = \frac{1}{6}$$

Then let's take a subset $A = \\{ 1,2 \\}$ of our background set $\Omega$, then we have:

$$P\( A \) = \frac{2}{3}$$

$$\tilde{P}\( A \) = \frac{5}{6}$$

Their probabilities are not the same, but they satisfy $P \( A \) > 0 \Leftrightarrow \tilde{P} \( A \) > 0 for \ all \ A \subset \Omega$

Therefore these two probability distributions are __equivalent__

__Example 2__

$$\Omega = \\{ 1,2,3 \\}$$

$$P\( 1 \) = \frac{1}{3}, P\( 2 \) = \frac{1}{3}, P\( 3 \) = \frac{1}{3}$$

$$\tilde{P}\( 1 \) = \frac{2}{3}, \tilde{P}\( 2 \) = \frac{1}{3}, \tilde{P}\( 3 \) = 0$$

Then let's take a subset $A = \\{ 3 \\}$ of our background set $\Omega$, then we have:


$$P\( A \) = \frac{1}{3}$$

$$\tilde{P}\( A \) = 0$$

they don't satisfy $P \( A \) > 0 \Leftrightarrow \tilde{P} \( A \) > 0 for \ all \ A \subset \Omega$

Therefore these two probability distributions are __not equivalent__

### Back to Girsanov theorem (Change of measure)

There exists a $Z$ such that $`P(\omega) = Z(\omega)\tilde{P}(\omega)`$ if and only if $P$ and $\tilde{P}$ are __equivalent__.

That means you can change from one probability measure to another probability measure just in terms of multiplication, if and only if they are equivalent. 

In the finite world this is very intuitive, but it's true for all probability spaces.

And these are called the Radon-Nikodym derivative. 

(Probability measure: 概率测度)


### Question: are these two Brownian motions equivalent?
One brownian motion is without drift, and the other brownian motion is with drift. Are they kind of the same but just skewed id distribution, or are they really fundamentally different? 

And what Girsanov's theorem says is that they are equivalent. 

This will also be used in pricing theory. You can switch some stochastic process into a stochastic process without drift, thus making it into a martingale. 

### Summary: Theorem: Girsanov theorem

$P$: probability distribution over $\[0, T\]^{\infty}$ defined by Brownian motion with dirft $\mu$

$\tilde{P}$: probability distribution over $\[0, T\]^{\infty}$ defined by Brownian motion without dirft

$\[0, T\]^{\infty}$ : means all the paths of stochastic process from $0$ to $T$

The $P$ and $\tilde{P}$ are equivalent. 

And the Radon-Nikodym derivative 

$$Z\(\omega\) = \frac{d \tilde{P} }{d P} \(\omega\) = e^{-\mu \omega \(T\) - \mu ^2 T/2 }$$


__More implications:__

We can compuate the expectation in our probability space:

$$\tilde{\mathbb{E}} \[ V_t \] = \mathbb{E}[Z_t V_t]$$

Where $\tilde{\mathbb{E}}$ is the expectation in probability space $\(\Omega, \tilde{P}\)$ (without drift)

Where $\mathbb{E}$ is the expectation in probability space $\(\Omega, P\)$ (with drift)

So we can transform the problems about Brownian motion with drift into a problem about Brownian motion without a drift. 
