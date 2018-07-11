# Agents and Environment Part 2: Structure of Agents

In my previous blog post, I have discussed on the [Nature of
Environment](https://medium.com/@rithesh18.k/agents-and-environment-part-1-the-nature-of-the-environment-4faaec5ec5ca)
that determines the design of the agent. In this post, we will discuss about the
different kinds of agent programs and how to convert them into learning agents
that can improvise their agent function and generate better actions.

## Agent programs

The agent program takes in the current percept of the environment from the
sensors of the agent  and returns an action to be performed by the actuators. If
you need to depend on the entire percept sequence, the agent will have to
remember the percepts.

In a simple **Table-driven Agent**, a lookup table is used to match *every
possible* *percept sequence* to the corresponding action. It is the most
effective form of implementing the desired agent function, but it comes with a
penalty of occupying humongous amounts of space. Even for a small game of chess
requires 150th power of 10 entries in the lookup table, forget about the lookup
table for the taxi driving agent(for comparison, the number of atoms in the
observable universe is less than 80th power of 10). This huge requirement of
space means that: 1) There is not much space in the entire universe to store
this huge amount of data. 2) The designer will not have time to fill up the
table. 3) Even if you make a learning agent to fill the lookup table on itself,
it’ll take ages for it.

The key challenge of AI is to frame efficient agent programs that produce
rational behavior from a small program instead of a huge table. Is this
possible? Yes is what we believe.

Let us discuss four basic kinds of agent programs, used in almost all
intelligent systems:

### Simple reflex agents

This is the simplest kind of agent, where the actions are selected based on the
*current percepts*, ignoring the history of percepts. This is very efficient for
simple agents like the vacuum-cleaning agent discussed previously. A simple
**condition-action rule** governs the actions taken by the agent: 

**if** *condition,* **then** *action*

<span class="figcaption_hack">Figure 1: Schematic Diagram of the Simple Reflex agents</span>

Simple reflex agents are simple, but of limited intelligence. The agent will
work only if the action can be made on the basis of *only the current percept*,
and if the environment is *fully observable*. Suppose that the vacuum-cleaning
agent cannot sense its location and can only sense the dirt on the tile. Then
its percepts are [*Clean*] and [*Dirty*]. If *Dirty*, it can perform *Clean*
action, but if *Clean*, it doesn’t know which direction it needs to move, as it
doesn’t know where it currently is. It could try to perform a [*Left*] and
[*Right*] action, but it can end up in infinite loop easily (performing [*Left*]
in Tile A, or [*Right*] in Tile B). Infinite loops are often unavoidable in
simple reflex agents in a partially observable environment.

One remedy to avoid infinite loop is to randomize the actions. But in a
single-agent environment, randomization is not an optimal solution, as more time
will be wasted on doing undesirable actions, which lowers the performance of the
agent. The Model-based reflex agent offers a solution to this problem.

### Model-based reflex agents

To handle the problem of partial observability, the agent needs to *keep track
of the world it can’t see*. The agent makes a model of the world internally
using the previous percepts and thereby reflects some of the unobserved aspects
of the current state. 

<span class="figcaption_hack">Figure 2: Schematic Diagram of the Model-based Reflex agents</span>

For the agent to maintain an internal state of the world, it must have knowledge
on  two aspects of the environment: 1) We need to know how the world evolves
independent of the agent. 2) We need to know how the agent’s own action affects
the world. The second aspect is determinable, the problem is in the first one.
It is seldom possible for the agent to determine the current state of a
partially observable environment exactly. The agent usually has a ‘best guess’
of the current state of environment based on the percept history to take the
decision.

### Goal-based agents

Knowing just the current state is sometimes not enough to decide the actions t
be performed. The agent needs some sort of goal information that indicates the
desirable states in the environment. It keeps track of the world state as well
as a set of goals it’s trying to achieve, and chooses an action that will
(eventually) lead to the achievement of its goals.

<span class="figcaption_hack">Figure 3: Schematic Diagram of the Model-based Goal-based agents</span>

In the reflex agents, this is not explicitly represented as the in-built rules
maps directly from percepts to actions. For example, in a taxi-driving
environment, the reflex agent brakes when it sees brake lights in the car ahead
of it. The goal-based agent could reason that the car ahead will slow down if
its brake lights are on, and so as to avoid collision, it has to apply its
brakes.

