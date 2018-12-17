# PPO-clip-and-PPO-penalty-on-Atari-Domain

![](https://img.shields.io/badge/language-python-blue.svg) 
![](https://img.shields.io/badge/license-MIT-000000.svg)
![](https://codebeat.co/webhooks/github/pull_requests/94a77fb4-b070-4c07-a6a8-8294f90a5b36)

<div align=center>
<img src="image/1.gif" width=400 >
<div align=left>
	
## Overview
This repo is based on [spinningup](https://github.com/openai/spinningup), sincerely grateful to it.

I do these things:
- Implement PPO-penalty. You will find that neither [spinningup](https://github.com/openai/spinningup) nor [baseline](https://github.com/openai/baselines) implements PPO-penalty.  Although PPO-penalty results are not as good as PPO-clip, this algorithm is meaningful as a good baseline.
- Implement PPO algorithm on Atari domain(if you read spinningup carefully, or run the program, you will find the program don't match the Atari domain. Because the input vector isn't flattened.)


Advantage
- This may be the only open source of PPO-penalty
- This program is very easy to configure.
- This code is readable, more readable than baseline, and more suitable for beginners.

References
- [Proximal Policy Optimization Algorithms](https://arxiv.org/abs/1707.06347), Schulman et al. 2017
- [Emergence of Locomotion Behaviours in Rich Environments](https://arxiv.org/abs/1707.02286),  Heess et al. 2017 
- [High Dimensional Continuous Control Using Generalized Advantage Estimation](https://arxiv.org/abs/1506.02438), Schulman et al. 2016

Blog
- my [blog](https://blog.csdn.net/weixin_41679411/article/details/82421121) on PPO
- [mpi4py blog](https://www.jianshu.com/p/505ab84fe725)

## Backgroud

PPO is motivated by the same question as TRPO: how can we take the biggest possible improvement step on a policy using the data we currently have, without stepping so far that we accidentally cause performance collapse? Where TRPO tries to solve this problem with a complex second-order method, PPO is a family of first-order methods that use a few other tricks to keep new policies close to old. PPO methods are significantly simpler to implement, and empirically seem to perform at least as well as TRPO.

There are two primary variants of PPO: PPO-Penalty and PPO-Clip.

PPO-Penalty approximately solves a KL-constrained update like TRPO, but penalizes the KL-divergence in the objective function instead of making it a hard constraint, and automatically adjusts the penalty coefficient over the course of training so that it's scaled appropriately.

PPO-Clip doesn't have a KL-divergence term in the objective and doesn't have a constraint at all. Instead relies on specialized clipping in the objective function to remove incentives for the new policy to get far from the old policy.

Here, we'll focus only on PPO-Clip (the primary variant used at OpenAI).

## Quick Facts
- PPO is an on-policy algorithm.
- PPO can be used for environments with either discrete or continuous action spaces.
- The Spinning Up implementation of PPO supports parallelization with MPI.

## Installation Dependencies

- cloudpickle==0.5.2
- gym>=0.10.8
- matplotlib
- numpy
- pandas
- scipy
- tensorflow>=1.8.0
- tqdm

## How to Install
```
	conda install tensorflow
	conda install gym
	conda install numpy 
```
mpi4py install on unix [click here](https://www.jianshu.com/p/ba6f7c9415a0)
mpi4py on windows [click here](https://blog.csdn.net/mengmengz07/article/details/70163140)

## How to Run
- Quick start
```
	python ppo.py
```
- Play with parallel (-np:set number of processings, take care of OOM!)
```
	mpiexec -np 4 python ppo.py
```
## Algorithm
The detail of PPO is the same as the original paper. you can have a look at my [bolg](https://mp.csdn.net/mdeditor/82421121#) to know the details. 
Pseudo-code is shown below.
	
<div align=center>
<img src="https://img-blog.csdnimg.cn/20181217211105351.png" width=50% height=50% div align="center" /> 
<div align=left>

PPO-clip and PPO-penalty's objective functions are below:
	
<div align=center>
<img src="https://img-blog.csdnimg.cn/20181217211547501.jpg" width=50% height=50% div align="center" /> 
<div align=left>

<div align=center>
<img src="https://img-blog.csdnimg.cn/20181217211610509.jpg" width=50% height=50% div align="center" /> 
<div align=left>

## Details
Most settings are the same with PPO, details as follow :
- Network Structure
    we used a fully-connected MLP with two hidden layers of 64 units,
and tanh nonlinearities, outputting the mean of a Gaussian distribution, with variable standard
deviations, following [Sch+15b; Dua+16]. We don’t share parameters between the policy and value
function (so coefficient c1 is irrelevant), and we don’t use an entropy bonus.

- Parameters in Detail

	Parameters on Mujoco and Atari
	
<div align=center>
<img src="https://img-blog.csdnimg.cn/20181217212830756.png" width=50% height=50% div align="center" /> 
<div align=left>

<div align=center>
<img src="https://img-blog.csdnimg.cn/20181217212928214.png" width=42% height=42% div align="center" /> 
<div align=left>

## References
- [Proximal Policy Optimization Algorithms](https://arxiv.org/abs/1707.06347), Schulman et al. 2017
- [Emergence of Locomotion Behaviours in Rich Environments](https://arxiv.org/abs/1707.02286),  Heess et al. 2017 
- [High Dimensional Continuous Control Using Generalized Advantage Estimation](https://arxiv.org/abs/1506.02438), Schulman et al. 2016





