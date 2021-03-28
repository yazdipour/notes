# AI

## Reinforcement Learning

The goal of reinforcement learning is for an agent to learn how to evolve in an environment.

### Markov decision processes

MDP is a 5-tuple (S,A,P_sa,γ,R)

- S is the set of states
- A is the set of actions
- {P_sa} are the state transition probabilities for s∈S and a∈A
- γ∈[0,1] is the discount factor
- R:S×A⟶R or R:S⟶R is the reward function that the algorithm wants to maximize

### Policy

A policy π is a function :SAπ:S⟶A that maps states to actions.

Remark: we say that we execute a given policy π if given a state ss we take the action a=(s)a=π(s).
