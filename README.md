# Reinforcement Learning

Contains notes from reinforcement learning courses, books, and online guides.

Reinforcement Learning is a concept of the same type as supervised and unsupervised learning. 

* In RL, there is no supervisor, only a reward signal (that was worth 3 points, that takes away 2 points, etc).  
* The feedback is delayed and not instantaneous. You might only see the effects of the reward signal further on.
* Time really matters in RL. We've got a dynamic system that depends on what the agent (ex: robot) sees at a given time since the next step will be correlated with the current step. The data is sequential.
* Agent's actions affect the subsequent data it receives. So if a robot is walking to one area of a room and then another area, both areas will give the robot different types of data. It's an active learning process that makes use of a combined set of differences that defines the RL paradigm.

## Examples of Reinforcement Learning

* Fly stunt manoeuvres in a helicopter
* Defeat the world champion at Backgammon Manage an investment portfolio
* Control a power station
* Make a humanoid robot walk
* Play many different Atari games better than humans
* Making a drone learn not to hit into things using computer vision to determine whether it is too close to a wall and needs to turn arround or it can continue moving in its current direction.

## Rewards

A reward Rt is a scalar feeback signal. It indicates how well the agent is doing at timestep t. The agent's job is to maximise cumulative reward.

Reinforcement learning is based on the reward hypothesis which is defined by:

> All goals can be described by the maximisation of expected cumulative reward.

## Examples of Rewards

* Fly stunt manoeuvres in a helicopter
⋅⋅* +ve reward for following desired trajectory 
⋅⋅* −ve reward for crashing
* Defeat the world champion at Backgammon 
⋅⋅* +/−ve reward for winning/losing a game
* Manage an investment portfolio 
⋅⋅* +ve reward for each $ in bank
* Control a power station
⋅⋅* +ve reward for producing power
⋅⋅* −ve reward for exceeding safety thresholds
* Make a humanoid robot walk +ve reward for forward motion 
⋅⋅* −ve reward for falling over
* Play many different Atari games better than humans 
⋅⋅* +/−ve reward for increasing/decreasing score
* Flying a drone that avoids hitting objects
⋅⋅* +ve reward for avoiding hitting object
⋅⋅* −ve reward for crashing into object

## Agent and Environment

At each timestep tn the agent:

* Excecutes action A_t
* Receives observation O_t
* Receives scalar reward R_t

At each timestep tn the agent:

* Receives action A_t
* Emits observation O_(t+1)
* Emits scalar reward R_(t+1)

## History and State

The history is the sequence of observations, actions, rewards:

> Ht = O1,R1,A1,...,At−1,Ot,Rt

We could use the history to determine what the agent should do next, but that could be very costly (especially if our history is a video for example). Since we want to reduce the amount of time taken to make a decision, we will use a State to make a decision.

> State is the information used to determine what happens next. It is a function of the history and helps the agent make a decision much quicker than if it used the history to make a decision. The state summarizes the history.

If we can capture the history and summarize it in a state, we can much more easily do things with it. 

We will be talking about three different definitions of state: Environment, Agent and Information (Markov).

## Environment State

The environment state is the information used with the environment to determine what to do next. In other words, a set of numbers that determines what to do next.

The environment state is the environment’s private representation i.e. whatever data the environment uses to pick the next observation/reward. The environment state is not visible to the agent.

Our algorithms only see the observation coming in and the reward, it does not see the environment which is intrinsic of the system. So, the Environment State doesn’t really tell us anything useful when we are building our algorithms. That’s why we turn to the Agent State to build our models.

## Agent State

The Agent State is the set of numbers that lives inside our algorithm. Whatever information that we choose to store and capture for our agent is what we call the agent state, which is our decision. Therefore, it’s the information used by the agent to pick the next action, the information used by reinforcement learning algorithms. It can be any function of the history.

The agent state is the agent’s internal representation.

## Information State (a.k.a. Markov State)

A Markov State contains all useful information from the history.

The Markov property essentially says that you only need the present state S_t to predict the future S_(t+1). This is only the case when you have a Markov State because, like we said, it contains all useful information of the history. In other words, the future is independent of the past given the present. So, once the state is known, we can throw away the history i.e. the state is a sufficient statistic of the future.

For example, if we’re looking at a helicopter doing tricks, if we have all the information of the present (speed, angular momentum, wind velocity, etc.), then we don’t need to know what the wind velocity or speed was ten minutes ago to know what will happen next.

