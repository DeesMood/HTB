`Reinforcement learning` (`RL`) introduces a unique paradigm in `machine learning` where an agent learns by interacting with an environment.
## How Reinforcement Learning Works
In `RL`, an agent interacts with an environment by acting and observing the consequences. The environment provides feedback through rewards or penalties, guiding the agent toward learning an optimal policy. A `policy` is a strategy for selecting actions that maximize cumulative rewards over time.

`Reinforcement learning` algorithms can be broadly categorized into:

1. `Model-Based RL:` The agent learns a model of the environment, which it uses to predict future states and plan its actions. This approach is analogous to having a map of a maze before navigating it. The agent can use this map to plan the most efficient path to the goal, reducing the need for trial and error.
2. `Model-Free RL:` The agent learns directly from experience without explicitly modeling the environment. This is like navigating a maze without a map, where the agent relies solely on trial and error and feedback from the environment to learn the best actions. The agent gradually improves its policy by exploring different paths and learning from the rewards or penalties it receives.

## Core Concepts in Reinforcement Learning
### Agent
The `agent` is the learner and decision-maker in an `RL` system.
### Environment
The `environment` is the external system or context in which the agent operates.
### State
The `state` represents the current situation or condition of the environment.
### Action
An `action` is an agent's move or decision that affects the environment.
### Reward
The `reward` is feedback from the environment indicating the desirability of the agent's action.
### Policy
A `policy` is a strategy or mapping from states to actions the agent follows.
### Value Function
The `value function` estimates the long-term value of being in a particular state or taking a specific action.

There are two main types of value functions:

- `State-value function:` Estimates the expected cumulative reward from starting in a given state and following a particular policy.
	- Question: _“If I start in this situation (being a high school senior) and follow my general strategy (policy), how good will my future be overall?”_

- `Action-value function:` Estimates the expected cumulative reward from taking a specific action in a given state and then following a particular policy.
	- Question: _“If I start in this situation (being a high school senior), pick a **specific major** (action), and then continue following my strategy (policy), how good will my future be?”_
### Discount Factor
The `discount factor` (`γ`) is a `RL` parameter that determines future rewards' present value. It ranges between 0 and 1, with values closer to 1 giving more weight to long-term rewards and values closer to 0 emphasizing short-term rewards.
- `γ=0` means the agent only considers immediate rewards.
- `γ=1` means the agent values all future rewards equally.
### Episodic vs. Continuous Tasks
`Episodic tasks` involve the agent interacting with the environment in episodes, each ending at a terminal state (e.g., reaching the goal in a maze). In contrast, `continuous tasks` have no explicit end and continue indefinitely (e.g., controlling a robot arm).
