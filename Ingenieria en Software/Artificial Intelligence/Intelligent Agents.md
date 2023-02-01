An agent is anything that can be viewed as perceiving its environment through sensors and Sensor acting upon that environment through actuators.

![[Pasted image 20230201163828.png|500]]


## Rational Agent

For each possible percept sequence, a rational agent should select an action that is expected to maximize its performance measure, given the evidence provided by the percept sequence (order of percepts) and whatever built-in knowledge the agent has.


## Simple Reflex Agent

These agents select actions on the basis Simple reflex agent of the current percept, ignoring the rest of the percept history. Meaning the do things by inertia more than decisions. This is the schematic of a simple reflex agent. It acts upon a condition-action rule, meaning, if x then y.

![[Pasted image 20230201174628.png|500]]

## Model-based reflex agents

That is, the agent should maintain some sort of internal state that depends on the percept history and thereby reflects at least some of the unobserved Internal state aspects of the current state. 

![[Pasted image 20230201175928.png|500]]

## Goal-based agents

The agent program can combine this with the model (the same information as was used in the model-based reflex agent) to choose actions that achieve the goal. Where the goal is the objective of the model.

![[Pasted image 20230201180139.png|500]]

## Utility-based agents
An agent’s utility function is essentially an internalization of the performance measure. Provided that the internal utility function and the external performance measure are in agreement, an agent that chooses actions to maximize its utility will be rational according to the external performance measure. Specifies the tradeoffs that can be done between multiple goals

![[Pasted image 20230201181035.png|500]]

## Learning agents

