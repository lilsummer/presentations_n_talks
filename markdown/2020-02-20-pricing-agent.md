---
layout: post
image: images/pricechart.png
title: A draft implementation of pricing agent in DRL
sitemap: false
permalink: projects/drl
# All dates must be YYYY-MM-DD format!
date: 2020-02-20
# labels:
#   - Deep reinforcement learning
#   - OpenAI gym
#   - python
#   - stable baseline
# summary: A draft implementation for a smart pricing agent based on real-world data
---
<p align="center"><img src="../images/slotmachine.jpg"></p>

#### Tech stack: deep reinforcement learning, openAI gym, stable baseline


Deep reinforcement learning (DRL) is a pivotal point for AI, in that it equips machines with **self-exploration** (Figure 1) ability rather than simply learning from data. OpenAI Gym has provided a simple configurable framework for us to build a prototype of pricing agent. Such agents need to have the following requirements:

* Being able to make decisions over a series of sales period;
* Allowing learning from recent decisions on the market;
* Allowing explorative behavior in pricing strategies;
* Considering long-term advantages; since short-term pricing may not benefit the utility of customers in the long run.

Considering the substantial landscape of different types of RL models, we need to narrow down what we need based on our assumptions. In this case, we choose **model-free and fully-observable environment**. We can thinking of a pricing robot that can intereact with the market, i.e. make decisions on how to price the products for the next sale period (the environment can also be partially observable in that usually we have no knowledge about its competitors, and the true demand of the market). 

To create a pricing environment, we have 1). Approximate the data based on real-world senario 2). Custom functions in the Gym framework, this includes:

* `_init__()`
Initialize the agent with baseline conditions

* `_next_observation()`
Get the observation space based on the current step. The observation can be from the previous x steps.

 
* `_take_action()`
Based on the action decided by the policy, take the actions to change the environment. Changed price lead to changed demand, changed revenue, and everything else in the environment.


* `Step()`
Take an incremental step, update the reward function and check the criteria for the completion of the epoch.

 
* `Reset()`
Reset the state variable so that it is ready for another new epoch.

Except for these functions, we will have to define action space and observation space. We experimented with proximal policy optimization (**PPO**)[https://arxiv.org/abs/1707.06347], A2C (**A synchronous, deterministic variant of Asynchronous Advantage Actor Critic**)[https://arxiv.org/abs/1602.01783] and Actor Critic using Kronecker-Factored Trust Region (**ACKTR**)[https://arxiv.org/abs/1708.05144] using stable_baseline library.

Interestingly, we found that under PPO2, agents tend to have more risk-adverse pricing strategy compared with other algorithms.

