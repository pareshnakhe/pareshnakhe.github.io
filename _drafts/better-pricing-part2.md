# Better Pricing: Part 2

## Optimization Function

$$
\mathcal{L}(\p) ~=~ \p \cdot \x ~-~ \lambda \norm{\p - \p^{old}}^2\\
$$

Given this function, we can compute the new optimal price as follows:

$$
\DeclareMathOperator*{\argmax}{arg\,max}
\norm{\p}^{new} ~=~ \argmax\limits_{\p} \mathcal{L}(\p)\\[8pt]
~~~~s.t.~~ \norm{\p^{new}} ~\leq~ 1.05 \cdot \norm{\p^{old}}\\
$$


Present solution for following toy examples:

1. Pricing policy with 2 unique price points.
2. Pricing policy with 10 unique price points.
3. Continuous pricing policy (assume linear for now) - don't know if this is a good idea..


- Discuss the dependence on lambda
- Discuss the assumption that changes in price do not impact demand.
- Introduce CES utilities and discuss how this can be used to model impact of changes in prices on demand.