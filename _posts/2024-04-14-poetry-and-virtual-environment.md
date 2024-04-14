---
title: "Poetry and Virtual Environment"
classes: wide
---

{% include figure image_path="/assets/images/mnist_scratch/mika-unsplash.jpg" alt="titleimage" caption="Photo by Mika Baumeister on Unsplash" %}

I learnt something interesting today: `poetry`. I am writing this post primarily to verbalize my understanding and having a record of it that I can come back to at a future point. It deals with the advantages it can bring in your workflow and does not go into specific details.

Poetry is a **dependency management** and **packaging tool** in Python. These are two things I don't really pay explicit attention to, primarily since I spend most of my time in notebook environments. (I've been trying to change that for a while now but the notebook environment is just so... easy.) Nevertheless, lately I've been focusing on the *tooling* around the Data Science work. In this post, I'll focus on *some* aspects poetry.

Let me start by posing a question: How do ensure that the piece of code you write is exactly reproducible irrespective of the enviroment where it is run? A common practice is the use of virtual environments. When you start or clone a new project, you create a new virtual environment and *try* to be disciplined about what we install or uninstall in this virtual environment. Often times, we use the same environment for multiple projects and thereby recreating the problems virtual environment were meant to solve i.e. an environment dedicated to a project. Even when you do maintain this discipline, how do you track the additions and removals of several libraries during development?

`poetry` addresses this question by using a very "containerized" approach to virtual environments, in that we can specify what the environment should look like but no directly access it. Instead of the developer managing the virtual environment this task is pushed within the domain of poetry. It allows interfaces to add and remove dependencies, run tests and scripts in this hidden environment. As a result, when somebody else clones this project and runs `poetry install`, a new virtual environment with the exact same specifications is created (by poetry) for them ensuring that code runs the way it should. On my Mac OS, this environment was created in `/Users/pnakhe/Library/Caches/pypoetry/virtualenvs`. This is really quite powerful and amazing!

**What if you use poetry within a virtual environment?**

This what I did first (being used to manage an environment myself for each project). In this case, poetry relinquishes the task of environment management and uses the user-specified environment to install and run tests/scripts.

> Poetry will detect and respect an existing virtual environment that has been externally activated. This is a powerful mechanism that is intended to be an alternative to Poetry’s built-in, simplified environment management.
>
> To take advantage of this, simply activate a virtual environment using your preferred method or tooling, before running any Poetry commands that expect to manipulate an environment.

That's all for this post.