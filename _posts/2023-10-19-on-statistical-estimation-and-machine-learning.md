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

$$
\widehat{Diff} = \bar{Y}_1 - \bar{Y}_0
$$

From a statistician’s perspective, this estimator is a random variable since from the entire population suffering from the same disease, treatment and control groups are simply random samples. Perhaps, if we were to choose a different set of people (from the same population) this same estimator could give us a different treatment effect. How do we then determine the true effect of the medicine?

This is a typical statistical estimation problem of estimating the “true” unknown parameter using the observed data. The quality of any solution to such a problem comes down to answering two questions about the estimator: What is the bias and variance of the proposed estimator?

Note how far this is from a typical learning problem where an estimator is derived by training a model on the training set and then used to make predictions for new/unseen data. Given that there is just one data sample we can work with, it is clear that we need provable guarantees (usually achieved by making assumptions on the properties of the population) or empirical guarantees (achieved using Monte Carlo simulations) on the goodness of the estimator.

You might say: _Okay, but what has this to do anything with ML problems?_ So far not a lot but interestingly, some statistical estimation problems, like the one above, can be formulated as linear regression problems (for those of us coming from the ML world, the simplest learning algorithm).

$$
\bar{Y}_i = \beta_0 + \beta_1 \cdot D_i + \epsilon
$$

In this formulation, $\beta_1$ captures the treatment effect and one can prove that under some assumptions on the data distribution, the estimator obtained using OLS regression is unbiased and has the smallest variance among all possible estimators. In this particular application of OLS, unlike ML problems, it is irrelevant how well the linear model “predicts” each individual point. The focus is squarely on getting the point estimates and confidence intervals of the _coefficients_ right.

In typical machine learning applications, our focus is not usually so much on getting accurate coefficients (as in the case above) as getting the best possible forecast accuracy using the available training data. Nevertheless, at its core, we are, however, doing something very similar. For example, even in the ML world, we assume that the data is drawn from some fixed distribution and that there exists an optimal estimator h such that:

$$
h(x) = \mathbb{E} \left[ t\mid \mathbf{x} \right]
$$

Using some ML algorithm, we can produce an estimator $\mathbf{g}$ by training the model on D. Essentially, here $\mathbf{g}$ is a random variable and although eventually we are interested in the accuracy, it is closely related to the bias and variance of $\mathbf{g}$.

$$
Bias(g(\mathbf{x}_0)) = \left(\mathbb{E}_{\mathcal{D}} \left[g(\mathbf{x}_0 \mid \mathcal{D} \right] - h(\mathbf{x}_0) \right)\\
Var(g(\mathbf{x}_0)) = \mathbb{E}_{\mathcal{D}}\left[ \left(g(\mathbf{x}_0 \mid \mathcal{D}) - \mathbb{E}_{\mathcal{D}} \left[ g(\mathbf{x}_0 \mid \mathcal{D} )\right] \right)^2 \right]
$$
