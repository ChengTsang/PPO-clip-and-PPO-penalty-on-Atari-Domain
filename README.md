## Overview
This repo is based on [spinningup](https://github.com/openai/spinningup), sincerely grateful to it.

I do these things:
- Implement PPO-penalty. You will find that neither [spinningup](https://github.com/openai/spinningup) nor [baseline](https://github.com/openai/baselines) only implements PPO-penalty.  Although PPO-penalty results are not as good as PPO-clip, this algorithm is meaningful as a good baseline.
- Implement PPO algorithm on Atari domain(if you read spinningup carefully, or run the program, you will find the program don't match the Atari domain. Because the input vector isn't flattened.)


Strength
- This is the only open source of PPO-penalty
- This program is very easy to configure.
- This code is readable, more readable than baseline, and more suitable for beginners.

References
- [Proximal Policy Optimization Algorithms](https://arxiv.org/abs/1707.06347)
- [Emergence of Locomotion Behaviours in Rich Environments](https://arxiv.org/abs/1707.02286)

Blog
- my blog on PPO
- [mpi4py blog](https://www.jianshu.com/p/505ab84fe725)

## Installation Dependencies

- python3
- tensorflow >= 1.8.0
- mpi4py(parallel train and play)
- gym

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
<center>
<img src="https://img-blog.csdnimg.cn/20181217211105351.png?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTY3OTQxMQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="75%" height="75%" />

PPO-clip and PPO-penalty's objective functions are below:
<center>
<img src="https://img-blog.csdnimg.cn/20181217211547501.jpg?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTY3OTQxMQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="75%" height="75%" />

<center>
<img src="https://img-blog.csdnimg.cn/20181217211610509.jpg?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTY3OTQxMQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="75%" height="75%" />

## Details
Most settings are the same with PPO, details as follow :
- Network Structure
    we used a fully-connected MLP with two hidden layers of 64 units,
and tanh nonlinearities, outputting the mean of a Gaussian distribution, with variable standard
deviations, following [Sch+15b; Dua+16]. We don’t share parameters between the policy and value
function (so coefficient c1 is irrelevant), and we don’t use an entropy bonus.

- Parameters in Detail

	Parameters on Mujoco and Atari
<center>
<img src="https://img-blog.csdnimg.cn/20181217212830756.png?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTY3OTQxMQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="75%" height="75%" />

<center>
<img src="https://img-blog.csdnimg.cn/20181217212928214.png?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTY3OTQxMQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="60%" height="60%" />



