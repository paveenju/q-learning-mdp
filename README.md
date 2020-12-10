# Training Q-learning agent in an MDP environment
This work is based on [this example](https://www.mathworks.com/help/reinforcement-learning/ug/train-reinforcement-learning-agent-in-mdp-environment.html) from [mathworks.com](https://www.mathworks.com). Please enjoy attached python notebook in this repository to understand how to train Q-learning agent in a generic Markov Decision Process (MDP) environment.

To have better understanding in this work, I introduce sections as follows:
- [Reinforcement learning](#reinforcement-learning)
- [Problem modeling with MDP](#problem-modeling-with-mdp)
- [Exploration vs Exploitation](#exploration-vs-exploitation)
- [Q-learning](#q-learning)
- [Parameters](#parameters)
- [Results](#results)

## Reinforcement learning
<p align="center" width="100%">
<img width="50%" src="https://dzone.com/storage/temp/6976061-screen-shot-2017-10-20-at-22200-pm.png">
</p>
<p align="center" width="100%">Reinforcement learning framework</p>
The reinforcement learning approach selects actions that maximize expected rewards generated by decisions. The agent learns how to choose actions through trial-and-error interactions with a dynamic environment to observe the signals or rewards returned from previous states. The agent may take a long sequence of actions to have a delayed rewards, receiving insignificant reinforcement, then finally arrive at a state with high reinforcement.

## Problem modeling with MDP
Assume that the environment of the problem is fully observable. Precisely, we can get all informations concerning all states (from begin to termianl states) and all state-to-state transitions. Therefore, we can formulate a generic MDP model. An example MDP can be represented as the following graph:
<p align="center" width="100%">
<img width="50%" src="RLGenericMDPExample.png">
</p>
<p align="center" width="100%">MDP Environment</p>
From this example, at each state there is a decision to go up or down. The agent begins from state 1. The state 7 and 8 are terminal states. The agent receives a reward equal to the value on each transition in the graph.

## Q-learning
In this work, we apply the Q-learning agent to train this MDP environment and solve the problem. The training goal is to collect the maximum cumulative reward. The algorithm has a function that calculates the quality of a state-action combination:

![Q:S\times{A}\rightarrow\mathbb{R}](https://latex.codecogs.com/svg.latex?Q:S\times{A}\rightarrow\mathbb{R})

To iteratively improve the behavior of the learning agent, at each time ![t](https://latex.codecogs.com/svg.latex?t) the agent selects an action ![a_t](https://latex.codecogs.com/svg.latex?a_t), observes a reward ![r_t](https://latex.codecogs.com/svg.latex?r_t), enters a new state ![s_{t+1}](https://latex.codecogs.com/svg.latex?s_{t+1}) and a new ![Q](https://latex.codecogs.com/svg.latex?Q) is updated with the following equation:

![Q(s',a)\gets(1-\alpha)\cdotQ(s,a)+\alpha\cdot(r+\gamma\cdot\max_{a'}Q(s',a'))](https://latex.codecogs.com/svg.latex?Q(s_t,a_t)\gets(1-\alpha)\cdot{Q(s_t,a_t)}+\alpha\cdot(r+\gamma\cdot\max_{a}{Q(s_{t+1},a)))

where
![s_t](https://latex.codecogs.com/svg.latex?s_t) : current state of the agent.<br>
![a_t](https://latex.codecogs.com/svg.latex?a_t) : current action picked according to some policy.<br>
![s_{t+1}](https://latex.codecogs.com/svg.latex?s_{t+1}) : next state where the agent ends up.<br>
![a_t](https://latex.codecogs.com/svg.latex?a): next best action to be picked using current Q-value estimation, i.e. pick the action with the maximum Q-value in the next state.<br>
![r_t](https://latex.codecogs.com/svg.latex?r_t) : current reward observed from the environment in response of current action.<br>
![\alpha](https://latex.codecogs.com/svg.latex?\alpha) : discounting Factor for Future Rewards and ![0<\alpha\le1](https://latex.codecogs.com/svg.latex?0<\alpha\le1).<br>
![\gamma](https://latex.codecogs.com/svg.latex?\gamma) : learning rate or step length taken to update the estimation of ![Q(s,a)](https://latex.codecogs.com/svg.latex?Q(s,a)).

Note that future rewards are less valuable than current rewards so they must be discounted. Since Q-value is an estimation of expected rewards from a state, discounting rule applies here as well.

## Exploration vs Exploitation
We select the action to take using 𝜖 -greedy policy. ![\epsilon](https://latex.codecogs.com/svg.latex?\epsilon)-greedy policy of is a simple policy of selecting actions using the current Q-value estimations. It goes as follows:

- with probability (![1-\epsilon](https://latex.codecogs.com/svg.latex?1-\epsilon)) select the action which has the highest Q-value.<br>
- with probability (![\epsilon](https://latex.codecogs.com/svg.latex?\epsilon)) randomly select any action.<br>

## Parameters
### Q-learning agent parameters
To create Q-learning agent, the discount factor, learning rate and epsilon-greedy exploration shall be configured as follows:
|Parameter   |Value   |
|---|--:|
|Discount factor, ![\alpha](https://latex.codecogs.com/svg.latex?\alpha) | 1.0 |
|Learning rate, ![\gamma](https://latex.codecogs.com/svg.latex?\gamma)   | 1.0 |
|Epsilon, ![\epsilon](https://latex.codecogs.com/svg.latex?\epsilon)     | 0.9 |
|Epsilon decay, ![\epsilon_{decay}](https://latex.codecogs.com/svg.latex?\epsilon_{decay})     | 0.01 |
|Final Epsilon, ![\epsilon_{final}](https://latex.codecogs.com/svg.latex?\epsilon_{final})     | 0.01 |

### Training parameters
To train the agent, number of steps, episodes, criteria to stop training and reward averaging window size  are configured as follows:
|Parameter   |Value/criteria   |
|---|--:|
|Maximum steps per episode                                                                     | 50   |
|Maximum episodes                                                                              | 200  |
|Stop training criteria                                                                        | ![r_{avg}<13](https://latex.codecogs.com/svg.latex?r_{avg}<13)|
|Reward averaging window size                                                                  | 30   |

## Results

![Results](q_agent_mdp.png)
