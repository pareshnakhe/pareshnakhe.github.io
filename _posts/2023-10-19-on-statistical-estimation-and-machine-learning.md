---
title: "On Statistical Estimation and Machine Learning"
classes: wide
---

I am an ML practitioner without much formal training in either ML or statistical techniques, although I can find my way around most ML-related topics. At work, I have colleagues focusing on econometric problems using ideas that are seemingly from the ML realm. For example, I didn’t know how linear regression could be repurposed to solve these problems. I also found it strange that we don’t speak the same language (after all ML origins can be traced back to ideas from statistical estimation); for example, these colleagues obsess over confidence intervals whereas I hardly ever worked on problems with this requirement. This post is based on some of my musings about how the two fields are connected; what are the differences? and why?

Let’s start with a simple statistical estimation problem of estimating the effectiveness of a medicine in a randomized controlled trial. The problem is as follows: We create two groups of people suffering from the same disease. One group (control, D_i =0) receives placebo tablets while the other group (treatment, D_i=1) receives the real medicine to be tested. What we want to know is if the medicine indeed contributes to recovery. At the end of the test, we collect data capturing the level of recovery, Y_i. For simplicity, say Y_i = 0 or 1. The sample means in each of the groups are:

$$
Y_0 ~=~ \frac{1}{n_0} \sum\limits_{i; D_i = 0} Y_i \\
Y_1 ~=~ \frac{1}{n_1} \sum\limits_{i; D_i = 1} Y_i \\
$$

Here $n_0$ and $n_1$ are the number of people in the control and treatment groups respectively. One way to estimate the effectiveness of the said medicine is to measure the effect using the so-called difference estimator.