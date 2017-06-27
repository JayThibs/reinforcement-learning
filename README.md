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



