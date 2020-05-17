# Deep Reinforcement Learning Nanodegree
# Project 1: Navigation

This repository includes the code to train two agents collaborating to solve the Tenis environment.

The agent algorithm is a DDPG, following the vanilla algorithm presented in the original [paper](https://arxiv.org/abs/1509.02971) and the improvements suggested in the Nanodegree lesson.

Most of the algorithm is the DDPG offered to solve the [pendulum environment](https://github.com/udacity/deep-reinforcement-learning/tree/master/ddpg-pendulum). The main differes are:
* Use 20 agents at the same time
* Use gradient clipping when training the critic network
* Update the networks 10 times after every 20 timesteps.
* Modify some hyperparameters:
 * BUFFER_SIZE = int(1e6)  # replay buffer size
 * BATCH_SIZE = 64         # minibatch size
 * GAMMA = 0.99            # discount factor
 * TAU = 1e-3              # for soft update of target parameters
 * LR_ACTOR = 1e-3         # learning rate of the actor
 * LR_CRITIC = 1e-4        # learning rate of the critic
 * WEIGHT_DECAY = 0        # L2 weight decay

The actor is a linear network with 400 and 300 units for the hidden layer. Input size is the state size and output the action size. Activation is relu but for the output layer, were I used tanh.
Similarly, the critic is also linear with 400 and 400 300 units for the hidden layer, but the second layer gets as input the output of the first one and the action. Also, there is no activation for the output layer.

In both cases, batch normalization was applied to the output of the first layer.


The agent solved the environment 1699 episodes (average of the max scores of 0.51), with the following evolution

![Agent evolution](scores.png)


### Future work

There's a lot that can be done here!

I tried the same algorithms as in the previous project and they work out of the box. The main problems with this approach is that agents don't really collaborate.

I would like to implement another algorithms that exploit this problem, such as MADDPG. Then I would like to test how some improvements affect the results, such as a better noise algorithm or a prioritized replay buffer.
