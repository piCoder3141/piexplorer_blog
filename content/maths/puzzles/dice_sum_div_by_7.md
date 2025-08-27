+++
date = '2025-08-12T08:24:12Z'
draft = false
title = 'Dice Sum Divisible by 7'
+++

## Problem
There are 4 fair six-sided dice, and they are each rolled once.
What is the probability that the sum of the values on the top faces is divisible by 7?
_Can you find the answer for any general $n$ fair six-sided dice?_

## Solution
_Naive Solution:_ Maximum sum of the four dice can be 24.
Out of these, 7, 14, and 21 are divisible by 7.
So, we need to count the number of configurations which yield the sum of 7, 14, or 21.

_Solution for general $n$_: Suppose that you fix the values of the first $n-1$ dice.
Compute the sum of these values modulo 7 (say $k$).
Then if $ k \neq 0$, there is **exactly** one value of the $n^{th}$ dice that would make the sum of all the dice divisible by 7, that is $7 - k$.
In the case when $k = 0$, we have no configuration which satisfies the condition.

Define,
\[
P_n = \text{Probability that the sum of values of $n$ dices is divisible by 7.}
\]
Then, using our observation, we can derive the recursive relation
\[
P_n = \frac 16 (1 - P_{n-1})
\]
We know that $P_1 = 0$, and hence, we can compute the successive values of $P_n$.
