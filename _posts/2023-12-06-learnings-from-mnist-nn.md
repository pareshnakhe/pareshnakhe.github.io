---
title: "Learnings from coding MNIST NN from Scratch"
classes: wide
---

{% include figure image_path="/assets/images/mnist_scratch/mika_unsplash.jpg" alt="titleimage" caption="Photo by <a href="https://unsplash.com/@mbaumi?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Mika Baumeister</a> on <a href="https://unsplash.com/photos/white-printing-paper-with-numbers-Wpnoqo2plFA?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>" %}

I recently decided to implement a neural network to classify handwritten digits using the MNIST dataset. Not with the goal of climbing the leaderboard in some data science competition but to look closely at the building blocks of the AI systems we are all surrounded by. I wanted to work through the details once myself to get a sense of some of the challenges ML scientists might be facing. 

I am also writing this for my future self to continue building on the modest beginnings I have undertaken here. Without further ado, here are my main learnings:

- **Sigmoid is not a good activation function**
  - For a sigmoid neuron with a large number of incoming links (which is often the case), the gradient tends very quickly to zero. When optimizing a function with thousands of dimensions, sigmoid just doesn't make the cut. The code I have presented below actually gets stuck in an efficient local minimum rather quickly.
  - The fact that the output is between 0 and 1 works well (in some cases) for the last layer. But for intermediate layers, it just leads to slow learning (see notes below for justification)
  - It is very susceptible to numerical overflow

- Google, Apple and Microsoft have jumped into the fray of creating their own "AI" chips. A simple feedforward network certainly does not compare with the generative AI magic we are seeing, but I do have a better appreciation for why technology giants are betting so much on improved hardware. My implementation of a simple feed-froward network in Python, (optimized a tiny little bit using JAX) takes annoyingly long to converge (somewhat). **Getting the theory and concepts right is not enough. (In addition to good hardware) you need a strong engineering mindset if want to apply these models in industrial settings.**

- **JAX is awesome** but has a pretty steep learning cure and has a lot of sharp edges. I was able to achieve a tremendous speed up on CPU just replacing a few frequently used functions with JAX equivalents. And I love easy they have made auto differentiation. *But* I spent hours fixing crypic errors thrown by JAX (who knew you can't use jit decorator for class methds!) All in all, I think JAX requires a lot of time investment before you truly (and correctly) unleash its try potential.

In this exercise, however, I still couldn't completely get a hang of somethings like how to best debug the model. It's easy when the code throws an error. But there were times when I was getting either rubbish or Nulls being outputed as loss and didn't know where to start. Also, hyperparameter initialization, like gradient step size, number of layers etc. I think I found something by trial and error, but the whole topic feels like black magic to me.

<script src="https://gist.github.com/pareshnakhe/44173c35388c43477aa016a57ccdd874.js"></script>

The entire code I used can be found [here](https://github.com/pareshnakhe/SundayAfternoonProjects/tree/master/mnist)