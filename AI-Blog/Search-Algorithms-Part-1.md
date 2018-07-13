# Search Algorithms Part 1: Problem Formulation and Searching for Solutions

In the previous series of blogs, we have seen the [different structures of the
agents](https://medium.com/@rithesh18.k/agents-and-environment-part-2-structure-of-agents-33a0e1a1c75)
based on the [nature of the
environment](https://medium.com/@rithesh18.k/agents-and-environment-part-1-the-nature-of-the-environment-4faaec5ec5ca)
it is operating in. In the current series, we will discuss more on the
goal-based agent, and the search algorithms that gives the ‘solution’ to the
‘problem’ in these agents.

As mentioned previously, these blogs are very similar to the book “Artificial
Intelligence: A Modern Approach”. In fact, this series can be seen as a
shorthand version of the book.

## Types of Goal-based agents

We have seen that the reflex agents, whose actions are a direct mapping from the
states of the environment, consumes a large space to store the mapping table and
is inflexible. The goal-based agents consider the long-term actions and the
desirability of the outcome, which is easier to train and is adaptable to the
changing environment.

There are two kinds of goal-based agents: **problem-solving agents** and
**planning agents**. Problem-solving agents consider each states of the world as
**indivisible**, with no internal structure of the states visible to the
problem-solving algorithms. Planning agents split up each state into
**variables** and establishes **relationship** between them.

In this series, we will discuss more on problem-solving agents and the
algorithms associated with them. We’ll keep the discussion on the planning
agents for some other time.

In this post (and further too), as an example to explain the various algorithms,
we consider the problem of traveling from one place to another (single-source
single-destination path). Figure 1 gives the road-map of a part of Romania.

![](https://cdn-images-1.medium.com/max/800/1*Lx_LKzRCpXnYaEn-ZdUu1Q.png)
<span class="figcaption_hack"></span>
Figure 1: A simplified road map of part of Romania.

The problem is to travel from Arad to Bucharest in a day. For the agent, the
goal will be to reach Bucharest the following day. Courses of action that
doesn’t make agent to reach Bucharest on time can be rejected without further
consideration, making the agent’s decision problem simplified.

## Problem definition and formulation

Before we jump on to finding the algorithm for evaluating the problem and
searching for the solution, we first need to define and formulate the problem.

Problem formulation involves deciding what actions and states to consider, given
the goal. For example, if the agent were to consider the action to be at the
level of “move the left foot by one inch” or “turn the steering wheel by 1
degree left”, there would be too many steps for the agent to leave the parking
lot, let alone to Bucharest. In general, we need to abstract the state details
from the representation.

A problem can be defined formally by 5 components:

1.  The **initial state** of the agent. In this case, the initial state can be
described as *In: Arad*
1.  The possible **actions** available to the agent, corresponding to each of the
state the agent resides in. For example, ACTIONS(*In: Arad*) = {*Go: Sibiu*,
*Go: Timisoara*, *Go: Zerind*}
1.  The **transition model** describing what each action does. Let us represent it
by RESULT(s, a) where s is the state the action is currently in and a is the
action performed by the agent. In this example, RESULT(*In: Arad, Go: Zerind*) =
*In: Zerind.*
1.  The **goal test**, determining whether the current state is a goal state. Here,
the goal state is {*In: Bucharest*}
1.  The **path cost** function, which determine the cost of each path, which is
reflecting in the performance measure. For the agent trying to reach Bucharest,
time is essential, so we can set the cost function to be the distance between
the places. (Here, we are ignoring the other factors that influence the
traveling time). By convention, we define the cost function as *c(s, a, s’)*,
where s is the current state and a is the action performed by the agent to reach
state s’.

The initial state, the actions and the transition model together define the
**state space** of the problem — the set of all states reachable by any sequence
of actions. Figure 1 is the graphical representation of the state space of the
traveling problem. A **path** in the state space is a sequence of states
connected by a sequence of actions.

The **solution** to the given problem is defined as the sequence of actions from
the initial state to the goal states. The quality of the solution is measured by
the cost function of the path, and an **optimal solution** has the lowest path
cost among all the solutions.

## Searching for Solutions

We can form a **search tree** from the state space of the problem to aid us in
finding the solution. The initial state forms the **root** node and the
**branches** from each node are the possible actions from the current node
(state) to the child nodes (next states).

![](https://cdn-images-1.medium.com/max/800/1*bYJworzIsOA-gSkPDhj37w.jpeg)
<span class="figcaption_hack"></span>
Figure 2: Partial search tree for finding route from Arad to Bucharest. The
nodes Arad and Sibiu are opened

The six nodes in Figure 2, which don’t have any children (at least until now)
are **leaf nodes**. The set of all leaf nodes available for expansion at any
given point is called the** frontier**. The search strategy involves the
expansion of the nodes in the frontier until the solution (or the goal state) is
found (or there are no more nodes to expand).

We have to notice one peculiar thing in the search tree in Figure 2. There is a
path from Arad to Sibiu, and back to Arad again. We say that *In(Arad) *is a
repeated state, generated by a **loopy path**. This means that the search tree
for Romania is *infinite*, even though the search space is limited. These loopy
paths makes some of the algorithms to fail, making the problem seem unsolvable.
In fact, a loopy path is a special case of **redundant paths**, where there are
more than one paths from one state to another (for example, Arad — Sibiu and
Arad — Zerind — Oradea — Sibiu).

The redundant path situation occurs in almost every problem, and often makes the
solution algorithm less efficient, worsening the performance of the searching
agent. One way to eliminate the redundancy is to utilize the advantage given by
the problem definition itself. For example, in the case of traveling from Arad
to Bucharest, since the path costs are additive and step costs are non-negative,
only one path among the various redundant paths has the least cost (and it is
the shortest distance between the two states), and loopy paths are never better
than the same path with loops removed.

Another idea to avoid exploring redundant paths is to remember which states have
been visited previously. Along with the search tree, an **explored set** is
maintained which contains all the states previously visited. Newly generates
which matches the previously generated nodes can be discarded. In this way,
every step moves the states in the frontier into the explored region, and some
states in the unexplored region into the frontier, until the solution is found.

![](https://cdn-images-1.medium.com/max/800/1*oc6Pl9rH9WcdtYK9Q3kdwA.png)
<span class="figcaption_hack"></span>
Figure 3: The separation property of the above mentioned algorithm, as
exploration is increased from the root (leftmost image) to its immediate
successors (rightmost image). The frontier (white nodes) always separates the
explores states (black) and the unexplored ones (gray).

### Performance measure of Problem-solving Algorithms

We can evaluate an algorithm’s performance with these metrics:

1.  **Completeness**: Is the algorithm guaranteed to find a solution if there exist
one?
1.  **Optimality**: Does the algorithm find the optimal solution?
1.  **Time complexity**: How long does it take for the algorithm to find a solution?
1.  **Space complexity**: How much memory is consumed in finding the solution?

In graph theory, the time and space complexity is measured using |V| and |E|,
where V and E are the number of vertices and the number of edges in the graph
respectively. But in AI, we explore the state space (which is a graph) of the
problem using its equivalent search tree. So it is meaningful if we use *b* and
*d* to measure the complexity, where *b* is the **branching factor** of the tree
(maximum number of successors of any node) and *d* is the **depth** of the
shallowest goal node.

## Summary

In this post we have discussed how to define the problem so as to assist in
formulation of the problem and to effectively find a solution. We have also seen
the use of search tree in finding the solution and the ways to avoid the problem
of redundancy. Finally, we have listed the metrics for measuring the performance
of the search algorithms.

In the next blog, we will discuss the classical search algorithms,starting with
uninformed search algorithms and then moving on to heuristic, or informed search
algorithms.

* [Programming](https://medium.com/tag/programming?source=post)
* [Search Algorithm](https://medium.com/tag/search-algorithm?source=post)
* [Problem Solving](https://medium.com/tag/problem-solving?source=post)
* [Problem Formulation](https://medium.com/tag/problem-formulation?source=post)

From a quick cheer to a standing ovation, clap to show how much you enjoyed this
story.

### [Rithesh K](https://medium.com/@rithesh18.k)

AI Enthusiast. Loves Mathematics. Short stories and Quotes are my hobbies.
