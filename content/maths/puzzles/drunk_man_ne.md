+++
date = '2025-08-02T04:49:51Z'
draft = false
title = 'Drunk Man moving North and East'
+++

## Problem
A drunk man leaves a bar and every second it gets harder for him to move.
In the $t^{th}$ second, he moves a distance of $\frac{1}{2^{t-1}}$ m, either in the north or east direction with equal probability.
What will be his expected Euclidean distance from the bar after a long time?

## Solution
Let $d^M_t$, and $d^E_t$ denote the Manhattan and Euclidean distance of the drunk man at time $t$.

Note that the Manhattan distance increases by $\frac{1}{2^t}$ regardless of whether the drunk man moves north or east.
Thus,
\[
\lim_{t \rightarrow \infty} d^M_t = 1 + \frac 12 + \frac 14 + \ldots = 2.
\]
This means the Manhattan distance of the drunk man would approach 2 after a long time, and the drunk man would land on the line $x+y=2$.
We have two ways to compute $d^E_t$. However, the first method can be used only to compute $(d^E_t)^2$. 

For computing $(d^E_t)^2$, define indicator variables $I_t$, such that $I_t$ is $1$ if the drunk man moves in the x-direction in the $t^{th}$ step, and $0$ otherwise.
Then, the final x-position of the drunk man can be represented by the random variable
\[
X = 1 I_{1} + \frac 12 I_{2} + \frac 14 + \ldots,
\]
Since the drunk man moves north or east with equal probability, $E[I_t] = 0.5$, for all $t$.
We know that the drunk man eventually lands on the line $x+y=2$, thus his y-position would eventually be $y = x - 2$.
Therefore, we can say that the expected value of the square of Euclidean distance would eventually be
\[
E\left[\lim_{t \rightarrow \infty} (d^E_t)^2 \right] = E[X^2 + (2 - X)^2] = 2 (E[X^2] - 2 E[X] + 2).
\]
The expected value of $X$ and $X^2$ can be computed as follows
\[
\begin{aligned}
E[X] &= \frac 12 \left( 1 + \frac 12 + \frac 14 + \ldots \right) = 1, \\
E[X^2] &= \sum_{i=1}^{\infty} \left[ \left( \frac{1}{2^{2(i-1)}} E[I_i^2] \right) + \left( \frac{1}{2^{i-1}} \sum_{j = 1; j \neq i}^\infty \frac{1}{2^{j-1}} E[I_i I_j] \right) \right] = \frac 43,
\end{aligned}
\]
using $E[I_i^2] = 0.5$, and $E[I_i I_j] = 0.25$ if $i \neq j$ (since $I_i$ and $I_j$ are independent events).
Therefore, 
\[
E\left[\lim_{t \rightarrow \infty} (d^E_t)^2 \right] = E[X^2 + (2 - X)^2] = 2 (E[X^2] - 2 E[X] + 2) = 2 \left(\frac 43 - 2 + 2\right) = \frac 83.
\]

Another way to approach this problem is to think where the drunk man lands on the line $x+y=2$ and with what probability?
It can be shown that the drunk man lands on every point of the line almost uniformly. (Look at the end of this article for the proof.)
Given this, the expected distance can be calculated simply by integrating over the line segment of the line $x+y=2$ in the first quadrant.
Parametrize the line as $(1+t, 1-t)$ for $-1 \leq t \leq 1$.
Then, $\lim_{t \rightarrow \infty} d^E_t$ and $\lim_{t \rightarrow \infty}(d^E_t)^2$ can be computed as
\[
\begin{aligned}
\lim_{t \rightarrow \infty} d^E_t &= \frac{1}{1 - (-1)} \int_{-1}^1 \sqrt{(1-t)^2 + (1+t)^2} dt = \frac{1}{\sqrt{2}} \left( ln(\sqrt{2} + 1) + \sqrt{2}\right) \approx 1.62\\
\lim_{t \rightarrow \infty} (d^E_t)^2 &= \frac{1}{1 - (-1)} \int_{-1}^1 (1-t)^2 + (1+t)^2 dt = \frac 83\\  
\end{aligned}
\]

_But why is the probability uniform?_

<!---
\[
\begin{aligned}
x_p &= vT + \frac 12 a_{acc}(T - T_p)^2 - L\\
x_s &= vT_p + \frac{v^2}{a_{dec}}
\end{aligned}
\]
where $x_p = $ distance for safely proceeding, $x_s = $ distance for safely stopping, $v = $ approach speed, $T = $ yellow light duration, $T_p = $ perception time, and $L = $ length of the car.

We want $x_p > x_s$ for no dilemma zone. That is, 
\[
\begin{aligned}
vT + \frac 12 a_{acc}(T - T_p)^2 - L > vT_p + \frac{v^2}{a_{dec}}\\
(T-T_p) \left( v + \frac 12 a_{acc}(T-T_p) \right) > \frac{v^2}{a_{dec}} + L\\
\end{aligned}
\]

_How to choose the optimal $T$ from here which would work for any given $v$?_
-->