The goal-based agent might seem less efficient, as it needs to process more
information than the reflex agent, thereby consuming more time. But it is very
flexible and can be easily modified. For example, if it starts to rain, the
agent can update its knowledge to change the duration of the application of
brakes, thereby altering all the relevant behaviors to adapt to the new
conditions. For the reflex agent, on the other hand, we would have to rewrite
many rules to have the same effect. Similarly, goal-based agent can easily be
modified to reach the destination via a different route (maybe the path closest
to the fuel station). The reflex agent’s rules works only for a particular
route; they must all be replaced to change the route.

### Utility-based agents

Goals alone are not sufficient to generate high-quality behavior in some of the
environments. For example, the taxi-driving agent  has many action sequences to
reach the destination, but some are quicker, safer, or less cost-effective than
the others. The performance measure should allow a comparison of the different
states based on how “happy” the agent would be at that stage. This is defined as
**utility** by the computer scientists. The utility-based agents maintains a
**utility function**, which the agents try to maximize based on the external
performance measure. 

<span class="figcaption_hack">Figure 4: Schematic Diagram of the Model-based Utility-based agents</span>

Utility, similar to defining a goal, is not the only way to be rational (we
can’t define the utility function for a vacuum cleaning agent) but, like the
goal-based agent, utility-based agent is flexible and adaptable to changing
environments. Furthermore, utility-based agents can make rational decisions even
when the goal-based agents fail to do so — this could happen in two cases: 1)
When there are conflicting goals (safety vs speed in taxi-driving situation). 2)
When there are multiple goals where none of them could be achieved with
certainty. In both the cases, the utility-based agent specifies the appropriate
trade-off (if the goals are conflicting), or the appropriate likelihood of
success (if the goals are co-operative).

Utility-based agents fair well in partially observable environments, as it
maximizes the expected utility to counteract the lack of observation. A reflex
agent will also try to maximize the external performance measure based on the
rules defined, but it doesn’t maintain an internal utility function to make up
for the partial observability of the environment.

The utility-based agents are the most intelligent of the ones discussed, but it
has to model and keep track of its environment tasks which involves a great
amount of research on perception and reasoning. Choosing the utility-maximizing
action is also a tedious task, and usually involves complex algorithms with high
computational complexity.

## Learning Agents

Currently, in many fields of AI, the idea of how to initiate the agent (make the
agent come into being) is solved by the technique of building the learning
models and then training them, as proposed by Alan Turing (the great) in 1950.
Learning  also allows the agent to operate in initially unknown environments and
to become more competent than its initial knowledge alone might allow.

<span class="figcaption_hack">Figure 5: Schematic Diagram of a Learning Agent</span>

A learning agent can be divided into four conceptual components. The previously
discussed agents comes under the **performance element**, which takes in
percepts and returns actions. The **learning element** is responsible for
modifying the behavior of the agent. It uses feedback from the **critic** on how
the agent is doing and determines how the performance element should be modified
to do better in the future. 

The **problem generator **is responsible for suggesting actions that will lead
to new and informative experiences. The performance measure commands the agent
to do the best action, given what it knows of the current situation. But if the
agent is willing to explore a little and do some perhaps suboptimal actions in
the short run, it might discover much better actions for the long run.

The critic has to distinguish the performance standard from the percepts, and
return a **reward** (or **penalty**) that provides a direct feedback on the
performance of the agent. For example, Hard-wired performance standards such as
pain and hunger in animals can be understood in this way.

Learning in intelligent agents can be summarized as the modification of agent’s
behavior based on the available feedback information to improve the overall
performance of the agent.

## Summary

The agent program is the implementation of the agent function, which maps the
percept sequence to the corresponding actions. The various designs of agent
programs aid in the development of intelligent agents. Reflex agents have a
pre-defined set of rules to be followed, some directly mapping the current
percept to the action (simple reflex) and some maintaining an internal state of
the environment (model-based reflex). Goal-based agents act to achieve their
goals, while utility-based agents maximize their own utility, or “happiness”.

The agents listed are in the increasing order of intelligence and the
adaptability to changing environment, but it doesn’t mean that the simple reflex
agents are not used widely, or the utility-based agents are the  most widely
used agents. A hybrid of all the above mentioned types of agents is used in
designing the agent. For example, the simple action of breaking in the
taxi-driving problem doesn’t require a utility function, or a long-term goal. A
simple reflex agent will take care of it. But to choose the path to reach the
destination, we need the performance measure of the path, and a utility function
to be maximized.

This concludes this introductory short series on Agents and Environment, though
further discussions on agents are implicit in the upcoming series. The next set
of blog posts will be based on the various search algorithms, starting from
classical search algorithms and their modifications, and a brief note on
adversarial search algorithms.
