# Better Pricing: Part 2

This post is a continuation of the previous post in the series "Better Pricing". Last time, I introduced the basic set-up of the problem at hand and the constraint we shall be using. And the objective? Maximizing revenue of course! But we shall go about it in a slightly different way by maximizing the following function:

$$
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

Let's first visualize the objective function and the solution space. Darker shades of green correspond to smaller numbers.

<!-- opt_prices_temp -->

Luckily for us, the objective function is quadratic with linear constraints. This will help with faster computation. The code snippet used to find *optimal prices* is as follows:

<script src="https://gist.github.com/pareshnakhe/05443f35faa69b99fe19c029794b138c.js"></script>

<!-- Present solution for following toy examples:

1. Pricing policy with 2 unique price points.
2. Pricing policy with 10 unique price points.
3. Continuous pricing policy (assume linear for now) - don't know if this is a good idea..


- Discuss the dependence on lambda
- Discuss the assumption that changes in price do not impact demand.
- Introduce CES utilities and discuss how this can be used to model impact of changes in prices on demand. -->
