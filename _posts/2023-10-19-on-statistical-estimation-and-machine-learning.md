---
title: "On Statistical Estimation and Machine Learning"
classes: wide
---

> My thoughts on the commonalities between these two disciplines and how diverging motivations have shaped their vastly different perspectives.

<!-- ![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/statistical_estimation_ml/title_image.jpg){: .align-center} -->

{% include figure image_path="/assets/images/statistical_estimation_ml/title_image.jpg" alt="titleimage" caption="Photo by Christopher Paul High on Unsplash" %}

As an ML practitioner I have dabbled in statistical techniques but often only to to the extent necessary to understand a learning algorithm. At work, I see colleagues use ideas, seemingly from the ML realm, to answer econometric questions. For example, I didn’t know how linear regression could be repurposed to answer econometric questions. I also found it surprising that we don’t speak the same language (after all ML origins can be traced back to ideas from statistical estimation); for instance, these colleagues obsess over confidence intervals whereas I hardly ever worked on problems with this requirement. This post is based on some of my musings about how the two fields are connected and the primary differences.

Let’s start with a simple statistical estimation problem of estimating the effectiveness of a medicine in a randomized controlled trial. The problem is as follows: We create two groups of people suffering from the same disease. One group (control, $D_i = 0$) receives placebo tablets while the other group (treatment, $D_i=1$) receives the real medicine to be tested. What we want to know is if the medicine indeed contributes to recovery. At the end of the test, we collect data capturing the level of recovery, $Y_i$. For simplicity, say $Y_i = 0$ or $1$. The sample means in each of the groups are:

$$
\bar{Y}_0 ~=~ \frac{1}{n_0} \sum\limits_{i; D_i = 0} Y_i \hspace{2cm} \bar{Y}_1 ~=~ \frac{1}{n_1} \sum\limits_{i; D_i = 1} Y_i
$$

Here $n_0$ and $n_1$ are the number of people in the control and treatment groups respectively. One way to estimate the effectiveness of the said medicine is to measure the effect using the so-called difference estimator.

$$
\widehat{Diff} = \bar{Y}_1 - \bar{Y}_0
$$

From a statistician’s perspective, this estimator is a random variable since from the entire population suffering from the same disease, treatment and control groups are simply random samples. Perhaps, if we were to choose a different set of people (from the same population) this same estimator could give us a different treatment effect. How do we then determine the true effect of the medicine?

This is a typical statistical estimation problem of estimating the "true" unknown parameter using the observed data. The quality of any solution to such a problem comes down to answering two questions about the estimator: What is the bias and variance of the proposed estimator?

Note how far this is from a typical learning problem where an estimator is derived by training a model on the training set and then used to make predictions for new/unseen data. Given that there is just one data sample to work with, it is clear we need provable guarantees (usually achieved by making assumptions on the properties of the population) or empirical guarantees (achieved using Monte Carlo simulations) on the goodness of the estimator.

You might say: _Okay, but what has this to do anything with ML problems?_ So far, not a lot but interestingly, some statistical estimation problems, like the one above, can be formulated as linear regression problems (for those of us coming from the ML world, the simplest learning algorithm).

$$
\bar{Y}_i = \beta_0 + \beta_1 \cdot D_i + \epsilon
$$

In this formulation, $\beta_1$ captures the treatment effect and it can be shown that under some assumptions on the data distribution, the estimator obtained using OLS regression is unbiased and has the smallest variance among all possible estimators. In this particular application of OLS, unlike ML problems, it is irrelevant how well the linear model "predicts" each individual point. The focus is squarely on getting the point estimates and confidence intervals of the _coefficients_ right.

In typical machine learning applications, our focus is not usually so much on getting accurate coefficients (as in the case above) as getting the best possible forecast accuracy using the available training data. Nevertheless, at its core, we are, however, doing something very similar. For example, even in the ML world, we assume that the data is drawn from some fixed distribution and that there exists an optimal estimator h such that:

$$
h(x) = \mathbb{E} \left[ y(x) \mid \mathbf{x}; \mathcal{D} \right]
$$

Using an off-the-shelf ML algorithm, we can produce an estimator $\mathbf{g}$ by training the model on D. Essentially, here $\mathbf{g}$ is a random variable and although eventually we are interested in the accuracy, it is closely related to the bias and variance of $\mathbf{g}$.

$$
Bias(g(\mathbf{x}_0)) = \left(\mathbb{E}_{\mathcal{D}} \left[g(\mathbf{x}_0 \mid \mathcal{D} \right] - h(\mathbf{x}_0) \right)\\[8pt]
Var(g(\mathbf{x}_0)) = \mathbb{E}_{\mathcal{D}}\left[ \left(g(\mathbf{x}_0 \mid \mathcal{D}) - \mathbb{E}_{\mathcal{D}} \left[ g(\mathbf{x}_0 \mid \mathcal{D} )\right] \right)^2 \right]
$$

Note how the bias of $\mathbf{g}$ is defined using the expected value of $\mathbf{g}(x)$ over all possible training sets D. And what does the variance exactly mean here?

Suppose we take 1000 samples of size N and for each sample, $D_i$, train a model $\mathbf{g}(D_i)$; then the variance of the model (i.e. the rule used to derive $g(D_i)$ from $D_i$) is:

$$
Var(f'(x_0)) = \frac{1}{1000} \cdot \sum\limits_i \left[ (g(x_0 \mid D_i) - \bar{g}(x_0))^2\right]
$$

We say $\mathbf{g}$ has a high variance if different sets of training data (chosen from the same population) give drastically different predictions. In ML terminology, this happens if we overfit the training data leading to high generalization error. Analogously, if the model is not flexible enough to capture the complexity of the data (read, high bias) the accuracy is going to suffer.

To complete the chain of thoughts: the goodness of an estimator, for both kinds of problems, is/can be assessed in very similar ways. The difference I see however is that the stats community is way more rigorous in giving provable guarantees, either by making assumptions on the distribution of the data and/or on the form of $\mathbf{g}$. In contrast, in the ML community, the questions about the bias and variance of a forecaster are not addressed with the same rigour. Honestly, I am not sure why.

## More Points of Comparison

For statistical estimation problems:

- bias and variance of estimators are key metrics

- the estimands are a few specific entities; e.g. average treatment effect or population mean

- as the estimand is a primary entity of interest, it always comes with confidence intervals.

- assumptions on the data-generating process (DGP) are made. The estimands are parameters of this process. If DGP indeed corresponds to reality, high-accuracy forecasts can also be made.

For (typical) machine learning problems:

- accuracy on the test set is the key metric (although concepts like cross-validation are needed)

- the estimands are the actual predictions; $g(x_0), \cdots ,g(x_n)$. $g$ is then judged based on some aggregation of these individual estimates.

- a rigorous and calibrated confidence interval is often not available. Even the accuracy metric is usually reported without CIs in the ML community.

- For most real-world learning problems, the space of DGP is too large and complex to be modelled. A lot of algorithms instead focus on learning the decision boundary.

That’s it, folks. Hope you enjoyed it as well. I'd be interested in knowing if you have a different viewpoint than the I discussed here.