In contrast, let’s say we have an imperfect state where we only have the position and not the velocity, we’ll have to look back in time to determine the velocity at the present time in order to make the prediction.

The environment state is Markov. The environment state fully characterizes what will happen in the environment so by definition it is Markov.

The history H_t is also Markov.

These two states show that it is always possible to have a Markov state.

## Fully observable environments

This is the best case scenario where we get to see everything i.e.  agent directly observes environment state. Therefore, the agent state is equal to the environment state and information state. The agent gets to see what’s going on in the environment state and gets to work with those numbers. Formally, this is a Markov decision process (MDP), which we will go into detail later.

## Partially Observable Environments

Partial observability: agent indirectly observes environment:

* A robot with camera vision isn’t told its absolute location
* A trading agent only observes current prices (might not know the trends or where the prices are coming from)
* A poker playing agent only observes public cards (the cards which are face up on the table)

In this environment, the agent state is not equal to the environment state.

Formally, this is a partially observable Markov decision process (POMDP).

The agent must construct its own state representation by either

* Taking the complete history
* Building beliefs of environment state (a probabilistic/Bayesian approach), keeping a probability distribution about where you are in the environment since you are not certain. It’s a vector of probabilities.
* Using a Recurrent Neural Network

## Major Components of an RL Agent

An RL agent may include one or more of these components (these are the main ones):

* Policy: agent’s behaviour function, how the agent picks its actions. A policy is the agent’s behaviour that maps the state and action through either a deterministic policy or stochastic policy.
* Value function: how good is each state and/or action, how much reward do we expect to get if we take a particular action in a particular state? The value function is a prediction of future reward used to evaluate the goodness/badness of states to select between actions.
* Model: agent’s representation of the environment. A model predicts what the environment will do next using Transitions and Rewards. Transitions P predicts of the next state, predicting the dynamics of the environment. Rewards R predicts the next (immediate) reward. It is not the actual environment (reality), but the agent’s model of the environment (reality).

We can categorize our RL agents in the following ways:

* Value Based: where the policy is implicit and the agent only looks at the value function
* Policy based: where the agent only relies on the policy and does not create any value function
* Actor Critic: stores the policy and the reward it’s getting from each state (value function)

We can also use the Model Free approach where we go directly to the policy or value function by seeing experience and figure out our policy or how to behave to get the most reward without having to do the indirect step of figuring out how the environment works.

We can also do model based reinforcement learning by, for example, building our dynamics model of our helicopter and then we plan with it (look to see what would happen if we look ahead to figure out the optimal way to behave.)

## Learning and Planning

There are two fundamental problems in sequential decision making:

Reinforcement Learning: The environment is initially unknown to the agent, the agent interacts with the environment to improve its policy and/or getting the most possible reward. Ex: putting a robot in an environment and have the robot figure things our for itself (not telling it the wind velocity, etc.). Ex: nobody tells the agent how the game works.

Planning: In this case we tell it all the rules of the game, we give it a model of the environment (giving it the differential equations describing the wind, for example.) Instead of interacting with the environment, it is now doing internal computations with its model. It doesn’t actually have to interact in the real word, it’s planning. As a result, the agent improves its policy. You can use something like a tree search to figure out what will give you the most reward by looking at all the possible states. Ex: we tell the agent how the game works. 

## Exploration and Exploitation

Reinforcement learning is like trial-and-error learning. The problem with doing that is that we might be losing reward along the way, so we need to have a balance between exploration and exploitation.

Exploration finds more information about the environment. In other words, it’s choosing the give up a reward you know about in order to find out more about the environment. Ex: on the left there are ten +1 rewards, but on the right there is one +20 reward at the very end. It would be worth it to explore the right in this case, but you won’t know it until you explore that side. If the agent doesn’t explore enough, it might think that the left is the ideal when it isn’t.

Exploitation exploits known information to maximize the reward. Ex: if we only used exploitation, the agent would only go left since it knows it has rewards there immediately.

Clearly, we need to balance exploration and exploitation to achieve the best results. It could be that the right has no reward and putting emphasis on exploring only lowers our chances of a maximum reward.

## Prediction and Control

Prediction: evaluate the future. How well will I do if I follow my current policy?

Control: optimise the future. Which policy is the best? Which policy should I follow to get the most reward?

What happens in RL is that we need to do is to evaluate all of our policies (prediction) in order to solve the control problem.
