---
title: "Better Pricing: Part 2"
---

This post is a continuation of the previous post in the series "Better Pricing". Last time, I introduced the basic set-up of the problem at hand and the constraint we shall be using. And the objective? Maximizing revenue of course! But we shall go about it in a slightly different way by maximizing the following function:

$$
\newcommand{\bm}[1]{\boldsymbol{#1}}
\newcommand{\norm}[1]{\left\lVert#1\right\rVert}
\newcommand{\p}{\bm{p}}
\newcommand{\x}{\bm{x}}
\mathcal{L}(\p) ~=~ \p \cdot \x ~-~ \lambda \norm{\p - \p^{old}}^2\\
$$

Given this function, we can compute the new optimal price as follows:

$$
\DeclareMathOperator*{\argmax}{arg\,max}
\norm{\p}^{new} ~=~ \argmax\limits_{\p} \mathcal{L}(\p)\\[8pt]
~~~~s.t.~~ \norm{\p^{new}} ~\leq~ 1.05 \cdot \norm{\p^{old}}\\
$$

## Toy Example

For purposes of illustration, let's consider a simplified (discrete) version of the problem, where WoG can be either 0 or 1 (representing two different demand scenarios).

<!-- add the two toy pics here -->
<figure class="half">
    <a href="/assets/images/better_pricing2/toy1.png"><img src="/assets/images/better_pricing2/toy1.png"></a>
    <a href="/assets/images/better_pricing2/toy2.png"><img src="/assets/images/better_pricing2/toy2.png"></a>
    <figcaption>Demand and Prices for different WoG scenarios</figcaption>
</figure>

Let's first visualize the objective function and the solution space. Darker shades of green correspond to smaller numbers.

<!-- opt_prices_temp -->
![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/better_pricing2/opt_prices_tmp.png){: .align-center}

Luckily for us, the objective function is quadratic with linear constraints. This will help us with faster computation. The code snippet used to find *optimal prices* is as follows:

<script src="https://gist.github.com/pareshnakhe/05443f35faa69b99fe19c029794b138c.js"></script>

Let's see what the new prices are:

<figure class="half">
    <a href="/assets/images/better_pricing2/opt_prices.png"><img src="/assets/images/better_pricing2/opt_prices.png"></a>
    <a href="/assets/images/better_pricing2/price_change.png"><img src="/assets/images/better_pricing2/price_change.png"></a>
    <figcaption>Prices after Optimization</figcaption>
</figure>

This seems to makes sense: for the low demand scenario (WoG=0), prices have decreased whereas for the high demand scenario (WoG=1) prices have increased. I should point out a couple of things at this point:
1. The optimal hyperparameter $\lambda$, responsible for penalizing changes in prices, in our basic model, cannot be determined in a methodical way. For this example, I manually tried different values to see which ones make sense.
2. Our model does not assume changes in demand on changes in prices. But since the price changes are expected to be rather small, I think the assumption is justified.

Let's try out a pricing policy with 10 unique price points and how the prices change. The only thing we need to change in the code above is p_old and x_old:
```
p_old = np.array([0.4]*5 + [0.6]*5)
x_old = np.array(np.linspace(0.2, 0.8, 10))
```

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/better_pricing2/price_change_10.png){: .align-center}

That's all for now folks. Hope you found the idea interesting!

<!-- Present solution for following toy examples:

1. Pricing policy with 2 unique price points.
2. Pricing policy with 10 unique price points.
3. Continuous pricing policy (assume linear for now) - don't know if this is a good idea..


- Discuss the dependence on lambda
- Discuss the assumption that changes in price do not impact demand.
- Introduce CES utilities and discuss how this can be used to model impact of changes in prices on demand. -->
