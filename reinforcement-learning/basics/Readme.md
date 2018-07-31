# Reinforcement learning basics

## Learning from interactions&nbsp;, not from labelled&nbsp;data

Action depends on state, but what is the state&nbsp;

Learn faster with minimal effort&nbsp;

How to measure effort, in case of robots it was force on its pi

#### What OpenAI gym&nbsp;contain?

- It includes dozens of environments for testing reinforcement learning agents.&nbsp;
- It was designed as a toolkit for developing and comparing reinforcement learning algorithms.&nbsp;
- It was developed to address lack of benchmarks and standardization in RL research

Agent interacts with the environment which results state action reward series&nbsp;

Environment decides how much rewards the agent receives&nbsp;

The agent is bound by the rules of the environment.

 ![](https://cdn-images-1.medium.com/max/1600/1*2IeyiutGmqkB3e7dIJ6U-A.jpeg)

 ![](https://cdn-images-1.medium.com/max/1600/1*nvD7SdPneUOek0tz9uRKUw.png)

* * *

#### Episodic vs continuous&nbsp;

Episodic tasks have well defined ending&nbsp;

- A **task** is an instance of the reinforcement learning (RL) problem.
- **Continuing tasks** are tasks that continue forever, without end.
- **Episodic tasks** are tasks with a well-defined starting and ending point.
- In this case, we refer to a complete sequence of interaction, from start to finish, as an **episode**.
- Episodic tasks come to an end whenever the agent reaches a **terminal state**.

 ![](https://cdn-images-1.medium.com/max/1200/1*HmD4hH0zNfIBoMBuNFAvhg.png)

Consider playing the game, an episode of the game would end once you win or lose. After each episode the agent would start again but now with the knowledge of its last episode, after repeating many episodes the agent understands the strategy to take actions to maximize the reward.

All goals can be framed or formulated as maximization of total cumulative rewards.

* * *

#### The rewards has to be designed thoughtfully&nbsp;

 ![](https://cdn-images-1.medium.com/max/2000/1*twqhvJlyvposftzFlQz2Eg.png)
*Reward mechanism designed by Deepmind for robotic motion&nbsp;training&nbsp;*

The ideas of the Deepmind was to train the robot to walk quickly for a long time with minimal effort, the reward mechanism was designed to achieve that.

\<More examples on the reward mechanism\>

\<Givec maze exzmple\>

* * *

Actions have long term and short term rewarwd&nbsp;

The agent has to working towards cumulative rewards over a longer sequence of actions though it may have to sacrifice upon immediate rewards.&nbsp;

Its not effective if the agent is focused on maximizing immediate rewards or rewards at every time step. Take the case of the playing the game of chess, weaving a winning path might involve complex strategies leading the opponent to trap, which means you may have to sacrifice one of your coins inorder open inroads to defeat the opponent, though the immediate reward is negative but it may lead to a winning path few steps ahead. In general the agent has to be focused on cumulative reward of all time steps.

 ![](https://cdn-images-1.medium.com/max/1600/1*eWnhJOPh_UXIM4cN-HGpFA.png)

* * *

> That’s sounds right! Which means every action of the agent at any time step has to be based on what’s ideal for the cumulative reward to be greater, not just the immediate reward?

yes, that’s right.

> &nbsp;But how does the agent know the rewards it would obtain in future time steps and take current actions based it&nbsp;? Is there a some kind of magic to understand the future consequence of current action&nbsp;?

 ![](https://cdn-images-1.medium.com/max/1200/1*Y5TKDOOcKqPxhOwmpXtSZg.png)

Yes, we can’t precisely calculate the future rewards, but we can estimate it using reinforcement learning techniques. This estimation or expected value of cumulative rewards in the future time step is called as **_return._**

>

> The agent “always and always” work towards maximizing the cumulative rewards, its the cumulative reward (past rewards + estimated future rewards) which has the say on the agent picking an action at any given time step. So you better be sure that the reward system is designed in a way to reach the intended&nbsp;goal

* * *

 ![](https://cdn-images-1.medium.com/max/1200/1*zOOlNjrDGLyGX40zzHQzuA.jpeg)

Its easy to be sure of the immediate reward than trying to estimate the expected future return. It gets more and more uncertain The further we think about future.&nbsp;

> But when we talk about taking current decisions based of estimation of future rewards, how far in the future should the agent care about&nbsp;?

This is decided by the discounting factor. Its a value between 0 and 1, higher the value the agent cares more about the far future or rewards which are many more time steps away and cares only the next or the immediate reward when its value is 0.

 ![](https://cdn-images-1.medium.com/max/1600/1*oB7sKXb-GpxuuIDz8pPwmg.png)

* * *

> You decide the goal for the agent, we ultimately care about the goal. But designing the right reward mechanism enables us to use Reinforcement-Learning or Deep-RL to come with the actions/strategies for the agent to achieve the&nbsp;goal.

* * *

 ![](https://cdn-images-1.medium.com/max/1600/1*l8sJLWcXKxeID0qD-QFeTQ.png)

* * *

#### Policies&nbsp;

Its a mapping of state to actions learned from training&nbsp;

#### State-value function

 ![](https://cdn-images-1.medium.com/max/1600/1*3IAYvy_-W3-vCOPRhCxJkg.png)

#### STATE VALUE&nbsp;FUNCTION&nbsp;

 ![](https://cdn-images-1.medium.com/max/2000/1*4g-I60HrYEhsFGEYmR9OwA.png)

 ![](https://cdn-images-1.medium.com/max/2000/1*1ya_sAS8cp9Ab8KKctMRqw.png)

#### GOOD VS BAD&nbsp;POLICY

 ![](https://cdn-images-1.medium.com/max/2000/1*2QpewsqyhxImcs51id3W-Q.png)

#### Optimal Policy

 ![](https://cdn-images-1.medium.com/max/1600/1*bgykgfj9WN-BlVO5OkPP3w.png)

 ![](https://cdn-images-1.medium.com/max/1600/1*q0keMwuTShBc7sL5DzKDZQ.png)

* * *

Action value function gives the expected return on choosing action `a` at state `s` and then using the policy to pick the action in the further states. You need to do this for every possible action, value pair to obtain the action value function.&nbsp;

 ![](https://cdn-images-1.medium.com/max/1600/1*tC_L-d0rRBliDRolrkLi0A.png)

An optimal action value policy is denoted by q\*

* * *

An optimal policy has to be derived from state-action function, the action which yields the highest expected return at every state forms the optimal policy. In the series of posts we’ll how to arrive at optimal state-action inroder to decide an optimal policy.&nbsp;

If the state space S\mathcal{S}S and action space A\mathcal{A}A are finite, we can represent the optimal action-value function q∗q\_\*q∗​ in a table, where we have one entry for each possible environment state s∈Ss \in \mathcal{S}s∈S and action a∈Aa\in\mathcal{A}a∈A.

The value for a particular state-action pair s,as,as,a is the expected return if the agent starts in state sss, takes action aaa, and then henceforth follows the optimal policy π∗\pi\_\*π∗​.

We have populated some values for a hypothetical Markov decision process (MDP) (where S={s1,s2,s3}\mathcal{S}=\{ s\_1, s\_2, s\_3 \}S={s1​,s2​,s3​} and A={a1,a2,a3}\mathcal{A}=\{a\_1, a\_2, a\_3\}A={a1​,a2​,a3​}) below.
