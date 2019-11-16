---
title: "Edge Case: Nested and Mixed Lists"
categories:
- Edge Case
tags:
- content
- css
- edge case
- lists
- markup
---

In this post, I am looking at a bins and balls variation of the classic problem. The analysis may seem high-school level
for some but I feel it is a cute and small problem for my first post. So the problem is this:
<blockquote>You have $latex { k}&fg=000000$ balls and $latex { n }&fg=000000$ bins. $latex { k \leq n }&fg=000000$ . If
    you throw the balls in bins uniformly at random, how many bins will have at least one ball? In other words, how many
    bins will remain empty.</blockquote>
Let $latex { X }&fg=000000$ be the random variable indicating the number of bins with at least one ball. Consider
indicator random variable $latex {X_i}&fg=000000$ as follows,
<p align="center">$latex \displaystyle X_i = \begin{cases} 1 & \text{if } i^{th} \text{bin has at least one ball} \\ 0 &
    \text{if } \text{otherwise} \end{cases} &fg=000000$</p>
Therefore, we can express $latex {X}&fg=000000$ as the sum of indicator random variables.

$latex {X = \sum_{i=1}^{n} X_i}&fg=000000$

Taking expectation, $latex { E[X] = \sum_{i=1}^{n} E[X_i] }&fg=000000$, which basically means we now have to find out
the the probability that a bin $latex {i}&fg=000000$ has at least one ball. This is equal to, 1 - probability that bin i
gets no ball in all the $latex {k}&fg=000000$ trials which is,
<p align="center">$latex {1 - (1- \frac{1}{n} )^k}&fg=000000$</p>
There is an interesting inequality which says that
<p align="center">$latex { (1 - \frac{1}{n})^{n-1} \geq e^{-1} }&fg=000000$</p>
Using this inequality, we can claim that the probability that bin $latex {i}&fg=000000$ has at least one ball is greater
than $latex { 1 - e^{ \frac{-k}{n-1} } }&fg=000000$. Using this value in the expectation expression earlier, the
expected number of bins with at least one ball is
<p align="center">$latex {n( 1 - e^{ \frac{-k}{n-1} } ) }&fg=000000$</p>
Now this wasn't too difficult right? So we make the problem a bit more interesting and ask, suppose you have $latex
{n}&fg=000000$ unique marbles in a box and you get to pick $latex {k}&fg=000000$ of them uniformly at random <i>with
    replacement</i>. When you draw these out, you colour each of them red, so that you know they have been drawn at
least once. You keep repeating this experiment till all marbles are colored red <i>with high probability</i>. What is
the number of times you repeat this experiment?

By the above calculation, we know now that when you pick $latex {k}&fg=000000$ marbles in any trial, you are actually
picking just $latex {n( 1 - e^{ \frac{-k}{n-1} } ) }&fg=000000$ distinct marbles. Now suppose that, there is one marble,
lets name it $latex {p}&fg=000000$. What is the probability that the $latex {p}&fg=000000$ will be coloured red in one
trial....that will be greater than,
<p align="center">$latex {\frac{n( 1 - e^{ \frac{-k}{n-1} } )}{n}}&fg=000000$</p>
Therefore, the probability of not selecting $latex {p}&fg=000000$ in one trial is,
<p align="center">$latex {1 - ( 1 - e^{ \frac{-k}{n-1} }) = e^{ \frac{-k}{n-1} }}&fg=000000$</p>
Suppose, you decide to conduct these trials for $latex { \frac{(n-1) \log n}{k} }&fg=000000$. Then the probability that
$latex {p}&fg=000000$ is not selected in any of the trials is
<p align="center">$latex { e^{ \frac{-k}{n-1} \cdot \frac{(n-1) \log n}{k}} = \frac{1}{n}}&fg=000000$</p>
So basically, we have proven that the probability that any marble $latex {p}&fg=000000$ is not coloured red for $latex {
\frac{(n-1) \log n}{k} }&fg=000000$ consecutive rounds is extremely small. So there it is, if you perform the trials for
$latex { O( \frac{n \log n}{k} )}&fg=000000$ rounds, with high probability every node will be coloured red.

This is all for today folks. Please let me know if there is some mistake or any suggestion of doing it in a better way.