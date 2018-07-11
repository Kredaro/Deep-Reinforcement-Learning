# Agents and Environment Part 1: Nature of Environment

We have seen a drastic increase in the demand for Artificial Intelligence and
Machine Learning. But before we dive into this magnificent field, let us learn
about what an agent is, and the basic designs of an agent, corresponding to its
environment. Then we will learn some of the popular search algorithms, classical
and adversarial.

This is the first of the series of blogs that is intended to give a general idea
on the popular search algorithms. These blogs will have a striking similarity
with the book “Artificial Intelligence: A Modern Approach”. In fact, this series
can be seen as a shorthand version of the book.

## Agent

An **agent** is anything which can perceive its environment through **sensors**
and acts upon that environment through **actuators**. The agent analyses the
complete history of its percepts using an **agent function** (or an **agent
program**), that maps the sequence of percepts to an action.

Now let us consider a simple case of a vacuum cleaning agent. There are 2 tiles:
Tile A and Tile B. The pile of dust could be on any, on both or on neither of
the two tiles. Your vacuum cleaner is on one of the tiles, and it can sense and
clean only one tile at a time. The cleaner could move left, move right, or clean
the tile it rests on.

![](https://cdn-images-1.medium.com/max/1600/0*6KFwkRH_OQxO62st)
<span class="figcaption_hack"></span>

Figure 1: The vacuum cleaner with two locations

The percept sequence consist of the history of percepts the vacuum cleaner
senses, and the agent function maps each percept of the sequence to an action.
The agent function for this vacuum cleaning agent is:

Agent function = {([A: Clean], Right), ([A: Dirty], Clean), ([B: Clean], Left),
([B: Dirty], Clean), ([A: Clean, B: Clean], Stop), ([A: Clean, B: Dirty],
Clean), …}

We need a metric or a rule to measure the performance of the agent in the
environment. For example, in this case, we measure the performance of the agent
as the number of *desirable* actions performed by the agent. If we had designed
another agent with a different agent function than the one mentioned above, it
might perform undesirable actions, and so its **performance measure** would be
low.

Now we have a general idea of what an agent is, let us discuss on the nature of
the environment on which an agent acts.

## Nature of environment

We need to analyze the task environment, which are the “problems” for which the
agents are the “solutions”. Some of the common features of the environment needs
to be understood, for they determine the appropriate agent design required.

### Fully Observable vs Partially Observable

If we can capture the complete state of the environment *relevant to the choice
of action* of the agent using the its sensors, then the environment is fully
observable. If the environment is not fully observable, then it needs to
maintain an internal state to keep track of the world.

The environment could be partially observable not just because of the noise or
the inaccuracy of the sensors, but could be due to the framework of the task
itself. For example, the classic game of **Chess** is fully observable as one
agent can perceive the positions and the moves of the other agent. But in the
**Kriegspiel** version of chess, the game environment is partially observable
(it is unobservable except for the invalid moves).

### Single agent vs Multi agent

In our discussions above, we have talked about two kinds of agents: a vacuum
cleaning agent and a chess engine. The vacuum cleaning environment is single
agent while chess is a two agent environment. We need to define what entities
must be viewed as agents with respect to a task environment.

If the performance measure of agent B depends on the action performed by agent
A, then the environment is said to have two agents. In chess, the ‘optimal’ move
of one agent, by rule, reduces the performance measure for the other agent, and
so it is said to be a **competitive** environment. Consider a case of two
taxi-driving agents. Here, avoiding collisions maximizes the performance of both
the agents, and so it is a **cooperative** environment.

### Deterministic vs Stochastic

If the next state is completely determined by the current action of the agent,
then the environment is deterministic. The vacuum world described above is a
deterministic one, while the game of ludo and backgammon is stochastic (the dice
will generate the uncertainty in the environment). We could consider the game of
chess as a deterministic environment though there can be uncertainty due to the
other agent in the game, because we could still determine the state of the game
to an extent by estimating the other agent’s moves.

Most real-life situations are so complex that we cannot keep track of all the
unobserved aspects, and must be treated as stochastic.

### Static vs Dynamic

If the environment can change while the agent is performing an action, then the
environment is dynamic for that agent; otherwise it is static. Agents in static
environments does not need to worry about the state of the environment during
the action, and so the environments are easy to deal with. Taxi driving is
dynamic, as the other cars keep moving while the agent is deciding for an
action. Chess is static.

### Discrete vs Continuous

The discrete/continuous distinction applies to the state of the environment, to
the way time is handled, and to the percepts and actions of the agent. For
example, the chess environment has a finite number of distinct states and has a
discrete set of percepts and actions. Taxi driving is a continuous-state and
continuous-time problem, and the corresponding actions are also continuous.

### Summary

We have discussed briefly what an agent is, and how the nature of environment
brings the variety factor in the agents. The design of the agents is relatively
easy for a fully observable, deterministic, static, discrete task environment
than for a partially observable, stochastic, dynamic, continuous task, and this
is the reason for the difference in the complexity of the vacuum cleaning agent
(mentioned above) and a taxi driving agent.

In the next blog, we will discuss on the design and structure of the agents, and
a brief note on learning agents.
