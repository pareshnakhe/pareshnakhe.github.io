---
title: "A Balls and Bins Variation"
---

In this post, I am looking at a bins and balls variation of the classic problem. The analysis may seem high-school level
for some but I feel it is a cute and small problem for my first post. So the problem is this:
<blockquote>You have $ { k}$ balls and $ { n }$ bins. $ { k \leq n }$ . If
    you throw the balls in bins uniformly at random, how many bins will have at least one ball? In other words, how many
    bins will remain empty.</blockquote>
Let $ { X }$ be the random variable indicating the number of bins with at least one ball. Consider
indicator random variable $ {X_i}$ as follows,
<p align="center">$ \displaystyle X_i = \begin{cases} 1 & \text{if } i^{th} \text{bin has at least one ball} \\ 0 &
    \text{if } \text{otherwise} \end{cases} $</p>
Therefore, we can express $ {X}$ as the sum of indicator random variables.

$ {X = \sum_{i=1}^{n} X_i}$

Taking expectation, $ { E[X] = \sum_{i=1}^{n} E[X_i] }$, which basically means we now have to find out
the the probability that a bin $ {i}$ has at least one ball. This is equal to, 1 - probability that bin i
gets no ball in all the $ {k}$ trials which is,
<p align="center">$ {1 - (1- \frac{1}{n} )^k}$</p>
There is an interesting inequality which says that
<p align="center">$ { (1 - \frac{1}{n})^{n-1} \geq e^{-1} }$</p>
Using this inequality, we can claim that the probability that bin $ {i}$ has at least one ball is greater
than $ { 1 - e^{ \frac{-k}{n-1} } }$. Using this value in the expectation expression earlier, the
expected number of bins with at least one ball is
<p align="center">$ {n( 1 - e^{ \frac{-k}{n-1} } ) }$</p>
Now this wasn't too difficult right? So we make the problem a bit more interesting and ask, suppose you have $
{n}$ unique marbles in a box and you get to pick $ {k}$ of them uniformly at random <i>with
    replacement</i>. When you draw these out, you colour each of them red, so that you know they have been drawn at
least once. You keep repeating this experiment till all marbles are colored red <i>with high probability</i>. What is
the number of times you repeat this experiment?

By the above calculation, we know now that when you pick $ {k}$ marbles in any trial, you are actually
picking just $ {n( 1 - e^{ \frac{-k}{n-1} } ) }$ distinct marbles. Now suppose that, there is one marble,
lets name it $ {p}$. What is the probability that the $ {p}$ will be coloured red in one
trial....that will be greater than,
<p align="center">$ {\frac{n( 1 - e^{ \frac{-k}{n-1} } )}{n}}$</p>
Therefore, the probability of not selecting $ {p}$ in one trial is,
<p align="center">$ {1 - ( 1 - e^{ \frac{-k}{n-1} }) = e^{ \frac{-k}{n-1} }}$</p>
Suppose, you decide to conduct these trials for $ { \frac{(n-1) \log n}{k} }$. Then the probability that
$ {p}$ is not selected in any of the trials is
<p align="center">$ { e^{ \frac{-k}{n-1} \cdot \frac{(n-1) \log n}{k}} = \frac{1}{n}}$</p>
So basically, we have proven that the probability that any marble $ {p}$ is not coloured red for $ {
\frac{(n-1) \log n}{k} }$ consecutive rounds is extremely small. So there it is, if you perform the trials for
$ { O( \frac{n \log n}{k} )}$ rounds, with high probability every node will be coloured red.

This is all for today folks. Please let me know if there is some mistake or any suggestion of doing it in a better way.