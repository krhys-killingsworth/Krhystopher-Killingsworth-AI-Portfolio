# Advanced AI Agent Concepts

## Problem Statement

Vision models perceive. Agents act on what they perceive. This project implements four distinct agent paradigms side by side, then compares how they learn, which is the bridge from single-model computer vision to the multi-agent architecture used in the RoadWatch final project.

## Approach

**Part 1 - Deep Q-Network.** A value-based agent that learns the expected return of each action in each state and acts greedily on those estimates.

**Part 2 - Policy Gradient.** A policy-based agent that learns action probabilities directly, outputting a distribution over actions rather than value estimates.

**Part 3 - Multi-Agent System.** Several agents operating on a shared grid, where each agent's moves affect the others' state.

**Part 4 - Federated Learning.** Three agents train independently on separate local experience, then aggregate their learned parameters without exchanging raw data.

**Part 5 - Comparison.** DQN and policy gradient trained on the same task for 100 episodes with average reward logged every 10 episodes.

## Results

**Policy gradient output.** The learned action distribution shifted steadily from near-even toward a decisive preference, moving from `{'move': 0.413, 'stop': 0.587}` to `{'move': 0.257, 'stop': 0.743}` across logged steps. Watching probabilities move is a direct view of a policy converging.

**Multi-agent coordination.** Agents propagated across the grid over five steps without collision, with per-step positions printed as a visual grid.

**Federated aggregation.** Before aggregation, three agents held completely disjoint knowledge, each aware only of its own position. After averaging, all three shared an identical merged parameter set covering all positions. No raw experience was exchanged.

**DQN vs. policy gradient over 100 episodes.** Both methods produced noisy average rewards oscillating between roughly -0.8 and +1.2, with neither showing clean monotonic improvement over the run.

## Key Findings

**Federated aggregation was the most striking result.** Three agents each knowing one position became three agents each knowing all three, with only parameters crossing the boundary. The privacy argument for federated learning stops being abstract once you can read the before and after dictionaries.

**Value-based and policy-based agents solve the same problem from opposite directions.** DQN asks "how good is this action here" and derives behavior from the answer. Policy gradient asks "what should I do here" and skips the value estimate. Implementing both made the distinction concrete rather than definitional.

**Noisy learning curves are the normal case.** Neither method improved smoothly across 100 episodes. Reinforcement learning explores by design, and an agent trying suboptimal actions produces exactly this oscillation. A single 10-episode window says almost nothing, which is a useful calibration against reading too much into short runs.

**This is where multi-agent design started making sense to me.** Coordinating several agents toward a shared objective is the pattern the RoadWatch Agent final project is built on.

## Technologies Used

Python, PyTorch, NumPy, reinforcement learning (DQN, REINFORCE-style policy gradient), federated parameter averaging, Google Colab

## Data

Simulated environments defined in the notebook. No external dataset required.

## How to Run

Open `Advanced_AI_Agent_Concepts.ipynb` in Google Colab and run all cells top to bottom. No GPU required. Reward values vary between runs because of exploration randomness.
